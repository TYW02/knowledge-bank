| Feature   | General Purpose    | RTC                | WDT                |
| :-------- | :----------------- | :----------------- | :----------------- |
| Main Goal | PWM/Delays/Capture | Human Time (Y/M/D) | System Safety      |
| Clocking  | System clock       | Low-power domain   | Independent source |
| Recovery  | Interrupt/Flag     | Battery backup     | Hardware Reboot    |

## Track time while main power is disconnected
> Use a Real-Time Clock (RTC), run it on a separate ultra-low-power domain powered by a coin cell battery.

