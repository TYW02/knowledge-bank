
## View WITH CHECK OPTION
> Any INSERT or UPDATE through the view is rejected if the new data violates the view's WHERE clause.


## View VS Table
| Feature     | View                         | Table                   |
| ----------- | ---------------------------- | ----------------------- |
| Storage     | Virtual (Query ONLY)         | Physical (Data on disk) |
| Freshness   | Always reflects current data | Persists until modified |
| Performance | Re-runs query each time      | Direct read of rows     |

## Multiple table updates
> The update is typically rejected unless specific strict conditions for 'updatable views' are met.

