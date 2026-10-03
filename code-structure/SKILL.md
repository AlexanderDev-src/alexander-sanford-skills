---
name: code-structure
description: "Sets the structure and the comment style of new code. Use every time code is written from scratch, in any language: a new project, app, API, script, tool, module, file, class, or function that does not exist yet, even when the user says nothing about structure or architecture. Triggers: 'สร้างโปรเจคใหม่', 'เขียนโค้ดให้หน่อย', 'เขียนโปรแกรม', 'ทำเว็บ', 'เริ่มจากศูนย์', 'เขียนใหม่ทั้งหมด', 'build me', 'create a new', 'write a script', 'scaffold', 'implement', 'from scratch'. Applies three rules: shape the code with category theory (small pure functions that compose, data modelled as types, side effects at the edge), use Clean Architecture only when the project is truly big, and keep comments few, short, and in simple words. Do NOT use for editing, fixing, or reviewing code that already exists, or for explaining code without writing any."
---

# Code Structure

Shape all new code the same way: small parts that join cleanly, a structure that fits the real size of the project, and comments only where they help. This skill protects three things: composition (category theory), the right amount of structure (Clean Architecture only when the project is big), and quiet, plain comments.

## When to use

- Starting a new project, app, service, library, or script.
- Writing a new module, file, class, or function that does not exist yet.
- Rewriting something from zero ("เขียนใหม่ทั้งหมด", "start over").
- "/code-structure"

## When not to use

- Changing code that already exists: editing, fixing a bug, refactoring. Follow the style the code already has.
- Reviewing or explaining code without writing new code.
- Config files, data files, and plain text.

If a request turns out not to be about new code, answer it normally without these rules.

## Workflow

1. Check that the request is for new code. If it changes existing code, stop using this skill.
2. Pick the project size from the table in Rule 2. When unsure, pick the smaller one.
3. Model the data first: write the types before the logic.
4. Write small pure functions that turn one type into the next, then join them into the full behavior.
5. Put every side effect in a thin outer layer that calls the pure functions.
6. Add a comment only where Rule 3 allows one.
7. Run the final check, then return the code in the output format.

## Rule 1: Category theory

Category theory is used here to shape the code, not to name things. The idea: types are the objects, functions are the arrows between them, and a program is built by joining arrows end to end. Code built this way is easy to test (no setup), easy to reuse, and safe to change, because each part can be read alone.

| Idea                   | What to do in the code                                                                                                                                              |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Composition            | Write small functions with a clear input type and output type. Make the output of one fit the input of the next, then build bigger behavior by joining them.         |
| Identity, associativity | Any part of a chain can be pulled out into a named function without changing the result. This holds only when a function depends on its arguments and nothing else. |
| Pure arrows            | Keep the logic pure: same input, same output, nothing else changed. Push side effects (file, network, database, clock, random, print) to the edge of the program.    |
| Immutable data         | Return a new value instead of changing the input. Changing a local variable is fine when nothing outside the function can see it.                                    |
| Product type           | Group values that belong together into one record or struct ("this AND that") instead of passing loose arguments.                                                    |
| Sum type               | Model "this OR that" as an enum or tagged union, not as flags, magic strings, or null. A state that makes no sense should be impossible to build.                    |
| Functor (`map`)        | Change the values inside a container (list, optional, result, future) with `map`. A `map` changes values only: it keeps the shape and has no side effects.           |
| Monad (chaining)       | Chain steps that can be missing or can fail with the language's own tool (`?`, `and_then`, `flatMap`, `?.`) instead of deep nested `if` and `try`.                   |
| Monoid (combining)     | When values are merged (totals, lists, settings, counts), write one combine function and one empty value, then use `fold` or `reduce`.                               |

Limits, so the theory does not make the code worse:

- **Use the language's own tools.** Do not build a category theory library or copy Haskell into another language. Use what the language already has (table below), because the next reader knows those tools.
- **No theory words in names or comments.** Write `parse_order`, not `OrderKleisli`. Write "apply to each item", not "fmap over the functor". The exception is an ecosystem that already uses these names (Haskell, Scala Cats, fp-ts).
- **Do not force it.** Three clear lines are better than one clever chain. If a long chain or a point-free style is harder to read, use plain named steps.

