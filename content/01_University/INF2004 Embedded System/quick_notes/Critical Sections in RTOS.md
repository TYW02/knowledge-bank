> [!Definition]
> Block of code that accesses **shared resources** (Global variables, hardware peripherals, shared memory buffers) and must **execute atomically**.



# Golden Rules for RTOS Critical Sections
- Keep them ultra short: A **long** critical section with interrupts disabled **destroys** the "real time" responsiveness of an RTOS
- Never block inside a critical section: **NEVER** call an RTOS API function that can **block or force a context switch** while inside an interrupt-disabled critical section. This can **LOCK UP** the entire system
- Match entry and exit: Every entrance to a critical section must have a **guaranteed exit path**. Be exceptionally careful with early `return` statements or conditional `break` loops that might accidentally bypass the unlock sequence

























































