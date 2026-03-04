<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>DuoTask</title>
    <style>
        :root {
            /* Duolingo Inspired Palette */
            --duo-green: #58CC02;
            --duo-green-shadow: #46A302;
            --duo-blue: #1CB0F6;
            --duo-blue-shadow: #1899D6;
            --duo-red: #FF4B4B;
            --duo-red-shadow: #D43F3F;
            --duo-yellow: #FFC800;
            --duo-bg: #FFFFFF;
            --duo-gray: #E5E5E5;
            --duo-text: #4B4B4B;
            --duo-text-light: #AFB2B7;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--duo-bg);
            color: var(--duo-text);
            height: 100vh;
            display: flex;
            justify-content: center;
        }

        .app-container {
            width: 100%;
            max-width: 480px;
            background-color: var(--duo-bg);
            display: flex;
            flex-direction: column;
            height: 100%;
            position: relative;
            overflow: hidden;
        }

        /* HEADER & STATS */
        header {
            padding: 16px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid var(--duo-gray);
        }

        .stats-container {
            display: flex;
            gap: 15px;
        }

        .stat-badge {
            display: flex;
            align-items: center;
            gap: 6px;
            font-weight: 800;
            color: var(--duo-yellow);
            font-size: 18px;
        }

        .fire-icon { color: #FF9600; }

        /* PROGRESS BAR */
        .progress-section {
            padding: 20px 20px 10px 20px;
        }

        .progress-track {
            height: 16px;
            background-color: var(--duo-gray);
            border-radius: 10px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background-color: var(--duo-yellow);
            width: 0%;
            transition: width 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
        }

        .section-title {
            font-size: 20px;
            font-weight: 800;
            margin: 20px 20px 10px 20px;
            color: var(--duo-text);
        }

        /* CONTENT SCROLL */
        .content {
            flex: 1;
            overflow-y: auto;
            padding-bottom: 30px;
        }

        /* INPUT AREA */
        .input-group {
            margin: 0 20px;
            display: flex;
            gap: 10px;
        }

        input[type="text"] {
            flex: 1;
            padding: 14px;
            border: 2px solid var(--duo-gray);
            border-radius: 12px;
            font-size: 17px;
            font-weight: 600;
            color: var(--duo-text);
            background: #F7F7F7;
            outline: none;
        }

        input[type="text"]:focus {
            border-color: var(--duo-blue);
            background: #FFF;
        }

        /* 3D BUTTONS */
        .btn-3d {
            border: none;
            border-radius: 12px;
            font-weight: 800;
            font-size: 15px;
            color: white;
            padding: 0 20px;
            cursor: pointer;
            transition: transform 0.1s;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .btn-primary {
            background-color: var(--duo-green);
            box-shadow: 0px 4px 0px var(--duo-green-shadow);
        }
        .btn-primary:active {
            transform: translateY(4px);
            box-shadow: none;
        }

        .btn-blue {
            background-color: var(--duo-blue);
            box-shadow: 0px 4px 0px var(--duo-blue-shadow);
        }
        .btn-blue:active {
            transform: translateY(4px);
            box-shadow: none;
        }

        /* TODO LIST ITEMS */
        .todo-list {
            list-style: none;
            padding: 10px 20px;
        }

        .todo-card {
            background: #FFF;
            border: 2px solid var(--duo-gray);
            border-radius: 16px;
            padding: 16px;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transition: all 0.2s;
        }

        .todo-card.completed {
            background-color: #F7F7F7;
            border-color: transparent;
        }

        .check-container {
            display: flex;
            align-items: center;
            gap: 12px;
            flex: 1;
            cursor: pointer;
        }

        .custom-checkbox {
            width: 32px;
            height: 32px;
            border: 2px solid var(--duo-gray);
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            color: white;
            transition: all 0.2s;
            background: white;
        }

        .todo-card.completed .custom-checkbox {
            background-color: var(--duo-green);
            border-color: var(--duo-green);
        }

        .todo-text {
            font-size: 17px;
            font-weight: 600;
            color: var(--duo-text);
        }

        .todo-card.completed .todo-text {
            color: var(--duo-text-light);
            text-decoration: line-through;
        }

        .btn-delete {
            background: none;
            border: none;
            color: var(--duo-gray);
            font-size: 24px;
            font-weight: 700;
            padding: 0 10px;
            cursor: pointer;
        }
        .btn-delete:hover { color: var(--duo-red); }

        /* NOTES AREA */
        .note-card {
            margin: 0 20px 20px 20px;
            border: 2px solid var(--duo-gray);
            border-radius: 16px;
            padding: 16px;
            background: #F7F7F7;
        }

        textarea {
            width: 100%;
            height: 120px;
            border: none;
            background: transparent;
            font-size: 16px;
            font-weight: 500;
            color: var(--duo-text);
            resize: none;
            outline: none;
        }

        .note-actions {
            display: flex;
            justify-content: flex-end;
            margin-top: 10px;
        }

        /* CONFETTI ANIMATION */
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #f00;
            animation: fall 2s linear forwards;
            pointer-events: none;
            z-index: 99;
        }

        @keyframes fall {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(100vh) rotate(720deg); opacity: 0; }
        }

    </style>
