
## Overflow
- Triggered when timer's counter register reaches its maximum capacity and rolls back to `0`

## Underflow
- Triggered in countdown mode when decrementing timer reaches `0` or its bottom limit before wrapping back to the maximum value

## Capture
- Triggered when external input pin detects a specific signal transition (Rising edge OR Falling edge), forcing the current counter value to be copied into a capture register


## Watchdog Purpose
- To recover or restart execution if the system hangs or fails to respond.

