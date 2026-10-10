# Module 04, Functions and Arrow Functions

[Português](../docs/04-funcoes-e-arrow-functions.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // The problem

If the "Full / Almost full / Spots available" logic from Module 03 needs to run for six different groups, copying and pasting that `if/else` block six times is exactly the kind of repetition that should become a single reusable piece.

## // What a function is

> **FUNCTION: IN SIMPLE WORDS**
> It is a named block of code that groups a task and can be run (called) as many times as needed, from anywhere in the code.

```javascript
function statusDoGrupo(participantes) {
  if (participantes >= 10) {
    return "Full";
  } else if (participantes >= 5) {
    return "Almost full";
  } else {
    return "Spots available";
  }
}

console.log(statusDoGrupo(8));  // Almost full
console.log(statusDoGrupo(12)); // Full
```

| Part | Meaning |
|---|---|
| `statusDoGrupo` | The function's name ("group status") |
| `participantes` | Parameter: the name the function uses to receive a value |
| `8`, `12` | Arguments: the real values passed in each call |
| `return` | The value the function gives back to whoever called it |

## // `return` stops the function

As soon as a `return` line runs, the function stops there: no line after it, inside the same function, runs. That is why the `if/else if/else` in the example above works without needing anything besides three `return`s.

## // Arrow functions

```javascript
function dobrar(numero) {
  return numero * 2;
}

const dobrar = (numero) => numero * 2;
```

Both forms do exactly the same thing: an arrow function is just a shorter syntax. When the function body is a single expression that is already the return value, the `return` and the braces `{}` can be left out, as in the example above.

For a body with more than one line, the braces and the explicit `return` are needed again:

```javascript
const statusDoGrupo = (participantes) => {
  if (participantes >= 10) {
    return "Full";
  }
  return "Spots available";
};
```

> **WHICH FORM TO USE**
> There is no universally "right" answer: this guide mainly uses `function name(...) { ... }` because it is more explicit for beginners, and arrow functions in short contexts (like inside `.map()`, in Module 05). Prefer the form that makes the code clearer for you to reread later: short code is not always easier code.

## // Scope: what a function "sees"

```javascript
function exemplo() {
  const valorLocal = "only exists in here";
  console.log(valorLocal);
}

exemplo();
console.log(valorLocal); // error: valorLocal does not exist out here
```

A variable created inside a function (with `let` or `const`) does not exist outside it: that boundary is called **scope**. It keeps any part of the code from changing any variable without control, and it is the reason two different functions can use the same variable name internally without conflict.

## // Why organize into functions, specifically this week

The whole second half of this guide depends on named, reusable functions: `renderizarGrupos(...)` (Module 12), `validarFormulario(...)` (Module 10), `filtrarPorBusca(...)`: each of these is a function that can be called again whenever the data changes, without duplicating logic. Without this habit, each new feature would become loose, copied-and-pasted code.

## // Good example × bad example

**Bad example**: duplicated logic instead of a function:

```javascript
if (participantesGrupo1 >= 10) { console.log("Full"); }
if (participantesGrupo2 >= 10) { console.log("Full"); }
if (participantesGrupo3 >= 10) { console.log("Full"); }
```

**Good example**: one function, called three times:

```javascript
function statusDoGrupo(participantes) {
  return participantes >= 10 ? "Full" : "Spots available";
}

console.log(statusDoGrupo(participantesGrupo1));
console.log(statusDoGrupo(participantesGrupo2));
console.log(statusDoGrupo(participantesGrupo3));
```

(Notice the ternary operator `condition ? valueIfTrue : valueIfFalse`: a short way of writing a one-line `if/else`, useful when both results are simple.)

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| The function "returns nothing" (`undefined`) | Forgetting the `return` | Every function that should give back a value needs an explicit `return` |
| A variable "does not exist" outside the function | Trying to use a variable created inside a function, outside it | Declare the variable outside the function if it needs to be used elsewhere |
| Mixing up parameter and argument | They are close concepts, easy to swap | A parameter is the name in the function definition; an argument is the value passed in the call |
| An arrow function with a multi-line body and no braces | Trying to apply the short form to a body that needs an explicit `return` | Add `{ }` and `return` when the body has more than one expression |

## // Guided practice

1. In `script.js`, write the `statusDoGrupo(participantes)` function, using the example in this section.
2. Call it three times, with different numbers, printing each result in the console.
3. Rewrite the same function as an arrow function, stored in a constant, and confirm the behavior is identical.

## // Practice on your own

> **CHALLENGE**
> Write a function `mensagemDeBoasVindas(nome)` that returns `"Welcome, " + nome + "!"`. Then write a second function `mensagemDeVagas(participantes, limite)` that returns how many spots are still left (`limite - participantes`), or `"Group full"` if the result is zero or negative.

## // Applying it to the week's project

1. Turn at least two pieces of logic in your project (for example, `statusDoGrupo` and a simple validation) into named, reusable functions.
2. Confirm that none of this logic is duplicated in more than one place in the code.
3. Commit: `git commit -m "Organize logic into reusable functions"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> A function `calcularStatus(participantes)` has a `console.log(status)` instead of `return status`. What happens when you try to use `const resultado = calcularStatus(8);` afterwards?

Answer: `resultado` will receive `undefined`. `console.log` only prints a value in the console: it does not *give back* anything to whoever called the function. Without an explicit `return`, every function returns `undefined` by default, even if it did something visible (like printing to the console) internally.

## // Module summary

- [ ] I can write a function with `function name(parameter) { ... return ...; }`.
- [ ] I can write the same logic as an arrow function.
- [ ] I can explain why `return` is needed for the function to give back a value.
- [ ] I know what scope means, and why a variable inside a function does not exist outside it.
- [ ] I have already organized at least two pieces of logic in my project into named functions.

---

**Next module:** `05-arrays-and-essential-methods.md`: functions are ready. Now, the tool you will use the most this week: transforming lists of data.

`Study Material // Coffee & Code`
