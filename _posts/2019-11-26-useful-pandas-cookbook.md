---
layout: ar-post
lang: ar
title:  "وصفات بانداس: مقتطفات مفيدة وقابلة لإعادة الاستخدام"
author: mohamed-ali
image: assets/images/pandas_logo.png
image_thumbnail: assets/images/pandas_logo_thumbnail.png
categories: [ code-snippets, python, pandas, وصفات ]
featured: true
published: true

---

هذا مرجع لبعض وصفات الترميز كثيرة الإستعمال باستخدام مكتبة بانداس.

#### إنشاء أعمدة بيانات متعددة من عمود بيانات موجود في إطار بيانات بانداس



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




#### فحص مدى استعمال إطار بيانات باندس للذاكرة




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


#### تحويل إطار بيانات بانداس لتنسيق البيانات tfrecords

تنسيق tfrecords أو Tensorflow records، أي سجلّات تنسورفلو، هو تنسيق بيانات كثير الإستعمال مع مكتبة تنسورفلو والتي تُستخدم بكثرة في بناء وتدريب أنظمة التعلّم الآلي. بعد تثبيت مكتبة pandas_tfrecords، يُمكنك استخدامُها لتحويل إطارات بيانات بانداس إلى تنسيق سجلّات تنسورفلور بالطريقة التّالية:   

```python
import random

import pandas as pd
from pandas_tfrecords import pd2tf, tf2pd

# تحديد عدد الأمثلة.
n_samples = 1024 * 100
# بناء الأمثلة

data = []
for j in range(n_samples):
    feature_1 = random.randint(1, 100)
    feature_2 = random.randint(1, 1000)
    target = 0.3 * feature_1 + 0.6 * feature_2
    data.append({
        "feature_1": feature_1,
        "feature_2": feature_2,
        "target": target
        })

# tfrecords كتابة إطار بيانات باندس بتنسيق 
pd2tf(
    # إنشاء إطار بيانات بانداس
    pd.DataFrame(data),
    os.path.join("data_chunks/tfrecords"),
    max_mb=1,
    compression_type=None
)
```

#### كيف تقرأ ملفات بتنسيق csv مُجزّءة باستعمال بانداس إنطلاقا من خدمة التخزين أمازون S3

مكتبة بانداس لا تحتوي على خاصيّة تُمكِّنُ من قراءة ملفات الcsv المُجزّءة مُباشرة. إلاّ أنّه من المُمكن استخدم مكتبة داسك (dask) والتي تُمكِّنُ من قراءة الملفات المُجزءة من أمازون S3. ثُمّ بعد الانتهاء من القراءة، يُمكن تحويل إطار بيانات داسك إلى إطار بيانات بانداس. 

```python
import dask.dataframe as dd

s3_sample_data_path = "s3://path of data in s3"
df = dd.read_csv(f"{s3_sample_data_path}/*")
print(type(df))
# dask.dataframe.core.DataFrame البيانات في إطار
pd_df = df.compute()
print(type(pd_df))
# pandas.core.frame.DataFrame البيانات في إطار

```
