

# Defining Database

```python
from sqlalchemy import Column, Integer, String, Float, DateTime, create_engine

from sqlalchemy.ext.declarative import declarative_base

from sqlalchemy.orm import sessionmaker

  

engine = create_engine('sqlite:///database.db', echo=True, connect_args={"check_same_thread": False}) 

Base = declarative_base()

  

class Minimart(Base):

    __tablename__ = 'minimart'

  

    id = Column(Integer, primary_key=True)

    name = Column(String, nullable=False)

    price = Column(Float, nullable=False)

    exp_date = Column(DateTime)

    brand = Column(String, nullable=False)

    description = Column(String)

  

Base.metadata.create_all(engine)

  

SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

  

def get_db():

    db = SessionLocal()

    try:

        yield db

    finally:

        db.close()
```


# Getting information from DB
#HTTP-GET
```python
from sqlalchemy.orm import Session

from sqlalchemy import delete, update

from datetime import datetime

from typing import Optional

from . import models


def get_all_item(db: Session):

    return db.query(models.Minimart).all()
```


```python
class ItemCreate(BaseModel):

    id: int

    name: str

    price: float

    exp_date: Optional[datetime] = None

    brand: str

    description: Optional[str] = None

  
  

router = APIRouter()

  

@router.get("/get-all-item")

async def all_my_item(db: Session = Depends(get_db)):

    item = get_all_item(db)

    return item # This is a model instance
```



## Getting info in frontend and displaying
```jsx
  const fetchItem = async () => {

    setIsLoading(true)

    setError(null)

  

    try{

      const data = await makeRequest("get-all-item")

      setItem(Array.isArray(data) ? data : data.items || [])
		/*This checks if data is array else create an empty array */
    }

    catch(err) {

      console.log(err)

    }

    finally{

      setIsLoading(false)

    }

  }







<div className='display-container'>

            <button className='show-all-btn' onClick={fetchItem}>Show All</button>

            <div className='display-db'>

              {Array.isArray(item) && item.map((i, idx) => (

                <div key={idx}>

                  {i.id} <strong>{i.name}</strong> - ${i.price} - {i.brand} - {i.exp_date} - {i.description}

                </div>

              ))}

            </div>

        </div>
```


The map function here loops through the item array `i` contains the data (hence why you can `i.id` ...) when created and `idx` is the item's idx in the item array



# HTTP-GET Workflow

1. User clicks button and it runs {fetchItem}
2. fetchItem makes an API call to get-all-items
3. api runs get_all_item function in db
4. db returns list of all items
5. setItem updates with all items
6. item.map loops through all items in array
7. items is displayed by idx and item fields



# Searching for Information in DB
#HTTP-GET 

```python
def get_item(db: Session, id: int):

    return(db.query(models.Minimart)

           .filter(models.Minimart.id == id)

           .first())
```


### API GET Request
```python
@router.get("/get-item")

async def my_item(id: int, db: Session = Depends(get_db)):

    search_item = get_item(db, id)

    return {

        "id": search_item.id,

        "name": search_item.name,

        "price": search_item.price,

        "exp_date": search_item.exp_date,

        "brand": search_item.brand,

        "description": search_item.description

    } # Returns Dictionary
```


### How Information is collected on frontend
```jsx
<div className='search-container'>

          <h3>Search Item</h3>

          <form className='search-form' onSubmit={searchItem}>

            <input type='number' name='search_id' placeholder='Search ID'/>

            <input type='submit'/>

          </form>

        </div>
```


### Frontend to API
```jsx
const searchItem = async (e) => {

    event.preventDefault()

    setIsLoading(true)

    setError(null)

  

    const search_id = e.target.search_id.value

  

    try{

      const data = await makeRequest(`get-item?id=${search_id}`

      )


      setSearch(data ? [data] : [])
	/*If data exists then make it an array else return [] */
    }

    catch(err){

      setError(err.message || "Failed to Search item")

    }

    finally{

      setIsLoading(false)

    }

  }
```

### Displaying Searched Results
```jsx
<div className='display-search-db'>

              {Array.isArray(itemSearched) && itemSearched.map((i) => (
				/*Since itemSearched is updated earlier to an array */
				/*Since its an array we can map it */
                <div key={i.id}>

                  {i.id} <strong>{i.name}</strong> - ${i.price} - {i.brand} - {i.exp_date} - {i.description}

                </div>

              ))}

        </div>
```


# Giving Information to DB
#HTTP-POST

```python
def create_item(db: Session, id: int, name: str, price: float, exp_date: datetime, brand: str, description: str):

    new_item = models.Minimart(id=id, name=name, price=price,
                              exp_date=exp_date, brand=brand, description=description)

    db.add(new_item)

    db.commit()

    db.refresh(new_item)

    return new_item
```

- This is what the database will do to "create" the item


### API POST Request

