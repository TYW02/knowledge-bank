
> A masked interrupt is a hardware interrupt signal that the processor temporarily ignore or disables because its interrupt mask bit is turned on.

- You mask an interrupt when you want it to be ignored (Permanently or temporarily)


> When the CPU accepts and jumps into a higher-priority Interrupt Service Routine, the hardware automatically updates an internal register tracking the Current Execution Priority.
> 
> Once, this level is set, the hardware automatically blocks or "Masks" any incoming interrupt whose priority number is equal to or lower than the currently running ISR.

> [!Note]
> You can also use a Non-Maskable Interrupt (NMI) or the highest priority hardware IRQ to ensure code executes instantly regardless of the main program state.

