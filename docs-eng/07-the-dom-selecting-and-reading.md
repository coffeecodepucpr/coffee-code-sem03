# Module 07, The DOM: Selecting and Reading

[Português](../docs/07-o-dom-selecionar-e-ler.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // The problem

All the code you have written so far runs in isolation, printing results only to the console. To really change what a person sees on the screen, JavaScript first needs to **find** the right HTML element. That is exactly what this module solves.

## // What the DOM is

> **DOM: IN SIMPLE WORDS**
> When the browser reads an HTML file, it builds, in memory, a representation of the whole page structure: the DOM (Document Object Model). It is this representation, not the `.html` file itself, that JavaScript can read and change.

This connects directly to Module 02 (HTML) from Week 02: the parent/child/sibling element tree you saw there *is* the DOM. Selecting an element means finding a specific point in that tree.

## // `document`: the entry point

Every access to the DOM starts from the global `document` object, which represents the whole page:

```javascript
console.log(document.title); // the text on the browser tab
```

## // Selecting elements

```javascript
const titulo = document.querySelector("h1");
const primeiroCard = document.querySelector(".card");
const todosOsCards = document.querySelectorAll(".card");
const campoEmail = document.querySelector("#email");
```

| Method | What it returns |
|---|---|
| `querySelector(selector)` | The **first** element that matches the CSS selector, or `null` if none matches |
| `querySelectorAll(selector)` | A collection with **all** the matching elements |
| `getElementById(id)` | The element with that specific `id` (without the `#` in front, unlike `querySelector`) |

The selector passed to `querySelector`/`querySelectorAll` uses exactly the same CSS syntax you have used since Week 02: `.class`, `#id`, `tag`, `.parent .child`: it all works the same way.

## // Why `querySelectorAll` is not a "real" array

```javascript
const cards = document.querySelectorAll(".card");
console.log(cards.length); // works, like an array
cards.forEach(function (card) {
  console.log(card); // works, like an array
});
```

`querySelectorAll` returns a **NodeList**, close enough to an array to use `.length` and `.forEach()`, but without `.map()` or `.filter()` natively. If you need those tools, convert it first: `Array.from(cards)`.

## // Reading content and attributes

```javascript
const titulo = document.querySelector("h1");
console.log(titulo.textContent); // the text inside the element

const campoEmail = document.querySelector("#email");
console.log(campoEmail.value); // what the person typed in the field
```

> **`VALUE` × `TEXTCONTENT`**
> `.value` reads (or changes) the value of form fields (`input`, `select`, `textarea`). `.textContent` reads (or changes) the text of regular elements (`p`, `span`, `h1`, `div`). Using one in place of the other is one of the most common beginner mistakes: an `input` has no useful `.textContent`, and a `<p>` has no `.value`.

## // Checking whether an element was found

```javascript
const elemento = document.querySelector(".card-destaque");
if (elemento) {
  console.log("Element found");
} else {
  console.log("No element with this class exists on the page");
}
```

When `querySelector` finds nothing, it returns `null`, which is falsy (Module 03). Testing `if (elemento)` before using the result avoids a common error: trying to read a property of `null`.

## // Good example × bad example

**Bad example**: assuming the element always exists:

```javascript
const campo = document.querySelector("#campo-que-nao-existe");
console.log(campo.value); // error: cannot read property of null
```

**Good example**: checking first:

```javascript
const campo = document.querySelector("#campo-que-nao-existe");
if (campo) {
  console.log(campo.value);
} else {
  console.log("Field not found, check the selector");
}
```

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| `Cannot read properties of null` | `querySelector` found nothing, and the code tried to use the result anyway | Check the selector; consider testing `if (elemento)` before using it |
| `.value` returning `undefined` on a `<p>` | Mixing up `.value` and `.textContent` | `<p>`, `<span>`, `<h1>` use `.textContent`; form fields use `.value` |
| `querySelectorAll(...).map is not a function` | A NodeList has no native `.map()` | Use `.forEach()`, or convert with `Array.from(...)` before using `.map()` |
| The selector finds nothing, even though it exists on the page | The script ran before the HTML existed | Confirm the `<script>` has `defer` (Module 01) |

## // Guided practice

1. In the Dashboard's `script.js`, select the page's `<h1>` element with `querySelector` and print its `.textContent` in the console.
2. Select all elements with the `.card` class using `querySelectorAll`, and print how many were found (`.length`).
3. Select the search field (`.busca`, from Week 02) and print `.value`. Even if empty, confirm there is no error.
4. Try selecting a selector you know does not exist on the page, and write the `if (elemento)` to handle that case without an error.

## // Practice on your own

> **CHALLENGE**
> On the Login, select the e-mail and password fields with `querySelector`. Print, in the console, a sentence combining the two values (even if empty), using template literals (as in Module 06).

## // Applying it to the week's project

1. In the `script.js` of each screen in your project, select at least three real elements (a heading, a container, a form field or button).
2. Confirm, with `console.log`, that each selection found the right element.
3. Commit: `git commit -m "Add initial DOM element selection"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> `document.querySelector("#busca").value` returns `undefined` instead of the typed text. The element with `id="busca"` exists on the page, and the `<script>` already has `defer`. What else would you investigate?

Answer: whether the selected element really is a form field (`input`, `select`, `textarea`), because `.value` only exists in a useful way on those elements. If `#busca` is, by mistake, a `<div>` or another element with no input field, `.value` will not contain the expected text. It is worth checking the exact tag of the element with that `id` in the HTML.

## // Module summary

- [ ] I know what the DOM is, and why it is different from the `.html` file itself.
- [ ] I can use `querySelector` and `querySelectorAll`.
- [ ] I know the difference between `.value` and `.textContent`, and when to use each one.
- [ ] I can check whether an element was found before using it.
- [ ] I have already selected real elements from my project's three screens.

---

**Next module:** `08-the-dom-creating-and-changing-elements.md`: selecting is only the first step. Now, how to create and change what is on the screen.

`Study Material // Coffee & Code`