```python
@router.post("/create-item")

async def create_my_item(item: ItemCreate, db: Session = Depends(get_db)):

    new_item = create_item(

        db,

        item.id,

        item.name,

        item.price,

        item.exp_date,

        item.brand,

        item.description

    )

    return {

        "id": new_item.id,

        "name": new_item.name,

        "price": new_item.price,

        "exp_date": new_item.exp_date.isoformat() if new_item.exp_date else None,

        "brand": new_item.brand,

        "description": new_item.description

    }
```


### How information is collected on frontend
```jsx
        <div className='input-container'>

            <h3>Create Item</h3>

            <form className='create-form' onSubmit={createItem}>

              <input type='number' name="id" placeholder='ID'/>

              <input type='text' name="name" placeholder='Name'/>

              <input type='number' name="price" placeholder='Price'/>

              <input type='date' name="exp_date" />

              <input type='text' name="brand" placeholder='Brand'/>

              <input type='text' name="description" placeholder='Description'/>

              <input type="submit" />

            </form>

        </div>
```


### Frontend passing information to backend API
```jsx
const createItem = async (e) => {

    event.preventDefault();

    setIsLoading(true)

    setError(null)

  

    const id = e.target.id.value;

    const name = e.target.name.value;

    const price = e.target.price.value;

    const exp_date = e.target.exp_date.value;

    const brand = e.target.brand.value;

    const description = e.target.description.value;

  

    try{

      const data = await makeRequest("create-item", {

          method: "POST",

          body: JSON.stringify({

                id: id,

                name: name,

                price: price,

                exp_date: exp_date,

                brand: brand,

                description: description

          })

        }

      )

      setItem(data)

      fetchItem();

    }

    catch(err) {

      setError(err.message || "Failed to create item")

    }

    finally {

      setIsLoading(false)

    }

  }
```


# Deleting Information from DB
#HTTP-DELETE

```python
def delete_item(db: Session, delete_id: int):

    item = db.query(models.Minimart).filter(models.Minimart.id == delete_id).first()

    db.delete(item)

    db.commit()

    return {"detail": "Item deleted"}
```
- First we find the ID we want to delete then we delete and commit it to the database


```python
@router.delete("/delete-item")

async def delete_my_item(id: int, db: Session = Depends(get_db)):

    delete_item(db, id)

    return delete_item
```


### Collecting ID to delete on frontend
```jsx
        <div className='delete-container'>

              <form className='delete-form' onSubmit={deleteItem}>

                  <input type='number' name="delete_id" placeholder='Delete ID'/>

                  <input type='submit'/>

              </form>

        </div>
```


### Frontend to Backend API
```jsx
  const deleteItem = async (e) => {

    event.preventDefault();

    setIsLoading(true)

    setError(null)

  

    try{

          await makeRequest(`delete-item?id=${e.target.delete_id.value}`, {

          method: "DELETE"

        }

      )

      fetchItem();  /*You can remove the setItem and fetchItem here if you dont want the display to refresh */

    }

  

    catch(err) {

      setError(err.message || "Failed to delete item")

    }

    finally {

      setIsLoading(false)

    }

  }
```

- The `?` in the API is to mark the start of the query parameters

- `http://localhost:8000/api/delete-item?id=1` (Example)
	- This means we want to delete an item with an ID = 1
	- We need this `?` because we are using DELETE method


# Updating Information in database
#HTTP-PUT


### Database code execution
```python
def update_item(db: Session, update_id: int, name: str, price: float, exp_date: datetime, brand: str, description: str):

    item = (update(models.Minimart)

            .where(models.Minimart.id == update_id)

            .values(name=name, price=price, exp_date=exp_date, brand=brand, description=description)

            )

    db.execute(item)

    db.commit()

    return {"detail": "Item Updated"}
```


```python
@router.put("/update-item")

async def update_my_item(item: ItemCreate, db: Session = Depends(get_db)):

    update_item(db, item.id, item.name, item.price, item.exp_date, item.brand, item.description)

    return update_item
```


### Collecting information on frontend
```jsx
<div className='update-container'>

              <form className='update-form' onSubmit={updateItem}>

                <input type='number' name="update_id" placeholder='ID'/>

                <input type='text' name="name" placeholder='Name'/>

                <input type='number' name="price" placeholder='Price'/>

                <input type='date' name="exp_date" />

                <input type='text' name="brand" placeholder='Brand'/>

                <input type='text' name="description" placeholder='Description'/>

                <input type="submit" />

              </form>

        </div>
```



```jsx
const updateItem = async (e) => {

    event.preventDefault()

    setIsLoading(true)

    setError(null)

  

    const update_id = e.target.update_id.value;

    const name = e.target.name.value;

    const price = e.target.price.value;

    const exp_date = e.target.exp_date.value;

    const brand = e.target.brand.value;

    const description = e.target.description.value;

  

    try{

        await makeRequest(`update-item?id=${update_id}`, {

        method: "PUT",

        body: JSON.stringify({

          id: update_id,

          name: name,

          price: price,

          exp_date: exp_date,

          brand: brand,

          description: description

        })

        }

      )

      fetchItem();

    }

  

    catch(err) {

      setError(err.message || "Failed to Update item")

    }

    finally {

      setIsLoading(false)

    }

  }
```







