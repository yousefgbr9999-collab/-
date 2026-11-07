<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مدير المهام والملاحظات المزامن</title>
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
            font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
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
            padding: 24px;
            border-radius: 12px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }

        h1 {
            text-align: center;
            margin-top: 0;
            color: #111827;
        }

        .sync-box {
            background-color: #eff6ff;
            border: 1px solid #bfdbfe;
            padding: 12px;
            border-radius: 8px;
            margin-bottom: 20px;
            font-size: 0.9em;
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
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
        }

        .input-group {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        input[type="text"] {
            flex: 1;
            padding: 10px 14px;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            font-size: 1rem;
        }

        .btn-add {
            padding: 10px 20px;
            background-color: var(--primary-color);
            color: white;
            border: none;
            border-radius: 6px;
            font-size: 1rem;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .btn-add:hover {
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
            border-radius: 6px;
            margin-bottom: 8px;
            background: #fff;
        }

        li.completed span {
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
        <label for="user-key"><strong>رمز المزامنة بين الأجهزة:</strong></label><br>
        <div style="display:flex; gap: 8px; margin-top: 6px;">
            <input type="text" id="user-key" placeholder="أدخل رمز المزامنة الخاص بك">
            <button onclick="saveKey()">حفظ الرمز</button>
        </div>
        <small style="color: #6b7280; display: block; margin-top: 4px;">ادخل نفس الرمز في الآيباد والكمبيوتر لمزامنة البيانات بينهما فوراً.</small>
    </div>

    <div class="input-group">
        <input type="text" id="task-input" placeholder="أضف ملاحظة أو مهمة جديدة...">
        <button class="btn-add" onclick="addTask()">إضافة</button>
    </div>

    <ul id="task-list"></ul>
</div>

<script>
    const defaultKey = 'my-sync-notes-key';
    let currentKey = localStorage.getItem('sync_user_key') || defaultKey;
    document.getElementById('user-key').value = currentKey;

    function saveKey() {
        const val = document.getElementById('user-key').value.trim();
        if (val) {
            localStorage.setItem('sync_user_key', val);
            currentKey = val;
            loadTasks();
            alert('تم حفظ رمز المزامنة وتحديث القائمة!');
        }
    }

    function getStorageKey() {
        return 'tasks_' + currentKey;
    }

    function getTasks() {
        return JSON.parse(localStorage.getItem(getStorageKey()) || '[]');
    }

    function saveTasks(tasks) {
        localStorage.setItem(getStorageKey(), JSON.stringify(tasks));
        renderTasks();
    }

    function addTask() {
        const input = document.getElementById('task-input');
        const text = input.value.trim();
        if (!text) return;

        const tasks = getTasks();
        tasks.push({ id: Date.now(), text: text, completed: false });
        saveTasks(tasks);
        input.value = '';
    }

    function toggleTask(id) {
        const tasks = getTasks().map(t => {
            if (t.id === id) t.completed = !t.completed;
            return t;
        });
        saveTasks(tasks);
    }

    function deleteTask(id) {
        const tasks = getTasks().filter(t => t.id !== id);
        saveTasks(tasks);
    }

    function renderTasks() {
        const list = document.getElementById('task-list');
        list.innerHTML = '';
        const tasks = getTasks();

        tasks.forEach(t => {
            const li = document.createElement('li');
            if (t.completed) li.classList.add('completed');

            li.innerHTML = `
                <span onclick="toggleTask(${t.id})" style="cursor:pointer; flex:1;">${escapeHtml(t.text)}</span>
                <div class="actions">
                    <button class="btn-delete" onclick="deleteTask(${t.id})">حذف</button>
                </div>
            `;
            list.appendChild(li);
        });
    }

    function escapeHtml(str) {
        return str.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
    }

    // Direct listener for basic cross-tab/local changes
    window.addEventListener('storage', (e) => {
        if (e.key === getStorageKey()) {
            renderTasks();
        }
    });

    renderTasks();
</script>

</body>
</html>
