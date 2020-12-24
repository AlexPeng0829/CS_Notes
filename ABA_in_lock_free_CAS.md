### Beware the ABA problem in lock-free data strcuture

Lock-free data structure using **CAS**(Compare And Swap) might suffer from ABA problem

```C
// stack: top -> a -> b -> c
// A naive implementation which might suffer ABA problem
element* pop()
{
    while(true){
    ret = top;
    top_new = ret->next;
    if(CAS(top, ret, top_new) == true){
    	    return ret;
    	}
    }
}
```

Just imagine when thread 1 is about to execute line 6, it got preempted by thread 2. Thread 2 call `pop()` twice and `push(a)`, now the stack would be: `top -> a -> c`.
Now thread 1 got the chance to run and find `top == a` as expeted and set `top = b`, which would cause serious problem as now element b is already removed from stack. A subsequent dereference of b would be a disaster.

This problem can be generalized as "Try to access a memory that might be already freed in a garbage-free system"(In system with GC, this acces can be guaranteed, as some sort of reference track would automatically deal with it).
```C
element* cur = head;  // assume it's atomic
element* next = cur->next; // assume it's atomic
```
Above code snippet shows a typical problem in lock free implementation. Another thread might change the head between `line 1` and `line 2`. To solve this problem, several apporaches can be applied:

- Use lock-free pattern such **RCU**(Read-Copy-Update), this scheme provides a `grace period` to free the data element that might be removed by one thread from the shared memory. The clean-up for those data element would only happen when all threads have done context switch. Note that to mark the begin and end of access for those shared data element, one might specifically use something like `rcu_read_lock()` and `rcu_read_unlock()` and `rcu_dereference()`. Also be noted that RCU might not be able to handle all above-mentioned scenarios.

- **Hazard Pointer** somehow provided a similar concept as **RCU**, as those pointers removed from a shared linked-list would not freed until no thread has a reference to it. To achieve that a per-thread hazard pointer list must be created to track the pointer that's referenced by each thread. A gc thread would track the "to-be-freed-later" linked list which would be added pointer by each thread execept the gc thread. gc thread would periodically free the element in "to-be-freed-later" linked list and not in any hazard pointer list.

- In byte-addressable machine, one can use **Tagged Pointer** to track the reference count for a single pointer with no extra memory overhead. For instance, in an X86-64 machine, a world-addressable memory adddress would always be the multiple of 8, thus leaving lowest 3 bits unsed which could be further exploited as the tag bits. In more general concept, current 64 bit virtual memory system only occupies a fraction of the memory bits(48 bits for example in X86-64 virtual memory) and leaves plenty of bits for later extension. However, as x86-64 follows the `Canonical Form of Address`, this unsed bits are marked either all 1s or 0s based on privilege level which in turn forbids the usage of tagged bits in these unsed bits.

- A more preferred approach over Tagged Pointer is a **seperate tag field** although it causes extra memory overhead. Note that to achieve that a double-width CAS might be supported.

- In other architecture such as MIPS/ARM, **load linked and store conditional**(LL/SC) somehow avoids the ABA problem as it provides a stronger check so that any update to A would cause latter read of A would fail.