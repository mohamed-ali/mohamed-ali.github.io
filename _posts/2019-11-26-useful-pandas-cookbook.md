---
layout: post
title:  "Pandas cookbook: Useful, reusable pandas code snippets"
author: mohamed-ali
image: assets/images/16.jpg
categories: [ scientific-conference, machine-learning, deep-learning ]
featured: true
hidden: true
---

After a while working with Pandas, the following set of code snippets seems to be quite useful and reusable in various scenarios.
Therefore, I am going to catalog it here as quick reference (for myself and others). 

### Create multiple columns from an existent column in a pandas dataframe

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
df[["new1", "new2"]] = df["original"].apply(lambda s: pd.Series({"new1": 2 * s, "new2": s + 1}))
# df.head()
#    original      new1      new2
# 0  0.185199  0.370399  1.185199
# 1  0.230932  0.461865  1.230932
# 2  0.034539  0.069078  1.034539
# 3  0.587919  1.175839  1.587919
# 4  0.876895  1.753790  1.876895
```
