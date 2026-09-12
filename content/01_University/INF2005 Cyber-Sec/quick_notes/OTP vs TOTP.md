
> TOTP -> Time-based One-Time Password

| Feature      | Random OTP                | TOTP                 |
| ------------ | ------------------------- | -------------------- |
| Storage      | Stored in server DB/Cache | Not Stored on server |
| Regeneration | Not possible              | Always possible      |
| Components   | Random generation         | Time-based component |

## Stateless TOTP vs Stateful OTP
> No OTP codes need to be stored on the server because they are recomputed on demand.


## Clock Drift
> [!Note]
> The TOTP system checks the code against a valid time window. To handle clock drift
> ```
> [T - 1], [T], [T + 1]
> ```

