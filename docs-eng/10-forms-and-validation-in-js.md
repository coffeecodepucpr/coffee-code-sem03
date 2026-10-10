# Module 10, Forms and Validation in JS

[Português](../docs/10-formularios-e-validacao-em-js.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // Before you start

Remember Module 03 (Week 02): `required` in HTML already prevents submitting an empty field, without any JavaScript. So why does this module exist? Because `required` alone does not validate *rules*: it does not confirm that a password has a minimum length, it does not show a specific, styled error message, and it does not check two related fields against each other. That is exactly what JavaScript solves, on top of what HTML already guarantees.

## // The validation flow

<div align="center">
<img src="../docs/assets/validation-flow.svg" alt="Validation flow: capture value, clean, check empty, check format, check rule, show feedback" width="560">
</div>

| Step | Question |
|---|---|
| 1. Capture | Which elements and values do I need to read? |
| 2. Clean | Do I need `.trim()` (remove spaces at the start/end) or `Number(...)`? |
| 3. Check empty | Was the required field filled in? |
| 4. Check format | Does the value follow the expected pattern (does an e-mail look like an e-mail)? |
| 5. Check rule | Does the data make sense for your system (a password with a minimum length, for example)? |
| 6. Show feedback | Does the message clearly say what the person needs to fix? |

## // Full example: validating the Login

```javascript
const form = document.querySelector("#form-login");
const campoEmail = document.querySelector("#email");
const campoSenha = document.querySelector("#senha");
const erroEmail = document.querySelector("#erro-email");
const erroSenha = document.querySelector("#erro-senha");

form.addEventListener("submit", function (event) {
  event.preventDefault();

  const email = campoEmail.value.trim();
  const senha = campoSenha.value;

  erroEmail.textContent = "";
  erroSenha.textContent = "";
  let valido = true;

  if (!email) {
    erroEmail.textContent = "Enter your e-mail.";
    valido = false;
  } else if (!email.includes("@")) {
    erroEmail.textContent = "Enter a valid e-mail.";
    valido = false;
  }

  if (senha.length < 8) {
    erroSenha.textContent = "The password must have at least 8 characters.";
    valido = false;
  }

  if (valido) {
    console.log("Valid form: the real submission would go here");
  }
});
```

Notice the structure: **each field** has its own check and its own error message, and the `valido` variable only becomes `false` when some rule fails, letting you show *all* errors at once, not only the first one found.

## // Why `.trim()` matters

```javascript
const nome = "   ".trim(); // ""
if (!nome) {
  console.log("Empty field, even though spaces were typed");
}
```

Without `.trim()`, someone typing only spaces would pass the empty-field check (since `"   "` is not, technically, an empty string). `.trim()` removes spaces from the start and end, revealing there is no real content there.

## // Good messages × vague messages

> **WHAT MAKES A GOOD ERROR MESSAGE**
> "Invalid data" does not say what to do. "The password must have at least 8 characters" says exactly what to fix. Whenever possible, the message should answer: what is wrong, and what the person needs to do to fix it.

## // Clearing previous error messages

Notice, in the full example, the two lines right at the start of the function: `erroEmail.textContent = ""` and `erroSenha.textContent = ""`. Without them, an error message from a previous attempt would stay on screen even after being fixed, because nothing ever clears it. Every validation should start by clearing the previous error state, before checking again.

## // Good example × bad example

**Bad example**: only using `alert()` to show an error:

```javascript
if (!email) {
  alert("Error!");
}
```

`alert()` blocks the whole page until the person clicks "OK", does not indicate *which* field is wrong, and cannot be styled in any way.

**Good example**: an inline, specific message, next to the field:

```javascript
if (!email) {
  erroEmail.textContent = "Enter your e-mail.";
}
```

## // Common mistakes

| Mistake | Why it happens | How to fix it |
|---|---|---|
| Only the first error shows up, the others are ignored | Using `return` inside each `if`, stopping the whole function | Use a `valido` variable that becomes `false`, without stopping the checks on the other fields |
| An old error message stays on screen | Forgot to clear it (`.textContent = ""`) at the start of the validation | Always clear the error messages before checking again |
| A field with only spaces passes as filled | `.trim()` missing before testing whether it is empty | Always `.trim()` text values before checking for empty |
| The form still reloads the page | `event.preventDefault()` missing (Module 09) | Add it as the first line of the `submit` function |

## // Guided practice

1. On the Login, add elements for the error message next to each field (a `<span>` or `<p>` with a unique `id`, if it does not exist yet).
2. Write the full validation, following the example in this section: required e-mail with "@", password with at least 8 characters.
3. Test: submit empty, submit with an e-mail without "@", submit with a short password, submit everything right. Confirm each case shows (or does not show) the expected error.
4. Confirm that fixing a field and resubmitting clears the previous error message.

## // Practice on your own

> **CHALLENGE**
> Add a second rule to the password field: it cannot be the same as the typed e-mail (a simple security check). Write the matching error message, and make sure it also follows the pattern of clearing old messages before validating again.

## // Applying it to the week's project

1. Implement the full validation of your project's Login form, with at least two rules per field (empty + format, or empty + minimum length).
2. Make sure the error messages are specific, not generic.
3. Commit: `git commit -m "Add form validation in JavaScript"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> Your validation uses `return` inside the first `if` that fails, instead of a `valido` variable. The person gets both the e-mail AND the password wrong, and submits the form. What do they see?

Answer: only the e-mail error message. Since `return` leaves the function as soon as the first condition fails, the password check never gets to run, even though it is also wrong. The person fixes the e-mail, resubmits, and only *then* finds out the password was wrong too. A frustrating "cascade" of errors. Using a `valido` variable (without an early `return`) lets you show all errors at once.

## // Module summary

- [ ] I know the six-step validation flow (capture → clean → empty → format → rule → feedback).
- [ ] I know why `.trim()` keeps blank spaces from passing as filled.
- [ ] I can write specific error messages, not generic ones.
- [ ] I know why using a `valido` variable (instead of an early `return`) lets me show all errors at once.
- [ ] My project's Login form already validates for real, with clear messages.

---

**Next module:** `11-json-and-mock-data.md`: before rendering a real list, how to represent and simulate that data without needing a backend yet.

`Study Material // Coffee & Code`
