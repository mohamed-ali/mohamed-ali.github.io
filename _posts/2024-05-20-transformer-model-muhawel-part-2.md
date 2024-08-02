---
layout: ar-post
lang: ar
title: "استكشاف تفاصيل آلية الانتباه في خوارزمية المُحوِّل"
author: mohamed-ali
image: assets/images/transformer-article2-header.jpg
image_thumbnail: assets/images/transformer-attention-details.png
categories: [ التعلّم الآلي , العربية , التعلّم العميق , المُحوّل ]
featured: false
hidden: true
published: true

---

في المقال السابق، تعرَّفنا على خوارزمية المُحوّل بشكل عام وعلى الدَّور المركزي الذي تلعبه آلية الانتباه في تصميمها. وقد خلُصنا إلى أن هدف تصميم هذه الآلية كان اِغتنام أفضل خواصِّ الخوارزميّات الموجودة حينها دون عيوبها، أي تحقيق القدرة على التعلُّم من سلاسل البيانات بشكل متوازٍ مع الحفاظ على قدرة النموذج على نمذجة التفاعلات بعيدة المدى في هذه السلاسل. 

ثُمّ أوضحنا أن هذا الهدف تُرجِمَ إلى تصميم آلية الانتباه المُعتمدة على الجداء السُلَّمِي المُحجَّم في شكلها العام التّالي:

$$ Attention(Q, K, V) = softmax(\frac{QK^T}{\sqrt{d_k}})V $$

حيث تُمثَّل المُدخلات $$Q$$ و $$K$$ و $$V$$ على التوالي:
* $$Q$$ هي الاِستعلام (Query)، أي البيانات التي نسعى إلى فهم علاقتها بالبقية.
* $$K$$ هي المفاتيح (Keys)، أي البيانات التي نريد قياس مُدى علاقتها بالاِستعلام.
* $$V$$ هي القيم (Values)، أي البيانات التي سنعمل على اِستخراجها أو حسابها كمُخرجات بعد قياس درجة علاقتها بالاِستعلام.

نعرف الآن صيغة آلية الانتباه بشكل عام، لكن الأهم هو فهم كيف تُؤدّي هذه الصيغة إلى تحقيق هدف تصميمها، أي تمكين النموذج من التعلُّم من سلاسل البيانات بطريقة متوازية مع القدرة على نمذجة التفاعلات بعيدة المدى.

#### فهم تفاصيل عملية الانتباه

لتسهيل فهم عمل آلية الانتباه، دعنا نتوقف للحظة عند كل جزء من المُعادلة السابقة:

1. **الجداء السّلمي**: هو عملية حساب حاصل ضرب القيم (كل مُدخل في $$Q$$ مع كل مُدخل في $$K$$). ويمثِّل هذا الجزء درجة التشابه أو العلاقة بين كل مُدخل في $$Q$$ مع كل مُدخل في $$K$$. فمثلاً، إذا كان هناك مُدخل في $$Q$$ له علاقة قوية مع مُدخل في $$K$$، سيكون الجداء السُّلمي للاثنين كبيرًا.

2. **التقسيم على الجذر التربيعي لطول المُدخل $$K$$**: نقوم بتقسيم نتائج الجداء السُّلمي على الجذر التربيعي لطول مُدخل $$K$$. وهذا مهم لتجنُّب أن تصبح قيم الجداء السُّلمي كبيرة جدًا مما قد يؤدّي إلى مشاكل في عملية التدريب.

3. **تطبيق دالّة softmax**: بعد الحصول على نتائج الجداء السُّلمي المُحجَّمة، نُطبِّق عليها دالّة softmax. وهذه الدالّة تتحكَّم في القيم الناتجة بحيث تصبح قِيَم الأعلى تقريبًا 1 والأقل تقريبًا 0. بذلك، تُصبح هذه النتائج عبارة عن أوزان ترجيحية متجمعة تُمثِّل مدى علاقة كل مُدخل في $$Q$$ بكل مُدخل في $$K$$.

