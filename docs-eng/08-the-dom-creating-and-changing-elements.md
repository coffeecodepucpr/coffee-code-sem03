# Module 08, The DOM: Creating and Changing Elements

[Português](../docs/08-o-dom-criar-e-modificar-elementos.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // Before you start

Module 07 solved "finding". This module solves "changing": changing text, classes, and even creating elements that did not exist in the original HTML. It is the missing piece before rendering any dynamic list (Module 12).

## // Changing text

```javascript
const titulo = document.querySelector("h1");
titulo.textContent = "Welcome back!";
```

Assigning a new value to `.textContent` replaces the element's text: the same property you used to *read* in Module 07 also works to *write*.

## // Changing classes with `classList`

```javascript
const card = document.querySelector(".card");
card.classList.add("destaque");
card.classList.remove("oculto");
card.classList.toggle("selecionado");
```

| Method | Effect |
|---|---|
| `.add("class")` | Adds the class, if it is not there yet |
| `.remove("class")` | Removes the class, if it is there |
| `.toggle("class")` | Adds it if missing, removes it if already there |

`classList` is the recommended way to change appearance via JavaScript: instead of writing CSS styles directly in JavaScript, you switch on and off classes that already have their rules defined in `styles.css`, keeping the separation between structure/behavior (JS) and presentation (CSS) that comes from Week 02.

## // Creating new elements

```javascript
const lista = document.querySelector(".lista-materias");
const item = document.createElement("li");
item.textContent = "Cálculo I";
lista.appendChild(item);
```

Three steps, always in the same order: **create** the element (`createElement`), **configure** it (text, classes, attributes), and **insert** it somewhere on the page (`appendChild`, on the element that will be its parent).

## // Removing elements

```javascript
const item = document.querySelector(".card-antigo");
item.remove();
```

## // `innerHTML`: powerful, but with a safety rule

```javascript
const card = document.querySelector(".card");
card.innerHTML = "<strong>Cálculo I</strong> | 5 participants";
```

`innerHTML` interprets the assigned text as real HTML: it lets you create several elements at once, in one line, instead of several `createElement` calls. It is the technique used in Module 12 to render whole lists.

> **THE RULE THAT DOES NOT CHANGE**
> `innerHTML` should never directly receive text a person typed without treatment: that opens room for code injection (someone typing a malicious `<script>` into a field, for example). When the content comes from data you control (an array you wrote yourself, or later on a trusted API), it is an acceptable use. When the content comes straight from a form field without any treatment, prefer `.textContent`.

## // Comparing the three ways to change content

| Option | Advantage | Watch out |
|---|---|---|
| `.textContent` | Simple, always safe for plain text | Does not interpret HTML tags: if you assign `"<b>text</b>"`, it shows up literally with the tags visible |
| `createElement` + `appendChild` | Full control of the structure, element by element | More lines of code for large structures |
| `innerHTML` | Creates several layers of HTML quickly, in one line | Never use it with untrusted, untreated text |

## // Good example × bad example

**Bad example**: `innerHTML` receiving text from a field, without any treatment:

```javascript
const nomeDigitado = document.querySelector("#nome").value;
resultado.innerHTML = nomeDigitado; // risky, if nomeDigitado can come from anyone
```

**Good example**: the same case, with `.textContent`, safe:

```javascript
const nomeDigitado = document.querySelector("#nome").value;
resultado.textContent = nomeDigitado;
```

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| Tags showing up as literal text on screen | Used `.textContent` expecting it to interpret tags like `innerHTML` | Use `innerHTML` when the content really contains HTML tags |
| Element created, but it does not show on the page | Forgot `appendChild` (or equivalent) after `createElement` | `createElement` only creates the element in memory; it needs to be inserted somewhere in the DOM |
| `classList.add` "doesn't work" | The class name does not match what exists in the CSS | Check the exact name, including upper/lowercase |
| `innerHTML` used with an untrusted value | Forgetting the safety rule | Switch to `.textContent` whenever the content comes from a person without treatment |

## // Guided practice

1. On the Dashboard, select the `<h1>` and change its `.textContent` to a different greeting.
2. Select a `.card` and use `classList.add` to add a new class (it can be just for testing, with no style defined yet).
3. Create a new `<li>` element with `createElement`, give it a `.textContent`, and insert it into some existing container with `appendChild`.
4. Remove an element from the page using `.remove()`.

## // Practice on your own

> **CHALLENGE**
> Create three different `<li>` elements, each with different text, and insert all of them into the same container, using a `for...of` (Module 03) combined with `createElement` and `appendChild` inside the loop.

## // Applying it to the week's project

1. On the Profile, use `classList` to visually highlight some element (for example, marking the currently selected group).
2. Practice creating at least one new element via `createElement` + `appendChild`, even if the content is still fixed (the real dynamic version comes in Module 12).
3. Commit: `git commit -m "Add creation and modification of DOM elements"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> You want to show, inside a card, text that includes `<strong>` to highlight a word. Does `.textContent` work for that?

Answer: no. `.textContent` treats anything assigned to it as plain text: if you write `"<strong>5 spots</strong>"`, the card will literally show the characters `<strong>` and `</strong>` on screen, instead of applying bold. For the tags to be interpreted as real HTML, you need `innerHTML` (or `createElement`, building the `<strong>` element separately). Since this content does not come from a person typing, it is an acceptable use of `innerHTML`.

## // Module summary

- [ ] I can change the text of an existing element.
- [ ] I can use `classList.add`, `.remove()` and `.toggle()`.
- [ ] I can create a new element with `createElement` and insert it with `appendChild`.
- [ ] I know the difference between `.textContent` and `innerHTML`, and when each one is safe to use.
- [ ] I have already practiced creating and changing real elements on at least one screen of my project.

---

**Next module:** `09-events.md`: so far, everything runs as soon as the page loads. Time to react to clicks, typing and form submissions.

`Study Material // Coffee & Code`
