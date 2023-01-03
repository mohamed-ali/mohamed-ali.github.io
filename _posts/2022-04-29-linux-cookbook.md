---
layout: ar-post
lang: ar
title:  "وصفات لينُكس"
author: mohamed-ali
image: assets/images/linux-cmd.jpg
categories: [ البرمجة , العربية , لينُكس , Linux ]
featured: false
hidden: false
published: true

---

في التّالي مجموعة من وصفات لينُكس

## ما هي الأنابيب المُسمات في لينُكس وكيف تُستعمل؟

الأنابيب المُسمات (named pipes)، هي عبارة عن ملف يُمكن إنشائه في لينُكس واستعماله كوسيلة لتخزين البيانات وقتيا و نقلها من الكاتب إلى القارئ عبر طريقة استرداد البيانات FIFO. وهي اختصار الجُملة "First in First out" و التي تعني "الأوّل دخولا هو الأوّل خروجا".


```
$ mkfifo test-pipe
$ ls -alh test-pipe
prw-r--r--  1 user  group     0B day month hour:min test-pipe
```

الآن لو نضع أمرا في طرفية لينُكس ليقرأ هذا الملف باستمرار:

```
$ tail -f test-pipe
```

ثم في طرفية أخرى نقوم بالكتابة في هذا الملف:

```
echo "مرحبا" > test-pipe
```

سنرى مُباشرة أن الرسالة "مرحبا" تظهر في الطرفية أين نقوم بالقراءة.

من خاصية الأنابيب المُسمات أنّها تضع البيانات في الذاكرة الحيّة، لذا فعمليّة القراءة والكتابة سريعة بالمقارنة مع الكتابة على القرص. كذلك، تُمحى البيانات مباشرة بعد عمليّة القراءة.

## كيف تجد الملفات المُنتهية برمز تنسيق مُعيّن باستعمال الأمر `find` ؟

مثلا، نقوم بإيجاد كُلّ الملفات المُنتهية ب `"*.md"` في مُجلّد بالأمر التّالي:

```
find ./ -type f  -name "*.md"
```

## كيف تجد الملفات المُنتهية برمز تنسيق مُعيّن باستعمال الأمر `find` ثُمّ تُغيِّرُ شيئًا فيها في آن واحد باستعمال الأمر `sed` ؟

في المثال التّالي يقوم الأمر `find` بإيجاد كُل الملفات المُنتهية برمز التنسيق `"*.md"` ثم باستعمال `exec-` يُمكننا تطبيق أمر آخر على نتائج `find`. 
في هذه الحالة نقوم بتطبيق الأمر `sed` كما هو مُبين لتغيير نصٍّ ما إلى نصٍّ آخر. ثُمّ نرمز إلى نهاية الأمر بعلامة `+`.

```
find ./ -type f  -name "*.md" -exec sed -i 's/<TO CHANGE>/<THE CHANGE>/g' {} +
```

## المصادر:

* الصورة في رأس المقال من تصوير <a href="https://unsplash.com/@anagani_saikiran?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Sai Kiran Anagani</a> على موقع <a href="https://unsplash.com/s/photos/linux?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  
