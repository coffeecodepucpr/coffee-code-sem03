# Deliverable, Week 03

[Português](../docs/entregavel.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

Use this file as the final checklist before considering Week 03 done. It gathers what is **required**; the extra challenges in `challenges.md` are optional.

## // What you should have in hand now

If you followed the modules in order, your repository should now have, in addition to everything from Weeks 01 and 02: a `script.js` (or one per screen) connected to the three pages, data structured as mock, a Login form that really validates, a Dashboard that renders and filters dynamically, and a Profile reflecting real data with at least one working action.

## // Deliverable checklist

### > Basic JavaScript

- [ ] `script.js` connected to the three pages with `defer`, with no console error when loading any of them.
- [ ] No comparison uses `==`, only `===`.
- [ ] All repeated logic is organized in named functions, not duplicated.

### > DOM and events

- [ ] Elements selected with `querySelector`/`querySelectorAll`, never assuming they exist without checking.
- [ ] At least three real interactions use `addEventListener` (form, search, an action button).
- [ ] The Login form uses `event.preventDefault()`.

### > Validation

- [ ] Login validates e-mail (required + format) and password (required + minimum length).
- [ ] Error messages are specific, appear next to the matching field, and are cleared on each new attempt.
- [ ] No field with only blank spaces passes as filled (`.trim()` applied).

### > Data and rendering

- [ ] The Dashboard data (and the Profile's, if applicable) is structured as an array of objects, named as mock, with a unique `id` per item.
- [ ] The Dashboard grid is generated entirely by `.map()` + `innerHTML` (or equivalent), not by fixed HTML.
- [ ] The Dashboard search filters in real time, without reloading the page.

### > State and componentization

- [ ] At least one action (remove, add) follows the state → render cycle, never changing the DOM directly without first updating the state.
- [ ] At least one component function (such as `criarCardHTML`) is reused in more than one place, or is ready to be.

## // What is NOT expected this week

- No backend, database or real network call to a server of your own is expected.
- No framework (React or equivalent) is expected: everything in plain JavaScript, on purpose.
- Sophisticated error handling for network failures is not expected (there is no real network yet).
- Persistence between page reloads is not expected: the mock data resets every time the page is opened, and that is expected.

> **CORRECT LOGIC IS WORTH MORE THAN VISUAL POLISH**
> A validation that correctly blocks a badly formatted e-mail, even with a simple error message, is worth more in this evaluation than a beautiful interface that accepts anything in the form. Correct behavior is what is being evaluated this week.

## // How to review before submitting

> **THE MOST IMPORTANT TEST THIS WEEK**
> Open the browser console (F12) on the three screens, without doing anything yet. Does any red error appear just from loading the page? Then use each screen normally: wrong login, right login, search, leaving a group. Does any error appear during use?

If the answer is "no errors" in both cases, your submission is on the right track. If any error appears, it almost always points to the exact file and line. Go back to the corresponding module.

## // Where to ask questions

Coffee & Code's weekly meetings exist for exactly this. "My dynamically rendered button doesn't respond to clicks, I already tried X and Y" is much faster to solve than "my JavaScript doesn't work".

If you want to go beyond what was asked, see `challenges.md`.

## // What comes in Week 04

Week 03 ends with an interface that reacts, validates and renders, but entirely with data that lives only in the code itself and disappears on every page reload. That gap (persistence, and then communication with a real server) is exactly what the club's next weeks start to fill.

Good work so far.

`Study Material // Coffee & Code`
