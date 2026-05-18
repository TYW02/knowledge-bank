---
tags:
  - Supabase
---
#env #Supabase 
First you need to keep your *SUPABASE_URL* and *SUPABASE_KEY* in your `.env`

Your *SUPABASE_URL* is under your project overview it should look something like https://[ ].supabase.co 
Your *SUPABASE_KEY*  is under API Keys `Secret Keys`

Make a file to connect to your Supabase DB
```python
import os
from dotenv import load_dotenv
from supabase import create_client, Client

load_dotenv()

url: str = os.environ.get("SUPABASE_URL")
key: str = os.environ.get("SUPABASE_KEY")

supabase: Client = create_client(url, key)
```

- `load_dotend()` reads your `.env` and makes values available via `os.environ`
- `create_client()` initializes the connection, think of it as "dialing in" to Supabase
- You get back a `Client` object you'll reuse everywhere

> [!NOTE]
> Common Mistake: Running this without a `.env` file, or having a typo in your variable name. If `url` or `key` is `None`, you'll get a confusing error later, not here.

