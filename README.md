<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مهام يوسف اليومية</title>
    <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;900&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-color: #0b132b;
            --card-bg: #1c2541;
            --card-border: #3a506b;
            --text-main: #edf2f4;
            --text-muted: #8d99ae;
            --accent-cyan: #48cae4;
            --accent-teal: #5bc0be;
            --accent-hover: #00b4d8;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --shadow-soft: 0 10px 25px -5px rgba(0, 0, 0, 0.4), 0 8px 10px -6px rgba(0, 0, 0, 0.3);
        }
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Tajawal', sans-serif;
        }
        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            min-height: 100vh;
            padding: 24px 16px;
            display: flex;
            justify-content: center;
        }
        .container {
            width: 100%;
            max-width: 860px;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        
        /* Header */
        header {
            text-align: center;
            padding: 12px 0 6px 0;
        }
        header h1 {
            font-size: 2.1rem;
            color: var(--text-main);
            margin-bottom: 8px;
            font-weight: 900;
            letter-spacing: -0.5px;
        }
        .date-badge {
            background: rgba(58, 80, 107, 0.4);
            border: 1px solid var(--card-border);
            padding: 6px 20px;
            border-radius: 30px;
            font-size: 0.95rem;
            color: var(--accent-teal);
            display: inline-block;
            font-weight: 500;
        }
        
        /* Main Cards */
        .card {
            background-color: var(--card-bg);
            border: 1px solid var(--card-border);
            border-radius: 18px;
            padding: 22px;
            box-shadow: var(--shadow-soft);
            transition: border-color 0.2s ease;
        }
        .card-title {
            font-size: 1.2rem;
            font-weight: 700;
            margin-bottom: 18px;
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--accent-cyan);
            border-bottom: 1px solid rgba(255, 255, 255, 0.06);
            padding-bottom: 10px;
        }

        /* Sync Box */
        .sync-box {
            background: rgba(72, 202, 228, 0.08);
            border: 1px solid rgba(72, 202, 228, 0.3);
            border-radius: 14px;
            padding: 16px;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .sync-box label {
            font-size: 0.95rem;
            font-weight: 700;
            color: var(--accent-cyan);
        }
        .sync-input-group {
            display: flex;
            gap: 10px;
        }
        .sync-input-group input {
            flex: 1;
            padding: 10px 14px;
            background: rgba(11, 19, 43, 0.7);
            border: 1px solid var(--card-border);
            border-radius: 10px;
            color: var(--text-main);
            font-size: 0.95rem;
            font-weight: 600;
        }
        .sync-input-group input:focus {
            outline: none;
            border-color: var(--accent-teal);
        }

        /* Task Items */
        #tasksList {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .task-item {
            display: flex;
            align-items: center;
            padding: 12px 16px;
            border: 1px solid rgba(58, 80, 107, 0.6);
            background: rgba(11, 19, 43, 0.5);
            border-radius: 12px;
            transition: all 0.2s ease;
        }
        .task-item:hover {
            border-color: var(--accent-teal);
            background: rgba(11, 19, 43, 0.8);
        }
        .task-label {
            display: flex;
            align-items: center;
            gap: 14px;
            cursor: pointer;
            font-size: 1rem;
            width: 100%;
            user-select: none;
        }
        input[type="checkbox"] {
            width: 20px;
            height: 20px;
            accent-color: var(--accent-teal);
            cursor: pointer;
            border-radius: 6px;
            flex-shrink: 0;
        }
        .completed span {
            text-decoration: line-through;
            color: var(--text-muted);
        }

        /* Subjects Responsive Grid */
        .subjects-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 14px;
        }
        @media (max-width: 680px) {
            .subjects-grid {
                grid-template-columns: 1fr;
            }
        }
        .subject-card {
            background: rgba(11, 19, 43, 0.5);
            border: 1px solid rgba(58, 80, 107, 0.6);
            border-radius: 14px;
            padding: 16px;
            display: flex;
            flex-direction: column;
            gap: 12px;
            transition: all 0.2s ease;
        }
        .subject-card:hover {
            border-color: var(--accent-cyan);
        }
        .subject-header {
            font-weight: 700;
            font-size: 1.05rem;
            color: var(--accent-teal);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .subject-inputs {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .input-group {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background: rgba(28, 37, 65, 0.7);
            padding: 8px 12px;
            border-radius: 10px;
            border: 1px solid rgba(255, 255, 255, 0.04);
            font-size: 0.9rem;
            color: var(--text-muted);
        }
        .input-group-controls {
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .input-group input {
            width: 55px;
            height: 32px;
            background: var(--bg-color);
            border: 1px solid var(--card-border);
            color: var(--accent-cyan);
            border-radius: 6px;
            text-align: center;
            font-size: 0.95rem;
            font-weight: 700;
        }
        .input-group input:focus {
            outline: none;
            border-color: var(--accent-teal);
        }

        /* Progress Bar */
        .progress-container {
            background: var(--card-bg);
            border: 1px solid var(--card-border);
            border-radius: 18px;
            padding: 18px 22px;
            box-shadow: var(--shadow-soft);
        }
        .progress-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: 700;
            font-size: 1.05rem;
        }
        .progress-bar-bg {
            background: var(--bg-color);
            border-radius: 10px;
            height: 12px;
            width: 100%;
            overflow: hidden;
            margin-top: 12px;
            border: 1px solid rgba(58, 80, 107, 0.5);
        }
        .progress-bar-fill {
            background: linear-gradient(90deg, var(--accent-teal), var(--accent-cyan));
            height: 100%;
            width: 0%;
            transition: width 0.4s ease;
            border-radius: 10px;
        }

        /* Action Buttons */
        .actions {
            display: flex;
            gap: 12px;
        }
        @media (max-width: 550px) {
            .actions {
                flex-direction: column;
            }
        }
        button {
            background-color: var(--accent-teal);
            color: #0b132b;
            border: none;
            padding: 12px 18px;
            border-radius: 12px;
            font-weight: 700;
            font-size: 0.95rem;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        button:hover {
            background-color: var(--accent-cyan);
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(91, 192, 190, 0.3);
        }
        .btn-secondary {
            background-color: rgba(58, 80, 107, 0.4);
            color: var(--text-main);
            border: 1px solid var(--card-border);
        }
        .btn-secondary:hover {
            background-color: rgba(58, 80, 107, 0.7);
            box-shadow: none;
        }

        /* History & Alerts */
        .history-item {
            background: rgba(11, 19, 43, 0.5);
            padding: 12px 16px;
            border-radius: 10px;
            margin-bottom: 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.9rem;
            border: 1px solid rgba(58, 80, 107, 0.4);
        }
        .alert-box {
            background: rgba(245, 158, 11, 0.1);
            border: 1px solid rgba(245, 158, 11, 0.3);
            border-radius: 14px;
            padding: 16px;
            color: #fde68a;
            font-size: 0.95rem;
            line-height: 1.5;
        }
        .tag-carried {
            background: rgba(245, 158, 11, 0.2);
            color: #fef08a;
            font-size: 0.75rem;
            padding: 2px 8px;
            border-radius: 6px;
            margin-left: 6px;
            border: 1px solid rgba(245, 158, 11, 0.3);
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>📋 مهام يوسف اليومية</h1>
        <div class="date-badge" id="currentDate">جاري تحميل التاريخ...</div>
    </header>

    <!-- رمز المزامنة -->
    <div class="card sync-box">
        <label for="syncKeyInput">🔗 رمز المزامنة بين الأجهزة:</label>
        <div class="sync-input-group">
            <input type="text" id="syncKeyInput" placeholder="أدخل رمز المزامنة (مثال: YOUSEF GBR)">
            <button onclick="saveSyncKey()">حفظ الرمز</button>
        </div>
        <div style="font-size: 0.82rem; color: var(--text-muted);">أدخل نفس الرمز في جهازك الآخر لمزامنة البيانات تلقائياً بينهما.</div>
    </div>

    <!-- تنبيه النواقص -->
    <div id="alertBox" class="alert-box" style="display: none;">
        <strong>⚠️ تنبيه نواقص الأمس:</strong> <span id="alertText"></span>
        <div style="margin-top:12px;">
            <button onclick="carryOverTasks()" style="padding:8px 14px; font-size:0.85rem; width: auto;" class="btn-secondary">ترحيل النواقص لجدول اليوم 🔄</button>
        </div>
    </div>

    <!-- مؤشر التقدم الإجمالي -->
    <div class="progress-container">
        <div class="progress-header">
            <span>مؤشر الإنجاز اليومي</span>
            <span id="progressText" style="color: var(--accent-teal);">0%</span>
        </div>
        <div class="progress-bar-bg">
            <div id="progressBar" class="progress-bar-fill"></div>
        </div>
    </div>

    <!-- المهمات اليومية -->
    <div class="card">
        <div class="card-title">📌 المهمات اليومية</div>
        <div id="tasksList"></div>
    </div>

    <!-- متابعة المواد -->
    <div class="card">
        <div class="card-title">📚 متابعة المواد الدراسية</div>
        <div class="subjects-grid" id="subjectsList"></div>
    </div>

    <!-- الأزرار -->
    <div class="actions">
        <button style="flex:2;" onclick="saveAndResetDay()">حفظ اليوم والانتقال لليوم الجديد 💾</button>
        <button style="flex:1;" class="btn-secondary" onclick="resetToday()">إعادة ضبط اليوم 🔄</button>
    </div>

    <!-- السجل السابق -->
    <div class="card">
        <div class="card-title">🕒 سجل الأيام السابقة</div>
        <div id="historyList">
            <p style="color: var(--text-muted); font-size: 0.9rem;">لا يوجد سجل سابق بعد.</p>
        </div>
    </div>
</div>

<script>
    const SYNC_KEY_NAME = 'youssef_sync_key';
    let currentSyncKey = localStorage.getItem(SYNC_KEY_NAME) || 'YOUSEF GBR';
    document.getElementById('syncKeyInput').value = currentSyncKey;

    function getStorageKey() {
        return 'youssef_daily_state_' + (localStorage.getItem(SYNC_KEY_NAME) || 'YOUSEF GBR');
    }

    const defaultTasks = [
        { id: 1, text: "4 صفحات قرآن", done: false },
        { id: 2, text: "زيارة آل ياسين", done: false },
        { id: 3, text: "صلاة الليل (أذا أمكن)", done: false },
        { id: 4, text: "درس في الرياضيات + حل 20 سؤال عليه", done: false },
        { id: 5, text: "تقليل استخدام الجوال (سوشل ميديا \\ المانهوا أو مانغا)", done: false }
    ];

    const defaultSubjects = [
        { name: "فيزياء", lessonsDone: 0, lessonsTotal: 10, pagesDone: 0, pagesTotal: 76 },
        { name: "رياضيات", lessonsDone: 0, lessonsTotal: 17, pagesDone: 0, pagesTotal: 83 },
        { name: "كيمياء", lessonsDone: 0, lessonsTotal: 11, pagesDone: 0, pagesTotal: 76 },
        { name: "الأحياء", lessonsDone: 0, lessonsTotal: 11, pagesDone: 0, pagesTotal: 78 }
    ];

    function loadState() {
        return JSON.parse(localStorage.getItem(getStorageKey())) || {
            date: new Date().toLocaleDateString('ar-SA', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' }),
            tasks: defaultTasks,
            subjects: defaultSubjects,
            history: []
        };
    }

    let state = loadState();
    document.getElementById('currentDate').innerText = state.date;

    function saveSyncKey() {
        const val = document.getElementById('syncKeyInput').value.trim();
        if (val) {
            localStorage.setItem(SYNC_KEY_NAME, val);
            state = loadState();
            render();
            alert('تم حفظ رمز المزامنة: ' + val);
        }
    }

    function render() {
        // Render Tasks
        const tasksContainer = document.getElementById('tasksList');
        tasksContainer.innerHTML = '';
        state.tasks.forEach((task, index) => {
            tasksContainer.innerHTML += `
                <div class="task-item ${task.done ? 'completed' : ''}">
                    <label class="task-label">
                        <input type="checkbox" ${task.done ? 'checked' : ''} onchange="toggleTask(${index})">
                        <span>${task.carried ? '<span class="tag-carried">مرحّل</span>' : ''}${task.text}</span>
                    </label>
                </div>
            `;
        });

        // Render Subjects (Grid)
        const subjectsContainer = document.getElementById('subjectsList');
        subjectsContainer.innerHTML = '';
        state.subjects.forEach((sub, index) => {
            subjectsContainer.innerHTML += `
                <div class="subject-card">
                    <div class="subject-header">
                        <span>${sub.name}</span>
                    </div>
                    <div class="subject-inputs">
                        <div class="input-group">
                            <span>الدروس المنجزة</span>
                            <div class="input-group-controls">
                                <input type="number" value="${sub.lessonsDone}" min="0" max="${sub.lessonsTotal}" onchange="updateSub(${index}, 'lessonsDone', this.value)">
                                <span>/ ${sub.lessonsTotal}</span>
                            </div>
                        </div>
                        <div class="input-group">
                            <span>الصفحات المنجزة</span>
                            <div class="input-group-controls">
                                <input type="number" value="${sub.pagesDone}" min="0" max="${sub.pagesTotal}" onchange="updateSub(${index}, 'pagesDone', this.value)">
                                <span>/ ${sub.pagesTotal}</span>
                            </div>
                        </div>
                    </div>
                </div>
            `;
        });

        // Calculate Progress Percentage
        let totalItems = state.tasks.length + state.subjects.length * 2;
        let completedItems = state.tasks.filter(t => t.done).length;
        
        state.subjects.forEach(sub => {
            if (sub.lessonsDone >= sub.lessonsTotal && sub.lessonsTotal > 0) completedItems++;
            if (sub.pagesDone >= sub.pagesTotal && sub.pagesTotal > 0) completedItems++;
        });

        let percent = totalItems > 0 ? Math.round((completedItems / totalItems) * 100) : 0;
        document.getElementById('progressBar').style.width = percent + '%';
        document.getElementById('progressText').innerText = percent + '%';

        // Render History
        const historyContainer = document.getElementById('historyList');
        if (!state.history || state.history.length === 0) {
            historyContainer.innerHTML = '<p style="color: var(--text-muted); font-size: 0.9rem;">لا يوجد سجل سابق بعد.</p>';
        } else {
            historyContainer.innerHTML = '';
            state.history.forEach((h, hIdx) => {
                historyContainer.innerHTML += `
                    <div class="history-item">
                        <span>📅 <strong>${h.date}</strong> - الإنجاز: <strong style="color: var(--accent-teal);">${h.percent}%</strong></span>
                        <button onclick="deleteHistory(${hIdx})" style="background:var(--danger); padding:4px 10px; font-size:0.75rem; border-radius:6px; width:auto; color:white;">حذف</button>
                    </div>
                `;
            });
        }

        localStorage.setItem(getStorageKey(), JSON.stringify(state));
    }

    function toggleTask(index) {
        state.tasks[index].done = !state.tasks[index].done;
        render();
    }

    function updateSub(index, field, val) {
        state.subjects[index][field] = Math.max(0, Number(val));
        render();
    }

    function resetToday() {
        if(confirm('هل أنت تأكد من إعادة ضبط إنجاز اليوم؟')) {
            state.tasks.forEach(t => t.done = false);
            state.subjects.forEach(s => { s.lessonsDone = 0; s.pagesDone = 0; });
            render();
        }
    }

    function saveAndResetDay() {
        let totalItems = state.tasks.length + state.subjects.length * 2;
        let completedItems = state.tasks.filter(t => t.done).length;
        state.subjects.forEach(sub => {
            if (sub.lessonsDone >= sub.lessonsTotal) completedItems++;
            if (sub.pagesDone >= sub.pagesTotal) completedItems++;
        });
        let percent = Math.round((completedItems / totalItems) * 100);

        if (!state.history) state.history = [];
        state.history.unshift({
            date: state.date,
            percent: percent,
            tasks: JSON.parse(JSON.stringify(state.tasks))
        });

        let unfinished = state.tasks.filter(t => !t.done).map(t => t.text);
        if(unfinished.length > 0) {
            localStorage.setItem('youssef_unfinished', JSON.stringify(unfinished));
        }

        state.date = new Date().toLocaleDateString('ar-SA', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
        state.tasks = JSON.parse(JSON.stringify(defaultTasks));
        state.subjects = JSON.parse(JSON.stringify(defaultSubjects));
        
        document.getElementById('currentDate').innerText = state.date;
        render();
        alert('تم حفظ إنجاز اليوم بنجاح وتهيئة اليوم الجديد!');
    }

    function carryOverTasks() {
        let unfs = JSON.parse(localStorage.getItem('youssef_unfinished'));
        if(unfs) {
            unfs.forEach(text => {
                if (!state.tasks.some(t => t.text === text)) {
                    state.tasks.push({ id: Date.now() + Math.random(), text: text, done: false, carried: true });
                }
            });
            localStorage.removeItem('youssef_unfinished');
            document.getElementById('alertBox').style.display = 'none';
            render();
        }
    }

    function deleteHistory(index) {
        state.history.splice(index, 1);
        render();
    }

    window.addEventListener('storage', (e) => {
        if (e.key === getStorageKey()) {
            state = loadState();
            render();
        }
    });

    window.onload = function() {
        let unfs = JSON.parse(localStorage.getItem('youssef_unfinished'));
        if(unfs && unfs.length > 0) {
            document.getElementById('alertBox').style.display = 'block';
            document.getElementById('alertText').innerText = unfs.join('، ');
        }
        render();
    }
</script>

</body>
</html>
