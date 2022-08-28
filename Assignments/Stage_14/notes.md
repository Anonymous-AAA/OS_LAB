# Stage 14  

1. Parts of the eXpOS kernel that implements code for certain standard repetitive tasks like scheduling, managing resources, buffer etc. are implemented as separate subroutines called modules.
2. Timer is a ISR (Interrupt Service Routine)
3. Boot module and Scheduler modules are Kernel modules
4. Modules cannot be invoked by a program executing in the user mode.
5. When a kernel routine invokes a module, the return address from the module gets pushed into the currently active kernel stack. 
6. We will write the Timer ISR in such a way that it does not use any registers.
7. The ExpL compiler fails to save the value of BP register before making a system call. To solve this problem, a patch is added to the scheduler so that the scheduler saves the current value of BP register to the kernel stack of the process being scheduled out.
8. Context switch happens by a change of SP, PTBR and PTLR registers.
9. The offset of SP register within the user area page will be stored in the KPTR field of the process table(and not the physical address of the kernel stack pointer). The value of the offset can be calculated by the fomula offset = SP – (512 * USER AREA PAGE NUMBER). The purpose of storing the offset (instead of the physical address) is to allow the OS to relocate the user area page to another physical memory page during swapping.
10. Scheduler module is also called the context switch module.