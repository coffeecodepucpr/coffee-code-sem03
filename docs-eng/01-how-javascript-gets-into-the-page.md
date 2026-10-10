# Module 01, How JavaScript Gets into the Page

[Português](../docs/01-como-o-javascript-entra-na-pagina.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // Before you start

In Module 00 you saw the model: HTML is structure, CSS is presentation, JavaScript is behavior. This module answers a very practical question before any logic: where does this code live, and when exactly does it run?

## // Connecting a `.js` file to the HTML

Just as CSS lives in a separate file connected by `<link>`, JavaScript lives in a `.js` file connected by `<script>`:

```html
<head>
  <script src="script.js" defer></script>
</head>
```

## // Why `defer` matters

> **THE PROBLEM WITHOUT `DEFER`**
> The browser reads the HTML from top to bottom. If a `<script>` shows up in the middle of the `<head>`, before the `<body>` exists, and that script tries to select an element from the `<body>` (Module 07), it simply will not find anything, because that element has not been read by the browser yet.

Two traditional solutions, and a modern one:

| Approach | How it works |
|---|---|
| `<script>` at the end of the `<body>` | Works, but mixes the HTML's organization with where the JS lives |
| `<script defer>` in the `<head>` | The browser downloads the file in parallel, but only runs it after all the HTML has been read; this is the recommended option |
| `<script async>` | Runs as soon as it finishes downloading, possibly interrupting the HTML reading, so it is rarely what you want for scripts that read the DOM |

Use `<script src="script.js" defer></script>` in the `<head>` as the default, for two reasons: it keeps the HTML organized (every `<script>` and `<link>` together, in the `<head>`) and it guarantees the whole HTML already exists before your code runs.

## // The console: where your code "talks" to you

Every browser has a **console**, accessible through the developer tools (usually the F12 key, or right-click → Inspect → Console tab). `console.log(...)` prints any value there, and it is the most used tool to understand what your code is doing:

```javascript
console.log("The script loaded");
console.log(2 + 2);
```

> **A HABIT WORTH BUILDING NOW**
> Whenever something does not do what you expect, the first step is to open the console. A red error there almost always tells you the exact file and line where the problem is. Ignoring that message and trying to guess costs much more time than reading it.

## // JavaScript runs once, from top to bottom

Contrary to what people sometimes imagine, a `.js` file does not sit "waiting" forever: it runs once, line by line, from top to bottom, at the moment it is loaded (respecting `defer`, as you saw above). Code that needs to run *later*, in response to something the person does (a click, for example), has to be organized for that, which is exactly what Module 09 (Events) teaches. For now, every example from this module on runs right away, as soon as the file loads.

## // Good example × bad example

**Bad example**: script in the middle of the `<head>`, without `defer`, trying to read the `<body>`:

```html
<head>
  <script src="script.js"></script>
</head>
<body>
  <h1>Study Group Finder</h1>
</body>
```

If `script.js` tries to select the `<h1>`, it fails: the `<body>` does not exist yet at the moment the script runs.

**Good example**: the same script, with `defer`:

```html
<head>
  <script src="script.js" defer></script>
</head>
<body>
  <h1>Study Group Finder</h1>
</body>
```

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| `null` when trying to select an element | The script ran before the HTML existed | Add `defer` to the `<script>` |
| Nothing shows up in the console | Wrong `src` path, or file not saved | Check the relative path and whether the file was saved |
| Red error ignored | It seems faster to keep trying without reading | Read the first error message: it almost always points to the exact cause |

## // Guided practice

1. Create the `script.js` file at the root of your project (or in a `js/` folder, if you prefer to organize it that way).
2. Connect it in `dashboard.html`, `login.html` and `perfil.html`, using `<script src="script.js" defer></script>` in the `<head>` of each one.
3. Inside `script.js`, write `console.log("Script loaded successfully");`.
4. Open each page in the browser, open the console (F12), and confirm the message shows up on all three.

## // Practice on your own

> **CHALLENGE**
> Temporarily remove `defer` from the Dashboard's `<script>`, and add, at the very top of `script.js`, a line trying to read something from the `<body>` (you will learn the exact syntax in Module 07; for now, if you just want to see the error, use `document.body.innerHTML` inside a `console.log`). See what shows up in the console. Then put `defer` back and confirm the error goes away.

## // Applying it to the week's project

1. Create `script.js` and connect it to your project's three pages, with `defer`.
2. Confirm, via `console.log`, that the script loads correctly on all three.
3. Commit: `git commit -m "Connect script.js to the three screens"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> A classmate removes `defer` from the `<script>` "because it seems simpler" and moves the `<script>` to the end of the `<body>` instead. Does that solve the same problem `defer` solves?

Answer: yes, it works: putting the `<script>` at the end of the `<body>` guarantees all the HTML above has already been read before the script runs, for the same reason `defer` guarantees it. The difference is organizational: with `defer` in the `<head>`, every `<link>` and `<script>` sits together, in a predictable place; moving the script to the end of the `<body>`, its location depends on where someone remembered to put it. Neither is "wrong": `defer` in the `<head>` is just the most common convention today.

## // Module summary

- [ ] I can connect an external `.js` file to the HTML.
- [ ] I know why `defer` avoids the most common mistake of people starting with JavaScript.
- [ ] I can open the browser console and use `console.log` to inspect values.
- [ ] I know a script runs once, from top to bottom, when the page loads.
- [ ] My project's three pages already have `script.js` connected correctly.

---

**Next module:** `02-variables-types-and-operators.md`: before any logic, the minimum vocabulary: where values are stored.

`Study Material // Coffee & Code`
