---
sidebar_position: 3
description: Homo LR Demo
keywords: [横向联邦学习, Homo LR, Primihub SDK Demo]
---
# Homo LR Demo

## Example

```python
# Using Python sdk client： home lr
import primihub as ph
from primihub.FL.model.logistic_regression.homo_lr_dev import run_party


config = {
    'mode': 'Plaintext', 
    'learning_rate': 'optimal',
    'alpha': 0.0001,
    'batch_size': 100,
    'max_iter': 200,
    'n_iter_no_change': 5,
    'compare_threshold': 1e-6,
    'category': 2,
    'feature_names': None,
}


@ph.context.function(role='arbiter',
                     protocol='lr',
                     datasets=['train_homo_lr'],
                     port='9010',
                     task_type="lr-train")
def run_arbiter_party():
    run_party('arbiter', config)


@ph.context.function(role='host',
                     protocol='lr',
                     datasets=['train_homo_lr_host'],
                     port='9020',
                     task_type="lr-train")
def run_host_party():
    run_party('host', config)


@ph.context.function(role='guest',
                     protocol='lr',
                     datasets=['train_homo_lr_guest'],
                     port='9030',
                     task_type="lr-train")
def run_guest_party():
    run_party('guest', config)
```
