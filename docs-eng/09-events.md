# Module 09, Events

[Português](../docs/09-eventos.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // The problem

Everything you have written so far runs **once**, as soon as the script loads (Module 01). But most of an interface's real behavior should only happen **in response** to an action: clicking "Sign in", typing in a field, submitting a form. This module is where "code that runs on its own" becomes "code that reacts".

## // What an event is

> **EVENT: IN SIMPLE WORDS**
> It is something that happens on the page (a click, a key pressed, a form submitted) that JavaScript can "listen to" and react to.

<div align="center">
<img src="../docs/assets/event-listener-flow.svg" alt="Flow: selected element, addEventListener listening, the person's action, callback function running" width="560">
</div>

## // `addEventListener`

```javascript
const botao = document.querySelector("#botao-entrar");

botao.addEventListener("click", function () {
  console.log("Button clicked");
});
```

Three parts: the **element** that will listen (`botao`), the **event type** (`"click"`), and the **function** that runs when the event happens: that function is usually called a *callback*, because JavaScript "calls it back" when the event occurs, not immediately when this line is read.

## // The most common events

| Event | When it happens |
|---|---|
| `click` | A click on any element |
| `input` | A field's value changes, on every key typed |
| `change` | A field's value changes **and** it loses focus (common in `select`) |
| `submit` | A form is submitted |
| `keydown` | A key is pressed |
| `DOMContentLoaded` | The HTML has finished being read (rarely needed if you already use `defer`, Module 01) |

## // The `event` object

The callback function automatically receives an object with information about what happened. By convention, it is called `event` or `e`:

```javascript
const form = document.querySelector("#form-login");

form.addEventListener("submit", function (event) {
  event.preventDefault();
  console.log("Submission handled by JavaScript, without reloading the page");
});
```

> **`EVENT.PREVENTDEFAULT()`**
> Forms, by default, try to reload the page when submitted: that is HTML's native behavior, from before JavaScript existed. `event.preventDefault()` cancels that default behavior, leaving you in full control of what happens with the form's data. Without this line, any validation logic (Module 10) would be interrupted by the reload before it could run.

## // `input` × `change`

```javascript
const campoBusca = document.querySelector(".busca");

campoBusca.addEventListener("input", function (event) {
  console.log("Searching for:", event.target.value);
});
```

`event.target` is the element that fired the event: in the case of a text field, `event.target.value` is the current value, key by key. This is exactly the pattern that connects the Dashboard's search field to `filtrarPorBusca(...)` (Module 12): on every key typed, the `input` event fires, and the search runs again.

## // The complete mental flow

1. I find the element (Module 07).
2. I listen to the right event, with `addEventListener`.
3. When it happens, I read the relevant data (`event.target.value`, for example).
4. I decide what to do with that data (Module 03, decisions).
5. I update the screen or the stored data (Module 08, and Module 12 for lists).

This five-step cycle is, in practice, the "skeleton" of practically every dynamic interaction you will build from now on.

## // Good example × bad example

**Bad example**: forgetting `preventDefault` on a form:

```javascript
form.addEventListener("submit", function (event) {
  console.log("This runs, but the page reloads right after");
});
```

**Good example**: full control of the submission:

```javascript
form.addEventListener("submit", function (event) {
  event.preventDefault();
  console.log("I process the form without reloading");
});
```

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| The page reloads when submitting the form | `event.preventDefault()` missing in the `submit` event | Add the call as the first line of the function |
| The callback does not receive the right event | Forgot to declare the parameter (`function (event) {...}`) | Always declare the parameter, even if you only use `event.target` sometimes |
| `addEventListener` "doesn't work" | Element selected before it existed, or wrong selector (Module 07) | Confirm the selection with `console.log(elemento)` before adding the listener |
| The event fires several times for a single action | `addEventListener` called more than once for the same element/event, usually because the function runs again unnecessarily | Make sure the event setup runs only once, when the page loads |

## // Guided practice

1. On the Dashboard, select a card's "Join" button and add an `addEventListener("click", ...)` that prints a message in the console.
2. On the Login, select the `<form>` and add a `submit` listener, with `event.preventDefault()` as the first line.
3. On the search field, add an `input` listener that prints `event.target.value` on every key typed.
4. Test all three in the browser, watching the console.

## // Practice on your own

> **CHALLENGE**
> Add a `click` listener to an element (any one) that, on each click, uses `classList.toggle("ativo")` on itself (`event.target.classList.toggle(...)`). Visually confirm, even without a style defined for `.ativo` yet, that the class appears and disappears on each click, by inspecting the element in DevTools.

## // Applying it to the week's project

1. Add `addEventListener` to your project's real interactive elements: the Login button, the Dashboard search field, and at least one Profile button.
2. Make sure the Login form uses `event.preventDefault()`.
3. Commit: `git commit -m "Add event listeners to the interactive elements"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> A "Join" button has an `addEventListener("click", ...)`, but nothing happens when you click it: no error in the console, no change at all. What would you investigate, in this order?

Answer: first, whether `querySelector` really found the button (`console.log(botao)`; if it is `null`, the listener was never actually added to anything). Second, whether the selector used matches exactly the right element, especially if there is more than one similar button on the page. Third, whether the callback itself has code that produces an observable effect: an `addEventListener` with no visible line inside the function "works", it just does not seem to do anything.

## // Module summary

- [ ] I can use `addEventListener` to listen to an event on an element.
- [ ] I know the difference between `click`, `input`, `change` and `submit`.
- [ ] I know what the `event` object is, and what `event.target` represents.
- [ ] I know why `event.preventDefault()` is needed on forms.
- [ ] I have already connected real events to my project's interactive elements.

---

**Next module:** `10-forms-and-validation-in-js.md`: with events ready, time to apply them directly to the Login form.

`Study Material // Coffee & Code`
