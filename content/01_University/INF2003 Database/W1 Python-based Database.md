---
title: W1 Python-based Database
tags:
  - SQLAlchemy
---
### Imports
```python
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy import Column, Integer, String, Enum, Float, ForeignKey
from sqlalchemy.orm import relationship, declarative_base

from sqlalchemy import create_engine, text
from sqlalchemy.orm import sessionmaker
```



# Creating a database table
```python
engine = create_engine("sqlite:///inf2003_lab1.db")
Base = declarative_base()

class Students(Base):
	__tablename__ = "INF2003TohYuanWei"
	sid = Column(Integer, primary_key=True)
	name = Column(String)
	grade =  Column(String)
	
Base.metadata.create_all(engine)

Session = sessionmaker(bind=engine)
session = Session()
```


## Reading from table
#SELECT 
```python
with engine.connect() as conn:
	result = conn.execute(text("SELECT * FROM INF2003TohYuanWei"))
	print(result.all())
```


## Insert to table
#Insert 
```python
with engine.connect() as conn:
	result = conn.execute(text("INSERT INTO INF2003TohYuanWei (sid, name, grade) VALUES (2500668, 'TohYuanWei', 'B')"))
	conn.commit()
	
with engine.connect() as conn:
	result = conn.execute(text("SELECT * FROM INF2003TohYuanWei"))
	print(result.all())
```

> [!NOTE]
> Take note of how name is being inserted, don't forget the ' ', also make sure you run `conn.commit()` else the changes will not be reflected.

## Update table
#Update 
```python
with engine.connect() as conn:
	result = conn.execute(text("UPDATE INF2003TohYuanWei SET grade='A-' WHERE sid=2202345"))
	conn.commit()
	
with engine.connect() as conn:
	result = conn.execute(text("SELECT * FROM INF2003TohYuanWei"))
	print(result.all())
```

> [!NOTE]
> For UPDATE statements they usually follow the format
> ```SQL
> UPDATE table_name
> SET column1 = value1, column2 = value2, ...
> WHERE condition;
> ```


## Delete from table
#Delete 
```python
with engine.connect() as conn:
	result = conn.execute(text("DELETE FROM INF2003TohYuanWei WHERE sid = 2002345"))
	conn.commit()
	
with engine.connect() as conn:
	result = conn.execute(text("SELECT * FROM INF2003TohYuanWei"))
	print(result.all())
```

> [!NOTE]
> REMEMBER to `conn.commit()`
> Delete statements usually follow the format
> ```SQL
> DELETE FROM table_name WHERE condition;
> ``` 


































