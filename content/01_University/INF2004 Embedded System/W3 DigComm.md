---
title: W3 DigComm
---
##### Link to PDF
[[W3.1 DigComm.pdf|Click here]]

# Hardware Constraint

## Parallel Communication 
- Multiple dedicated wires
- Sends multiple bits simultaneously
- Extremely fast

![[Pasted image 20260913154916.png]]


## Serial Communication
- Vastly reduced physical footprint
- Sends bits sequentially over a single data line
- Universal standard for chip-to-chip comms

![[Pasted image 20260913154925.png]]


# 3 Core Variables
> Every specific serial protocol is simply a unique combination of 3 fundamental engineering choices

## Timing

### Synchronous
Device share a dedicated physical **Clock Wire (SCLK)**. The receiver exactly knows when to read the data line because it watches for the clock line to transition.
![[Pasted image 20260913155127.png]]

### Asynchronous
**No shared clock line**. Both devices must be pre-configured to the exact same speed (Baud rate). Uses "Start" and "Stop" bits wrapped around the payload
![[Pasted image 20260913155303.png]]


## Direction of Data Flow

### Simplex
> Strict one-way street. Data only ever flows from the transmitter to the receiver

### Half-Duplex
> Two-way street, but only 1 device can talk at a time over a shared line.

### Full-Duplex
> Simultaneous two-way communication. Requires dedicated TX and RX lines


## Topology

### Point-to-Point
> Direct dedicated 1-to-1 connection. Simple and secure, but doesn't scale well if you need to connect many devices to a single microcontroller

### Bus (Multi-drop)
> 1 controller communicates with multiple Peripherals on shared wires. Requires hardware selection pins or software addressing to route messages correctly.



# UART: Configuration & Purpose

## Configuration
- Timing: Asynchronous
- Direction: Full-Duplex (Usually)
- Topology: Point-to-Point
- Typical Speed: 9.6kbps - 115.2 kbps

Universal Asynchronous Receiver-Transmitter is not technically a protocol, but a physical circuit in microcontroller that translates data between parallel and serial forms.

### Why choose UART ?
- **Minimalism**: 2 wires (TX & RX) are the bare minimum needed for 2 devices to talk back and forth simultaneously. By dropping the clock wire, you save a physical pin on the microcontroller

- **Real-World Uses**: Because it operates at slower, reliable speeds without a clock, it's perfect for Legacy sensor (GPS, RFID) Bluetooth modules, and simple debug consoles.


### UART: How it Works
- Because there is no clock wire to keep synchronized, both the sender and receiver must be **pre-configured** to talk at the exact same speed (**Baud Rate**).

- Devices are cross-wired: TX connects to RX
![[Pasted image 20260913160936.png]]


# Baud Rate Calculation for UART
![[Pasted image 20260913161025.png]]


## UART: Variation & Consideration

### Flow Control
> What happens if Device A sends data faster than Device B can process it? **Buffer Overflow**

#### Hardware Flow Control
> Adds 2 extra wires (RTS - Request to Send, CTS - Clear to Send) so **device can pause** each other

#### Software Flow Control
> Sends **special characters** (XON/XOFF) inside the data stream to **pause/resume** transmission without extra wires.

### Distance vs Noise (RS-232 / RS-485)
> Standard UART uses TTL logic levels (OV and 3.3V/5V), which are highly susceptible to electrical noise over long cables.

#### RS-232
- Uses **higher voltage swings** (-15V to +15V) to increase range
#### RS-485
Converts the UART signal into **differential signaling** over twisted pairs, allowing communication over thousands of feet in **noisy industrial environments**.

![[Pasted image 20260913161734.png]]


# SPI: Configuration & Purpose

## The Configuration
- Timing: Synchronous
- Direction: Full-Duplex
- Topology: Bus (Single-Master, Multi-Slave)
- Typical Speed: 10 MHz - 50+ MHz

> SPI (Serial Peripheral Interface) was developed by Motorola in the 1980s as a high-speed backbone for embedded systems.

## Why choose SPI ?

### Raw Speed
> Because it has a dedicated clock line and push-pull drivers, massive amounts of data can flow continuously. The separate transmit and receive lines mean data flows both ways simultaneously.

### Real-World Uses
> Applications requiring enormous data pipelines like high-resolution LCDs, OLED displays, SD cards, and fast ADCs (Analog-to-Digital Converters)


## SPI: How it Works
![[Pasted image 20260913162244.png]]


## SPI Modes

### Clock Polarity and Phase (CPOL / CPHA)
> Because there is no universal standard for SPI, manufacturers design chips differently.
> 
> You must configure the Master to match the Slave's expected behaviour
> - CPOL (Polarity): Is the clock line idling HIGH (1) or LOW (0) when nothing is being sent?
> - CPHA (Phase): Is data captured on the first edge (transition) of the clock, or the second edge ?
> This creates 4 distinct "SPI Modes" (Mode 0, 1, 2, 3).

![[Pasted image 20260913162723.png]]


# I^2C: Configuration & Purpose

## The Configuration
- Timing: Synchronous
- Direction: Half-Duplex
- Topology: Bus (Multi-Master, Multi-Slave)
- Typical Speed: 100 kHz (Standard) - 400 kHz (Fast)

> I2C (Inter-Integrated Circuit) was invented by Philips Semiconductor to allow multiple chips on a TV board to communicate easily.

## Why choose I2C ?

### Pin Conservation
> You can connect over 100 devices to a microcontroller using exactly 2 wires (SCL & SDA). No dedicated Chip Select pins are required

### Real-World Uses
> Because physical pull-up resistors limit the switching speed, it's perfect for low-bandwidth sensors that don't need to send much data (Temperature, humidity, accelerometers), and Real Time Clocks (RTCs)

## I2C: How it Works
![[Pasted image 20260913163354.png]]

## Advanced Concepts

### Clock Stretching
> Usually, the Master controls the clock (SCL) entirely. However, if a Slave is too slow to process the data the Slave can physically hold the SCL line LOW

> The Master will see the clock line is low and wait. Once the Slave is ready, it releases the SCL line, it floats back HIGH via the pull-up resistor, and the Master Resumes generating the clock. This allows slow devices to pause fast masters.

### Multi-Master Arbitration
> What if 2 Masters try to talk on the bus at the exact same time ?

> Because the lines are open-drain, pulling a line LOW always wins over letting it float HIGH. Both masters monitor the SDA line as they transmit.
> 
> If Master A tries to send a '1' (Letting it float HIGH), but sees the line go LOW, it knows Master B is transmitting a '0'. Master A instantly backs off and lets Master B finish.

![[Pasted image 20260913164348.png]]

# Protocol Selection: Speed vs Application

![[Pasted image 20260913164433.png]]

![[Pasted image 20260913164448.png]]






































