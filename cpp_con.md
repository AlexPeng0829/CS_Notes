# Comments and remarks of watching CPP Conference

This document is created to record the comments and remarks while watching the video of CPP conferences. Only a fraction of videos are selected in the first place based on my interest.

## **C++ and beyond 2012**
| Title                                                              | Author              | Category              | Comment                                                              | Rank                           |
| ------------------------------------------------------------------ | ------------------- | --------------------- | -------------------------------------------------------------------- | ------------------------------ |
| atomic<> Weapons part 1&2                                          | Herb Sutter         | Atomic & Memory model | Very good explanation of the memory order and atomic feature in C++. | :star::star::star::star::star: |
| C++ concurrency                                                    | Herb Sutter         | Cocurrency            | Excellent explanation of concurrency in C++.                         | :star::star::star::star::star: |
| Universal References in C++11                                      | Scott Meyer         | Type deduction        | Thorough illustration on type deduction.                             | :star::star::star::star:       |
| Systematic Error Handling in C++                                   | Andrei Alexandrescu | Error handling        |
| You don't know [blank] and [blank]                                 | Herb Sutter         | General               |
| Convincing your Colleagues                                         | Panel               | Talk                  |
| Ask us anything                                                    | Panel               | Talk                  |
| On Static If, C++11 in 2012, Modern Libraries, and Metaprogramming | Panel               | Talk                  |


## **CPP Con 2014**
| Title                                                          | Author              | Category              | Comment                                                                                                                                                                                                                                | Rank                     |
| -------------------------------------------------------------- | ------------------- | --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| Paying for lunch - C++ in many core age                        | Various authors     | Talk                  | Basic intro to the challange brought up by the multi-core architecture, An talk by the authors who have background in concurrency/parallelism/GPU/transactional memory to share their view/experience in writing C++ with multi cores. | :star:                   |
| Back to basics - essentials of modern C++ style                | Herb Sutter         | Best practice         | An overview of best practice in using modern C++11. features.                                                                                                                                                                          | :star::star::star:       |
| Type deduction and why you care                                | Scott Meyer         | Type deduction        | A comprehensive type deduction regarding auto/template/lambda/decltype.                                                                                                                                                                | :star::star::star::star: |
| Make simple tasks simple                                       | Bjarne Stroustrup   | Philosophy            | Understand how the father of C++ view modern C++.                                                                                                                                                                                      | :star::star::star:       |
| Overview of parallel programming in C++                        | Pablo Halpern       | Parallel programming  | General concept of parallel programming.                                                                                                                                                                                               | :star::star:             |
| Lock free by example                                           | Tony Van Eerd       | Lock free programming | An example of lock-free multi producer & multi consumer queue.                                                                                                                                                                         | :star::star:             |
| Lock-free programming part 1&2                                 | Herb Sutter         | Lock free programming | Lock-free programming by Herb, how to correctly write a lock-free single linked list?                                                                                                                                                  | :star::star::star::star: |
| Optimization tips- more hustle more problems                   | Andrei Alexandrescu | Optimization          | Intersting to know the performance issue caused by icache. miss.                                                                                                                                                                       | :star::star::star:       |
| What did C++ do for transactional memory?                      | Michael Wong        | Transactional memory  | Intro to transactional memory TS in C++.                                                                                                                                                                                               | :star::star:             |
| Making allocator work part 1&2                                 | Alisdair Meredith   | Allocator             | An intro of allocatos by the author of std::allocator, quite informative.                                                                                                                                                              | :star::star::star:       |
| C++ memory model meets high-update-rate data structures        | Pual E. McKenney    | NUMA                  | RCU implementation and usage.                                                                                                                                                                                                          | :star::star::star:       |
| Meet the authors                                               | various authors     | Talk                  | Meet the book writer of many famous C++ books.                                                                                                                                                                                         | :star:                   |
| Boost: a bridge from C++ 98 to C++ 11, An intro to using boost | Cheng & Vanloon     | boost                 | A very brief intro to boost, only covers a small range of it.                                                                                                                                                                          | :star:                   |  |
| Grill the committee                                            | C++ committee       | Talk                  | Meet the committee of C++, good to familiar with the guys and know their names/faces. :stuck_out_tongue_winking_eye:                                                                                                                   | :star:                   |
| The canonical class                                            | Michael Caisse      | Move semantics        | Some advices on how to correctly adpot the feature of Move.                                                                                                                                                                            | :star::star::star:       |  |

