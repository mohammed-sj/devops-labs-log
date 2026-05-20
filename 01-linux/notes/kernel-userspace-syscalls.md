# Kernelspace, userspace and syscalls

## Keywords & Connections
 
- **Userspace**: The unprivileged space where programs run. 
    - What programs can do in userspace: run normal logic, do calculations, manipulate their own memory
    - They cannot directly: access hardware, control the CPU, read disk, manipulate other programs. **They need the kernel for this**
    - Example of userspace programs: ls, bash, vim.

- **Kernel space**: the privilaged space where the kernel runs and has access to hardware.
    - **What it does**:
        - manages **CPU scheduling**
        - mediates **hardware access**
        - manages **processes**
        - manages **memory**
        - manages **containers**
        - handles **syscalls**
        - enforces **permissions**
        - enforces **isolation**
        - arbitrates shared **resource access**
    - **Examples**: 
        - permissions denied: the kernel refusing a syscall.     
        - isolation: the kernel prevents programs from hogging CPU, from a process arbitrarily overwriting another process, from a faulty program to crash the whole system, from a program reading another program. 
    - Drivers are the layer within the kernel which interfaces with hardware. Meaning the kernel doesn't directly access hardware, they use drivers. 
- privilege/permission domains
    - **Isolation**: The kernel prevents processes from reading or writing to kernel RAM, or another process's RAM. 
    - **Arbitration**: the kernel sequences the turn of accessing resources between processes
        - **CPU scheduling**: kernel manages allocation of CPU time to each process.
        - **Disk and network I/O (input/output)**: it also manages access to process requests of reading and writing to disk and network.
- **Syscalls**: Operations used by userspace to access hardware through kernel.
    - **Example syscalls**
        - **Filesystem & input/output syscalls**
            - `open`: request to find file and prepare it for reading.
            - `read`: copies a specified amount of data from file or device node to RAM.
            - `write`: copies data from program memory and pushes it to file, device node or terminal.
            - `close`: tells the kernel it is finished with a file, freeing resources and ensuring remaining data is saved to disk.
            - `getdents`: reads directory entries (this is what ls uses under the hood).
        - **Process management syscalls**
            - fork: duplicates the shell process. The dublicate is called the child process and the original the parent process.
            - exec: replaces the child process with the program.

## What problem does this solve? 
- security: the kernel's privilege seperation prevents a malware from accessing password keychains, from a buggy program to corrupt the whole system, from a process interfering with another. 
- Kernel isolation and arbitration is essential for a number of things:
    - Prevents processes from overwriting the kernels or other processes data and corrupting them.
    - Managing access to hardware so multiple programs don't "fight" over it simultaneously.
    - Prevents an infinite loop from hogging CPU forever.

## Commands / Syntax to remember [Only the ones worth remembering]
- `strace` | troubleshooting tool for tracing systemcalls
- `echo $$` | gives your shell process id (PID)
## Quick Example 
- Syscalls (very concise workflow of what happens when you `ls`): 
    1. shell runs fork and exec syscalls to run the program ls
    2. ls is ran as a seperate child process, and this process runs another syscall (`getdents`) to read files
    3. kernel checks permissions, then passes a request to drivers to get data from hardware
    4. hardware returns data through drivers and the kernel to ls
    5. ls performs a `write` syscall to send its output to the terminal, then exits on its own.
    6. Kernel signals to shell that `ls`process has exited, after which the shell prints the next prompt.
