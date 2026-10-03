# alexander-sanford-skills

This repository is a collection of skills for Claude Code. A skill is a set of instructions, written in a `SKILL.md` file, that tells Claude how to work on one kind of task. When a request matches the description of a skill, Claude applies that skill.

The skills are written in English. Their descriptions include trigger phrases in both Thai and English.

## Skills in this repository

The repository currently holds four skills.

| Skill             | What it does                                                                 | When it is used                                                                                 |
| ----------------- | ---------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `code-structure`  | Sets the structure of new code and the style of its comments.                | Code is written from scratch: a new project, a new file, or a new function.                     |
| `friendly-friend` | Sets the voice of the reply to that of a warm and honest friend.             | Every conversation, above all when the user shares work, asks for advice, or feels discouraged. |
| `language-expert` | Writes, rewrites, and reviews report text in formal or semi-formal language. | A report is written or edited.                                                                  |
| `orator`          | Teaches a programming topic with an answer that always has three parts.      | The user wants to learn or understand a topic.                                                  |

## Details of each skill

### code-structure

This skill applies three rules to new code.

1. Shape the code with ideas from category theory: split the work into small functions that can be joined together, define the data types before the logic, and keep the parts that reach outside the program (files, the network, the database) at its edge.
2. Choose the structure by the size of the project. A small task uses one file. A medium task uses one folder for each feature. Clean Architecture, a way of dividing code into layers by responsibility, is used only for a large project or when the user asks for it.
3. Write comments only where they are needed. Each comment must be short and must use simple words.

This skill does not apply to editing, fixing, or reviewing code that already exists.

### friendly-friend

This skill sets the voice of the chat reply. It does not set the content.

- In Thai, it uses the words เรา ("I"), นาย ("you"), and เอง (a soft emphasis word), together with emoji or kaomoji that fit the mood. A kaomoji is a face made from text characters.
- It names what is good first, even when the good thing is small, and it states exactly where the good thing is.
- It treats the mistakes of a first attempt as normal.
- It still states a real problem clearly. It selects the one or two most important problems and gives the reason and the next step for each.
- It praises only what is truly good, and it does not agree only to keep the mood pleasant.

This skill does not apply to content written for other readers, such as code, reports, and emails.

### language-expert

- It supports Thai and English.
- It writes in a formal or semi-formal register only.
- It does not use strange or difficult words. The test is whether a first-year university student would understand the word without a dictionary.
- It does not invent facts, numbers, or references. Where information is missing, it leaves a marker in square brackets for the user to fill in.

This skill does not apply to emails, chat messages, creative writing, or code.

### orator

- Every answer has three parts in the same order: the topic, what it is, and example code.
- It leaves blank lines between headings, paragraphs, and code so that the answer is easy to read.
- The example code is short, runs as written, and shows only the topic being taught.

This skill does not apply when the user wants code written, fixed, or reviewed in a project.

## Repository structure

```
.
├── code-structure/
│   └── SKILL.md
├── friendly-friend/
│   └── SKILL.md
├── language-expert/
│   └── SKILL.md
├── orator/
│   └── SKILL.md
└── README.md
```

Each folder is one skill. A `SKILL.md` file has two parts.

- The header states the `name` and the `description` of the skill. Claude uses the description to decide when to apply the skill.
- The body states the rules, the steps, and examples.

## Installation

The following steps are for Claude Code.

1. Clone the repository.

   ```bash
   git clone https://github.com/AlexanderDev-src/alexander-sanford-skills.git
   cd alexander-sanford-skills
   ```

2. Copy the folders of the skills you need into `~/.claude/skills/`.

   ```bash
   mkdir -p ~/.claude/skills
   cp -r code-structure friendly-friend language-expert orator ~/.claude/skills/
   ```

3. Check the list of skills in Claude Code. If a skill does not appear, restart Claude Code.

To use a skill in one project only, copy its folder into the `.claude/skills/` directory of that project instead.

## Usage

A skill is applied in one of two ways.

- Claude applies the skill by itself when a request matches the description of the skill.
- The user calls the skill directly by typing `/` followed by the name of the skill, for example `/language-expert`.

Example requests and the skill that handles each one:

| Request                                                                   | Skill             |
| ------------------------------------------------------------------------- | ----------------- |
| Write a script that reads `orders.json` and prints the total with 7% VAT. | `code-structure`  |
| This is my first to-do web app. Could you take a look?                    | `friendly-friend` |
| Help me write the introduction of my report.                              | `language-expert` |
| What is a closure?                                                        | `orator`          |
