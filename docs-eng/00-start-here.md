# Module 00, Start Here

[Português](../docs/00-comece-aqui.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // Welcome to Week 03

If you followed Week 02, you now have three pages (Login, Dashboard and Profile) that look good, are organized and responsive. Open the Dashboard now and click "Join" on any card. Nothing happens. Type anything (or nothing) into the Login form and click "Sign in". Nothing happens, and no error shows up if you left the field empty.

That is not a flaw in what you built, and it is exactly where Week 02 said it would stop. HTML and CSS handle structure and appearance. Neither handles *behavior*. That is what this week is about.

## // What changes from now on

<div align="center">
<img src="../docs/assets/mock-data-to-render.svg" alt="Array of objects, with .map(), turning into elements rendered on screen" width="480">
</div>

Until Week 02, the Dashboard HTML had the cards written by hand, one by one, right in the file. From this week on, the cards will be born from a list of data (an array), and the screen will update itself when that list changes. It is the difference between a fixed shop window and one that rearranges itself as the stock changes.

## // What you will build by the end of the week

- The Login form validating for real: empty field, badly formatted e-mail, short password, all blocked before any submission, with a visible error message.
- The Dashboard grid rendered entirely from an array of data (simulated, no backend yet): adding an item to the array should, on its own, add a card to the screen.
- A search that actually filters the displayed groups, without reloading the page.
- The Profile reflecting data from an object, with at least one action (such as leaving a group) updating the screen without a reload.

## // What is still left out

Even though you will write a lot of new logic, the scope stays deliberately contained:

> **NOT THIS WEEK YET**
> No real backend, no database, no real network call to a server of your own. The "outside" data stays simulated: an array written in the JavaScript itself, representing what will one day come from an API. The difference from Week 02 is that now there is *logic* processing that data, not that there is a new server.

## // Why JavaScript, and not something else

> **JAVASCRIPT: IN SIMPLE WORDS**
> It is the language that runs in the browser and lets a page react, read values, make decisions, repeat actions and change what is on the screen, without needing to reload.

Back to the model from Week 02's Module 01: HTML is structure, CSS is presentation, JavaScript is behavior. The first two pieces already exist on your three screens. This week builds exactly the third.

## // The two tracks

**If you are just starting**, you have never written a line of JavaScript. The main path of each module assumes this: each concept (variable, function, event) is introduced before it is needed, never after.

**If you already have experience**, you have programmed in JavaScript or another language before. Each module has deeper-dive blocks, clearly identified, after the essential content: state management and a simple pattern for organizing the interface into components, without using any framework yet.

Nobody works on a different project: everyone gives behavior to the same three screens of the Study Group Finder (*Buscador de Grupos de Estudo*), or to their own project. What changes is the depth.

## // Map of Week 03

| Module | Content | You will be able to |
|---|---|---|
| 01 | How JavaScript gets into the page | Connect a `.js` to the HTML correctly |
| 02 | Variables, types and operators | Store and compare values |
| 03 | Decisions and loops | Control what happens, and how many times |
| 04 | Functions and arrow functions | Organize logic into reusable blocks |
| 05 | Arrays and essential methods | Transform lists of data |
| 06 | Objects and destructuring | Model "one thing" with several properties |
| 07 | The DOM: selecting and reading | Find elements that already exist on the page |
| 08 | The DOM: creating and changing elements | Add and change content on the screen |
| 09 | Events | React to clicks, typing, form submission |
| 10 | Forms and validation in JS | Block invalid submissions, with clear messages |
| 11 | JSON and mock data | Simulate data from an API, without needing one |
| 12 | Rendering lists dynamically | Data array → cards on screen, automatically |
| 13 | State and componentization | Organize the interface as it grows |
| 14 | Guided project | Dynamic Login, Dashboard and Profile, from start to finish |

Each module is a standalone file, but they were written to be read in this order: a function only makes sense after you understand variables and decisions; rendering a list only makes sense after you already know how to select and create elements in the DOM.

---

**Next module:** `01-how-javascript-gets-into-the-page.md`: before writing the first line of logic, understand where and when it runs.

`Study Material // Coffee & Code`
