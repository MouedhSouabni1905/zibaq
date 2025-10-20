**Tags:** [[Operating Systems]] [[Networking]]

**Everything is a file** in Linux. Whether it's processes, hardware, or code, the linux kernel treats everything as a file.

In x86 assembly, to make a syscall to the linux kernel, we move the [number of the syscall](https://x64.syscall.sh)  to the **rax** register, and the arguments in rdi, rsi, rdx, r10, r8, r9, in that order. Rax contains the return value.

Sockets are opened using the socket() system call. The bind() system call assigns the socket to an address (to listen to any connection,  we specify *sin_addr=inet_addr("0.0.0.0")* ). The listen() system call marks the socket as passive, meaning ready to accept a connection using the accept() system call. The latter then creates a new socket and returns the file descriptor referring to that socket.

The fork() system call creates a new process, called the child process and the calling process is called the parent process. It does so by duplicating the calling process. They're identified by their PID and Parent PID (PPID).
