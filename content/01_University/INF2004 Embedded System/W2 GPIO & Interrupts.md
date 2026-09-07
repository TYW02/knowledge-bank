---
title: W2 GPIO & Interrupts
tags:
  - GPIO
  - Interrupt
---
# What is a GPIO
General Purpose Input Output (Configurable digital signal pin, whose behavior and direction are controlled by software)


> GPIO carries 1 digital state per pin
> External State (Voltage) -> GPIO PIN 0 or 1 (Logical Level) -> Application Meaning (Pressed ? Ready ?)


An external circuit (sensor) senses data and sends it to MCU input.
The MCU output then drives the external load (Actuators)

## Fundamental Electronics
![[Pasted image 20260907185618.png]]
- Every pin has a high and low range, anything that is outside of this range can result in unexpected behaviors.

> [!NOTE]
> When connecting different GPIO pins make sure to share a COMMON GND, so both pins know what is the baseline GND value / what is 0

## Pull-up
![[Pasted image 20260907185816.png]]

> [!Pull-up]
> Whenever the button is **NOT pressed**, the GPIO will give off a `1` signal.
> And when it is **PRESSED** it will give off a `0` signal.
> This is also called `Active-low`

## Pull-Down
![[Pasted image 20260907185952.png]]

> [!Pull-Down]
> When button is **NOT** pressed, signal is `0`
> When button is **PRESSED**, signal is `1`
> This is also called `Active-High`

> [!NOTE]
> If you are trying to get something to switch on and you give off a `1` signal.
> DO NOT use that raw signal to power that device, let another power supply power it instead.


![[Pasted image 20260907190301.png]]

> [!Formula]
> I = V/R.
> You should always have a resistor even for a small LED as the power can fluctuate and that might end up shorting the LED.


# GPIO Configuration
A GPIO pin can support many outputs, FIRST you must select 1 output owner for 1 pin.
(UART/ SPI / PWM, PIO)

## Changing only 1 bit

| 1   | 0   | 1   | 0   | 0   | 1   | 0   | 1   |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0   | 0   | 0   | 0   | 1   | 0   | 0   | 0   |
| 1   | 0   | 1   | 0   | 1   | 1   | 0   | 1   |
> 0xA5 | 0x08 = 0xAD


| Intent       | Expression   | Other Bits  |
| ------------ | ------------ | ----------- |
| Set bit 3    | OUT \|= Mask | Preserved   |
| Clear Bit 3  | OUT &= ~mask | Preserved   |
| Toggle Bit 3 | OUT ^= mask  | Preserved   |
| Replace Port | OUT = mask   | Overwritten |

## Configuring GPIO
> Identify (Pin + Function) -> Preload (Safe Output Level) -> Enable (Output Driver) -> Verify (Read / Measure)

```C
/* OUTPUT: GP15 */
gpio_init(15);
gpio_put(15, 0); // Sets GP15 to 0 or LOW
gpio_set_dir(15, GPIO_OUT); // Sets to output

/* Input: GP2 */
gpio_init(2);
gpio_set_dir(2, GPIO_IN); // Set to input
gpio_pull_up(2); // Set to pull-up / Active-low
```


## Convert electrical level into meaning
| BUTTON   | RAW INPUT | LED OUTPUT |
| -------- | --------- | ---------- |
| Released | 1         | 0 -> Off   |
| Pressed  | 0         | 1 -> On    |
```C
pressed = (button.value() == 0)
led.value(1 if pressed else 0)
```

![[Pasted image 20260907191237.png]]
- User can press button multiple times at once and that can produce many edges, before settling at a value

## Debouncing
![[Pasted image 20260907191327.png]]

> When pressed start timer, if the signal is stable for x amount of time, then process the event.


![[Pasted image 20260907191458.png]]


# What is Programmable I/O (PIO)
- Enables creation of custom hardware interfaces from scratch, including completely novel protocols
- An instance operates as a tiny, independent "Processor" running completely separately from the main core.

## PIO Instructions
- in()
- out()
- push()
- pull()
- mov()
- irq()
- wait()
- jmp()
- set()

## How to use PIO
> - Select PIO0 or PIO1 and claim an unused state machine.
> - Configure: Load the program, map its GPIO pins, and choose a divided clock
> - Run: Enabled the state machine. It controls the pins while main() continues.
> The CPU configures PIO -> PIO runs independently