4. **ضرب الأوزان الترجيحية في القيم $$V$$**: بعد الحصول على الأوزان الترجيحية، نُضرِبها في القيم $$V$$ لننتج الناتج النهائي لعملية الانتباه. أي أننا نُحسِّن القيم $$V$$ بناءً على درجة علاقتها بالاِستعلام $$Q$$.

إذًا، بشكل عام، آلية الانتباه تُقيِّم درجة علاقة كل عنصر في الاِستعلام $$Q$$ بكل عنصر في المفاتيح $$K$$، ثم تُطبِّق هذه الأوزان الترجيحية على القيم $$V$$ لاِستخراج الناتج النهائي. وهذا ما يُمكِّن النموذج من التعلُّم من سلاسل البيانات بطريقة متوازية وليس تسلسليّة، بخلاف الشبكات العصبية التكرارية.

#### كيف تُساهم آلية الانتباه في تحقيق هدف التصميم؟

لنشرح كيف تُساعد آلية الانتباه في تحقيق هدف التصميم:

1. **التعلُّم بطريقة متوازية**: بإمكان النموذج الذي يَعتمِد على آلية الانتباه حساب مُخرجاته لكل عنصر في التسلسل بطريقة مستقلة عن بعضها البعض، دون الحاجة إلى الاعتماد على الحسابات التي تمت في الخطوات السابقة
2. **نمذجة التفاعلات بعيدة المدى**: تُتيح آلية الانتباه للنموذج إمكانية التعلُّم من تفاعلات كل عنصر في التسلسل مع كل العناصر الأخرى، بغض النظر عن مدى بُعدها في التسلسل. فبخلاف الشبكات العصبية الترشيحية التي تكون قدرتها محدودة على نمذجة التفاعلات بعيدة المدى، فإن آلية الانتباه تُتيح للنموذج إمكانية التعلُّم من هذه التفاعلات بكفاءة عالية.

هذا يعني أن آلية الانتباه تُمكِّن النموذج من الاستفادة من المعلومات الموجودة في كامل التسلسل عند حساب مُخرج أي عنصر فيه، بدلاً من الاقتصار على المعلومات الموجودة في محيط هذا العنصر فقط. وهذا ما يُفسِّر قدرة هذه الآلية على نمذجة التفاعلات بعيدة المدى في التسلسلات.

#### كيف يتم تطبيق آلية الانتباه في خوارزمية المُحوّل؟

لقد وضَّحنا في المقال السابق أن خوارزمية المُحوّل تتكوَّن من جزأين رئيسيين: جزء الترميز (encoder) وجزء فك الترميز (decoder). ويتضمَّن كل جزء 6 طبقات متكرِّرة، وتحتوي كل طبقة على طبقتَين فرعيتَين: طبقة الانتباه الذاتي متعدِّد الرؤوس وطبقة التغذية الأمامية.

في جزء الترميز، تُطبَّق طبقة الانتباه الذاتي على التسلسل المُدخل لاِستخراج ما يُسمَّى بموجِّه السياق (context vector)، وهو عبارة عن ملخِّص للمعلومات الموجودة في التسلسل المُدخل. 

أمَّا في جزء فك الترميز، فتُطبَّق طبقتا الانتباه الذاتي على التسلسل المُخرج (وهو ما تم إنشاؤه حتى الآن) مرتَّبطَيْن بموجِّه السياق المُستخرج من جزء الترميز. وذلك لضمان أن يكون التسلسل المُخرج مُرتبطًا بشكل وثيق بالمعلومات الموجودة في التسلسل المُدخل.

<img class="img-fluid" src="/assets/images/transformer-attention-detailed.png" alt="نظرة تفصيلية في تركيبة معماريّة خوارزمية المُحوِّل">

