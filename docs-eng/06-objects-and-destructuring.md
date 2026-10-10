# Module 06, Objects and Destructuring

[Português](../docs/06-objetos-e-desestruturacao.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // The problem

A study group is not just a name: it has a subject, a number of participants, a meeting time, and probably more information in the future. Storing all of that in loose variables (`materia1`, `participantes1`, `horario1`) completely loses the notion that this information belongs to the same thing. An object solves exactly that.

## // Object: grouping the properties of a single thing

```javascript
const grupo = {
  materia: "Cálculo I",
  participantes: 5,
  horario: "Tuesdays at 6 PM",
};

console.log(grupo.materia); // Cálculo I
console.log(grupo["materia"]); // same thing (alternative form)
```

> **OBJECT: IN SIMPLE WORDS**
> It is a way of grouping several related pieces of information (properties) inside a single named thing, instead of spreading each piece across a separate variable.

## // Array × object: when to use each one

| | Array | Object |
|---|---|---|
| Represents | A **list** of things | The **characteristics** of one thing |
| Access | By position (`array[0]`) | By name (`object.property`) |
| Example this week | The whole list of groups | One specific group, with its information |

In practice, the two almost always show up together in an **array of objects**: exactly the structure you already used in Module 05 (`grupos`, where each item is a `{ materia, participantes }` object).

## // Reading and changing properties

```javascript
grupo.participantes = grupo.participantes + 1;
console.log(grupo.participantes); // 6
```

Unlike an array (where `.map()`/`.filter()` always return something new), changing an object's property directly (`grupo.participantes = ...`) changes the original object. This matters especially when the same object is stored inside an array: changing one of its properties changes the corresponding item inside the array too.

## // Methods inside an object

An object can store not only values, but also functions:

```javascript
const grupo = {
  materia: "Cálculo I",
  participantes: 5,
  estaCheio: function () {
    return this.participantes >= 10;
  },
};

console.log(grupo.estaCheio()); // false
```

`this`, inside an object method, refers to the object itself: `this.participantes` is the same as `grupo.participantes`, except the function does not need to know the outside variable's name. You will not use `this` extensively this week (Module 13 comes back to this topic in more depth), but it is worth recognizing the pattern.

## // Destructuring: pulling properties out directly

```javascript
const grupo = { materia: "Cálculo I", participantes: 5, horario: "Tuesdays at 6 PM" };

// without destructuring
const materia1 = grupo.materia;
const participantes1 = grupo.participantes;

// with destructuring: same result, one line
const { materia, participantes } = grupo;

console.log(materia); // Cálculo I
console.log(participantes); // 5
```

> **DESTRUCTURING: IN SIMPLE WORDS**
> It is a direct way of pulling properties out of an object (or items out of an array) into separate variables, without writing `object.property` over and over.

This shows up very often inside functions that receive an object as a parameter:

```javascript
function descreverGrupo({ materia, participantes }) {
  return `${materia} has ${participantes} participants`;
}

console.log(descreverGrupo(grupo));
```

The function receives the whole object, but already "opens" it into `materia` and `participantes` right in the parameter definition, without an extra line for that inside the function body.

## // Good example × bad example

**Bad example**: related information spread across loose variables:

```javascript
const materiaGrupo1 = "Cálculo I";
const participantesGrupo1 = 5;
const materiaGrupo2 = "Estrutura de Dados";
const participantesGrupo2 = 3;
```

**Good example**: grouped as it should be, ready to become an array:

```javascript
const grupos = [
  { materia: "Cálculo I", participantes: 5 },
  { materia: "Estrutura de Dados", participantes: 3 },
];
```

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| `undefined` when accessing a property | Property name typed wrong (`grupo.materias` instead of `grupo.materia`) | Check the exact name, including upper/lowercase |
| Changing an object without noticing that another place also references it | Objects are changed "in place", unlike the result of `.map()`/`.filter()` | Be clear about when you want to change the original, and when you want a copy |
| Destructuring with the wrong name | The name in the destructuring has to match the property name in the object | `const { materia } = grupo` only works if the property is called exactly `materia` |

## // Guided practice

1. In `script.js`, create a `grupo` object with `materia`, `participantes` and `horario`.
2. Read and print each property using `object.property`.
3. Rewrite the reading using destructuring (`const { materia, participantes, horario } = grupo;`).
4. Write a function `descreverGrupo({ materia, participantes })` that returns a sentence combining the two pieces of information.

## // Practice on your own

> **CHALLENGE**
> Create a `usuario` object representing the project's Profile (`nome`, `email` and `materias`, the last one an array). Write a function `resumoDoUsuario(usuario)` that uses destructuring in the parameter and returns a sentence including the name and the number of subjects (`usuario.materias.length`).

## // Applying it to the week's project

1. Confirm each group in your data array is an object with clearly named properties.
2. Write at least one function that receives an object as a parameter and uses destructuring on it.
3. Commit: `git commit -m "Structure the Profile data as an object, with destructuring"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> A `grupos` array stores objects. You take one of those objects (`const g = grupos[0];`) and change `g.participantes = 99;`. Does the corresponding item inside the `grupos` array change too?

Answer: yes. `g` is not a copy of the object: it is a reference to the same object that was already inside the array. Changing a property through `g` changes the object itself, which is the same one sitting in `grupos[0]`. That is different from the behavior of `.map()`/`.filter()` (Module 05), which always return a new structure.

## // Module summary

- [ ] I can create an object and read/change its properties.
- [ ] I know the difference between when to use an array and when to use an object.
- [ ] I can use destructuring to pull out properties, including inside function parameters.
- [ ] I know that changing an object's property changes the original, unlike `.map()`/`.filter()`.
- [ ] My project's data (groups, user) is already structured as clear objects.

---

**Next module:** `07-the-dom-selecting-and-reading.md`: variables, functions, arrays and objects are ready. Time to connect all of it to the real page.

`Study Material // Coffee & Code`
