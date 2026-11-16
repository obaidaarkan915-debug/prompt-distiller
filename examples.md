# Examples (before / after)

Voice-dictated inputs and the ideal distilled output. English is the base language.
Use these as evals: after editing `SKILL.md`, rerun the inputs and compare with the expected output.

---

## 1. Simple request with a self-correction

**Input**
> ايي اممم شوف أريد منك تكتبلي ايميل، يعني مو رسمي كلش بس يكون محترم، للدكتور تبعي، اممم أريد أطلب منه تمديد للـ deadline، لا مو تمديد، يعني يومين زيادة بس، لان صار عندي ظرف، فهمت شلون؟ وخليه قصير

**Expected output**
```
Write a short, respectful, not-too-formal email in Arabic to my lecturer, asking for a 2-day extension on the submission deadline because of an urgent circumstance.
```
Assumptions: the email is in Arabic (the language of the request).

**Why:** the self-correction ("not an extension, just two extra days") keeps only the final version. Tone and length constraints are kept. The prompt is in English, but the output language is stated so the email does not change language. No invented details about the circumstance.

---

## 2. Technical request (code and errors stay exact)

**Input**
> هلو اممم عندي مشكلة بالكود، يعني Python، وكل ما أشغله يطلع لي هذا الخطأ KeyError: 'user_id' فشوف اني أحاول أقرأ ملف JSON وأطبع الاسم لكل مستخدم، والملف اسمه users.json، أريدك تصلحه بس لا تغير الهيكل مال الكود كله، بس الإصلاح، وأشرح لي بجملة وحدة شنو كان الغلط

**Expected output**
```
Goal: Fix a Python bug.
Error: KeyError: 'user_id'
Context: The code reads users.json and prints each user's name.
Constraints: Minimal fix only. Do not restructure the code.
Output: The corrected code plus a one-sentence explanation of the cause, in Arabic.
```
Assumptions: the code will be attached; the explanation is in Arabic (the language of the request).

**Why:** the error message and file name are copied exactly. The code was not pasted, so that is flagged as an assumption instead of guessed.

---

## 3. Numbers, correction, and format

**Input**
> أريد خطة دراسة لمدة أسبوعين، لا لا ثلاثة أسابيع، للـ physics، يعني ساعتين باليوم، مو ثلاث ساعات، وعندي امتحان يوم 20 من الشهر، وأريدها جدول

**Expected output**
```
Create a physics study plan: 3 weeks, 2 hours per day, finishing before the exam on the 20th of the month. Format: table. Write it in Arabic.
```
Assumptions: the exam is on the 20th of the current month; the plan is in Arabic.

**Why:** both corrections (3 weeks, 2 hours) take the final value. Every number survives (3, 2, 20). The unclear month and the output language become explicit assumptions.

---

## 4. Glossary applied silently

**Input**
> أريد تكتب لي README لمشروع على جيت هب، المشروع هو skill لـ كلود كود، وظيفته ينظف الـ prompts اللي أكتبها بـ ويسبر فلو، واكتبه بالإنجليزي وخليه قصير وفيه قسم للـ usage

**Expected output**
```
Write a short README in English for a GitHub project: a Claude Code skill that cleans prompts dictated with Wispr Flow. Include a Usage section.
```

**Why:** "جيت هب", "كلود كود", "ويسبر فلو" are fixed through the glossary. The user asked for English, so the output language is English and no assumption is needed.

---

## 5. Critical ambiguity: ask one question

**Input**
> سوي لي شي مثل اللي سويته المرة الماضية بس أحسن

**Expected output** (the question is asked in the language the user dictated in)
```
ما أقدر أحدد المطلوب: شنو الشي اللي سويته المرة الماضية (الملف أو الموضوع)؟ وشنو تقصد بـ "أحسن"؟
```

**Why:** the request depends on missing context, and a guess would waste a full response. Ask one short question instead of inventing a task.

---

## 6. Already clean: do not over-edit or translate

**Input**
> لخص لي هذا المقال بثلاث نقاط.

**Expected output**
```
لخص لي هذا المقال بثلاث نقاط.
```

**Why:** the prompt is already short and clear. Leave it unchanged, in its original language.

---

## 7. English dictation

**Input**
> so um I need you to like write a SQL query, basically get the top 5 customers by revenue last quarter, from the orders table, and uh make it Postgres, not MySQL, yeah

**Expected output**
```
Write a Postgres query that returns the top 5 customers by revenue last quarter from the orders table.
```

**Why:** English in, English out. Filler is removed, and the number (5), the table name, and the dialect are kept.