هذا التصميم يتيح للنموذج التعلُّم من كامل التسلسل المُدخل عند حساب كل عنصر في التسلسل المُخرج، مما يُعزِّز قدرته على نمذجة التفاعلات بعيدة المدى. كما أنه يُمكِّن النموذج من حساب مُخرجاته بشكل متوازٍ، وليس تسلسلي كما هو الحال في الشبكات العصبية التكرارية.

#### خلاصة

لقد رأينا في هذا المقال كيف تُساهم آلية الانتباه في خوارزمية المُحوّل في تحقيق هدف التصميم المُتمثِّل في التعلُّم من سلاسل البيانات بشكل متوازٍ مع القدرة على نمذجة التفاعلات بعيدة المدى. 

حيث تُتيح آلية الانتباه للنموذج إمكانية التعلُّم من تفاعلات كل عنصر في التسلسل مع كل العناصر الأخرى، بغض النظر عن مدى بُعدها في التسلسل. كما تُمكِّن النموذج من حساب مُخرجاته لكل عنصر في التسلسل بطريقة مستقلة عن بعضها البعض، دون الحاجة إلى الاعتماد على الحسابات التي تمت في الخطوات السابقة.

وقد رأينا كيف يتم تطبيق هذه الآلية في جزئَي الترميز وفك الترميز لخوارزمية المُحوّل، لتحقيق التوازن بين السرعة والقدرة على نمذجة التفاعلات بعيدة المدى.

هذه المفاهيم الأساسية حول آلية الانتباه وكيفية توظيفها في خوارزمية المُحوّل تُعتبر مفتاحًا لفهم عمل هذه الخوارزمية وتطبيقاتها المُتنوِّعة في مجالات مُعالجة اللغات الطبيعية والذكاء الاصطناعي بشكل عام.

<div markdown="1" class="callout callout-info">

* لمزيد من التفاصيل حول آلية الانتباه وتطبيقاتها في الذكاء الاصطناعي، يُمكنك الاطِّلاع على المصادر التالية:
  - [مقدِّمة شاملة في آلية الانتباه (باللغة الإنجليزية)](https://lilianweng.github.io/lil-log/2018/06/24/attention-mechanism.html)
  - [شرح مُفصَّل لآلية الانتباه في خوارزمية المُحوّل (باللغة الإنجليزية)](https://www.youtube.com/watch?v=iDulhoQ2pro)
  - [تطبيقات آلية الانتباه في مجالات مُختلفة من الذكاء الاصطناعي (باللغة الإنجليزية)](https://lilianweng.github.io/lil-log/2018/06/24/attention-mechanism.html#applications-of-attention-mechanism)
* كما يُمكنك البحث في مصادر باللغة العربية لمزيد من الشروحات والأمثلة التطبيقية.

</div>

### المُصطلحات التقنية ومُرادفاتُها الإنجليزية

- موجِّه السياق: context vector
- جزء الترميز: encoder
- جزء فك الترميز: decoder
- الانتباه الذاتي: self-attention
- التغذية الأمامية: feedforward

### المصادر

1. [مقدِّمة شاملة في آلية الانتباه (باللغة الإنجليزية)](https://lilianweng.github.io/lil-log/2018/06/24/attention-mechanism.html)
2. [شرح مُفصَّل لآلية الانتباه في خوارزمية المُحوّل (باللغة الإنجليزية)](https://www.youtube.com/watch?v=iDulhoQ2pro)
3. [تطبيقات آلية الانتباه في مجالات مُختلفة من الذكاء الاصطناعي (باللغة الإنجليزية)](https://lilianweng.github.io/lil-log/2018/06/24/attention-mechanism.html#applications-of-attention-mechanism)
4. الصورة في رأس المقال من تصوير <a href="https://unsplash.com/@rwlinder?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Robert Linder</a> على موقع <a href="https://unsplash.com/s/photos/transformer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>