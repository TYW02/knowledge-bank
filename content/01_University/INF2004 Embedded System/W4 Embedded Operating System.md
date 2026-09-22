---
title: W4 Embedded Operating Sytem
---
# Real-Time = Predictable

- The correctness depends on both the **computed result** and **WHEN** it is **delivered**
- Deadline may be **hard**, **soft**, or **none**; the consequence of lateness differs
- **Worst-case latency** and **bounded blocking** matter more than **average throughput**
- RTOS provides mechanisms
- Application designer proves timing assumptions

## RTOS makes Concurrency & Timing Explicit
- Split work into [[RTOS Tasks#What is Tasks|Tasks]]
- Wait instead of Polling
- Protect Shared Resources
- Use Kernel Messaging
- Control Timing


# 6 Time-Critical Kernel Services

## Task Management
> Execution of "parallel" tasks on a processor by **scheduling them** to ensure **fairness** in **sharing** the resources.

## Device I/O Management
> Embedded system comprises of **various components** other than CPU and memory that needs to be **managed** by the OS as a resource.


## Interrupt & Event Handling
> Managing and servicing **real-time events**

## Synchronization & Communication
> Task **synchronization** (Critical sections, semaphores, monitors, mutual exclusion)
> 
> Inter-task **communication** (Queuing of request)


## Memory Management
> Critical component in RTOS to ensure the device works **indefinitely** without needing a **reboot** (e.g. *memory leaks*, *memory fragmentation*)

## Timer Management
> Support of real-time clocks, timers, delays, etc




# microT-Kernel 3.0 API

### Example
```C
// C API: tk_<operation>_<object>

tk_cre_tsk // Create a task
tk_wai_sem // Wait for tokens
tk_loc_mtx // Lock a mutex
tk_snd_mbf // Send copied data
```


## A TASK repeatedly waits and works

- A function runs when **called**
- A task runs **independently** 
- A task waits when **idle**
- An event makes the task **ready again**

![[Pasted image 20260921191952.png]]


## Task States
- Task goes through several states during its life in a multitasking system
- Tasks are moved from 1 state to another in response to the stimuli marked on the arrow

![[RTOS Tasks#Key Characteristics of RTOS Tasks]]

![[Pasted image 20260921192116.png]]


## Preemptive Scheduling
- Higher priority task becomes **READY** after an interrupt, signal or message
- Scheduler preempts the lower-priority running tasks
- Within equal priorities, an implementation may use FIFO or [[Time Slicing#How Time Slicing Works|Time Slicing]]
- Priority assignment encodes urgency, not "importance" in a human sense

## Context Switch MUST have a bounded cost
![[Pasted image 20260921193318.png]]

![[Time Slicing#Benefit and Trade-offs]]



# Interleaving turns SHARED RESOURCE into a race
![[Pasted image 20260921193357.png]]

![[Interleaving#How it Works|How it Works]]


# Critical Sections must be short
![[Pasted image 20260921193842.png]]

![[Critical Sections in RTOS#Golden Rules for RTOS Critical Sections]]


# SEMAPHORE represents countable availability

![[Semaphore#^ca9f3f]]

![[Pasted image 20260921194449.png]]

![[Semaphore#Core Operations]]

![[Pasted image 20260921195202.png]]


# Mutex 
![[Mutex#^184c1f]]

![[Pasted image 20260921195259.png]]

![[Pasted image 20260921200459.png]]


![[Mutex#Key Concepts of Mutex]]


![[Pasted image 20260921202552.png]]

> [!Definition]
> Individual bits grouped into a variable (often 24 to 32 bits wide) used to synchronize tasks and signal whether specific events have occurred.


## How Event Flag Work
- Bit representation: Each bit in the event group **corresponds** to a **unique** boolean **flag** (1 for occurred, 0 for not occurred)
- Setting Flag: Any **task** or **ISR** can set or **clear** individual bits using **logical operations** like OR or AND
- Waiting for Flags: A task can **pend** (enter the BLOCKED state without consuming CPU cycles) until a **specific condition is met**
- Clearing flags: Upon waking up, the task can automatically or manually **clear the flag** so the system is ready for the next occurrence.


![[Pasted image 20260921202959.png]]

> [!Definition]
> Designed to pass variable-length, discrete messages between tasks or between an ISR and a task


![[Pasted image 20260921203004.png]]

![[Mailboxes]]



![[Pasted image 20260921203011.png]]


![[Pasted image 20260921204130.png]]

[[Time Services|Link to Time Services]]





![[Pasted image 20260921205004.png]]


![[Pasted image 20260921205013.png]]

[[Fixed Pools in RTOS|Link to Fixed Pools]]


![[Pasted image 20260921205021.png]]

![[Pasted image 20260921205026.png]]



















