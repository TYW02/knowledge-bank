
# What is Tasks
> [!Definition]
> Independent, self-contained unit of execution that performs a specific job.
> 
> Similar to a thread 

## Key Characteristics of RTOS Tasks
- Independent Function: Written as a continuous C function that typically runs in an infinite loop **without ever exiting**
- Dedicated Stack: Each task has its own private stack memory to store local variables and function call histories
- Assigned Priority: Every task is given a **priority level**, which tells the RTOS scheduler how **urgent** its job is compared to other tasks.
- Task State: Tasks shift dynamically between states like **Running** (Using CPU), **Ready** (Waiting for CPU), and **Blocked/Waiting** (Waiting for a delay or an event)


## How RTOS Tasks Work
- The scheduler: Internal kernel component that decides **which task** gets to **run on the CPU** at any given millisecond
- Preemption: If a **high-priority task** becomes **ready** (sensor triggered an event), RTOS will **instantly pause** (Preempt) the **current running lower-priority** task to handle the **critical one immediately**
- Multi-tasking: By **switching rapidly** between tasks, the RTOS gives the **illusion** that multiple operations are happening at the **exact same time**.

