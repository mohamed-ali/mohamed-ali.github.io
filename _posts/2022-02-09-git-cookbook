---
layout: ar-post
lang: ar
title:  "وصفات لاستعمال Git"
author: mohamed-ali
image: assets/images/16.jpg
categories: [ البرمجة , العربية , git ]
featured: true
hidden: false
published: true

---

في التّالي مجموعة من الوصفات المُساعدة على إستخدام git بفعاليّة.

## كيف نبسط قائمة الملفات الموجودة في مستودع git؟

يُمكن استعمال svn كالتّالي

```
!svn ls https://github.com/aws/amazon-sagemaker-examples.git/trunk
```


## كيف تُزامن بين تفرُّع (fork) خاص بك و مستودع أصلي في git ؟

```
# أضف المستودع الأصلي إلى تفرّع المستودع الخاصّ بك بالطريقة التّالية
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git

# أطلق عمليّة التّزامن بالأوامر التّالية
git fetch upstream
git checkout master
git merge upstream/master
```
