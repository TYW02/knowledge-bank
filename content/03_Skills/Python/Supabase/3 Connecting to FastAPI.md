---
tags:
  - FastAPI
---
This is where you expose your data layer as an API so a frontend or another service can consume it.

### Example
```
GET /inventory   -> returns all items
GET /inventory/low-stock   -> returns items below a threshold
POST /inventory   -> adds a new item
```
Using FastAPI, your Supabase functions are already written. Now we just need to wrap them in HTTP endpoints.

```python
from fastapi import FastAPI
import query

app = FastAPI()

@app.get("/inventory")
def get_inventory():
	return query.get_all_inventory()
```

> [!NOTE]
> Remember "What does this function actually return to the caller?"
> You HAVE to return something here else FastAPI will return `null` to every client that hits this endpoint.