</head>
<body>

<div class="app-container">
    <header>
        <div style="font-weight: 800; font-size: 22px; color: var(--duo-green);">DuoTask</div>
        <div class="stats-container">
            <div class="stat-badge">
                <span class="fire-icon">🔥</span> <span id="streakCount">0</span>
            </div>
            <div class="stat-badge">
                💎 <span id="xpCount">0</span>
            </div>
        </div>
    </header>

    <div class="progress-section">
        <div style="display:flex; justify-content:space-between; margin-bottom:5px; font-weight:700; color:var(--duo-yellow); font-size:12px; text-transform:uppercase;">
            <span>Daily Progress</span>
            <span id="progressText">0%</span>
        </div>
        <div class="progress-track">
            <div class="progress-fill" id="progressBar"></div>
        </div>
    </div>

    <div class="content">
        <div class="section-title">TASKS</div>
        <div class="input-group">
            <input type="text" id="newTodo" placeholder="Add a new task..." onkeypress="handleEnter(event)">
            <button class="btn-3d btn-primary" onclick="addTodo()">ADD</button>
        </div>

        <ul class="todo-list" id="todoList">
            <!-- Items injected via JS -->
        </ul>

        <div class="section-title">SCRATCHPAD</div>
        <div class="note-card">
            <textarea id="noteArea" placeholder="Type quick notes here..."></textarea>
            <div class="note-actions">
                <button class="btn-3d btn-blue" onclick="saveNote()">SAVE</button>
            </div>
        </div>
    </div>
</div>

