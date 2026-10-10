# Module 13, State and Componentization

[Português](../docs/13-estado-e-componentizacao.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // Before you start

This module assumes Module 12 is already solid: rendering a list from an array. Here the question changes: as the interface grows, how do you keep the data from becoming inconsistent across different parts of the screen, and how do you avoid rewriting the same HTML in several places?

## // The problem

Imagine the Dashboard shows "6 groups found" in a piece of text, **in addition to** the card grid. If a person leaves a group (removing an item from the array) and you remember to update the grid but forget to update that text, the screen now shows contradictory information. The more places on the screen depend on the same data, the greater the risk of forgetting to update one of them.

## // What "state" is

> **STATE: IN SIMPLE WORDS**
> It is the "source of truth" for your application's data, in a single place: everything that appears on screen should be a reflection of that state, never a copy changed separately from it.

In your project, the `gruposMock` array (Module 11) already **is** the Dashboard's state. What this module formalizes is a rule about how to handle it.

## // The state → render cycle

<div align="center">
<img src="../docs/assets/state-render-cycle.svg" alt="Cycle: state, rendering, screen, and the person's action feeding back into the state" width="480">
</div>

> **THE CENTRAL RULE OF THIS MODULE**
> Never change the screen directly in response to an action. Change the **state**, and call the rendering function again: let the screen always be a reflection of the current state, never a manual edit running parallel to it.

## // Applying the rule: removing an item

```javascript
let gruposMock = [
  { id: 1, materia: "Cálculo I", participantes: 5 },
  { id: 2, materia: "Estrutura de Dados", participantes: 3 },
  { id: 3, materia: "Banco de Dados", participantes: 8 },
];

function removerGrupo(id) {
  gruposMock = gruposMock.filter((grupo) => grupo.id !== id);
  renderizarGrupos(gruposMock);
}
```

Notice that `removerGrupo` never touches the DOM: it only updates the array (`gruposMock`) and calls `renderizarGrupos` again, which already knows how to rebuild the whole screen from the current state (Module 12). The rendering function never needs to know *why* the data changed, only *that* it changed.

> **WHY `GRUPOSMOCK` BECAME `LET`**
> Since Module 02: `const` prevents reassigning the whole variable. Since `removerGrupo` reassigns `gruposMock` (`gruposMock = gruposMock.filter(...)`), the variable needs to be `let`. If you only changed items inside the array (without reassigning the whole array), `const` would keep working. But filtering always creates a new array, so the variable holding it needs to accept reassignment.

## // Componentization: one function per "piece" of interface

> **COMPONENTIZATION: IN SIMPLE WORDS**
> It means extracting a function that knows how to build a specific, reusable piece of the interface, instead of rewriting the same HTML structure in several places in the code.

<div align="center">
<img src="../docs/assets/component-function-pattern.svg" alt="A criarCardHTML function reused on the Dashboard, on the Profile and in the filtered search" width="560">
</div>

```javascript
function criarCardHTML(grupo) {
  return `
    <article class="card">
      <h3>${grupo.materia}</h3>
      <p>${grupo.participantes} participants</p>
      <button class="botao botao-primario" data-id="${grupo.id}">Join</button>
    </article>
  `;
}

function renderizarGrupos(lista) {
  container.innerHTML = lista.map(criarCardHTML).join("");
}
```

Notice that `.map(criarCardHTML)` passes the function directly, without needing to write `.map((grupo) => criarCardHTML(grupo))`: when the function already receives exactly the argument `.map()` provides, there is no need to wrap it in another function.

## // Why this pays off, even in a small project

If the Profile also needs to show group cards (the groups the person belongs to), `criarCardHTML` can be reused there, without duplicating the card's structure. If the card's look needs to change (a new button, new information), it changes in a single place, and it is reflected on every screen that uses that function.

## // No framework, on purpose

Frameworks like React (which you will meet in future weeks of the club, if the path continues) formalize exactly these two concepts (state and componentization) with their own, more powerful tools. Understanding the pattern in plain JavaScript first is what makes a framework, later on, feel like a natural extension of what you already know, instead of a new, arbitrary syntax to memorize.

## // Good example × bad example

**Bad example**: changing the screen directly, without going through the state:

```javascript
botaoSair.addEventListener("click", function () {
  document.querySelector(".card").remove(); // removes it only from the screen
  // gruposMock still has the "removed" item, out of sync
});
```

**Good example**: changing the state, letting the rendering reflect it:

```javascript
botaoSair.addEventListener("click", function () {
  gruposMock = gruposMock.filter((g) => g.id !== idDoGrupo);
  renderizarGrupos(gruposMock);
});
```

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| Screen and data out of sync | Changing the DOM directly (`.remove()`, `.textContent`) instead of updating the state and re-rendering | Always update the state array/object first, then call the rendering |
| The card's HTML duplicated in several places in the code | Not having extracted a component function | Extract `criarCardHTML(...)` (or an equivalent name) as soon as the same structure shows up a second time |
| `const gruposMock` preventing items from being removed | Forgetting to switch to `let` once the array starts being reassigned | Use `let` whenever the state variable is reassigned, not only changed inside |
| A component function mixing in state-changing logic | Making the HTML-building function also change data | Keep rendering functions "dumb"; they only read the state, never change it |

## // Guided practice

1. Extract `criarCardHTML(grupo)` from your `renderizarGrupos`, following the example in this section.
2. Write `removerGrupo(id)`, updating `gruposMock` (now `let`) and calling `renderizarGrupos` again.
3. Connect a "Leave group" button (it can be on the Profile) to that function, using the matching group's `id`.
4. Test: clicking "Leave group" should update the screen immediately, without a reload, and without leaving any data out of sync.

## // Practice on your own

> **CHALLENGE**
> Write a function `adicionarGrupo(novoGrupo)` that receives a `{ materia, participantes }` object, automatically generates a new `id` (a simple way: `Date.now()`, which always returns a different number), adds it to `gruposMock`, and calls `renderizarGrupos` again. Test it by calling the function manually from the console.

## // Applying it to the week's project

1. Extract at least one component function (`criarCardHTML` or equivalent) in your project.
2. Implement `removerGrupo(id)` (or an equivalent action in your domain), strictly following the state → render cycle.
3. Confirm that no part of your code changes the DOM directly in response to an action without going through the state first.
4. Commit: `git commit -m "Formalize state and extract a reusable component function"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> A classmate suggests handling the removal of a group by calling `elemento.remove()` directly on the clicked card, "because it's faster". What real problem does that create, even if it seems to work visually at the moment?

Answer: the card disappears from the screen, but the matching item stays in the state array (`gruposMock`). Any part of the code that depends on that state later (a group counter, a new render after a search, saving the data down the road) will keep counting the "removed" group, because it was never actually removed from the source of truth. The screen and the data get out of sync: a problem that only grows as more parts of the interface start depending on the same data.

## // Module summary

- [ ] I can explain what "state" means in the context of an interface.
- [ ] I know why changing the screen directly, without going through the state, causes things to get out of sync.
- [ ] I can extract a reusable component function, instead of duplicating HTML.
- [ ] I can implement an action (remove, add) following the state → render cycle.
- [ ] My project already has at least one complete action following this pattern, without changing the DOM directly.

---

**Next module:** `14-guided-project.md`: putting it all together, from start to finish, on the three complete screens.

`Study Material // Coffee & Code`
