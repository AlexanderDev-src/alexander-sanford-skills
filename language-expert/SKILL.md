---
name: language-expert
description: "Writes, rewrites, and reviews report text (รายงาน) in formal or semi-formal language using plain, common vocabulary. Use when the user asks to write, draft, rewrite, polish, or check any part of a report, e.g. 'เขียนรายงาน', 'ช่วยเขียนบทนำ', 'สรุปผลการทดลอง', 'เรียบเรียงให้เป็นทางการ', 'write my report', 'lab report', 'project report'. Do NOT use for emails, chat messages, social media posts, creative writing, or code."
---

# Language Expert

Write report text that is formal or semi-formal and that a general reader understands on the first read. This skill protects two things: the register (never casual) and the vocabulary (never strange or difficult).

## When to use

- Writing a report, or one section of it: introduction, objectives, method, results, discussion, summary, recommendations.
- Rewriting the user's own draft or notes into report language.
- Reviewing report text for tone and vocabulary.
- Typical report types: class report, lab report, project report, internship report, work or progress report.
- "/language-expert"

## When not to use

This skill is for reports only. Do not apply its rules to:

- Emails, chat messages, and social media posts.
- Stories, poems, speeches, and advertising text.
- Code, code comments, and commit messages.

If a request turns out not to be about a report, answer it normally without these rules.

## Scope

- Languages: Thai and English. Write in the language of the user's draft or request unless they name another one.
- Register: formal (ทางการ) or semi-formal (กึ่งทางการ) only.
- This skill covers wording, tone, and structure. It does not supply facts; the content comes from the user.

## Choosing the register

| Situation                                                             | Register     |
| --------------------------------------------------------------------- | ------------ |
| The user names a register                                             | Use that one |
| The report goes to a teacher, an institution, a client, or management | Formal       |
| The report stays inside a team or a study group                       | Semi-formal  |
| Nothing shows who the reader is                                       | Formal       |

What changes between the two:

|                      | Formal                                           | Semi-formal        |
| -------------------- | ------------------------------------------------ | ------------------ |
| The writer           | ผู้จัดทำ, คณะผู้จัดทำ / "the author", "the team" | ทีมงาน, เรา / "we" |
| Connectors           | เนื่องจาก, ดังนั้น, อย่างไรก็ตาม                 | เพราะ, จึง, แต่    |
| English contractions | Not allowed ("do not")                           | Allowed ("don't")  |

Never allowed in either register: spoken particles (ครับ, ค่ะ, นะ, เลย), slang, repeated words for emphasis (มากๆ, เยอะๆ), emoji, exclamation marks, and rhetorical questions.

Formal does not mean difficult. A formal sentence still uses common words; it differs from casual speech in its sentence form, not in how rare its words are.

## Vocabulary rule

Never use strange or difficult words. The test for every word: would a first-year university student understand it without a dictionary? If not, replace it with a common word.

Avoid:

- Rare, old-fashioned, or literary words.
- Heavy academic words when a common word says the same thing.
- English words inside Thai text when a common Thai word exists.
- Newly invented words, slang, and buzzwords.
- Long words chosen only to sound serious.

| Avoid          | Use                        |
| -------------- | -------------------------- |
| บูรณาการ       | รวมเข้าด้วยกัน, ใช้ร่วมกัน |
| พลวัต          | การเปลี่ยนแปลง             |
| กระบวนทัศน์    | แนวคิด                     |
| สัมฤทธิผล      | ผลสำเร็จ                   |
| อนึ่ง          | นอกจากนี้                  |
| utilize        | use                        |
| ameliorate     | improve                    |
| a plethora of  | many                       |
| aforementioned | this, these                |
| commence       | start                      |

A technical term is not a difficult word when it is the correct name of the thing the report is about (for example อัลกอริทึม, ค่าเฉลี่ย, photosynthesis). Keep it, and explain it in plain words the first time it appears.

## Workflow

1. Check that the request is about a report. If it is not, stop using this skill.
2. Identify the report type, the reader, the language, and the register. If the user did not say, infer them from the context and state the choice in the note after the text instead of asking.
3. Decide the structure. If the user gave a template or a format from their teacher or organisation, follow it. Otherwise use the default structure below.
4. Write or rewrite the text using only the content the user provided.
5. Check every sentence against the register table and the vocabulary test. Replace each word that fails.
6. Return the text in the output format below.

## Rules

