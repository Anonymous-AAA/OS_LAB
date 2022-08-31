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

11. Very Very Important:
The control flow at this point is tricky and must be carefully understood. The key point to note here is that although the scheduler module was called by one process (from the timer ISR), since the stack was changed inside the scheduler, the return is to a program instruction in some other process! (determined by the value on top of the kernel stack of the newly scheduled process). The return is to that instruction which immediately follows the call scheduler instruction in the newly selected process. 

An exception to this rule happens only when the newly selected process to be scheduled is in the CREATED state. Here, the process was never run and hence there is no return address in the kernel stack. Hence, the scheduler directly kick-starts execution of the process by initiating user mode execution of the process (using the ireturn instruction). The design of eXpOS guarantees that a process can invoke the scheduler module only from the kernel mode. Consequently, the return address will be always stored on top of the kernel stack of the process.