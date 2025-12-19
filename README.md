# 📋 Agile Board Task Management

A modern, responsive task management application built with vanilla JavaScript, featuring Kanban-style boards, local storage persistence, and a sleek dark/light theme toggle.


---

## Key Features

- **Multi-Board Organization**: Create and manage tasks across different project boards
- **Kanban Workflow**: Organize tasks into TODO, DOING, and DONE columns
- **Task Management**: Create, edit, update, and delete tasks with detailed descriptions
- **Theme Customization**: Toggle between light and dark themes with persistent preferences
- **Responsive Design**: Fully responsive layout that works seamlessly on desktop and mobile
- **Local Storage**: Data persistence using browser's localStorage API
- **Collapsible Sidebar**: Maximize workspace with a toggleable navigation sidebar
- **Real-time Updates**: Instant UI updates reflecting all task changes

---

## 🛠️ Tech Stack

- **Frontend**: HTML5, CSS3, Vanilla JavaScript (ES6+)
- **Storage**: LocalStorage API
- **Module System**: ES6 Modules
- **Design**: Custom CSS with Google Fonts (IBM Plex Sans, Comic Neue)
- **Icons**: SVG assets for scalable UI elements

---

## 📦 Installation & Setup

### Prerequisites

- A modern web browser (Chrome, Firefox, Safari, or Edge)
- [VS Code](https://code.visualstudio.com/) with [Live Server extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) (recommended)

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/Robotbino/To-do-List-App.git
   cd To-do-List-App
   ```

2. **Open in VS Code**
   ```bash
   code .
   ```

3. **Launch with Live Server**
   - Right-click on `index.html`
   - Select "Open with Live Server"
   - The app will automatically open in your default browser

   **Alternative**: If you don't have Live Server installed:
   - Install it from VS Code Extensions (search for "Live Server" by Ritwick Dey)
   - Or click the "Go Live" button in the VS Code status bar

4. **Start managing tasks!**
   - The app comes pre-loaded with sample data to help you get started

---

## 🎯 Usage Guide

### Managing Boards

- **Switch Boards**: Click on any board name in the sidebar to view its tasks
- **Active Board**: The currently selected board is highlighted in the sidebar

### Working with Tasks

1. **Create a Task**
   - Click the "+ Add New Task" button
   - Fill in the title, description, and select a status
   - Click "Create Task" to add it to your board

2. **Edit a Task**
   - Click on any task card to open the edit modal
   - Modify the title, description, or status
   - Click "Save Changes" to update

3. **Delete a Task**
   - Open the task in edit mode
   - Click the "Delete Task" button
   - The task will be removed immediately

4. **Move Tasks**
   - Edit the task and change its status dropdown
   - The task will automatically move to the corresponding column

### Customization

- **Theme Toggle**: Use the sun/moon switch in the sidebar to toggle between light and dark themes
- **Sidebar**: Click "Hide Sidebar" to maximize workspace, click the show button to restore

---

## 📁 Project Structure

```
to-do-list-app/
│
├── index.html              # Main HTML structure
├── index.css               # Styling and theme definitions
├── index.js                # Main application logic and event handlers
├── initialData.js          # Sample data for initial app state
│
├── utils/
│   └── taskFunctions.js    # CRUD operations for task management
│
└── assets/                 # Icons and images
    ├── logo-dark.svg
    ├── logo-light.svg
    └── [other icons]
```

---

## 🔧 Core Functionality

### Data Management

The application uses a modular approach with utility functions:

```javascript
// From utils/taskFunctions.js
getTasks()              // Retrieve all tasks from localStorage
createNewTask(task)     // Add a new task
patchTask(id, updates)  // Update an existing task
deleteTask(id)          // Remove a task
```

### State Persistence

- All tasks are stored in localStorage as JSON
- Theme preferences and sidebar state are persisted
- Active board selection is remembered across sessions

---

## 🚧 Future Enhancements

- [ ] Drag-and-drop task reordering
- [ ] Task due dates and reminders
- [ ] Task priority levels and color coding
- [ ] Search and filter functionality
- [ ] Export/import tasks (JSON, CSV)
- [ ] Backend integration with REST API
- [ ] User authentication and cloud sync
- [ ] Task comments and collaboration features

---

## 🙏 Acknowledgments

- Design inspiration from modern project management tools
- Icons and assets from various open-source projects
- Font families from Google Fonts

---

## 📸 Screenshots

<!-- Add screenshots of your application here -->

### Dark Theme
![Dark Theme](./screenshots/dark-theme.png)

### Light Theme
![Light Theme](./screenshots/light-theme.png)

### Mobile View
![Mobile View](./screenshots/mobile-view.png)

---

**⭐ If you found this project helpful, please consider giving it a star!**
