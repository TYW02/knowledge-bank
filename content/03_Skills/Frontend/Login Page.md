---
title: Building the Login Page
tags:
  - Login
  - Props
  - useEffect
---
Firstly you should create a folder where all your API calls live instead of holding them in your components.
You components should not care how data is fetched, it just calls it and handles the result.
#Login
```js
// src/api/inventory.js
const API_URL = import.meta.env.VITE_API_URL

export async function loginUser(email, password) {
    const response = await fetch(`${API_URL}/auth/login`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ email, password })
    })

    if (!response.ok) {
        throw new Error("Invalid credentials")
    }

    return response.json() // returns { access_token, token_type }
}
```


## Props Explained
#Props
Imagine a manager (`App`) and an employee (`LoginForm`). The manager has a safe where tokens are stored (state). The employee doesn't have access to the safe directly. So the manager gives the employee a walkie-talkie and says "when you get the token, call me on this and I'll put it in the safe"
> [!NOTE]
> App = Manager, owns the safe (token state)
> setToken = The safe combination
> onLogin = the walkie-talkie given to the child
> LoginForm = the employee doing the work


### Example
```jsx
// App.jsx
const [token, setToken] = useState(null)

<LoginPage onLogin={setToken} /> 
// onLogin is the prop name and what the child calls 
// setToken it what it actually is, what the parent passes

// LoginPage.jsx
function LoginPage({ onLogin }) {
return <LoginForm onLogin={onLogin}/> 
// onLogin here IS setToken from App
// LoginPage doesn't use it, just passes it to LoginForm
}

//LoginForm.jsx
function LoginForm({ onLogin }){
async function handleSubmit(e) {
	const data = await loginUser(email, password)
	onLogin(data.access_token) // This line IS: setToken(data.access_token)
	//Updates App's state, causes App to re-render, shows dashboard page
}
}
```



# useEffect
#useEffect
```js
useEffect(() => { ... }, []) // runs ONCE after first render only
useEffect(() => { ... }, [token]) // runs when token changes
useEffect(() => { ... }) // runs after EVERY render 
```

## Key Patterns to Note
| Situation          | Pattern                         |
| ------------------ | ------------------------------- |
| Loop in JSX        | `.map()` not `.forEach()`       |
| Variable in JSX    | `{variable}` not `variable`     |
| Async in useEffect | Define function inside, call it |
| List items         | Always add `key` prop           |