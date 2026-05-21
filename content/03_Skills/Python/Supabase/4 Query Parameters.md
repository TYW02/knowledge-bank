When you declare other function parameters that are not part of the path parameters, they are automatically interpreted as "query" parameters.

```python
@app.get("/inventory/low-stock")
def get_low_stock(threshold: int = 0):
	return query.get_less_than_inventory(threshold)
```

The query is the set of key-value pairs that go after the `?` in the URL, separated by `&` characters.

> [!NOTE]
> In this example, the URL will be: https://127.0.0.1:8000/inventory/low-stock/?threshold=3
> [Documentation](https://fastapi.tiangolo.com/tutorial/query-params/)

