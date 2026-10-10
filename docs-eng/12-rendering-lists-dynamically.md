# Module 12, Rendering Lists Dynamically

[Português](../docs/12-renderizando-listas-dinamicamente.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // The problem

Look at your Dashboard HTML, inherited from Week 02:

```html
<section class="dashboard-grid">
  <article class="card">
    <h3>Cálculo I</h3>
    <p>5 participants · meetings on Tuesdays</p>
    <button class="botao botao-primario">Join</button>
  </article>
  <article class="card">
    <h3>Estrutura de Dados</h3>
    <p>3 participants · meetings on Thursdays</p>
    <button class="botao botao-primario">Join</button>
  </article>
  <!-- ...four more cards, each one copied and pasted -->
</section>
```

Every card was written by hand. If a new group is created, someone has to edit the HTML. If a group is removed, someone has to remember to delete the right snippet. This does not scale. And, more importantly, it is not how a real interface works: the list of groups comes from somewhere (for now, an array you write yourself; in the club's next weeks, a real API), and the screen needs to arrange itself on top of it.

## // The central idea

> **DYNAMIC RENDERING: IN SIMPLE WORDS**
> It means generating the HTML of a list of elements automatically, from an array of data, instead of writing each element by hand. Change the array, and the screen changes along with it, without touching the HTML.

The path, in three steps:

1. Have an **array of objects** representing the data (you saw this in Module 06 and will formalize it as JSON in Module 11).
2. For each object in the array, **build** the matching piece of HTML (or DOM element).
3. **Insert** that HTML inside a container that already exists on the page.

## // From array to elements, visually

<div align="center">
<img src="../docs/assets/mock-data-to-render.svg" alt="Array of objects, with .map(), turning into elements rendered on screen" width="520">
</div>

Each object in the array (like `{ materia: "Cálculo I", participantes: 5 }`) becomes, on screen, a card with that information. The order is kept: the first item in the array is the first card; if the array has six items, the screen has six cards.

## // The `.map()` method applied to rendering

You already saw `.map()` in Module 05 turning one array into another. Rendering uses exactly that idea, except the output array is an array of **HTML strings**:

```javascript
const grupos = [
  { materia: "Cálculo I", participantes: 5 },
  { materia: "Estrutura de Dados", participantes: 3 },
  { materia: "Banco de Dados", participantes: 8 },
];

const htmlDosCards = grupos.map(function (grupo) {
  return `
    <article class="card">
      <h3>${grupo.materia}</h3>
      <p>${grupo.participantes} participants</p>
      <button class="botao botao-primario">Join</button>
    </article>
  `;
});
```

`htmlDosCards` is now an array of three strings, each one a ready piece of HTML. All that is left is to join these strings and put them on the page.

## // Template literals: writing HTML inside JavaScript

Notice that the HTML in the example above is between backticks, not regular quotes. This is called a *template literal*: a kind of string that lets you break lines freely and, above all, **insert variable values directly**, using `${...}`:

```javascript
const materia = "Cálculo I";
const texto = `The subject is ${materia}.`;
// texto is now: "The subject is Cálculo I."
```

Without template literals, the same result would require concatenating strings with `+`, which is much harder to read when the HTML has several lines and several values, as in the cards example.

## // Putting it all together and inserting it into the page

```javascript
const container = document.querySelector(".dashboard-grid");

function renderizarGrupos(lista) {
  const html = lista.map(function (grupo) {
    return `
      <article class="card">
        <h3>${grupo.materia}</h3>
        <p>${grupo.participantes} participants</p>
        <button class="botao botao-primario">Join</button>
      </article>
    `;
  }).join("");

  container.innerHTML = html;
}

renderizarGrupos(grupos);
```

Three points that deserve attention:

| Part | Why it is there |
|---|---|
| `.join("")` | `.map()` returns an array of strings; `.join("")` joins them all into a single string, with no separator between them |
| `container.innerHTML = html` | Replaces the container's entire content with the generated HTML, including erasing what was there before |
| `function renderizarGrupos(lista)` | A function, not a loose script: that way you can call it again whenever the data changes (after a search, for example) |

> **ABOUT `INNERHTML` AND SAFETY**
> You already saw in Module 08 (Week 03) that `innerHTML` should not receive text typed by a person without treatment: the risk is code injection. In this specific case, the data comes from an array *you* wrote (or, later on, from a controlled API), not from a form field open to the public; that is why it is an acceptable use of `innerHTML` here. If, in the future, any of these values can be typed by a user without any treatment, the same caution from Module 08 applies again.

## // Re-rendering: the pattern that makes it all work together

The part that really connects this module to the rest of the week: `renderizarGrupos` can be called **again**, as many times as needed, with a different list, and the screen reflects it instantly:

```javascript
function filtrarPorBusca(termo) {
  const filtrados = grupos.filter(function (grupo) {
    return grupo.materia.toLowerCase().includes(termo.toLowerCase());
  });
  renderizarGrupos(filtrados);
}
```

Call `filtrarPorBusca("cálculo")`, and the screen starts showing only the groups whose name contains "cálculo", with no reload and no rewriting HTML by hand. It is the same rendering function as always, just fed a different array on each call.

## // Good example × bad example

**Bad example**: appending to the container instead of replacing it:

```javascript
grupos.forEach(function (grupo) {
  container.innerHTML += `<article class="card">...</article>`;
});
```

Each `+=` redoes the whole `innerHTML` from scratch and adds on top: slow, and if this function runs again (after a search, for example), the old cards are never removed; they just pile up.

**Good example**: build all the HTML first, write it once:

```javascript
const html = grupos.map(function (grupo) {
  return `<article class="card">...</article>`;
}).join("");
container.innerHTML = html;
```

A single write to the DOM, and each call to `renderizarGrupos` completely replaces the previous content, with no pile-up.

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| Cards duplicating on every search | Using `+=` instead of replacing `innerHTML` | Build the whole string with `.map().join("")` and assign it once |
| `undefined` showing up in the card | Object property name typed wrong (`grupo.materias` instead of `grupo.materia`) | Check the exact property names in the data array |
| Nothing shows up on screen | Selected the container before it existed in the HTML, or `querySelector` with a wrong selector | Confirm the `<script>` runs after the HTML (Module 01) and that the class/id matches |
| The rendering function does not run again after a filter | Forgetting to call `renderizarGrupos(...)` again inside the search function | Every change to the displayed data needs to end in a new rendering call |

## // Guided practice

1. In the Dashboard's `script.js`, create the `grupos` array with at least 4 objects (`materia`, `participantes`).
2. Write `renderizarGrupos(lista)`, using `.map()` and template literals, following the example in this section.
3. Call `renderizarGrupos(grupos)` once, when the page loads.
4. Open the Dashboard in the browser and confirm: the cards that used to be fixed HTML now come from the array. Add a fifth object to the array, save, reload. Does the fifth card appear on its own?

## // Practice on your own

> **CHALLENGE**
> Connect the Dashboard's search field (which exists since Week 02) to a `filtrarPorBusca(termo)` function, using `.filter()` followed by `renderizarGrupos(...)`. Test by typing part of a subject name and confirm only the matching cards stay on screen, without a reload.

## // Applying it to the week's project

1. Turn your project's Dashboard card grid into content rendered from an array, no longer fixed HTML.
2. Implement a search that really works, using the filter → render pattern.
3. Confirm that adding or removing an item from the array (directly in the code, for now) is correctly reflected on screen after reloading.
4. Commit: `git commit -m "Render the Dashboard grid dynamically from an array"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> Your search function calls `grupos.filter(...)`, but forgets to call `renderizarGrupos(...)` with the result. What will the person using the search see, and why?

Answer: nothing changes on screen. `.filter()` only creates a new filtered array: it has no visual effect on its own. The screen only reflects new data when `renderizarGrupos` (or an equivalent) is called again, passing that filtered array as the argument. Filtering data and updating the screen are two separate steps; the first does not imply the second.

## // Module summary

- [ ] I can explain why cards written by hand in the HTML do not scale.
- [ ] I can use `.map()` combined with template literals to generate HTML from an array.
- [ ] I know why `.join("")` is needed after `.map()`.
- [ ] I know why replacing `innerHTML` (not appending with `+=`) avoids duplication.
- [ ] I know every change to the displayed data needs to end in a new call to the rendering function.
- [ ] My project's Dashboard grid already renders from an array, with a working search.

---

**Next module:** `13-state-and-componentization.md`: the list renders. Now, how do you organize this when the interface grows and several parts of the screen depend on the same data?

`Study Material // Coffee & Code`
