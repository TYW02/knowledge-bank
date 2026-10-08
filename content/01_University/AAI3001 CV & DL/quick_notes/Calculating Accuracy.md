
```python
_, preds = torch.max(cpuout, 1)
accuracy = (accuracy * datasize + torch.sum(preds == labels)) / (datasize + inputs.shape[0])
datasize += inputs.shape[0]
```

## `_, preds = torch.max(cpuout, 1)`
- `cpuout` is the model output for a batch, shape=(batch_size, num_classes)
- `torch.max(cputout, 1)` returns two things
	- The maximum value in each row (ignored with `_`)
	- The index of that maximum (The predicted class)
- So `preds` has shape (batch_size,) and contains **predicted class labels**

## `torch.sum(preds == labels)`
- `preds == labels` gives a boolean tensor of shape (batch_size,)
- `torch.sum(...)` counts how many predictions are correct in this batch
- This is the number of correct samples in the current mini-batch

## `accuracy = (accuracy * datasize + torch.sum(preds == labels) / (datasize + inputs.shape[0])`

This computes the **running average** over all batches seen so far

- `accuracy` before this batch = average accuracy over previous `datasize` samples
- `accuracy * datasize` = total number of correct predictions **before this batch**
- `torch.sum(preds == labels)` = correct predictions in current batch
- `datasize + inputs.shape[0]` = total number of samples after **including current batch** (input shape at index 0 is the batch size)

### So new accuracy is
$$
accuracy_{new} = \frac{total\,correct}{total\,samples}
$$
## `datasize += inputs.shape[0]`
- After computing the new average, update the total number of samples seen
- This must happen **AFTER** the accuracy calculation, because the accuracy formula needs the old `datasize`



# Evaluation 
```python
measure, _ = evaluate(model, dataLoader_cvtest, criterion=None, device=device)
if measure > best_measure:
    bestweights = model.state_dict()
    best_measure = measure
```
- `measure` is the validation accuracy
- The `accuracy` line in `evaluate()` therefore decides which epoch's weights are kept


























































