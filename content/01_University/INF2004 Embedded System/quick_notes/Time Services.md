> [!Definition]
> Foundational timing mechanisms that provide determinism, task scheduling, delays and timeouts

^a39347


# Delay Service (Task Delays)

## What it is
A service that pauses the currently executing task for a specific duration of time

## Mechanism
The calling tasks transitions from the **RUNNING** state to the **WAITING** (or blocked) state. It remains blocked until the requested number of system ticks has elapsed

## Best used for
Giving other tasks CPU time, debouncing switches, or creating simple pacing inside a specific task loop 

# Cyclic Handlers (Periodic Execution)

## What it is
A time-activated management object used to execute a specific function or trigger a task at regular, repeating intervals.

## Mechanism
Kernel automatically manages the period. Once started, it counts down, executes the designated handler when it hits zero, resets itself to the defined interval, and repeats indefinitely until stopped

## Best used for
Regular periodic operations like polling sensors, updating a display at a set frame rate, or running PID control loops

# Alarm Handlers(One-shot Timers)

## What it is
Time-activated management object used to execute a specific function exactly **once** after a designated time interval

## Mechanism
Acts as a one-shot countdown timer. You set the alarm, it counts down, executes the handler function exactly once when the time expires, and then enters an inactive state

## Best used for 
Handling system timeouts, implementing watchdog features, or scheduling a single future event


















































