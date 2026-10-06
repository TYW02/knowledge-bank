
# Background Information
In PyTorch, **gradients accumulate by default**. Every time you call `loss.backward()`, the computed gradients are **added** to the `.grad` attribute of each parameter.

- So if you **never clear them**, you **end summing gradients across iterations**.
- `zero_grad()` **clears** those **accumulated gradients**

```python
optimizer.zero_grad() # clears .grad for ALL parameters in the optimizer
```
- Internally it loops over all parameter groups in the optimizer and sets each parameter's `.grad` to either:
	- a zero tensor, OR
	- `None` (if `set_to_none=True`)

# How it affects everything else

## 1. It affects future `backward()` calls

If you **DO NOT** call `zero_grad`, gradients from the **previous iteration stay** in `.grad`. The next `backward()` adds to them
```python
# iteration 1
loss1.backward()   # p.grad = g1

# iteration 2 without zero_grad
loss2.backward()   # p.grad = g1 + g2
```

With `zero_grad`
```python
optimizer.zero_grad()  # p.grad = 0 or None
loss2.backward()       # p.grad = g2
```

> [!warning]
> So `zero_grad` ensures each `optimizer.step()` uses **only the gradients** from the **current backward pass**.

## 2. It does not affect the forward pass or computation graph


## 3. It does not reset optimizer state
Optimizers like SGD **with momentum**, Adam, RMSProp, etc..., **keep internal state** (momentum buffers, running averages of gradients and squared gradients). 
- `zero_grad` does **not** reset that state. 
So even after **zeroing gradients**, **Adam** still uses its **past moment estimates** for the next update

## 4. It does not reset parameters
`zero_grad` only clears gradients. Model weights stay exactly as they were after the last `optimizer.step()`

## 5. It only affects parameters in the optimizer
`optimizer.zero_grad()` zeros ==🔵only the parameters that were passed to that optimizer==. If you have multiple optimizers, or parameters not included in the optimizer, their gradients are not touched. 
- `model.zero_grad()` **zeros all parameters** of the model, **regardless of optimizer**.


# Typical Order
```python
for x, y in train_loader:
    optimizer.zero_grad()      # clear old gradients
    outputs = model(x)
    loss = criterion(outputs, y)
    loss.backward()            # accumulate fresh gradients
    optimizer.step()           # update weights
```

- You can also do `zero_grad` **after** `step`:
```python
loss.backward()
optimizer.step()
optimizer.zero_grad()
```

Both work. The important thing is that `zero_grad` happens **before** the next `backward()` if you want **fresh gradients each iteration**.


## When you intentionally skip `zero_grad`
Gradient accumulation is a common technique to simulate a larger batch size
```python
for i, (x, y) in enumerate(loader):
    outputs = model(x)
    loss = criterion(outputs, y) / accumulation_steps
    loss.backward()

    if (i + 1) % accumulation_steps == 0:
        optimizer.step()
        optimizer.zero_grad()
```
- Here you deliberately let gradients accumulate over several mini-batches before stepping.


## Common pitfalls
- **Calling `zero_grad` after `backward` but before `step`** → you throw away the gradients you just computed.
- **Forgetting `zero_grad`** → gradients keep adding, causing wrong updates and often exploding losses.
- **Using `optimizer.zero_grad()` when some parameters are not in the optimizer** → those parameters keep stale gradients.
- **Assuming `.grad` is always a tensor** → with `set_to_none=True`, it may be `None`. Use `set_to_none=False` if your code needs a tensor.

##### TLDR
`zero_grad` **clears accumulated** parameter **gradients** so the **next** `backward()` ==🟡starts from zero==. 
- It **does not touch weights**, optimizer state, or the graph. 
- Its **main job** is to **prevent unintended gradient accumulation** between training steps.































































