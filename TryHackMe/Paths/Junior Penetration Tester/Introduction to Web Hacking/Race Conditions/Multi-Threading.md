## Programs
A program is a set of instructions to achieve a specific task. You need to excuse the program to accomplish what you want.
## Processes
is a program in execution. In some literature, you might come across the term job.
### Program
The executable code related to the process
### Memory
Temporary data storage
### State
A process usually hops between different states.
## Threads
A threads is a lightweight unit of execution. It shares various memory parts and instructions with the process.
- Serial
	- One process is running; it serves one user after the other sequentially. New users are enqueued.
- Parallel
	- One process is running; it creates a thread to serve every new user. New users are only enqueued after the maximum number of running threads is reached.