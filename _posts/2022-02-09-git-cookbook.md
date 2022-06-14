---
layout: ar-post
lang: ar
title:  "وصفات لاستعمال Git"
author: mohamed-ali
image: assets/images/yancy-min-842ofHC6MaI-unsplash.jpg
categories: [ البرمجة , العربية , git ]
featured: true
hidden: false
published: true

---

في التّالي مجموعة من الوصفات المُساعدة على إستخدام git بفعاليّة.

## كيف تبسُط قائمة الملفات الموجودة في مستودع git؟

يُمكن استعمال svn كالتّالي

```
!svn ls https://github.com/aws/amazon-sagemaker-examples.git/trunk
```

## كيف تنسخ ملفًا أو مُجلّدًا من مستودع git؟

في العموم يُمكن استخدام svn بالشكل التّالي لتنزيل جزء مُعيّن من مستودع git  
```
!svn export <git repo>/trunk/<folder name>
```
مثال تطبيقي لتنزيل المُجلّد "training" من المشروع  amazon-sagemaker-examples:

```
!svn export https://github.com/aws/amazon-sagemaker-examples.git/trunk/training
```
ستجد بعد تنفيذ هذا الأمر أن المُجلّد قد نُسخ إلى حاسبوك.

## كيف تُزامن بين تفرُّع (fork) خاص بك و مُستودع الترميز الأصلي المُنحدر منه في git ؟

```
# أضف المستودع الأصلي إلى تفرّع المستودع الخاصّ بك بالطريقة التّالية
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git

# أطلق عمليّة التّزامن بالأوامر التّالية
git fetch upstream
git checkout master
git merge upstream/master
```


## مصادر:

* الصورة من طرف <a href="https://unsplash.com/@yancymin?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Yancy Min</a> على <a href="https://unsplash.com/s/photos/git?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
