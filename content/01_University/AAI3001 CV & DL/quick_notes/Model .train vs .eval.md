
`model.train()` and `model.eval()` are **NOT** about enabling / disabling gradient computation or updating weights. They only set a flag, `self.training` on the model and recursively on all submodules. 

- Layers that behave differently in training vs inference check this flag
```python
model.train() # sets model.training = True for model and all children
model.eval() # sets model.training = False for model and all children
```

## How it affects common layers

| Layer                                       | `model.train()`                                                                              | `model.eval()`                                        |
| ------------------------------------------- | -------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| `Dropout`, `Dropout2d`, `AlphaDropout`, etc | Randomly zero elements with probability `p`, then scales by `1/(1-p)` to keep expected value | Identity - NO Dropout                                 |
| `BatchNorm1d/2d/3d`, `SyncBatchNorm`        | Uses batch statistics (mean/var of current batch); updates `running_mean` and `running_var`  | Uses **running statistics**; does **not** update them |
| `LayerNorm`, `GroupNorm`                    | Same in both modes (no running stats)                                                        | Same                                                  |

## BatchNorm Detail

- In `train()`: Normalizes using the current batch's mean / variance and updates `running_mean` / `running_var` with momentum
- In `eval()`: Normalizes using the stored `running_mean` / `running_var`. If those were never updated properly, they are just the initial values `0` and `1`, so outputs will be poor


# Common Pitfalls

## `eval()` does not disable gradients
It only **changes layer behavior**. To **save memory/compute** during validation/inference, wrap the forward pass in `torch.no_grad()` or `torch.inference_mode()`:
```python
model.eval()
with torch.no_grad():
    outputs = model(inputs)
```

## Forgetting `eval()` during validation
Dropout stays active, and BatchNorm uses batch stats and updates running stats, both corrupt your validation results and pollute the running statistics

## Forgetting `train()` after validation
Training then uses running stats and no dropout, which hurts learning

## You can selectively override
`model.eval()` then `model.some_branch.train()` if only part of the model should be in training mode


# Typical Training Loop
```python
model.train()
for x, y in train_loader:
    optimizer.zero_grad()
    loss = criterion(model(x), y)
    loss.backward()
    optimizer.step()

model.eval()
with torch.no_grad():
    for x, y in val_loader:
        outputs = model(x)
        # compute validation metrics
```

#### TLDR
- `train()` makes layers ==🟢use training behavior== (dropout **active**, BatchNorm uses **batch stats**)
- `eval()` makes them ==🔴use inference behavior== (dropout **off**, BatchNorm uses **running stats**)

- `torch.no_grad()` is a **separate concern** for gradient tracking.











































































