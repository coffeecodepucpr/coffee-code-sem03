# Module 14, Guided Project: Dynamic Login, Dashboard and Profile

[Português](../docs/14-projeto-guiado.md) · English

`WEEK 03 // Web Interface, Part 2: Interactivity`

---

## // What this module is for

No new concept shows up here. This module brings together, in order, everything Modules 01 to 13 taught separately, showing how the project's three screens gain behavior, from start to finish, in a single workflow.

## // Step 1, Connect the JavaScript (Module 01)

Confirm that the three pages (`login.html`, `dashboard.html`, `perfil.html`) have `<script src="script.js" defer></script>` in the `<head>`. If your project organizes scripts per page, it can be one file per screen (`login.js`, `dashboard.js`, `perfil.js`); the reasoning is identical.

## // Step 2, Structure the mock data (Modules 05, 06, 11)

```javascript
let gruposMock = [
  { id: 1, materia: "Cálculo I", participantes: 5, horario: "Tuesdays at 6 PM" },
  { id: 2, materia: "Estrutura de Dados", participantes: 3, horario: "Thursdays at 7 PM" },
  { id: 3, materia: "Banco de Dados", participantes: 8, horario: "Saturdays at 10 AM" },
  { id: 4, materia: "Engenharia de Software", participantes: 4, horario: "Mondays at 5 PM" },
];

const usuarioMock = {
  nome: "Ana Martins",
  email: "ana.martins@exemplo.com",
  materias: [1, 2],
};
```

## // Step 3, Login: full validation (Modules 09, 10)

Connect the form, prevent the reload, validate e-mail and password, show specific errors (clearing old messages on each new attempt), following exactly the example from Module 10.

```javascript
const formLogin = document.querySelector("#form-login");

if (formLogin) {
  formLogin.addEventListener("submit", function (event) {
    event.preventDefault();
    // full validation, as in Module 10
    console.log("Login validated: the redirect would go here");
  });
}
```

> **WHY THE `IF (FORMLOGIN)`**
> Since the same `script.js` may be connected to the three pages, `#form-login` only really exists on the Login page. Testing `if (formLogin)` before adding the listener avoids an error on the other two pages, where that element does not exist (Module 07).

## // Step 4, Dashboard: rendering and search (Modules 07, 08, 12)

```javascript
const containerGrid = document.querySelector(".dashboard-grid");

function criarCardHTML(grupo) {
  return `
    <article class="card">
      <h3>${grupo.materia}</h3>
      <p>${grupo.participantes} participants · ${grupo.horario}</p>
      <button class="botao botao-primario" data-id="${grupo.id}">Join</button>
    </article>
  `;
}

function renderizarGrupos(lista) {
  if (!containerGrid) return;
  containerGrid.innerHTML = lista.map(criarCardHTML).join("");
}

const campoBusca = document.querySelector(".busca");
if (campoBusca) {
  campoBusca.addEventListener("input", function (event) {
    const termo = event.target.value.toLowerCase();
    const filtrados = gruposMock.filter((g) => g.materia.toLowerCase().includes(termo));
    renderizarGrupos(filtrados);
  });
}

renderizarGrupos(gruposMock);
```

## // Step 5, Profile: user data and the leave-group action (Modules 06, 13)

```javascript
const nomeElemento = document.querySelector(".perfil-info h2");
const emailElemento = document.querySelector(".perfil-info p");

if (nomeElemento && emailElemento) {
  nomeElemento.textContent = usuarioMock.nome;
  emailElemento.textContent = usuarioMock.email;
}

function removerGrupo(id) {
  gruposMock = gruposMock.filter((g) => g.id !== id);
  renderizarMeusGrupos();
}

function renderizarMeusGrupos() {
  const container = document.querySelector(".dashboard-grid");
  if (!container) return;
  const meusGrupos = gruposMock.filter((g) => usuarioMock.materias.includes(g.id));
  container.innerHTML = meusGrupos.map(function (grupo) {
    return `
      <article class="card">
        <h3>${grupo.materia}</h3>
        <p>${grupo.participantes} participants</p>
        <button class="botao botao-secundario" data-id="${grupo.id}">Leave group</button>
      </article>
    `;
  }).join("");
}
```

## // Step 6, Connecting clicks to the rendered buttons (Module 09)

Buttons created via `innerHTML` (Steps 4 and 5) did not exist at the moment a direct `addEventListener` would be added to each of them: they only start existing after rendering. The simplest way to solve this, with what you already know, is to add the listener to the **container** (which exists from the start), and check, inside the callback, whether the click really happened on a button:

```javascript
if (containerGrid) {
  containerGrid.addEventListener("click", function (event) {
    if (event.target.matches(".botao-secundario")) {
      const id = Number(event.target.dataset.id);
      removerGrupo(id);
    }
  });
}
```

`event.target.dataset.id` reads the `data-id` attribute you already included in `criarCardHTML`: that is how the click knows *which* group to remove, even though the button was created dynamically.

## // Wrap-up checklist for the three screens

- [ ] Login really validates, with specific messages per field, without reloading the page.
- [ ] The Dashboard renders the cards from `gruposMock`, not from fixed HTML.
- [ ] The Dashboard search filters in real time, without a reload.
- [ ] The Profile shows data from `usuarioMock`, not fixed text.
- [ ] At least one action (leaving a group) follows the state → render cycle (Module 13), without changing the DOM directly.
- [ ] None of the three pages throws an error in the console when loading.

## // Common mistakes when putting it all together

| Mistake | Why it happens | How to fix it |
|---|---|---|
| A console error on pages where an element does not exist | The same `script.js` runs on the three pages, but not every element exists on all of them | Always test `if (elemento)` before using it, especially screen-specific forms and containers |
| Clicking a dynamically rendered button does nothing | `addEventListener` was put directly on the button, before it existed | Put the listener on the container (which already existed), and check `event.target` inside the callback |
| Data and screen out of sync after an action | Changing the DOM directly instead of going through the state | Review Module 13: every action should end in updating the state and calling the rendering again |

## // Applying it to the week's project

This is the application: there is no separate activity. By the end of this module, the three screens should pass the Module 15 checklist.

Final commit for this step: `git commit -m "Finish the dynamic behavior of the three screens"`.

## // Checkpoint

> **BEFORE MOVING ON, THINK ABOUT THIS**
> If you had to explain to someone, in three sentences, why the order connected JavaScript → structured data → DOM and events → validation → rendering made sense, what would you say?

Possible answer: without the script connected (Module 01), no logic runs. Without structured data (Modules 05, 06, 11), there is nothing to validate or render. And only after knowing how to select/change the DOM and listen to events (Modules 07 to 09) do validation (Module 10) and dynamic rendering (Modules 12, 13) make sense. Each of these last two steps is, in practice, a combination of the previous ones applied to a specific goal.

## // Module summary

- [ ] I can repeat, from memory, the sequence of steps used to give a screen behavior from scratch.
- [ ] My project's three screens (Login, Dashboard, Profile) went through all six steps.
- [ ] The wrap-up checklist for the three screens is complete.

---

**Next module:** `15`: before considering the week done, a final review against the deliverable's real criteria (see `deliverable.md`).

`Study Material // Coffee & Code`
