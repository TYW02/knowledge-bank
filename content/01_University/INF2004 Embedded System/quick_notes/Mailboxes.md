> [!Definition]
> Kernel object used for inter-task communication and synchronization, acting like a small holding box where tasks or ISR can deposit and read a single message or pointer

^5cbdff



## How it Works
- Pointer-Sized Buffer: Store a **single pointer** or a **fixed-size value** (Memory address of a data structure) **rather** than copying **heavy chunks** of data
- Blocking Semantics: If a task tries to **read** from an **empty mailbox**, it enters a **blocked** or pending state until **another task** posts a message or a set **timeout expires**
- Task Synchronization: Mailboxes **naturally synchronize** producer and consumer tasks, forcing the consumer to wait until **new data is posted**.
























































