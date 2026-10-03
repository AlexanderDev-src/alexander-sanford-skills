---
name: orator
description: >
  Teaches a programming topic with a fixed three-part answer: (1) the topic
  being answered, (2) what it is, (3) example code, laid out with clear blank
  lines so nothing is cramped. Use when the user wants to learn or understand
  something rather than get a task done, e.g. "คืออะไร", "อธิบายหน่อย",
  "สอนหน่อย", "ยกตัวอย่าง", "ต่างกันยังไง", "what is", "explain", "how does X
  work", "show me an example". Do NOT use when the user wants code written,
  fixed, or reviewed in their project, or wants report text (use
  language-expert for that).
---

# Orator

Teach one topic at a time with an answer that always has the same three parts, in the same order, with enough blank space that each part is easy to find. The learner should know where to look before they start reading.

## When to use

- The user asks what something is: "closure คืออะไร", "what is a pointer".
- The user asks for an explanation or an example: "อธิบาย async/await หน่อย", "ยกตัวอย่าง recursion".
- The user asks how two things differ: "list กับ tuple ต่างกันยังไง".
- "/orator"

## When not to use

- The user wants code written, fixed, or reviewed in their project. That is a task, not a lesson.
- The user wants report text. Use language-expert.
- The user asks a quick factual question that needs one line, such as a command flag or a version number.

## Answer structure

Every answer has these three parts, numbered, in this order. Do not skip a part and do not add other top-level parts.

| Part | Thai heading | English heading | What goes in it |
|---|---|---|---|
| 1 | `## 1. หัวข้อ` | `## 1. Topic` | The name of the topic and one sentence saying what this answer covers. |
| 2 | `## 2. คืออะไร` | `## 2. What it is` | What it is in plain words, then what it is used for. No code here. |
| 3 | `## 3. โค้ดตัวอย่าง` | `## 3. Example code` | One small example that runs, then a short list explaining what happens. |

Use the headings in the language of the user's question. Keep technical terms and code in English.

### Part 1: Topic

- Name the topic and the language or tool it belongs to, for example "Closure ใน JavaScript".
- Add one sentence saying what the answer covers. If the question was unclear, this is where the chosen meaning is stated.

### Part 2: What it is

- Start with one sentence that defines the topic in plain words.
- Follow with what problem it solves or when to use it.
- Keep it to two short paragraphs at most. Detail belongs in the example.

### Part 3: Example code

- Give one example that shows only this topic. Leave out everything the topic does not need.
- The example must be complete and must run as written.
- Show the result, either as a comment beside the line or in a separate block.
- After the code, explain what happens in a short list, one point per step.

## Spacing rules

These rules exist because a learner reads slowly and looks back often. Text that is packed together hides where one idea ends and the next one starts.

In the text:

- Put one blank line before and after every heading, every code block, and every list.
- Put one blank line between paragraphs.
- Keep a paragraph to two sentences at most. Start a new paragraph for a new idea.
- When any list item is longer than one line, put a blank line between the items.
- When the answer covers more than one topic, separate the topics with `---` and a blank line on each side.
- Use exactly one blank line each time. Two or more in a row make the answer look broken.

In the code:

- Put a blank line between logical steps: setting up, doing the work, showing the result.
- Write one statement per line.
- Put a comment on its own line above the code it describes, not at the end of a long line.
- Put spaces around operators and after commas.

Cramped, do not write this:

```python
def average(nums):
    total=0
    for n in nums: total+=n
    return total/len(nums)
print(average([2,4,6]))
```

Spaced, write this:

```python
def average(nums):
    total = 0

    for n in nums:
        total += n

    return total / len(nums)


print(average([2, 4, 6]))  # 4.0
```

## Teaching rules

- **Use plain words.** Explain a technical term in a few words the first time it appears, so the learner does not have to stop and look it up.
- **Teach one topic per block.** A second topic gets its own three parts. Mixing two topics in one example makes it unclear which line shows which idea.
- **Answer in the user's language.** Write comments inside the code in that language too, since the comments are part of the lesson.
- **Keep the example short**, about 25 lines at most. A long example makes the learner search for the lines that matter.
- **Use names that say what the thing is**, such as `count` and `makeCounter`, not `x` and `foo`.
- **Do not teach more than was asked.** Related topics can be named in one closing line, not explained.

## Template

````markdown
## 1. หัวข้อ

<topic name and the language or tool>

<one sentence: what this answer covers>

## 2. คืออะไร

<one-sentence definition in plain words>

<what problem it solves, or when to use it>

## 3. โค้ดตัวอย่าง

```<language>
<small example that runs, with blank lines between steps>
```

<one line introducing the explanation>

- <step 1>
- <step 2>
- <step 3>
````

## Example

**Input:** closure คืออะไร

**Output:**

````markdown
## 1. หัวข้อ

Closure ใน JavaScript

คำตอบนี้อธิบายว่า closure คืออะไร และใช้ทำอะไร

## 2. คืออะไร

Closure คือฟังก์ชันที่ยังจำตัวแปรของฟังก์ชันด้านนอกได้ แม้ฟังก์ชันด้านนอกจะทำงานจบไปแล้ว

ใช้เมื่อต้องการเก็บค่าไว้ใช้ต่อ โดยไม่ให้โค้ดส่วนอื่นเข้ามาแก้ค่านั้นโดยตรง

## 3. โค้ดตัวอย่าง

```javascript
function makeCounter() {
  // count เป็นตัวแปรของ makeCounter
  let count = 0;

  // ฟังก์ชันด้านในจำ count ไว้ได้
  return function () {
    count = count + 1;
    return count;
  };
}

const counter = makeCounter();

console.log(counter()); // 1
console.log(counter()); // 2
```

สิ่งที่เกิดขึ้นในโค้ด:

- `makeCounter` สร้างตัวแปร `count` แล้วคืนฟังก์ชันด้านในออกมา
- ฟังก์ชันด้านในยังจำ `count` ได้ ค่าจึงเพิ่มขึ้นทุกครั้งที่เรียก
- โค้ดด้านนอกแก้ `count` โดยตรงไม่ได้ ต้องเรียกผ่าน `counter()` เท่านั้น
````

## Edge cases

- **The question covers several topics.** Write the three parts once per topic and separate the topics with `---`.
- **The question compares two things.** Part 1 names the comparison. Part 2 gives one short paragraph for each thing, then one for the difference. Part 3 shows one small code block for each thing.
- **No programming language is given.** Use the language of the open file or of the conversation so far. If there is none, pick the language most often used for that topic and name it in Part 1.
- **The topic has no code** (for example a working method or a general idea). Show the closest code that makes it concrete. If there truly is none, give a worked example in words and name Part 3 `## 3. ตัวอย่าง`.
- **A short follow-up on the same topic** ("แล้วบรรทัดนี้ทำอะไร"). Answer it directly without repeating all three parts, but keep the spacing rules.
- **The user asks to change their code in the middle of a lesson.** That is a task. Stop using this skill for that request.
