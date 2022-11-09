# Stage 27

1. At any time if the OS finds that the available (free) memory drops below a critical level, a swap out is initiated. 
2. A swapped out process is swapped back into memory, when one of the following events occur:

      1) A process has remained in swapped out state for more than a threshold amount of time.
      2) The available memory pages exceed certain level denoted by MEM_HIGH (MEM_HIGH is set to 12 in present design)
3. The swapper daemon shares the code of the idle process, and is essentially a duplicate idle process running with a different PID. Its sole purpose is to set up a user context for swapping operations. 


## Errors
1. In documentation of System Status Table, Swap Out/Swap In are indicated by 1 and 2, respectively.
2. Update memory free list and processes in terminated status in boot_module not mentioned as changes to be made.


## Doubts
1. What if the code pages are shared among processes. (in SWAP_OUT this condition is not checked while releasing the page for code).
A. There is demand paging, so if the code page is required , page fault is generated, so the page will be loaded back. 
-  But that is possible in case of heap also right, why check if its being shared
- I guess its because heap pages when needed are allocated together (not as a single page).

2. What is the reasoning behind the order of choosing the process to swap out? Why is a process in WAIT_PROCESS swapped out ahead of a process waiting for the terminal? What about processes waiting for the disk?

3. Is it possible that there are processes waiting for memory, even when MEM_FREE_COUNT > MEM_HIGH?


## Changes made
1.In line 50 of MOD_5 I made a change to check whether newPID is greater or equal to SWAPPER_DAEMON, instead of just checking whether its equal to SWAPPER_DAEMON