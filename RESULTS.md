# Results

Implemented cooperative user-level threads and a simple mutex in xv6 user space.

Context switching
- Fixed thread table with states FREE, RUNNABLE, RUNNING, ZOMBIE.
- thread_create allocates a 4 KB stack and initializes context to start at thread_stub.
- thread_stub runs fn(arg), marks ZOMBIE, then yields.
- uswtch saves/restores thread context during switches.

Scheduling and join
- Cooperative round-robin via thread_yield.
- thread_join yields until target is ZOMBIE, then frees its stack and resets slot state.

Mutex and demo
- mutex_lock cooperatively spins with thread_yield; mutex_unlock clears lock.
- test_pc uses 2 producers + 1 consumer on a bounded buffer protected by the mutex.
- Run completes with final done message, indicating no deadlock and consistent buffer updates.

Limitations
- Max threads: 16 total (including main).
- Stack size: 4096 bytes per thread.
- Non-preemptive scheduling; fairness depends on explicit yields.
- Mutex has no queueing/ownership checks.
