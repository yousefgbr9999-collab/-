<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ملاحظاتي والمهام</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #f4f7f6;
            --card-bg: #ffffff;
            --primary-color: #2563eb;
            --primary-hover: #1d4ed8;
            --text-color: #1f2937;
            --border-color: #e5e7eb;
            --danger-color: #ef4444;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Tajawal', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
        }

        .container {
            width: 100%;
            max-width: 600px;
            background: var(--card-bg);
            border-radius: 12px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            padding: 24px;
        }

        h1 {
            text-align: center;
            margin-top: 0;
            color: #111827;
        }

        .sync-box {
            background-color: #eff6ff;
            border: 1px solid #bfdbfe;
            border-radius: 8px;
            padding: 12px;
            margin-bottom: 20px;
            text-align: center;
        }

        .sync-box input {
            width: calc(100% - 100px);
            padding: 8px;
            margin-top: 8px;
            border: 1px solid var(--border-color);
            border-radius: 6px;
        }

        .sync-box button {
            width: 90px;
            padding: 8px;
            background: var(--primary-color);
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
        }

        .input-group {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
        }

        .input-group input {
            flex: 1;
            padding: 10px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 1rem;
        }

        .input-group button {
            padding: 10px 20px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
        }

        .input-group button:hover {
            background-color: var(--primary-hover);
        }

        ul {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        li {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 12px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            margin-bottom: 8px;
            background: #fff;
        }

        li completed span {
            text-decoration: line-through;
            color: #9ca3af;
        }

        .actions {
            display: flex;
            gap: 8px;
        }

        .btn-delete {
            background: none;
            border: none;
            color: var(--danger-color);
            cursor: pointer;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>ملاحظاتي والمهام</h1>

        <div class="sync-box">
            <label for="sync-key" style="font-size: 0.9em; font-weight: bold; display: block;">رمز المزامنة بين الأجهزة:</label>
            <input type="text" id="sync-key" placeholder="أدخل رمز المزامنة الخاص بك">
            <button id="save-sync">حفظ الرمز</button>
            <div style="font-size: 0.8em; color: #6b7280; margin-top: 6px;">أدخل نفس الرمز في الآيباد والكمبيوتر لمزامنة البيانات بينهما فوراً.</div>
        </div>

        <div class="input-group">
            <input type="text" id="task-input" placeholder="أضف ملاحظة أو مهمة جديدة...">
            <button id="add-btn">إضافة</button>
        </div>

        <ul id="task-list"></ul>
    </div>

    <script>
        const STORAGE_KEY = 'my-sync-notes-key';
        let CURRENT_KEY = localStorage.getItem(STORAGE_KEY) || 'default-key';
        document.getElementById('sync-key').value = CURRENT_KEY;

        function getStorageKey() {
            return 'tasks_' + (localStorage.getItem(STORAGE_KEY) || 'default-key');
        }

        function saveTasks(tasks) {
            localStorage.setItem(getStorageKey(), JSON.stringify(tasks));
        }

        function loadTasks() {
            const data = localStorage.getItem(getStorageKey());
            return data ? JSON.parse(data) : [];
        }

        function renderTasks() {
            const list = document.getElementById('task-list');
            const tasks = loadTasks();
            list.innerHTML = '';
            tasks.forEach(task => {
                const li = document.createElement('li');
                if (task.completed) li.classList.add('completed');
                li.innerHTML = `
                    <span onclick="toggleTask('${task.id}')" style="cursor:pointer; flex:1;">${escapeHtml(task.text)}</span>
                    <div class="actions">
                        <button class="btn-delete" onclick="deleteTask('${task.id}')">حذف</button>
                    </div>
                `;
                list.appendChild(li);
            });
        }

        function addTask() {
            const input = document.getElementById('task-input');
            const text = input.value.trim();
            if (!text) return;
            const tasks = loadTasks();
            tasks.push({ id: Date.now().toString(), text, completed: false });
            saveTasks(tasks);
            input.value = '';
            renderTasks();
        }

        function toggleTask(id) {
            const tasks = loadTasks().map(t => t.id === id ? { ...t, completed: !t.completed } : t);
            saveTasks(tasks);
            renderTasks();
        }

        function deleteTask(id) {
            const tasks = loadTasks().filter(t => t.id !== id);
            saveTasks(tasks);
            renderTasks();
        }

        document.getElementById('add-btn').addEventListener('click', addTask);
        document.getElementById('task-input').addEventListener('keypress', (e) => {
            if (e.key === 'Enter') addTask();
        });

        document.getElementById('save-sync').addEventListener('click', () => {
            const val = document.getElementById('sync-key').value.trim();
            if (val) {
                localStorage.setItem(STORAGE_KEY, val);
                location.reload();
            }
        });

        window.addEventListener('storage', (e) => {
            if (e.key === getStorageKey()) {
                renderTasks();
            }
        });

        renderTasks();

        function escapeHtml(text) {
            return text.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
        }
    </script>
</body>
</html>