| Language      | "This OR that"                                         | Missing or failed                                      | Chaining                                   |
| ------------- | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------ |
| Rust          | `enum`                                                 | `Option`, `Result`                                     | `?`, `map`, `and_then`, iterators          |
| TypeScript    | union with a `kind` field                              | `T \| undefined`; a `Result` union for expected errors | `map`, `filter`, `reduce`, `?.`            |
| Python        | `Enum`, or a union of frozen dataclasses with `match`  | `T \| None`; raise an exception, catch it at the edge  | comprehensions, generators, `reduce`       |
| Java, Kotlin  | sealed interface with records, sealed class            | `Optional`, nullable types                             | streams, `map`, `let`                      |
| Go            | small interface, or a struct with a kind field         | `(value, error)`, `(value, ok)`                        | early returns                              |
| C, C++        | `enum` with `union`, `std::variant`                    | return code, `std::optional`, `std::expected`          | plain calls                                |

## Rule 2: Structure by size

Clean Architecture costs extra files, interfaces, and mapping code. That cost pays back only in a big project. In a small one it hides a few lines of logic under many folders. Pick the structure from the real size of the work, not from how serious the request sounds.

| Size   | Signs                                                   | Structure                                                                                |
| ------ | ------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| Small  | One job: a script, a tool, an exercise, one feature.    | One file, or a few. Pure functions at the top, one entry function with the I/O below.    |
| Medium | Several features, one app, one database or API.         | One folder per feature. Inside each: the pure logic in one file, the I/O in another.     |
| Big    | The user asks for it, or three or more signs below.     | Clean Architecture.                                                                      |

Signs of a big project:

- The user says it is big, long-lived, or built by a team.
- Many features with real business rules, not only create, read, update, delete.
- Two or more outside systems (database, third-party API, queue, storage).
- Two or more ways in (web API, CLI, background worker, mobile app).
- A stated need to swap a part later, or to test the rules without the database.

When unsure, choose the smaller structure. Growing a small structure later is cheap; removing unused layers is not.

### When Clean Architecture applies

Folders, listed from the inside out:

```
src/
  exceptions/     error types; imports nothing
  domain/         core types and pure rules; imports only exceptions
  usecases/       one action per file; declares the repository interfaces it needs
  repositories/   database and outside API code; implements those interfaces
  models/         database row shapes; used only by repositories
  controllers/    HTTP or CLI handlers; turn a request into a use case call
  dto/            request and response shapes; used only by controllers
  main            builds the repositories and passes them to the use cases
```

- Imports point inward only: `controllers` → `usecases` → `domain`, and `repositories` → `usecases` → `domain`. The domain never imports a framework, a database driver, or an HTTP library. The folders sit side by side, so the tree does not show this direction: check the imports.
- Rule 1 still holds. `domain` is the pure core, a repository interface is a function type, and `repositories` and `controllers` are the edge where the side effects live.
- Add a type to `dto/` or `models/` only when its shape differs from the domain type (the API hides a field, the table stores it another way). When the fields are the same, use the domain type, and leave out a folder that would be empty.
- Add a part only when it does real work. No interface with one implementation that crosses no I/O boundary, and no use case that only forwards a call.
- When a folder passes about ten files, group by feature first (`orders/`, `users/`) and keep these folders inside each feature.
- Use the names the language expects: `errors/` where errors are returned as values (Rust, Go), `internal/` in Go, packages in Java.

## Rule 3: Comments

The default is no comment. Names and types should say what the code does. Most functions need none, and a file with zero comments is normal. A comment is one more thing to read and to keep true: long or frequent comments hide the code and go out of date, while a short one in simple words gets read.

Write a comment only when the code cannot say it:

- **The reason**, when it is not obvious: a business rule, a workaround, a choice that looks wrong but is right.
- **A unit, limit, or format** that the type does not show (`// seconds`, `// sorted, oldest first`).
- **A warning** about something that breaks if it is changed.
- **A one-line doc** on a public function, where the language expects one (docstring, rustdoc, JSDoc, godoc).

How to write it:

- **Short.** One line, about twelve words or fewer. If it needs more than two lines, make the code simpler or the name better instead.
- **Simple words.** Words a first-year student knows: "use", not "utilize"; "check", not "validate the integrity of".
- **English**, unless the user asks for another language.

Do not write:

- A comment that repeats the code or the function name.
- Section banners (`// ===== HELPERS =====`) and decorative lines.
- Commented-out code.
- Notes about the conversation or the edit: "as requested", "new version", "fixed here".
- A doc block that lists every parameter when the names and types already explain them.
- Emoji, or shouting (`IMPORTANT!!!`).