## **CPP Con 2015**
| Title                                                           | Author                     | Category      | Comment                                                                                            | Rank                     |
| --------------------------------------------------------------- | -------------------------- | ------------- | -------------------------------------------------------------------------------------------------- | ------------------------ |
| std::allocator is to allocation what std::vector is to vexation | Andrei Alexandrescu        | Allocator     | Different type of allocators. How to correctly implement and use them.                             | :star::star::star::star: |
| Declarative control flow                                        | Andrei Alexandrescu        | Exception     | Scoped macro to write beautiful exception-safe code.                                               | :star::star::star:       |
| Writing good C++ 14                                             | Bjarne Stroustrup          | Best practice | An intro to guideline for writing good C++14, this guideline is now publicly accessable in github. | :star::star::star:       |
| Writing Good C++14... By Default                                | Herb Sutter                | Best practice |
| C++ in Open Source Robotics                                     | Jackie Kay & Louise Poubel | ROS           |
| C++11/14/17 atomics and memory model                            | Michael Wong               | Memory model  |
| C++ atomics                                                     | Paul E. McKenney           | Atomics       |
| string_view                                                     | Marshall Clow              | String        |

## **CPP Con 2016**
| Title                                         | Author            | Category    | Comment | Rank |
| --------------------------------------------- | ----------------- | ----------- | ------- | ---- |
| The evoluyion of C++ Past, Present and Future | Bjarne Stroustrup | History     |
| Leak-freedom in C++...                        | Herb Sutter       |
| Introduction to C++ Coroutines                | James McNellis    | Coroutine   |
| The continuing future of C++ concurrency      | Anthony Williams  | Concurrency |
| A Chrono tutorial - it's about time           | Howard Hinnant    | Library     |
| Asynchronous IO with Boost.Asio               | Michael Caisse    | Async IO    |


## **CPP Con 2017**
| Title                                               | Author            | Category       | Comment                                        | Rank               |
| --------------------------------------------------- | ----------------- | -------------- | ---------------------------------------------- | ------------------ |
| Allocators: the good parts                          | Pablo Halpern     | Allocator      | More implementation details of STL allocators. | :star::star::star: |
| Meta: thoughts on generative C++                    | Herb Sutter       | General        |
| Learning and teaching modern C++                    | Bjarne Stroustrup | General        |
| An allocator model for std2                         | Alisdair Meredith | Allocator      |
| The nightmare of move semantics for trivial classes | Nicolai Josuttis  | Move semantics |
## **CPP Con 2018**
| Title                                               | Author              | Category       | Comment                                           | Rank               |
| --------------------------------------------------- | ------------------- | -------------- | ------------------------------------------------- | ------------------ |
| An Allocator is a handle to a heap                  | Arthur O'Dwyer      | Allocator      | Allocators are really handle to memory resources. | :star::star::star: |
| Concepts: the future of generic programming         | Bjarne Stroustrup   | Concept        |
| Thoughts on a more powerful and simpler C++(5 of N) | Herb Sutter         | General        |
| The nightmare of initialization in C++              | Nicolai Josuttis    | Initialization |
| Expect the expected                                 | Andrei Alexandrescu |



## **CPP Con 2019**
| Title                                                                     | Author                            | Category         | Comment                        | Rank               |
| ------------------------------------------------------------------------- | --------------------------------- | ---------------- | ------------------------------ | ------------------ |
| C++20: C++ at 40                                                          | Bjarne Stroustrup                 | General          |
| Speeds in found in the minds of people                                    | Andrei Alexandrescu               |
| De-fragmenting C++: Making exceptions and RTTI more affordable and usable | Herb Sutter                       |
| Getting Allocators out of our way                                         | Pablo Halpern & Alisdair Meredith | Allocators       |
| Back to basics: virtual dispatch and its alternatives                     | Inbal Levi                        | Virtual function |
| Back to basics: RAII and rule of zero                                     | Arthur O'Dwyer                    | RAII             |
| Back to basics: move semantics                                            | Klaus Iglberger                   | Move semantics   |
| Back to basics: Const as a promise                                        | Dan Saks                          | Const            |
| Back to basics: Understanding value Categories                            | Ben Saks                          |
| Back to basics: exception handling and exception handling                 | Ben Saks                          | Exception        |
| Back to basics: lambda from scratch                                       | Arthur O'Dwyer                    | Lambda           |
| Back to basics: type erasure                                              | Arthur O'Dywer                    | Type             |
| Back to basics: in-place construction                                     | Ben deane                         | Constructor      |
| Back to basics: Object-oriented programming                               | Jon Kalb                          | OOP              |
| Back to basics: funtion and class templates                               | Dan saks                          | Templates        |
| Back to basics: smart pointers                                            | Arthur O'Dwyer                    | Smart pointer    | An overview of smart pointers. | :star::star::star: |