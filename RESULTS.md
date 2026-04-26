The user-level threading system uses a fixed thread table where each thread has its own stack, state, and saved context. The main thread starts as RUNNING, while others are initially FREE.

thread_create() allocates a stack and sets up thread_stub, which runs the function and marks the thread as ZOMBIE when done. uswtch() handles context switching by saving and restoring thread contexts.

Scheduling is cooperative and round-robin via thread_yield(), which switches to the next RUNNABLE thread. thread_join() waits for completion, then frees the thread’s resources.

Overall, the system implements user-level threads using manual context switching and cooperative scheduling without kernel support.
