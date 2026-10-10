# Coffee & Code | WEEK 03 | Web Interface (Part 2: Interactivity)

[Português](README.md) · English

```text
> module: sem-03
> topic: web interface (interactivity)
> status: online
> coffee loaded
```

Material for **Week 03** of the Coffee & Code track, a technology club founded by Software Engineering students at PUCPR and open to anyone who wants to learn by building.

In Week 02 you built the three screens in HTML and CSS. They open in the browser and adapt to phones, but they do not do anything. The Login form accepts anything, the Dashboard always shows the same fixed cards, the leave-group button does not leave anywhere.

Week 03 exists to give these screens behavior: ES6+ JavaScript, the DOM, events, form validation and JSON data. By the end of the week the interface reacts, validates and renders, still without a backend, but with real logic.

> **About the language:** the English material lives in [`docs-eng/`](docs-eng/), with the same structure as [`docs/`](docs/) (Portuguese); the READMEs have an English version with the `.en.md` suffix. The diagrams, the runnable example and the example code's variable names stay in Portuguese.

## Where to start

**[docs-eng/00-start-here.md](docs-eng/00-start-here.md)**: read this one first. It explains the week's path and what comes from Week 02.

Then follow the modules in order:

| # | Module | About |
|---|---|---|
| 01 | [How JavaScript gets into the page](docs-eng/01-how-javascript-gets-into-the-page.md) | `<script>`, `defer`, browser console |
| 02 | [Variables, types and operators](docs-eng/02-variables-types-and-operators.md) | `let`/`const`, primitive types, `===` |
| 03 | [Decisions and loops](docs-eng/03-decisions-and-loops.md) | `if/else`, `for`, `while`, `for...of` |
| 04 | [Functions and arrow functions](docs-eng/04-functions-and-arrow-functions.md) | Functions, arrow functions, scope |
| 05 | [Arrays and essential methods](docs-eng/05-arrays-and-essential-methods.md) | `.map()`, `.filter()`, `.find()` |
| 06 | [Objects and destructuring](docs-eng/06-objects-and-destructuring.md) | Objects, destructuring |
| 07 | [The DOM: selecting and reading](docs-eng/07-the-dom-selecting-and-reading.md) | `querySelector`, `.value`, `.textContent` |
| 08 | [The DOM: creating and changing elements](docs-eng/08-the-dom-creating-and-changing-elements.md) | `classList`, `createElement`, `innerHTML` |
| 09 | [Events](docs-eng/09-events.md) | `addEventListener`, `event.preventDefault()` |
| 10 | [Forms and validation in JS](docs-eng/10-forms-and-validation-in-js.md) | Full Login validation |
| 11 | [JSON and mock data](docs-eng/11-json-and-mock-data.md) | JSON, `JSON.stringify`/`parse`, mock data |
| 12 | [Rendering lists dynamically](docs-eng/12-rendering-lists-dynamically.md) | Data array → cards on screen |
| 13 | [State and componentization](docs-eng/13-state-and-componentization.md) | State, render cycle, componentization |
| 14 | [Guided project](docs-eng/14-guided-project.md) | Building the three dynamic screens, from start to finish |

And, to look up whenever you need:

- [Runnable example](docs-eng/example/README.md): the three screens with real JavaScript, for reference
- [Challenges](docs-eng/challenges.md): optional, to go beyond what is asked
- [Deliverable](docs-eng/deliverable.md): final checklist before closing the week

## The runnable example

