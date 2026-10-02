
- Writing a `1` to a GPIO configured as an output **drives** the pin to a **high** voltage level


- Writing a `0` to a GPIO as an output drives the pin towards **Ground** because the internal transistors pull the output voltage down to the reference 0V level.


## Which Register is responsible for whether a pin acts as input or output ?
- The **Direction** or **Output Enable** (DIR/OE) Register

> This register controls the **internal drivers** to determine if the pin is **driven** by the internal latch or **sampled** by the input buffer.


## Handshake

### Purpose of ACK
- To **confirm** that the **data** has been successfully **captured**

> The **ACK** signal **completes** the handshake, informing the sender that it can **stop holding** the **current data** and **prepare** the **next set**.


## Masking
```C
(1u << 3)
```

> [!Note]
> This equals 0x08 because shift 1 left by 3 gives us 1000 which is 8 in hexadecimal


