Pydantic Models are used to define and enforce data structure for API requests and response.

### Example
```python
# model.py
from pydantic import BaseModel

class NewItem(BaseModel):
	name: str
	quantity: int
	price: float
	
class UpdateQuantity(BaseModel):
	quantity: int
```

# Using Pydantic Model in FastAPI 
```python
from fastapi import FastAPI, status
import query
import model

app = FastAPI()

@app.post("/inventory", status_code = status.HTTP_201_CREATED)
def post_inventory(data: NewItem):
	return query.add_item(data)
	
@app.patch("/inventory/{item_id}")
def update_inventory(item_id: int, data: UpdateQuantity):
	return query.update_quantity(item_id, data)
	
@app.delete("/inventory/{item_id}")
def delete_inventory(item_id: int):
	return query.delete_item(item_id)
```

> [!NOTE]
> You should return a 201 code when you successfully send a post request instead of a 200 status code.
> More status code can be found [here](https://fastapi.tiangolo.com/reference/status/)
> 
> Path parameters pattern Rule of thumb: **identifiers go in the path, filters go in query params, data being written goes in the body.**


