---
layout: ar-post
title:  "وصفات بانداس: مقتطفات مفيدة وقابلة لإعادة الاستخدام"
author: mohamed-ali
image: assets/images/pandas_logo.png
image_thumbnail: assets/images/pandas_logo_thumbnail.png
categories: [ code-snippets, python, pandas, وصفات ]
featured: true
published: true

---

هذا مرجع لبعض وصفات الترميز كثيرة الإستعمال باستخدام مكتبة بانداس.

#### قم بإنشاء أعمدة بيانات متعددة من عمود بيانات موجود في إطار بيانات بانداس



<code class="language-python highlighter-rouge" dir="ltr">

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
</code>


#### إفحص مدى استعمال إطار بيانات باندس للذاكرة



<code class="language-python highlighter-rouge" dir="ltr">
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
</code>

