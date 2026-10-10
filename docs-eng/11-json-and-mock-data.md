# Module 11, JSON and Mock Data

[Português](../docs/11-json-e-dados-mock.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // The problem

The Dashboard groups, so far, live right in `script.js`, as an array written by hand. That works for studying, but a real system fetches this data from somewhere external (a server). Coffee & Code has not reached the backend week yet, so the question is: how do you simulate that reality without having a real server yet?

## // What JSON is

> **JSON: IN SIMPLE WORDS**
> It is a text format for representing data, similar to a JavaScript object or array, but it is *plain text*. Because of that, it can be sent over a network, saved in a file, or exchanged between different programming languages (JSON is not exclusive to JavaScript, even though the name comes from it: *JavaScript Object Notation*).

<div align="center">
<img src="../docs/assets/json-vs-js-object.svg" alt="Comparison between a JavaScript object and its equivalent JSON representation" width="540">
</div>

## // JSON × JavaScript object: similar, but not the same

```javascript
// JavaScript object (lives in memory, while the script runs)
const grupo = {
  materia: "Cálculo I",
  participantes: 5,
};
```

```json
{
  "materia": "Cálculo I",
  "participantes": 5
}
```

| | JavaScript object | JSON |
|---|---|---|
| What it is | A data structure, in memory | **Text**, following a specific format |
| Property keys | Can go without quotes (`materia:`) | Always in double quotes (`"materia":`) |
| Can it have functions/methods inside? | Yes | No: JSON only represents data, never behavior |
| Where it shows up | Directly in JavaScript code | `.json` files, API responses, `localStorage` |

## // Converting between the two formats

```javascript
const grupo = { materia: "Cálculo I", participantes: 5 };

const textoJSON = JSON.stringify(grupo);
console.log(textoJSON); // '{"materia":"Cálculo I","participantes":5}'

const objetoDeVolta = JSON.parse(textoJSON);
console.log(objetoDeVolta.materia); // Cálculo I
```

| Function | Direction |
|---|---|
| `JSON.stringify(object)` | JavaScript object/array → JSON text |
| `JSON.parse(text)` | JSON text → JavaScript object/array |

You will not need to convert all the time this week, but you will need to understand this pair of functions when the club gets to saving data (`localStorage`) or fetching from a real API, in future weeks.

## // Mock data: simulating an API before it exists

> **MOCK DATA: IN SIMPLE WORDS**
> It is fake data, written by hand, in the format the real data *will* have once it exists, used to develop and test an interface before the backend is ready.

```javascript
const gruposMock = [
  { id: 1, materia: "Cálculo I", participantes: 5, horario: "Tuesdays at 6 PM" },
  { id: 2, materia: "Estrutura de Dados", participantes: 3, horario: "Thursdays at 7 PM" },
  { id: 3, materia: "Banco de Dados", participantes: 8, horario: "Saturdays at 10 AM" },
];
```

The `gruposMock` array is not structurally different from the `grupos` array you have been using since Module 05; the difference is **intent**: naming it "mock" makes it clear, to anyone reading the code, that this data is temporary, and that one day it will be replaced by a real fetch from a server, without the rendering logic (Module 12) having to change anything.

## // Why this matters: separating data from display

If `renderizarGrupos(lista)` (Module 12) only depends on receiving an array in the right format, it does not matter whether that array came from `gruposMock` (today) or from a real API response (in the future): the rendering function does not change. This decoupling is what makes the migration from mock to real data, later in the club, a smooth process instead of a rewrite.

## // Adding an `id` to each item

Notice that each object in the `gruposMock` above has an `id` field, which the examples in earlier modules did not have. This matters from now on: when a person clicks "Leave group" (Module 14), the code will need to know *which* exact item in the array to remove. Comparing by `materia` would work until two groups had similar names. A unique `id` solves this reliably.

## // Good example × bad example

**Bad example**: mock data with no clear identification and no `id`:

```javascript
const dados = [
  ["Cálculo I", 5],
  ["Estrutura de Dados", 3],
];
```

Hard to read, no property names, and no `id` to find a specific item later.

**Good example**: an array of objects, named as mock, with an `id`:

```javascript
const gruposMock = [
  { id: 1, materia: "Cálculo I", participantes: 5 },
  { id: 2, materia: "Estrutura de Dados", participantes: 3 },
];
```

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| `JSON.parse` breaking with an error | The text is not valid JSON (single quotes, an extra comma) | JSON requires double quotes on keys, and does not accept a comma after the last item |
| Mixing up a JavaScript object and JSON | The two look very similar | Remember: JSON is always text; an object is a live structure in memory |
| Forgetting the `id` in mock data | It seems unnecessary when you are only reading the data | Add it right away; it avoids rework when remove/edit actions arrive |
| Naming mock data as if it were final | Forgetting to signal that it is temporary | Use a name like `gruposMock` or a comment making it explicit |

## // Guided practice

1. Turn the `grupos` array you have been using into `gruposMock`, adding a unique `id` to each item.
2. Use `JSON.stringify(gruposMock)` and print the result in the console. Notice the double quotes on the keys.
3. Use `JSON.parse(...)` on the generated text, and confirm the result is equivalent to the original array.

## // Practice on your own

> **CHALLENGE**
> Write, in a comment or a separate string, valid JSON representing a `usuario` object (name, e-mail, `materias` array). Use `JSON.parse(...)` to turn that text into a real object, and confirm it by reading `usuario.materias.length` in the console.

## // Applying it to the week's project

1. Rename your Dashboard's data array to `gruposMock`, making sure each item has a unique `id`.
2. Do the same for the Profile data, if applicable.
3. Commit: `git commit -m "Formalize the data as mock, with a unique id per item"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> Why does naming the data `gruposMock`, instead of just `grupos`, help anyone (including you, months later) understand the code faster?

Answer: the name communicates, without any extra comment, that this data is temporary and will be replaced by a real source (an API) in the future, keeping someone from mistakenly assuming that this array is already the system's final data source. It is the same principle of clear names that already showed up in earlier modules: a variable's name should communicate its role, not just its content.

## // Module summary

- [ ] I can explain the difference between a JavaScript object and JSON.
- [ ] I can use `JSON.stringify` and `JSON.parse`, and I know which direction each one converts.
- [ ] I know what mock data is, and why naming it as such matters.
- [ ] I know why each item in a mock array should have a unique `id`.
- [ ] My project's data is already organized as mock, with an `id`.

---

**Next module:** `12-rendering-lists-dynamically.md`: data ready, structured, with an `id`. Time to put it on the screen for real.

`Study Material // Coffee & Code`
