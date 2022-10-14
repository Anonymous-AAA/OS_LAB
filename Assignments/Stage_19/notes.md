# Stage 19

1. There are four events that result in generation of an exception in XSM. These events are 
    - illegal memory access
    - illegal instruction
    - arithmetic exception
    - page fault.

2. In current implementation of demand paging two pages for heap is allocated instead of one (very lazy loading) because of some compllications in implementing the fork system call