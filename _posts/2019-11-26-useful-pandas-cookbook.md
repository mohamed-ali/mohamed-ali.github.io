---
layout: post
title:  "Pandas cookbook: Useful, reusable pandas code snippets"
author: mohamed-ali
image: assets/images/pandas_logo.png
image_thumbnail: assets/images/pandas_logo_thumbnail.png
categories: [ code-snippets, python, pandas, cookbook ]
featured: true
---

After a while working with Pandas, the following set of code snippets seems to be quite useful and reusable in various scenarios.
Therefore, I am going to catalog it here as a quick reference for myself and others:

#### Create multiple columns from an existent column in a pandas dataframe

```python
import pandas as pd
import numpy as np
# generate a random dataframe with a column "original"
df = pd.DataFrame({'original' : np.random.rand(5)})
# df.head()
#    original
# 0  0.185199
# 1  0.230932
# 2  0.034539
# 3  0.587919
# 4  0.876895
df[["new1", "new2"]] = df["original"].apply(
    lambda s: pd.Series({"new1": 2 * s, "new2": s + 1})
)
# df.head()
#    original      new1      new2
# 0  0.185199  0.370399  1.185199
# 1  0.230932  0.461865  1.230932
# 2  0.034539  0.069078  1.034539
# 3  0.587919  1.175839  1.587919
# 4  0.876895  1.753790  1.876895
```
#### Inspect pandas DataFrames memory usage

```python
import pandas as pd
import numpy as np
df = pd.DataFrame(np.random.randn(1000, 4),  columns=list('ABCD'))
df.info(memory_usage="deep")
# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 1000 entries, 0 to 999
# Data columns (total 4 columns):
# A    1000 non-null float64
# B    1000 non-null float64
# C    1000 non-null float64
# D    1000 non-null float64
# dtypes: float64(4)
# memory usage: 31.3 KB

df = pd.DataFrame(np.random.randn(1000000, 6),  columns=list('ABCDEF'))
df.info(memory_usage="deep")
# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 1000000 entries, 0 to 999999
# Data columns (total 6 columns):
# A    1000000 non-null float64
# B    1000000 non-null float64
# C    1000000 non-null float64
# D    1000000 non-null float64
# E    1000000 non-null float64
# F    1000000 non-null float64
# dtypes: float64(6)
# memory usage: 45.8 MB
```
