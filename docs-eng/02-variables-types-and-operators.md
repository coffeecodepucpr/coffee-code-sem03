# Module 02, Variables, Types and Operators

[Português](../docs/02-variaveis-tipos-e-operadores.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // The problem

Any program needs to store values temporarily: the name typed into a field, the number of groups found, whether a form is valid or not. Without a way to store and name these values, every line of code would have to recalculate everything from scratch, with no memory of what was already processed.

## // Variables

> **VARIABLE: IN SIMPLE WORDS**
> It is a name that points to a value stored in the browser's memory while the page is open, letting you use that value again, anywhere in the code, just by its name.

```javascript
let materia = "Cálculo I";
console.log(materia); // Cálculo I
```

> The example code keeps Portuguese names (`materia` = subject, `participantes` = participants, `temVaga` = has a spot) so it matches the runnable example and the rest of the track.

## // `let` × `const`

```javascript
const nomeDoProjeto = "Buscador de Grupos de Estudo"; // will never change
let quantidadeDeGrupos = 3; // may change later
quantidadeDeGrupos = 4; // valid
```

| Keyword | When to use it |
|---|---|
| `const` | The value will not be reassigned after it is created; most of your variables should start as `const` |
| `let` | The value needs to change at some point (a counter, a search result that updates) |

> **WATCH OUT**
> You may find `var` in older code. Avoid using it in new code: `var` has more confusing scoping behavior and was replaced by `let`/`const` years ago. If `const` fails because the value really needs to change, use `let`, never `var`.

`const` prevents reassigning the whole variable, but it does not automatically "freeze" an array or object stored in it: you can still change items inside it. Modules 05 and 06 come back to this point.

## // The primitive types

```javascript
const materia = "Cálculo I";       // string, text
let participantes = 5;              // number
let temVaga = true;                 // boolean, true/false
let observacao = null;              // intentional absence of a value
let horario;                        // undefined, declared but without a value yet
```

| Type | Represents | Example |
|---|---|---|
| `string` | Text, always in quotes (or backticks, for template literals) | `"Cálculo I"` |
| `number` | Any number, integer or decimal; there is no separate decimal type | `5`, `3.5` |
| `boolean` | Only two possible values | `true`, `false` |
| `null` | "No value here, on purpose" | `null` |
| `undefined` | "Has not received any value yet" | a variable that was only declared |

The difference between `null` and `undefined` is subtle but real: `null` is an absence of value that *you* explicitly decided; `undefined` is what JavaScript itself puts there when nothing has been assigned yet.

## // Arithmetic operators

```javascript
const total = 5 + 3;   // 8
const resto = 10 % 3;  // 1, the remainder of the division
```

`%` (modulo) is less common day to day, but it shows up a lot in alternating logic: for example, to give a different background to even and odd rows of a table.

## // Comparison operators: `===` matters

```javascript
console.log(5 === 5);     // true
console.log(5 === "5");   // false
console.log(5 == "5");    // true, avoid it!
```

> **WHY `===` AND NOT `==`**
> `==` compares the value after *converting* the types first: `5 == "5"` gives `true`, even though one is a number and the other a string. `===` compares value *and* type, without converting anything. It is more predictable, and it is the recommended standard in any new code. Treat `==` as a trap to avoid, not as an equivalent, shorter option.

| Operator | Meaning |
|---|---|
| `===` | Equal (value and type) |
| `!==` | Not equal (value and type) |
| `>`, `<`, `>=`, `<=` | Greater, less, greater or equal, less or equal |

## // Logical operators

```javascript
const podeParticipar = temVaga && participantes < 10;
const precisaAvisar = !temVaga || participantes === 0;
```

| Operator | Meaning |
|---|---|
| `&&` (AND) | True only if both sides are true |
| \|\| (OR) | True if at least one side is true |
| `!` (NOT) | Inverts a boolean value |

## // Good example × bad example

**Bad example**: comparing with `==`, producing an unexpected result:

```javascript
const participantesTexto = "5"; // came from an input, for example
if (participantesTexto == 5) {
  console.log("This runs, even though the types are different");
}
```

**Good example**: converting the type explicitly, then comparing with `===`:

```javascript
const participantesTexto = "5";
const participantesNumero = Number(participantesTexto);
if (participantesNumero === 5) {
  console.log("Clear comparison, no surprises");
}
```

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| `const` "won't let me change the value" when it should | Trying to reassign a variable that changes throughout the code | Use `let` from the start |
| A `==` comparison giving an unexpected result | Automatic type conversion hiding the real problem | Always use `===` |
| `undefined` showing up with no explanation | Variable used before receiving a value | Make sure the variable was initialized before it is read |
| A number treated as text (`"5" + "3"` = `"53"`) | The value came from a form field, which always delivers a string | Convert with `Number(...)` before doing math |

## // Guided practice

1. In `script.js`, create three variables with `const`: `nomeDoProjeto`, `materiaPrincipal`, `totalDeGrupos`.
2. Print all three in the console, one per `console.log`.
3. Create a variable `let vagasDisponiveis = 3;`. Write a line that subtracts 1 from it and prints the result.
4. Write a comparison with `===` between two different variables and print the result (`true` or `false`).

## // Practice on your own

> **CHALLENGE**
> Create a variable `participantesTexto = "8"` (a string, on purpose). Without using `Number(...)`, try adding `participantesTexto + 1` and look at the result in the console: it is probably not what you expected. Then fix it by converting with `Number(participantesTexto)` before adding, and compare the two results.

## // Applying it to the week's project

1. In `script.js`, declare as `const` the values that will not change in your project (the app name, for example) and as `let` the ones that will.
2. Make sure every comparison in your code uses `===`, never `==`.
3. Commit: `git commit -m "Add the project's base variables and types"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> A form field always delivers the typed value as a `string`, even if the person types only numbers. Why does that matter for the rest of the logic you will write this week?

Answer: because any comparison or calculation that expects a `number` will behave unexpectedly if it receives a `string` without conversion. For example, `"5" + "3"` results in `"53"` (text concatenation), not `8`. Whenever a value comes from a form field and needs to be treated as a number, you must convert it explicitly with `Number(...)` first.

## // Module summary

- [ ] I know the difference between `let` and `const`, and why to avoid `var`.
- [ ] I can name the primitive types (`string`, `number`, `boolean`, `null`, `undefined`).
- [ ] I know why `===` is safer than `==`.
- [ ] I can use `&&`, `||` and `!`.
- [ ] I know why a value coming from a form needs conversion before becoming a number.

---

**Next module:** `03-decisions-and-loops.md`: with variables and comparisons ready, it is time to control what the code does, and how many times.

`Study Material // Coffee & Code`
