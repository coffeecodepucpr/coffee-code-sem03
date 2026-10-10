# Runnable example: Study Group Finder (Week 03)

[Português](../../docs/example/README.md) · English

An evolution of the Week 02 example, now with real JavaScript. The three screens (Login, Dashboard, Profile) have real behavior: no backend, no framework.

> The example's pages, texts and code are in Portuguese, the same as the rest of the track. The files themselves live in [`docs/example/`](../../docs/example/).

## This is NOT a required answer key

It is a reference for an achievable level. Your real project does not need to look like this one: it needs to apply the same concepts (validation, DOM, events, rendering from data, state).

## What this example shows

- `<script defer>` connecting `script.js` to the three pages (Module 01)
- Full Login validation (empty, format, minimum length, specific messages, cleared on each attempt) (Module 10)
- Dashboard rendered entirely from `gruposMock` via `.map()` + `innerHTML`, never fixed HTML (Module 12)
- A search that really works, filtering in real time without a reload (Modules 05, 09, 12)
- An empty state ("Nenhum grupo encontrado", no groups found) when the search returns nothing
- The Profile reflecting `usuarioMock` (name, e-mail, tags), never fixed text (Module 06)
- "Sair do grupo" (leave group) strictly following the state → render cycle: it never removes the card directly from the DOM, it always updates `usuarioMock.materias` first (Module 13)
- `criarCardHTML(grupo, opts)` as a component function, reused on the Dashboard *and* the Profile, with the button changing according to the context (Module 13)
- Event delegation: a single `addEventListener` on the grid, not one per card, since the cards are created after the page loads (Module 14)
- `if (!elemento) return;` at the top of each initialization function, since the same `script.js` runs on the three pages (Module 07)

## Files

```
docs/example/
├── index.html
├── login.html
├── dashboard.html
├── perfil.html
├── styles.css       (inherited from Week 02, with small additions)
└── script.js         (new: all of Week 03's logic)
```

## Testing

Open any page directly in the browser, or [open it online](https://coffeecodepucpr.github.io/coffee-code-sem03/docs/example/index.html). On the Dashboard, type in the search to filter. On the Profile, click "Sair do grupo" and watch the screen (and the count, and the tags) update without a reload. Open the console (F12) to see the logs for each action.

## A note on screenshot tools

If you use an old rendering tool (such as `wkhtmltoimage`, based on a ~2013 WebKit) to take a screenshot, the grid may show up in 1 column: CSS Grid did not exist when that engine was created. In any current browser, it renders correctly.
