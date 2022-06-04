---
layout: ar-post
lang: ar
title:  "وصفات لينُكس"
author: mohamed-ali
image: assets/images/linux-cmd.jpg
categories: [ البرمجة , العربية , لينُكس , Linux ]
featured: true
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

## المصادر:

* الصورة في رأس المقال من تصوير <a href="https://unsplash.com/@anagani_saikiran?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Sai Kiran Anagani</a> على موقع <a href="https://unsplash.com/s/photos/linux?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  
