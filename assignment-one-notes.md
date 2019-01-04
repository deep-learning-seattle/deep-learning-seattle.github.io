# 1. Error: No module named 'past'

On this line:

```python
from cs231n.classifiers import KNearestNeighbor
```

__Solution__: Just install the future, Marty

```bash
pip install future
```

# 2. Got 57 / 500 correct => accuracy: 0.114000 (may happen both on k=1 and k=5)

__Problem__:  predict_labels probably return scalar 0

__Solution__: probably missing index i y_pred[i]

# 4. from __future__ imports must occur at the beginning of the file

__Solution__: just give it what it needs - put this line in the beginning of the first cell:

```python
from __future__ import print_function
```
