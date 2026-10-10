# Module 05, Arrays and Essential Methods

[Português](../docs/05-arrays-e-metodos-essenciais.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // The problem

The Dashboard does not have "one group": it has several. Storing each group in a separate variable (`grupo1`, `grupo2`, `grupo3`...) does not scale and does not let you go through all of them at once with the `for...of` you already know from Module 03. That is exactly what an array solves.

## // Array: an ordered list

```javascript
const materias = ["Cálculo I", "Estrutura de Dados", "Banco de Dados"];
console.log(materias[0]); // Cálculo I (the first index is 0, not 1)
console.log(materias.length); // 3
```

## // Adding and removing items

```javascript
materias.push("Redes de Computadores"); // adds to the end
materias.pop(); // removes the last one
```

## // `.forEach()`: doing something for each item

```javascript
materias.forEach(function (materia) {
  console.log(materia);
});
```

Similar to the `for...of` from Module 03, but as an array method. It is very common when you only need to *do something* with each item (like printing it), without creating a new array from it.

## // `.map()`: turning each item into something else

```javascript
const participantes = [5, 3, 8];
const dobro = participantes.map(function (numero) {
  return numero * 2;
});
console.log(dobro); // [10, 6, 16]
```

`.map()` always returns a **new array**, the same size as the original, with each item transformed by the function. The original array (`participantes`) is not changed.

## // `.filter()`: keeping only what passes a test

```javascript
const grupos = [
  { materia: "Cálculo I", participantes: 5 },
  { materia: "Estrutura de Dados", participantes: 12 },
  { materia: "Banco de Dados", participantes: 3 },
];

const comVagas = grupos.filter(function (grupo) {
  return grupo.participantes < 10;
});
console.log(comVagas.length); // 2
```

`.filter()` also returns a new array, but instead of transforming each item, it decides, item by item, whether that item stays in the resulting array (when the function returns `true`) or is discarded (when it returns `false`).

## // `.map()` × `.filter()`, side by side

| | `.map()` | `.filter()` |
|---|---|---|
| What it returns | An array of the **same size**, with each item transformed | An array **smaller or equal**, with only the items that passed the test |
| The inner function | Returns the new value of each item | Returns `true` or `false` for each item |
| Typical use this week | Turning data into HTML (Module 12) | Implementing search/filter (Dashboard) |

The two are often combined in sequence: first filter, then transform what is left.

## // `.find()`: finding a single item

```javascript
const grupo = grupos.find(function (g) {
  return g.materia === "Banco de Dados";
});
console.log(grupo); // { materia: "Banco de Dados", participantes: 3 }
```

Unlike `.filter()`, `.find()` returns only the **first** item that matches the condition, not an array. If no item matches, it returns `undefined`.

## // Arrow functions inside array methods

In practice, it is very common to see `.map()`/`.filter()` with arrow functions, since they are shorter:

```javascript
const dobro = participantes.map((numero) => numero * 2);
const comVagas = grupos.filter((grupo) => grupo.participantes < 10);
```

This is exactly the same logic as the previous examples, just in the short form you saw in Module 04.

## // Good example × bad example

**Bad example**: using `.forEach()` when the goal was to transform:

```javascript
let dobro = [];
participantes.forEach(function (numero) {
  dobro.push(numero * 2);
});
```

It works, but you have to create an empty array by hand and keep pushing items: more code to do what `.map()` already solves in one line.

**Good example**: the right tool for the goal:

```javascript
const dobro = participantes.map((numero) => numero * 2);
```

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| Expecting `.map()` to change the original array | `.map()` always returns a **new** array | Store the result in a new variable, or reassign the same one |
| Using `.map()` when you only needed to filter | Both "process" the array, easy to mix up the goal | Ask: do I want to keep them all, transformed (`.map`), or discard some (`.filter`)? |
| Treating `.find()` as if it returned an array | `.find()` returns a single item (or `undefined`) | Use `.filter()` if you need several results |
| Forgetting that array indexes start at `0` | The habit of counting from `1` | The first item is always `array[0]` |

## // Guided practice

1. In `script.js`, create the `grupos` array, with at least 5 `{ materia, participantes }` objects.
2. Use `.map()` to create an array with only the subject names (`grupo.materia`).
3. Use `.filter()` to create an array with only the groups that have fewer than 8 participants.
4. Use `.find()` to find a specific group by subject name.
5. Print the three results in the console and confirm each one does what you expected.

## // Practice on your own

> **CHALLENGE**
> Starting from the `grupos` array, use `.filter()` followed by `.map()` in sequence to produce an array with only the *names* of the groups that have 5 or more participants (filter first, then transform the result).

## // Applying it to the week's project

1. Structure your Dashboard's data as an array of objects (even if it is not going to the screen yet; that comes in Module 12).
2. Write, using `.filter()`, the search logic that will feed the Dashboard's search field.
3. Commit: `git commit -m "Add the groups array and filter logic"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> You want the subject names, in uppercase, only for groups with spots available (fewer than 10 participants). Which two methods do you combine, and in which order does it make more sense to apply them?

Answer: `.filter()` first, to keep only the groups with fewer than 10 participants, followed by `.map()`, to turn each remaining group into the subject name in uppercase (`grupo.materia.toUpperCase()`). The order matters for efficiency, not correctness: filtering first means the following `.map()` processes fewer items.

## // Module summary

- [ ] I can create, read and modify an array.
- [ ] I know the difference between `.forEach()`, `.map()` and `.filter()`.
- [ ] I know `.map()` and `.filter()` always return a new array, without changing the original.
- [ ] I can use `.find()` to locate a single item.
- [ ] I have already structured my project's data as an array of objects.

---

**Next module:** `06-objects-and-destructuring.md`: each item in these arrays is an object. Time to understand that structure in depth.

`Study Material // Coffee & Code`