The [`docs/example/`](docs/example/) folder has a reference implementation of the three screens (Login, Dashboard, Profile), evolving the Week 02 example with real JavaScript. Download the repository and open `index.html` in the browser to move between them, or [open it online](https://coffeecodepucpr.github.io/coffee-code-sem03/docs/example/index.html).

It is **reference material, not an answer key**. Your project has its own screens: the example is there for you to see one possible solution when you get stuck, not to copy.

## The deliverable

At the end of Week 03, the repository of **your project** (not this one) should have, in addition to everything from Weeks 01 and 02:

```text
login.html
dashboard.html
perfil.html
script.js         ← new (or one per screen), connected to the pages with defer
css/
└── styles.css
```

The Login needs to really validate, the Dashboard needs to render and filter the cards from mock data, and the Profile needs at least one action working without reloading the page.

The full checklist is in [docs-eng/deliverable.md](docs-eng/deliverable.md).

> **Correct logic is worth more than visual polish.** A validation that correctly blocks a badly formatted e-mail, even with a simple message, is worth more this week than a beautiful interface that accepts anything.

## Class submissions

Projects from people who submitted Week 03. Want to submit yours? See [how to submit](entregas/README.en.md).

| Person | Project | About | Links |
|---|---|---|---|
| Luis Medina | Estom | Price tracking for online products | [folder](entregas/Luis%20Medina/) · [Figma](https://www.figma.com/proto/oL9MehNA1Gea3Zhzh8I69z/Sem-t%C3%ADtulo?node-id=0-1&t=SoRcZQfwCZWOKUVi-1) · [view screens](https://coffeecodepucpr.github.io/coffee-code-sem03/entregas/Luis%20Medina/index.html) |
| Mikhail Kalinin | Learnplat | Online course platform connecting teachers and students | [folder](entregas/Mikhail%20Kalinin/) · [view screens](https://coffeecodepucpr.github.io/coffee-code-sem03/entregas/Mikhail%20Kalinin/pages/index.html) |
| Pedro Henrique Gouveia | No name yet | Login, sign-up, subjects dashboard with search and profile | [folder](entregas/Pedro%20Henrique%20Gouveia/) · [view screens](https://coffeecodepucpr.github.io/coffee-code-sem03/entregas/Pedro%20Henrique%20Gouveia/login.html) |
| Rodrigo Fagnani | FixAqui | Connects clients with professionals for small services | [folder](entregas/Rodrigo%20Fagnani/) · [Figma](https://www.figma.com/proto/8NBkV8NkIjlPJSXg4am1bf/Untitled?node-id=0-1&t=aBlZ6abbcyV5SmwH-1) · [view screens](https://coffeecodepucpr.github.io/coffee-code-sem03/entregas/Rodrigo%20Fagnani/login.html) |

## What is not part of this week

No backend, database or real network call. No framework (React or equivalent); everything in plain JavaScript, on purpose. And the mock data resets on every page reload: that is expected.

## Ongoing project

All modules use the same fictional project from the previous weeks: the **Study Group Finder** (*Buscador de Grupos de Estudo*). If you have your own project, the reasoning in each module applies the same way: just change the name.

## How it works

Coffee & Code is **100% online**. Each module was written to be self-contained: you study at your own pace, and you can move ahead faster, go back to previous weeks and look things up during the project.

The weekly meetings, also online, are there to answer questions, review concepts, code together and show what you have built, **not to lecture** (Brasília time, UTC-3):

- **Wednesday**: 8:00 PM to 9:30 PM
- **Saturday**: 10:00 AM to 11:30 AM

Both cover the same content. Pick whichever fits your week best, and you do not need to stay on the call for the whole time.

## Stuck?

Bring a specific question to the meeting or to Discord. `"my dynamically rendered button doesn't respond to clicks, I already tried X and Y"` usually gets solved much faster than `"my JavaScript doesn't work"`.

And remember: not knowing something is not a problem. Knowing how to research is part of the field.

## Diagrams

All the diagrams used in the modules are in [`docs/assets/`](docs/assets/), as editable SVG.

## Previous weeks

- [WEEK 01: Kickoff & Design System](https://github.com/coffeecodepucpr/coffee-code-sem01)
- [WEEK 02: Web Interface (Part 1: Layout)](https://github.com/coffeecodepucpr/coffee-code-sem02)

Full track and upcoming weeks: [Coffee & Code profile](https://github.com/coffeecodepucpr)

---

```text
HTTP 418: I'm a teapot
> ready to code
```