### Simple PIO Example
```pio
.program blink
.wrap_target
	set pins, 1 [19]
	nop         [19]
	nop         [19]
	nop         [19]
	nop         [19]
	set pins, 0 [19]
	nop         [19]
	nop         [19]
	nop         [19]
	nop         [19]
.wrap
```

## Host-side setup
1. Claim an unused state machine
2. Load `blink.pio`
3. Map GPIO 25 and set 2 kHz
4. Enable the state machine

> The PIO loop now produces 100 cycles HIGH and 100 cycles LOW:
> A 10 Hz waveform
> main() can sleep while the LED keeps blinking.



# Polling discovers events when you ask
![[Pasted image 20260907193149.png]]
- In this case, since the event does not happen during a polling check, we miss the event and nothing happens

## Polling vs Interrupt
![[Pasted image 20260907193238.png]]

> [!Utilisation Polling]
> Utilisation = $c / p$
> c = CPU time taken to handle an event
> p = polling period

> [!Utilisation Interrupt]
> Utilisation = $(h + c) / T$
> h = Hardware response time
> T = Time between events occuring

- Usually you would use Polling if the interrupts are **consistent** and **predictable**
- Interrupts are better for **random**, **sporadic** interrupts which is what is usually seen in the real world


| Poll                    | Interrupt                           | DMA + Interrupt             |
| ----------------------- | ----------------------------------- | --------------------------- |
| Ask Repeatedly          | React to an event                   | React to a completed block  |
| Short, Predictable Wait | Sporadic / time-sensitive event     | Sustained data stream       |
| Simple Control Flow     | Useful work or sleep between events | Lower per-item CPU overhead |

DMA = Direct Memory Access

## Interrupt Flow
![[Pasted image 20260907193710.png]]

- CPU doing main work
- Interrupt occurs, sends an Interrupt Request
- Creates entry in Interrupt Vector Table (IVT) with relevant information like priority
- If priority is high, Interrupt Service Routine will service that request
- Once handled, clear status, and return back to main work

## Source, Request, Handler
Source: Timer reaches a match
Interrupt Request: Request for attention
Interrupt Service Routine: Code handles the cause

## Types of Interrupt
- Something that interrupts the normal flow of program execution
- A signal that immediate action is needed
- For example:
	- Computer reset button
	- Over-pressure sensor in nuclear reactor
	- Deep Sleep Wake-up in Edge Nodes
	- A memory error, a floating point error
- Interrupts are good

> Run -> Respond -> Resume


## 3 gates decide whether an ISR can start
Source: Cause enabled (Signal that enables interrupt)
Controller: IRQ enabled 
CPU: Mask + Priority allow

If all 3 pass: ISR will start service

## RESET Button
A CPU runs a program by:
1. Read instruction from Program Counter (PC)
2. Execute instruction
3. Increment PC

- When you press RESET, it sets the PC to a new value
	- The reset vector in the interrupt vector table (IVT)

# Interrupt Vector Table (IVT)
![[Pasted image 20260907194749.png]]

- Code 'jumps' to a fixed location in the IVT when any interrupt occurs
- The programmer or OS puts instructions at each fixed vector location to handle the interrupt
- There is 1 interrupt service routine (ISR) for each kind of reset you want to handle
- ISRs itself can be located anywhere is memory

# Interrupt Process
- Before the CPU jumps to the IVT, it stores context (Current Program Counter, Status Register) and others
- This is so after the interrupt is serviced, it can restore context and return to where it left off.
- The place where PC, SR and others get stored to is a block of memory called the **stack**


# The Stack
- Area in RAM to store miscellaneous things for a while, then retrieve them
- CPU and **PUSH** onto the stack and MUST **POP** them off later
- The Stack Pointer (SP) is a register that indicated the address of the last item put into the stack

![[Pasted image 20260907195616.png]]



## Configure first, Enable last
![[Pasted image 20260907195647.png]]

1. Keep this source disabled
2. Set pin / timer / trigger mode
3. Install handler + initialise shared state
4. Clear stale status, set priority
5. Enable the intended source and route

# Writing ISR
- ISR code should be tiny, fast and efficient. It should affect the rest of the system as little as possible
- They can happen at any time
- Turn off (mask) interrupts you don't need, but some are non-maskable interrupts
- On exit from ISR, leave CPU in the same state as it was at entry (same context) 
- Before exit, Clear the interrupt flag (Otherwise it will be triggered again immediately)
- ISR uses global variables, you can't pass parameters to them
- Some process allow nested interrupts. Most use interrupt priorities for cases when they coincide

