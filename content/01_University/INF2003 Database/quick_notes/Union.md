
## Without ALL
> Duplicate rows are removed from the result set because it performs a standard set operation


## Union vs Union ALL
| Feature    | UNION                        | UNION ALL             |
| ---------- | ---------------------------- | --------------------- |
| Duplicates | Removed                      | Retained              |
| Efficiency | Slower (Sorting / Filtering) | Faster (Direct Merge) |
| Logic      | Set Operation                | Multiset Operation    |