# Challenges, Week 03

[Português](../docs/desafios.md) · English

Optional challenges, organized by the week's modules. None is required for the basic submission; see `deliverable.md` for what is required. Use these challenges if you finished the main modules and want to go further, or if you want to make the deliverable more robust.

---

## // JavaScript fundamentals (Modules 02 to 04)

**If you are just starting**
- Write a function `formatarParticipantes(n)` that returns `"1 participant"` (singular) when `n` is 1, and `"N participants"` (plural) for any other value.
- Research template literals with multiple variables and rewrite one of the error messages from Module 10 using one.

**If you already have experience**
- Research the difference between a declared `function` and an arrow function regarding the value of `this`, and write your own example showing a case where that difference matters.

---

## // Arrays and objects (Modules 05 to 06)

**If you are just starting**
- Use `.sort()` to order `gruposMock` by number of participants, from lowest to highest, and confirm the result in the console.

**If you already have experience**
- Research `.reduce()` and use it to add up the total participants of all groups into a single number.
- Research the spread operator (`...`) to create a copy of an object with one property changed, without mutating the original.

---

## // DOM and events (Modules 07 to 09)

**If you are just starting**
- Add a visible counter on screen ("X groups found"), updated every time the Dashboard search filters the list.

**If you already have experience**
- Research event delegation (the pattern you already used in Module 14, with `event.target.matches(...)`) and apply the same pattern in another context of your project, such as clicks on subject tags on the Profile.
- Research `event.stopPropagation()` and identify a scenario in your project where it would make sense.

---

## // Validation (Module 10)

**If you are just starting**
- Add a password confirmation check (two fields that need to match) to the sign-up screen, if you have one.

**If you already have experience**
- Research Regular Expressions (Regex) and use one to validate the e-mail format more strictly than just checking `.includes("@")`.

---

## // JSON and mock data (Module 11)

**If you are just starting**
- Export `gruposMock` as a separate `.json` file (copy the result of `JSON.stringify(gruposMock, null, 2)`), and document that decision in `docs/arquitetura.md`.

**If you already have experience**
- Research `fetch()` to read that same local `.json` file (instead of having it written directly in `script.js`), without worrying about sending data anywhere yet, just fetching a static file.

---

## // Rendering, state and componentization (Modules 12 to 13)

**If you are just starting**
- Add a visible empty state ("No groups found") when a search returns no results.

**If you already have experience**
- Extract a second reusable component (for example, `criarTagHTML(materia)` for the Profile tags) and apply the same reuse reasoning from Module 13.
- Implement `adicionarGrupo(novoGrupo)` (from the Module 13 challenge) connected to a real "create group" form, following the state → render cycle.

---

## // General challenge (everyone)

Ask someone else (or yourself, reviewing after a break) to use your three screens with no explanation from you: try a wrong login and a right one, search for a group on the Dashboard, leave a group on the Profile. Does that person understand what is happening with each action, even without knowing the data is mock? If the answer is yes, your deliverable is at a good level. If not, go back to the corresponding module.
