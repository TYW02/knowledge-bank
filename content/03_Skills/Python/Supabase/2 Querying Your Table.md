Let's say you have an **inventory** table with columns, `id`, `name`, `quantity`, `price`

In `query.py`
```python
from db import supabase

def get_all_items():
    response = supabase.table("inventory").select("*").execute()
    return response.data  # This is a list of dicts

def get_low_stock(threshold: int):
    response = (
        supabase.table("inventory")
        .select("name, quantity")
        .lt("quantity", threshold)   # lt = less than
        .execute()
    )
    return response.data

# Run it
items = get_all_items()
for item in items:
    print(item["name"], "-", item["quantity"])
```

>[!NOTE]
>The client uses a query builder pattern, you chain methods that build up a query, then `.execute()` fires it. Each method maps to a SQL concept
>[Documentation](https://supabase.com/docs/reference/python/introduction)


# Small But Important Issues

### Wrong return type on errors
```python
# You returned [] on count errors
def get_total_inventory_count():
    except Exception as e:
        return []  # ❌ This function should return a number, not a list
```
When a function promises to return one type, it should **always** return that type. Returning `[]` from a count function will silently break any code that does math on the result.

Fixed:
```python
# Correct
except Exception as e:
    print(f"Database Error: {e}")
    return 0  # ✓ Consistent with what the function promises
```

### No Type Hints
```python
# What you wrote
def add_item(name, quantity, price):

# What it should be
def add_item(name: str, quantity: int, price: float):
```
Type hints are documentation. They tell the next developer exactly what this function expects

### Return Meaningful Signals
```python
# Fragile — caller can't tell success from empty result
result = add_item("Bolt", 100, 0.50)
if result:  # What does this actually mean?
    ...
```
Right now, the write functions return `response.data` on success and `[]` on failure. That makes it hard for calling code to know if something actually worked.

A cleaner pattern used in real apps:
```python
def add_item(name: str, quantity: int, price: float):
    try:
        response = (
            supabase.table("inventory")
            .insert({"name": name, "quantity": quantity, "price": price})
            .execute()
        )
        return {"success": True, "data": response.data}
    except Exception as e:
        print(f"Error inserting: {e}")
        return {"success": False, "error": str(e)}
```

This way you can call code by doing this:
```python
result = add_item("Bolt", 100, 0.50)
if result["success"]:
    print("Item added:", result["data"])
else:
    print("Failed:", result["error"])
```