<script>
    // --- Initial Data ---
    const defaultTodos = [
        { id: 1, text: "Practice Spanish", completed: false },
        { id: 2, text: "Drink water", completed: true },
        { id: 3, text: "Read 10 pages", completed: false }
    ];
    const defaultNote = "DuoTask is ready! \nDon't forget to keep your streak alive.";

    // --- State ---
    let todos = JSON.parse(localStorage.getItem('duo_todos')) || defaultTodos;
    let note = localStorage.getItem('duo_note');
    let xp = parseInt(localStorage.getItem('duo_xp')) || 120;
    let streak = parseInt(localStorage.getItem('duo_streak')) || 3;

    if (note === null) note = defaultNote;

    // --- DOM Elements ---
    const listEl = document.getElementById('todoList');
    const noteEl = document.getElementById('noteArea');
    const xpEl = document.getElementById('xpCount');
    const streakEl = document.getElementById('streakCount');
    const progressEl = document.getElementById('progressBar');
    const progressTextEl = document.getElementById('progressText');

    // --- Init ---
    function init() {
        renderTodos();
        noteEl.value = note;
        updateStats();
    }

    // --- Core Functions ---
    function renderTodos() {
        listEl.innerHTML = '';
        let completedCount = 0;

        todos.forEach(todo => {
            if (todo.completed) completedCount++;

            const li = document.createElement('li');
            li.className = `todo-card ${todo.completed ? 'completed' : ''}`;
            li.innerHTML = `
                <div class="check-container" onclick="toggleTodo(${todo.id}, this)">
                    <div class="custom-checkbox">
                        ${todo.completed ? '✓' : ''}
                    </div>
                    <span class="todo-text">${escapeHtml(todo.text)}</span>
                </div>
                <button class="btn-delete" onclick="deleteTodo(${todo.id})">×</button>
            `;
            listEl.appendChild(li);
        });

        // Update Progress Bar
        const percent = todos.length > 0 ? Math.round((completedCount / todos.length) * 100) : 0;
        progressEl.style.width = percent + '%';
        progressTextEl.innerText = percent + '%';
    }

    function updateStats() {
        xpEl.innerText = xp;
        streakEl.innerText = streak;
    }

    function addTodo() {
        const input = document.getElementById('newTodo');
        const text = input.value.trim();
        if(!text) return;

        todos.unshift({ id: Date.now(), text: text, completed: false });
        input.value = '';
        saveAndRender();
    }

    function toggleTodo(id, element) {
        let isCompleting = false;

        todos = todos.map(t => {
            if (t.id === id) {
                if (!t.completed) isCompleting = true;
                return { ...t, completed: !t.completed };
            }
            return t;
        });

        if (isCompleting) {
            xp += 10;
            triggerConfetti(element);
            saveXP();
        } else {
            xp = Math.max(0, xp - 10);
            saveXP();
        }

        saveAndRender();
        updateStats();
    }

    function deleteTodo(id) {
        todos = todos.filter(t => t.id !== id);
        saveAndRender();
    }

    function saveNote() {
        localStorage.setItem('duo_note', noteEl.value);
        // Visual feedback on button
        const btn = document.querySelector('.btn-blue');
        const originalText = btn.innerText;
        btn.innerText = "SAVED!";
        setTimeout(() => btn.innerText = originalText, 1500);
    }

    function saveAndRender() {
        localStorage.setItem('duo_todos', JSON.stringify(todos));
        renderTodos();
    }

    function saveXP() {
        localStorage.setItem('duo_xp', xp);
    }

    function handleEnter(e) {
        if(e.key === 'Enter') addTodo();
    }

    function escapeHtml(text) {
        return text.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    }

    // --- Simple Confetti Effect ---
    function triggerConfetti(element) {
        const colors = ['#58CC02', '#1CB0F6', '#FFC800', '#FF4B4B'];
        const rect = element.getBoundingClientRect();
        const centerX = rect.left + rect.width / 2;
        const centerY = rect.top + rect.height / 2;

        for (let i = 0; i < 20; i++) {
            const confetti = document.createElement('div');
            confetti.className = 'confetti';
            confetti.style.left = centerX + 'px';
            confetti.style.top = centerY + 'px';
            confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];

            // Random direction
            const angle = Math.random() * Math.PI * 2;
            const velocity = 5 + Math.random() * 5;
            const tx = Math.cos(angle) * 100 * (Math.random() + 0.5);
            const ty = Math.sin(angle) * 100 * (Math.random() + 0.5);

            confetti.animate([
                { transform: `translate(0,0) scale(1)`, opacity: 1 },
                { transform: `translate(${tx}px, ${ty}px) scale(0.5) rotate(180deg)`, opacity: 0 }
            ], {
                duration: 800,
                easing: 'ease-out',
                fill: 'forwards'
            });

            document.body.appendChild(confetti);
            setTimeout(() => confetti.remove(), 800);
        }
    }

    init();
</script>

</body>
</html># Projet1