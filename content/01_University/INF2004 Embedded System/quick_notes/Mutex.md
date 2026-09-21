> [!Definition]
> Synchronization primitive used to protect shared resources from simultaneous access by multiple tasks.
> 
> Acts like a unique locking key, only the task holding the key can access the resource, preventing data corruption and race condition

^184c1f

## Key Concepts of Mutex
- Strict Ownership: Enforces strict ownership. The tasks that locks (**takes**) the mutex **MUST** be the same tasks that **unlocks** (gives) it
- Priority Inheritance: This **MOST** crucial feature of mutex. If **high priority** task gets **blocked** **waiting** for a mutex held by **low-priority task**, RTOS **temporarily elevates** the low-priority task's priority. This **prevents medium-priority** tasks from preempting it
- Task-only scope: Mutex are designed for use **between tasks** and **CANNOT** be used inside ISR because interrupts cannot block to wait for a lock





















