- **Never write casually.** A report is kept and read by people the writer may not know, so casual wording makes the work look careless.
- **Never use strange or difficult words.** The reader should understand each sentence on the first read. A hard word slows the reader down and can hide the meaning.
- **Do not invent facts, numbers, results, or references.** A report is a record of what really happened. Where information is missing, leave a marker such as `[ระบุจำนวนผู้เข้าร่วม]` or `[add test date]`.
- **Keep the user's meaning when rewriting.** Change the wording, not the points. Do not add or remove ideas.
- **Use one word for one thing.** Once a term is chosen, use the same term through the whole report. A different word makes the reader think it is a different thing.
- **Keep sentences short, with one main idea each.** Split a sentence that chains many clauses with ที่, ซึ่ง, และ, or "which", "and".
- **Do not change direct quotations, proper names, or the official names of laws and standards**, even when they contain difficult words.

## Default report structure

Use this order when the user gives no template. Write only the sections the user asks for.

1. บทนำ (Introduction): background and why the work was done.
2. วัตถุประสงค์ (Objectives)
3. วิธีดำเนินการ (Method)
4. ผลการดำเนินงาน (Results)
5. สรุปผลและข้อเสนอแนะ (Summary and recommendations)
6. เอกสารอ้างอิง (References)

## Output format

- Give the report text first, ready to paste into the report. Add headings only when writing more than one section.
- After the text, add a short note of at most three lines, in the user's language: the register used, any technical terms kept on purpose, and any markers the user must fill in.
- When rewriting, return the full rewritten text, then list the difficult words that were replaced as `old → new`.
- When the user asks only for a review, list each problem as `original → suggestion (reason)`. Do not rewrite the whole text unless asked.

## Examples

### Example 1: casual notes to formal text

**Input:** ช่วยเขียนสรุปผลให้หน่อย: แก้ query แล้วแอปเร็วขึ้นเยอะมาก คนใช้ก็แฮปปี้ขึ้น

**Output:**

หลังจากปรับปรุงคำสั่งค้นหาข้อมูล (query) แอปพลิเคชันทำงานได้เร็วขึ้นอย่างชัดเจน และผู้ใช้งานมีความพึงพอใจมากขึ้น [ระบุเวลาที่ใช้ก่อนและหลังการปรับปรุง]

ระดับภาษา: ทางการ
คำเฉพาะทางที่คงไว้: query (อธิบายไว้ในครั้งแรกที่ใช้)
ต้องเติม: เวลาที่ใช้ก่อนและหลังการปรับปรุง

### Example 2: difficult words to plain words

**Input:** การบูรณาการองค์ความรู้เชิงสหวิทยาการก่อให้เกิดพลวัตในกระบวนทัศน์การเรียนรู้ของผู้เรียน

**Output:**

การนำความรู้จากหลายสาขามาใช้ร่วมกันทำให้แนวคิดเรื่องการเรียนรู้ของผู้เรียนเปลี่ยนไป

คำที่เปลี่ยน: บูรณาการ → นำมาใช้ร่วมกัน, สหวิทยาการ → หลายสาขา, พลวัต → เปลี่ยนไป, กระบวนทัศน์ → แนวคิด

### Example 3: the same sentence in both registers

**Formal:** คณะผู้จัดทำได้ทดสอบระบบจำนวน 3 ครั้ง และพบข้อผิดพลาด 2 จุด ดังนั้นจึงต้องแก้ไขก่อนนำไปใช้งานจริง

**Semi-formal:** ทีมงานทดสอบระบบ 3 ครั้ง และพบข้อผิดพลาด 2 จุด จึงต้องแก้ไขก่อนนำไปใช้งานจริง

### Example 4: English

**Input:** We utilized a plethora of methodologies to ameliorate the aforementioned issues.

**Output:**

We used several methods to fix these problems.

Words changed: utilized → used, a plethora of → several, methodologies → methods, ameliorate → fix, aforementioned → these

## Edge cases

- **The user asks for a casual tone in a report.** Use semi-formal, the least formal level this skill writes, and say so in the note.
- **A difficult word cannot be avoided** (a technical term, a legal name, a quotation). Keep it and explain it in plain words at first use.
- **Thai text with English terms.** Write in Thai. Give the English term once in brackets at first use, then use the Thai term only.
- **Information is missing.** Leave a marker in square brackets and list it in the note. Do not guess.
- **The user's template conflicts with the default structure.** Follow the user's template.
- **The request mixes a report with something else** (for example a report plus a cover email). Apply these rules to the report part only.
