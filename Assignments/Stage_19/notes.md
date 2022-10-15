# Stage 19

1. There are four events that result in generation of an exception in XSM. These events are 
    - illegal memory access
    - illegal instruction
    - arithmetic exception
    - page fault.

2. In current implementation of demand paging two pages for heap is allocated instead of one (very lazy loading) because of some compllications in implementing the fork system call


3. In module 2 contrary to what I did in module 1, I am checking whether a page is valid by checking whether the address pointed by page table is "-1" rather than checking the valid bit.

4. We are not releasing code pages from disk in free page table , as we need them atleast in the disk.


# Doubt
1. Why is pid passed for release block function? (It is not used in final version)