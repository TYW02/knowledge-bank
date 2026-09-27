
## What does it do
> [!Note] `volatile`
> `volatile` **does prevent** the compiler from **optimizing away repeated reads/writes**, BUT `volatile` says **nothing about atomicity**. A read-modify-write like `count++` is still **multiple machine instructions**, and an ISR **can interrupt** between them, **corrupting the result**. You still need masking, atomic ops, or an RTOS primitive for that.

























