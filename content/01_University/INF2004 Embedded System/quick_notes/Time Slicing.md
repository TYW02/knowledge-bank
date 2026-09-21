> [!Definition]
> Technique used by operating systems to **divide CPU time** into **small**, **fixed intervals** so multiple tasks can share a **single processor**


## How Time Slicing Works
- Task Rotation: OS assigns each process or thread a **short duration** to run, usually lasting between 10 to 100 milliseconds
- Preemption: When a task's time **slice expires**, a **hardware timer** interrupts the CPU, and the scheduler forces the task to **pause**
- Context Switching: OS saves the **current** task's **state** and **loads** the **next** task's state from **memory**
- Illusion of Concurrency: By switching between tasks rapidly, the system creates the **smooth illusion** that multiple programs are running at the same time on a single core.


## Benefit and Trade-offs
- Fairness: Prevents any single program from **hogging** the processor and ensure every active task **makes progress**
- Responsiveness: Keeps interactive applications **responsive** to user input
- Too Short Slices: If time slice is **too small**, the system spends too much time to context-switching **overhead** rather than actual computing
- Too Long Slices: If the time slice is too large, interactive tasks start to feel **sluggish** and lose quick responsiveness.





