> [!NOTE]
> ISR should NOT have Infinite Loops, or `printf`


## Setup with Pico SDK
```C
static void uart0_isr(void) {  
	while (uart_is_readable(uart0)) {  
		uint8_t b = uart_getc(uart0);  
		ring_push(b);  
	}  
}  

uart_set_irq_enables(uart0, true, false); 
irq_set_exclusive_handler(UART0_IRQ, uart0_isr);  
irq_set_priority(UART0_IRQ, 0x40);  
irq_set_enabled(UART0_IRQ, true)
```

1. Prepare peripheral (Configure and clear stale status flag)
2. Install handler (Use exclusive handler, or a shared handler for multiplexed IRQ)
3. Enable the event (Allow peripheral to assert its IRQ line)
4. Enable the NVIC (`irq_set_enabeled()` affects the executing core)


![[Pasted image 20260907200437.png]]


# High Priority IRQ may Interrupt ISR
![[Pasted image 20260907200519.png]]


![[Pasted image 20260907200529.png]]
$ISR = f * c$

## ARM vs RISC-V
| Target                         | IRQ Control     | Handler Entry                   |
| ------------------------------ | --------------- | ------------------------------- |
| RP2040 Arm Cortex-M0+ (Pico 1) | NVIC (ARM)      | Vector table -> Handler         |
| RP235- Arm Cortex-M33 (Pico 2) | NVIC (ARM)      | Vector table -> Handler         |
| RP2350 Hazard3 RISC-V          | Xh3irq (RISC-V) | Trap entry -> Software dispatch |

# How to debug ISR
![[Pasted image 20260907200829.png]]
- You can use the GPIO LED to blink at different stages of the ISR
- Higher frequency of blinking at each later stage of ISR

# Interrupt Latency: Tail-Chaining
![[Pasted image 20260907200930.png]]
- Normally you will **push** the ISR 1 on the stack, resolve it then **pop** it
- Then **push** ISR 2, resolve it then **pop** it

BUT in Tail-Chaining
- You **push** both ISR 1 & 2, the **directly switch** from ISR 1 to ISR 2 (Tail-chaining) then **pop** them both



# Interrupt Latency: Late Arrival
![[Pasted image 20260907204846.png]]

## What happens when a higher priority comes later ?
- We push both ISR 1 & 2 onto the stack, then service ISR 1 first, then tail-chain ISR 2 and finally pop them off the stack

# Interrupt Source Catalogue: Time and Inputs
| Source Family            | Typical Cause                  | Example Use                           |
| ------------------------ | ------------------------------ | ------------------------------------- |
| GPIO / External IRQ      | Rising, falling, active level  | Buttons, Encoders, Sensor data-ready  |
| Timer / Counter          | Compare, overflow, capture     | Scheduling, timeouts, timestamps      |
| PWM                      | Wrap / Cycle Boundary / Fault  | Motor-Control updates, waveform steps |
| RTC / Low-Power Timer    | Alarm / Periodic Wake          | Scheduled wake-up, timekeeping        |
| ADC / Comparator / Touch | Result Ready, Threshold, touch | Measurement, threshold detection      |


# Interrupt Source Catalogue: Data and I/O

| Source Family         | Typical Cause                  | Example Use                       |
| --------------------- | ------------------------------ | --------------------------------- |
| UART / Serial         | RX, TX Space, Framing Error    | Console, GPS, device links        |
| SPI / $I^{2}C$        | FIFO, completion, bus error    | Sensors, Memories, Displays       |
| USB / CAN / Ethernet  | Transfer / Packet / Bus Event  | Connectivity and Protocol Stacks  |
| DMA / Accelerators    | Block complete / Error         | Streaming data, checksum / crypto |
| PIO / Storage / Radio | FIFO, Custom Event, Completion | Custom interfaces, buffered I/O   |

# System Events also change control flow

| Source Family             | Purpose                         | Key Distinction                       |
| ------------------------- | ------------------------------- | ------------------------------------- |
| Software / Inter-core IRQ | Notify another context / core   | Often used with queues or mailboxes   |
| OS tick / timer           | Scheduling and timeouts         | Peripheral or core-local timer        |
| Power / Clock / NMI       | Wake or urgent system condition | Special enable/masking rules          |
| Fault / SVC / ecall       | Error handling / system service | Synchronous exception, not an I/O IRQ |
| Reset / Watchdog          | Recover or restart execution    | Usually not the normal return path    |