| Avoid                                                                                                    | Use                                                     |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| `// This function iterates over every user and validates that each email conforms to the correct format` | no comment; name the function `invalid_emails`          |
| `// Initialize the counter variable to zero`                                                             | no comment                                              |
| `timeout = 30  // set the timeout`                                                                       | `timeout = 30  // seconds`                              |
| `// We utilize exponential backoff in order to mitigate rate limiting`                                   | `// Wait longer on each retry: the API limits requests.` |
| `// IMPORTANT!!! DO NOT TOUCH`                                                                           | `// Order matters: auth must run before logging.`       |

## Final check

- Does each function do one job and depend only on its arguments?
- Is every side effect in the outer layer?
- Can the types build a state that makes no sense? If yes, change the types.
- Is this the smallest structure that fits the project?
- For each comment: would the reader lose anything if it were deleted? If not, delete it.
- Is each remaining comment one short line in simple words?

## Output format

- Before the code, state the structure in one line: the size and the layout, for example "Small: one file, pure functions and a `main`".
- For a medium or big project, show the folder tree first, then the files.
- Do not add a lesson on category theory or architecture unless the user asks for one.

## Examples

### Example 1: a small script

**Input:** เขียนสคริปต์อ่าน orders.json แล้วพิมพ์ยอดรวมที่บวก VAT 7%

**Avoid:** one function that does everything, with comments that repeat the code.

```python
# This function is responsible for opening the JSON file, loading all of the
# orders, iterating through every order to compute the subtotal, applying the
# value added tax, and finally printing the result to the console.
def process():
    f = open("orders.json")  # open the file
    data = json.load(f)
    total = 0  # initialize total to zero
    # Loop over all items
    for d in data:
        total += d["price"] * d["qty"]
    print(total * 1.07)
```

**Output:**

Small: one file, pure functions and a `main`.

```python
import json
from dataclasses import dataclass

VAT_PERCENT = 7


@dataclass(frozen=True)
class Item:
    price: int  # satang
    qty: int


def subtotal(items: list[Item]) -> int:
    return sum(item.price * item.qty for item in items)


def with_vat(amount: int) -> int:
    return amount + amount * VAT_PERCENT // 100


def total(items: list[Item]) -> int:
    return with_vat(subtotal(items))


def load_items(path: str) -> list[Item]:
    with open(path) as file:
        return [Item(**row) for row in json.load(file)]


def main() -> None:
    print(total(load_items("orders.json")))


if __name__ == "__main__":
    main()
```

The data has a type, `total` is two pure functions joined together, and the file and the screen are touched only in `load_items` and `main`. The file has one comment: the unit, the only thing the code could not say.

### Example 2: "this OR that" as a type

**Avoid:** flags that allow a state that makes no sense (card and cash at once, or a card with no number).

```ts
type Payment = { isCard: boolean; isCash: boolean; last4?: string; bank?: string };
```

**Use:**

```ts
type Payment =
  | { kind: "card"; last4: string }
  | { kind: "cash" }
  | { kind: "transfer"; bank: string };
```

### Example 3: choosing the size

| Request                                                                              | Size   | Structure                                        |
| ------------------------------------------------------------------------------------ | ------ | ------------------------------------------------ |
| เขียนสคริปต์เปลี่ยนชื่อไฟล์ในโฟลเดอร์                                                   | Small  | One file                                         |
| ทำ REST API ร้านกาแฟ มีเมนู ออเดอร์ สมาชิก ใช้ฐานข้อมูลเดียว                           | Medium | One folder per feature, pure logic apart from I/O |
| ระบบขายของออนไลน์: เว็บ, API สำหรับมือถือ, worker, Postgres, Stripe, อีเมล, ทีม 5 คน | Big    | Clean Architecture                               |

## Edge cases

- **A new file inside an existing project.** The project's own conventions come first. Apply these rules only where they do not conflict.
- **A framework sets the layout** (Django, Rails, Next.js, Spring, Flutter). Follow the framework's layout. Keep the logic in plain pure functions that the framework code calls.
- **The language lacks a feature** (no sum types, no `Option`). Use the closest native idiom from the language table. Do not fake the feature with a homemade library.
- **Classes are expected** (Java, C#, or the user asks for OOP). Classes are fine: data classes that do not change, methods that return new values, small interfaces. The same rules apply.
- **Speed matters.** Loops and local mutation are fine inside a function, as long as the function stays pure from the outside.
- **Very small code** (a 20-line script, one function). No separate types file and no folders. Still keep the logic pure and the I/O at the edge.
- **The user asks for Clean Architecture on a small project.** Use it. Note in one line that a smaller layout would also work.
- **The user asks for many comments** (a lesson, a lab hand-in, a teacher's rule). Follow the user on how many. Still keep each one short and in simple words.
