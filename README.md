# Process scoped shared memory mutex

This is an example repository to demonstrate how to use process-scoped mutexes and shared memory in tandem to achieve inter process communication.

The binary generated from this C++ program, operates as follows:
1. Recursively spawns a hierarchy child processes. 
2. Each child process spawns 1 to 3 children.
3. Without any communication, the growth is unbounded. 
4. A shared segment of memory, to count the number of total processes.
5. Additionally, a pthread mutex with the `PTHREAD_PROCESS_SHARED` attribute is also allocated into shared memory.
6. Before spawning new child processes, each process consults this mutex, and spawns children only if the counter does not 
exceed a predefined ceiling.

# Running the program
Run `make` to create the binary and `make clean` to clean build artifacts.

# Caveats and warnings
1. Careful to tweak the program. The unbounded process growth can literally bring down the system to a halt.
2. Note the system value of maximum memory that can be segmented into shared space. If this value is exceeded, the `shmget` syscall fails with
`No space left on device`.

# License 
MIT