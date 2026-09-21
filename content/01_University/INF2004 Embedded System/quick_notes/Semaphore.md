
> [!Definition]
> Kernel-managed integer variable used to synchronize tasks and control access to shared resources using atomic operations (Uninterruptible actions)

^ca9f3f


## Core Operations
- Take / Pend / Wait: **Decrement** the semaphore value. If the value is zero, the calling task **blocks** (suspends execution) until **another task** or **interrupt** makes the semaphore **available**
- Give / Post / Signal: **Increments** the semaphore value. This **wakes up** any task waiting for the semaphore


## Key Characteristics
- No Ownership: Unlike Mutex, semaphore has **NO concept of ownership**. Any task or Interrupt Service Routine can "**Give**" a semaphore, and any task can "**take**" it
- Use Mutexes for Shared Memory: Semaphore lack ownership, using them for protecting critical sections can lead to **priority inversion** or **accidental unlocking** by the wrong tasks. Use Mutex when you need **strict mutual exclusion** for a shared variable or peripheral
- Use Semaphore for Signaling: Semaphore excel at **event notification**, synchronization, and producer-consumer queue coordination























































