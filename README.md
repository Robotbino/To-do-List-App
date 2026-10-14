# 📋 Agile Board Task Management

A Kanban-style task manager in plain HTML, CSS and JavaScript. Tasks live on boards, every board
shows TODO, DOING and DONE columns, and everything you change is kept in the browser's
`localStorage`, so it survives a reload without a server.

It is a small front-end project, not a product. It shows what you can do with no framework and no
build step: ES modules for structure, one render path that redraws the columns from stored data, a
dark/light theme on CSS custom properties, and a layout that holds up from a phone to a wide
monitor. The whole app is five source files, and you can read it end to end in one sitting.

[![Vanilla JS](https://img.shields.io/badge/Vanilla%20JS-ES%20modules-F7DF1E)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)
[![HTML5](https://img.shields.io/badge/HTML5-static%20site-E34F26)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-custom%20properties-1572B6)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![localStorage](https://img.shields.io/badge/Storage-localStorage-4A4A4A)](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage)

> **Live demo:** _none_ (runs locally) · **Author:** [Robotbino](https://github.com/Robotbino)

---

## Contents

- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Installation & Setup](#installation--setup)
- [Usage Guide](#usage-guide)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [Future Enhancements](#future-enhancements)
- [Known Limitations](#known-limitations)
- [Acknowledgments](#acknowledgments)
- [Related](#related)

---

## Key Features

### Boards

- **Boards come from the tasks.** The sidebar lists every distinct `board` value found in the saved
  tasks (`fetchAndDisplayBoardsAndTasks()` in `index.js`), so a board exists for as long as at least
  one task is on it.
- **Switch boards** by clicking a name in the sidebar. The active board is highlighted, shown in the
  header, and remembered in `localStorage`, so a reload opens the board you were on.
- **Delete a board** from the **⋮** menu at the right end of the header, next to **+ Add Task**. A
  browser `confirm()` dialog asks first; then the board and every task on it are removed and the
  first remaining board becomes active.
- **No create-board control.** New tasks always land on the board you are looking at. Creating boards
  from the UI is listed under [Future Enhancements](#future-enhancements).

### Tasks

- **Add a task** with **+ Add Task** in the header: a title, a description and a status of `todo`,
  `doing` or `done`. **Create Task** saves it to the active board and the columns redraw.
- **Three columns, built from status.** TODO, DOING and DONE are the three `.column-div` elements in
  `index.html`. Each render clears them and refills them with the active board's tasks grouped by
  `status`; the heading text and the coloured dot come from the column's `data-status` attribute.
- **Edit a task** by clicking its card. The edit modal shows the title, description and status;
  **Save Changes** writes the update through `patchTask()` and redraws.
- **Move a task** by changing the status dropdown in the edit modal. The task appears in its new
  column on the next render. There is no drag-and-drop.
- **Delete a task** with **Delete Task** in the edit modal. It is removed at once, with no confirmation.
- **Close a modal** with its Cancel button or by clicking the dimmed overlay behind it.
- Cards show the title only; the description is visible in the edit modal.

### Theme, sidebar and persistence

- **Dark by default, light on request.** The switch at the bottom of the sidebar (between a moon and
  a sun icon) toggles a `light-theme` class on `<body>`. `index.css` defines both palettes as custom
  properties, in `:root` for dark and `.light-theme` for light.
- **Hide Sidebar** collapses the sidebar and shows a **☰** button in the bottom-left corner to bring
  it back.
- **Everything is remembered.** Four `localStorage` keys hold the whole state: the tasks, the active
  board, whether the sidebar is open, and the theme. The keys are listed under
  [How It Works](#how-it-works).
- **Sample data on first run.** If there are no saved tasks, `initialData.js` seeds 13 tasks across
  two boards, **Launch Career** (6 tasks) and **Roadmap** (7).

### Responsive layout

- Five media queries in `index.css`, with breakpoints at 480, 800, 1024 and 2560 px. At 480 px and
  below the three columns stack vertically and **+ Add Task** becomes a round **+** button. At 800 px
  and below the sidebar turns into a floating board picker, opened from the chevron beside the board
  name. From 1025 px the sidebar is a 300 px-wide rail; at 2560 px and up it widens to 350 px and
  the header and card type get larger.

---

## Tech Stack

| Layer | Choice |
|---|---|
| Markup | One HTML page, `index.html`: sidebar, header, three status columns, two modal forms and an overlay |
| Logic | Vanilla JavaScript (ES2015+), loaded as ES modules with `<script type="module">`. No framework, no bundler, no transpiler |
| Styling | One stylesheet, `index.css`: design tokens as CSS custom properties (`:root` for dark, `.light-theme` for light), flexbox layout, five media queries |
| Storage | The browser's `localStorage` API, wrapped by `utils/taskFunctions.js` |
| Fonts | Atkinson Hyperlegible (body) and Inter (banner) from Google Fonts |
| Icons | Inline SVGs from Font Awesome Free 7.1.0 for the theme switch and the Hide Sidebar icon; two files from `assets/` (the favicon and the header chevron) |
| Tooling | `.vscode/settings.json` pins the Live Server extension to port 5501. There is no `package.json`, no dependencies, no build and no test runner |

---

## Installation & Setup

### Prerequisites

- A modern browser (Chrome, Edge, Firefox or Safari).
- Something to serve static files. [VS Code](https://code.visualstudio.com/) with the
  [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension
  is the setup the repo is configured for; any static server works.

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/Robotbino/To-do-List-App.git
   cd To-do-List-App
   ```

2. **Serve the folder**
   - **VS Code + Live Server:** run `code .`, right-click `index.html` and choose
     **Open with Live Server** (or click **Go Live** in the status bar). The repo's
     `.vscode/settings.json` sets the port to **5501**.
   - **Any other static server:** for example `npx serve .` or `python -m http.server 8000`, then
     open the printed URL.

   `index.js` is loaded as an ES module, so serve the folder over HTTP rather than opening
   `index.html` straight from disk. Chrome and Edge refuse to load module scripts from `file://` URLs.

3. **Start managing tasks.** There is no install step, no configuration and no account. The app
   seeds its sample data on first load. To start from a clean slate, clear the site's
   `localStorage` (DevTools → Application → Local Storage, or `localStorage.clear()` in the console)
   and reload.

---

## Usage Guide

### Managing Boards

- **Switch boards:** click a board name in the sidebar. The active board is highlighted and its name
  shows in the header.
- **Delete a board:** click **⋮** at the right end of the header (next to **+ Add Task**), then
  **Delete Board**, and confirm. Every task on that board goes with it.
- **Create a board:** not available in the UI yet. See [Known Limitations](#known-limitations).

### Working with Tasks

1. **Create a task:** click **+ Add Task**, fill in the title, description and status, then click
   **Create Task**. The task is added to the board you are viewing.
2. **Edit a task:** click a card to open the edit modal, change the title, description or status,
   then click **Save Changes**.
3. **Move a task:** open it, change the status dropdown, save. The card moves to the matching column.
4. **Delete a task:** open it and click **Delete Task**. It is removed immediately.
5. **Cancel:** click **Cancel** in either modal, or click the dimmed background.

### Customisation

- **Theme:** use the switch at the bottom of the sidebar. The choice is kept across reloads.
- **Sidebar:** click **Hide Sidebar** to use the full width; click **☰** to bring it back. On screens
  800 px and narrower, the chevron beside the board name opens the sidebar as a board picker.

---

## Project Structure

```
To-do-List-App/
├── index.html              # The page: sidebar, header, TODO/DOING/DONE columns, two modals, overlay
├── index.css               # All styling: dark and light tokens, layout, modals, five media queries
├── index.js                # Entry module: DOM lookups, rendering, event listeners, theme and sidebar
├── initialData.js          # 13 sample tasks on the "Launch Career" and "Roadmap" boards
├── utils/
│   └── taskFunctions.js    # localStorage CRUD: getTasks, createNewTask, patchTask, putTask, deleteTask
├── assets/                 # 14 SVGs; index.html uses favicon-32x32.svg and icon-chevron-down.svg
├── .vscode/
│   └── settings.json       # Live Server port 5501
└── README.md
```

---

## How It Works

Three ES modules, one page, one storage key for the data.

- **`index.html`** is a static shell. The three columns are `.column-div` elements with
  `data-status="todo" | "doing" | "done"`. The two modals (`#new-task-modal-window` and
  `.edit-task-modal-window`) and the `#filterDiv` overlay are in the page from the start and are
  shown or hidden by setting `display`.
- **`index.js`** is the entry point (`<script type="module">`). On `DOMContentLoaded` it runs
  `init()`: seed `localStorage` if it is empty, wire up the event listeners, restore the sidebar and
  theme, then render. Rendering is one path. `fetchAndDisplayBoardsAndTasks()` reads all tasks,
  derives the board list, picks the active board and calls `filterAndDisplayTasksByBoard()`, which
  rebuilds each column's `innerHTML` from the tasks whose `board` and `status` match. Every change
  (create, edit, delete, delete board, switch board) writes to `localStorage` and then redraws; the
  one in-place insert, `addTaskToUI()`, is overwritten by the redraw that follows it.
- **`utils/taskFunctions.js`** wraps the `tasks` key. `getTasks()` parses it, `saveTasks()`
  serialises it, and `createNewTask()`, `patchTask()` and `deleteTask()` are read-modify-write
  wrappers around those two. `index.js` touches the key directly in two places only: the first-run
  seed and Delete Board. A new task's `id` is the current timestamp (`new Date().getTime()`).
  `putTask()` is exported but not used.
- **`initialData.js`** exports the seed array that `initializeData()` writes on first run.

A task is a flat object:

```json
{
  "id": 1,
  "title": "Launch Epic Career 🚀",
  "description": "Create a killer Resume",
  "status": "todo",
  "board": "Launch Career"
}
```

Everything the app remembers lives under four `localStorage` keys:

| Key | Value | Written by |
|---|---|---|
| `tasks` | JSON array of task objects | `taskFunctions.js`, the first-run seed, and Delete Board |
| `activeBoard` | The board name as a JSON string | Clicking a board. Removed when a board is deleted |
| `showSideBar` | `"true"` or `"false"` | `toggleSidebar()`; set to `"true"` on first run |
| `light-theme` | `"enabled"` or `"disabled"` | `toggleTheme()` |

---

## Future Enhancements

- [ ] Create a new board from the UI (a `#create-board-btn` rule already exists in `index.css`; the button does not)
- [ ] Drag-and-drop to move tasks between columns and reorder them
- [ ] Task due dates and reminders
- [ ] Task priority levels and colour coding
- [ ] Search and filter
- [ ] Export/import tasks (JSON, CSV)
- [ ] Backend integration with a REST API
- [ ] User authentication and cloud sync
- [ ] Task comments and collaboration features

---

## Known Limitations

- **No way to create a board.** Boards exist only while they have tasks: delete a board's last task
  and the board drops out of the sidebar on the next reload (the board list is rebuilt only at
  start-up and after Delete Board), although the header and the saved `activeBoard` still name it
  until you pick another board. Once every board is deleted the app stays empty: **+ Add Task**
  saves tasks with an empty board name, which show until the next reload and then never again,
  because the board list ignores empty names and the seed does not run again while the `tasks` key
  exists. Recovery is `localStorage.removeItem('tasks')` and a reload.
- **No drag-and-drop.** Tasks move by changing the status dropdown in the edit modal.
- **No validation.** A task with an empty title can be created and shows as a blank card. Deleting a
  task asks for no confirmation.
- **Tasks cannot move between boards.** Saving an edit sets the task's `board` to the active board.
- **The mobile board picker has no close control.** At 800 px and below the sidebar is a floating
  panel; the Hide Sidebar row is hidden at that width, and picking a board does not close the panel.
- **Data stays in one browser.** `localStorage` only; no export and no sync.
- **No tests, no linter, no build step, no live demo.**
- **Starter-code leftovers.** `index.js` still carries the scaffold's `// TASK:` and `FIX BUGS!!!`
  comments and five `console.log` calls. Some dead code remains: `putTask()` (unused, and it calls
  `location.reload()`), `elements.logo` and `elements.buttons` (there is no `#logo` element, and
  neither is read), `addTaskToUI()` (its output is redrawn immediately by `refreshTasksUI()`), a
  `#create-board-btn` CSS rule with no element, 12 of the 14 SVGs in `assets/`, and a Google Fonts
  `@import` in the `<style>` block of `index.html` for Comic Neue and IBM Plex Sans, two fonts
  `index.css` never uses.

---

## Acknowledgments

- The theme-switch and Hide Sidebar icons are inline SVGs from
  [Font Awesome Free 7.1.0](https://fontawesome.com/license/free).
- Atkinson Hyperlegible and Inter are served from Google Fonts.

---

## Related

- [github.com/Robotbino](https://github.com/Robotbino): more projects, including the full-stack
  [GameStore](https://github.com/Robotbino/gameStore).

---

**⭐ If you found this project helpful, consider giving it a star.**
