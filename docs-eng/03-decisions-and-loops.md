# Module 03, Decisions and Loops

[Português](../docs/03-decisoes-e-repeticoes.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // The problem

A Login form needs to behave differently depending on what was typed: an empty field blocks submission, an e-mail without "@" blocks submission, everything correct allows submission. A Dashboard needs to go through each group in the list to decide how to show it. None of this is possible with code that only runs one line after another, always the same way: you need to *decide* and *repeat*.

## // `if`, `else if`, `else`

```javascript
const participantes = 8;

if (participantes >= 10) {
  console.log("Group full");
} else if (participantes >= 5) {
  console.log("Almost full");
} else {
  console.log("Spots available");
}
```

JavaScript tests the conditions **from top to bottom** and enters the first true block, ignoring the rest. That is why the order of the conditions matters. If `participantes >= 5` came before `participantes >= 10`, a group with 12 participants would fall into the wrong block ("Almost full"), because 12 is also `>= 5`.

## // Truthy and falsy values

Inside a condition, JavaScript automatically converts any value to `true` or `false`. The list of what is treated as false is short; it is worth memorizing:

> **FALSY: THE ONLY VALUES TREATED AS FALSE**
> `false`, `0`, `""` (empty string), `null`, `undefined` and `NaN`. Practically any other value, including `"0"` (a string) and empty arrays `[]`, is treated as true.

```javascript
const nome = "";
if (!nome) {
  console.log("Name not filled in");
}
```

`!nome` can be read as "there is no name filled in", and it works because an empty string is falsy. That reading ("there is no X") is a natural way to check for empty fields before moving on with any logic.

## // `for`: repeating a known number of times

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i); // 0, 1, 2, 3, 4
}
```

The three parts inside the parentheses: `let i = 0` (starting point), `i < 5` (condition to keep going), `i++` (what changes on each round). The loop stops as soon as the condition becomes false.

## // `for...of`: going through the values of a collection

```javascript
const materias = ["Cálculo I", "Estrutura de Dados", "Banco de Dados"];

for (const materia of materias) {
  console.log(materia);
}
```

Unlike the traditional `for`, `for...of` does not work with an index: on each round, it hands you the collection's next *value* directly. For arrays of data (the most common case in the rest of this week), `for...of` is usually more direct to read than managing an index by hand.

## // `while`: repeating while a condition is true

```javascript
let tentativas = 0;
while (tentativas < 3) {
  console.log("Attempt " + tentativas);
  tentativas++;
}
```

Use `while` when you do not know in advance *how many* times you will repeat: you only know the condition that must stay true. `for` is more common when the number of repetitions is already known (like going through an array).

> **WATCH OUT FOR INFINITE LOOPS**
> If a `while` condition never becomes false (for example, if you forget the `tentativas++`), the code freezes the browser tab, repeating forever. Always make sure there is something inside the loop that eventually makes the condition false.

## // Good example × bad example

**Bad example**: the order of the conditions hiding a case:

```javascript
if (participantes >= 0) {
  console.log("Spots available");
} else if (participantes >= 10) {
  console.log("Group full"); // will never run
}
```

Since `participantes >= 0` is true for practically any valid number, the second block is never reached.

**Good example**: the most restrictive condition first:

```javascript
if (participantes >= 10) {
  console.log("Group full");
} else if (participantes >= 0) {
  console.log("Spots available");
}
```

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| The wrong block runs | Conditions in the wrong order, a broader one "catching" the case before the more specific one | Put the most restrictive conditions first |
| A loop that never ends | Forgetting to update the variable the `while` condition depends on | Make sure there is an update inside the loop |
| `for...of` used to try to get the index | `for...of` gives you the value, not the position | Use a traditional `for`, or `array.forEach((item, indice) => ...)`, if you need the index |
| Mixing up `=` and `===` inside an `if` | A common typo | `=` assigns a value (and should not appear inside an `if`); `===` compares |

## // Guided practice

1. In `script.js`, create a `materias` array with at least 4 strings.
2. Use `for...of` to print each subject in the console, preceded by "Subject: ".
3. Write an `if/else if/else` that takes a number of participants and prints "Full", "Almost full" or "Spots available", following the logic in this section.
4. Test with at least three different values, confirming each one falls into the right block.

## // Practice on your own

> **CHALLENGE**
> Write a `for` that prints, from 1 to 10, only the even numbers (tip: use `%` to check whether the remainder of dividing by 2 is zero). Then rewrite the same logic using `while`, and confirm the result is identical.

## // Applying it to the week's project

1. In `script.js`, write a `for...of` that goes through a list of subjects from your project and prints each one in the console. This does not show on screen yet (that comes in Module 12), but it confirms the repetition logic is correct before connecting it to the DOM.
2. Write a real `if/else` condition from your project: for example, deciding on a different message depending on how many participants a group has.
3. Commit: `git commit -m "Add initial decision and loop logic"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> You have an array with 5 subjects and need to decide, for each one, whether the name is "long" (more than 15 characters) or "short". Which combination of tools from this module solves that?

Answer: a `for...of` to go through the array, combined with an `if/else` inside the loop, comparing `materia.length > 15` on each round. The repetition (`for...of`) guarantees every subject is evaluated; the decision (`if/else`), inside the loop, handles each one individually.

## // Module summary

- [ ] I can write `if`, `else if`, `else`, and I know why the order of the conditions matters.
- [ ] I can list the values treated as falsy.
- [ ] I know the difference between `for`, `for...of` and `while`, and when to use each one.
- [ ] I can recognize the risk of an infinite loop.
- [ ] I have already written at least one real decision and one real loop in my project.

---

**Next module:** `04-functions-and-arrow-functions.md`: decisions and loops already work on their own. Time to organize them into reusable blocks.

`Study Material // Coffee & Code`
