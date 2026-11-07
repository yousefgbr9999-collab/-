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
            --accent: #48cae4;
            --accent-hover: #00b4d8;
            --success: #5bc0be;
            --danger: #e63946;
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
            max-width: 850px;
        }

        header {
            text-align: center;
            margin-bottom: 28px;
        }

        header h1 {
            font-size: 2.2rem;
            font-weight: 900;
            color: #ffffff;
            margin-bottom: 8px;
            letter-spacing: -0.5px;
        }

        .date-badge {
            background: var(--card-bg);
            border: 1px solid var(--card-border);
            padding: 6px 18px;
            border-radius: 20px;
            font-size: 0.95rem;
            color: var(--accent);
            display: inline-block;
            font-weight: 500;
        }

        .card {
            background-color: var(--card-bg);
            border: 1px solid var(--card-border);
            border-radius: 16px;
            padding: 24px;
            margin-bottom: 24px;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.3);
        }

        .card-title {
            font-size: 1.25rem;
            font-weight: 700;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            color: var(--accent);
            border-bottom: 1px solid var(--card-border);
            padding-bottom: 12px;
        }

        .tasks-container {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .task-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            background: rgba(11, 19, 43, 0.5);
            border: 1px solid var(--card-border);
            padding: 14px 18px;
            border-radius: 12px;
            transition: all 0.2s ease;
        }

        .task-item:hover {
            border-color: var(--accent);
        }

        .task-label {
            display: flex;
            align-items: center;
            gap: 14px;
            cursor: pointer;
            font-size: 1.05rem;
            flex: 1;
            user-select: none;
        }

        input[type="checkbox"] {
            width: 22px;
            height: 22px;
            accent-color: var(--accent);
            cursor: pointer;
            border-radius: 6px;
        }

        .completed span {
            text-decoration: line-through;
            color: var(--text-muted);
        }

        .subjects-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(360px, 1fr));
            gap: 16px;
        }

        .subject-card {
            background: rgba(11, 19, 43, 0.5);
            border: 1px solid var(--card-border);
            border-radius: 12px;
            padding: 16px 20px;
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .subject-header {
            font-weight: 700;
            font-size: 1.1rem;
            color: #ffffff;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .subject-inputs {
            display: flex;
            gap: 16px;
            font-size: 0.95rem;
            color: var(--text-muted);
            justify-content: space-between;
        }

        .input-group {
            display: flex;
            align-items: center;
            gap: 8px;
            background: var(--card-bg);
            padding: 6px 12px;
            border-radius: 8px;
            border: 1px solid var(--card-border);
        }

        .input-group input {
            width: 55px;
            background: var(--bg-color);
            border: 1px solid var(--card-border);
            color: #ffffff;
            padding: 4px 8px;
            border-radius: 6px;
            text-align: center;
            font-size: 0.95rem;
            font-weight: 700;
            outline: none;
        }

        .input-group input:focus {
            border-color: var(--accent);
        }

        .progress-container {
            background: var(--card-bg);
            border: 1px solid var(--card-border);
            border-radius: 16px;
            padding: 20px 24px;
            margin-bottom: 24px;
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.3);
        }

        .progress-bar-bg {
            background: var(--bg-color);
            border-radius: 10px;
            height: 14px;
            width: 100%;
            overflow: hidden;
            margin-top: 12px;
            border: 1px solid var(--card-border);
        }

        .progress-bar-fill {
            background: linear-gradient(90deg, var(--accent), var(--success));
            height: 100%;
            width: 0%;
            transition: width 0.4s ease;
        }

        .actions {
            display: flex;
            gap: 12px;
            margin-top: 24px;
        }

        button {
            flex: 1;
            background-color: var(--accent);
            color: #0b132b;
            border: none;
            padding: 14px;
            border-radius: 12px;
            font-weight: 700;
            font-size: 1.05rem;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        button:hover {
            background-color: var(--accent-hover);
            transform: translateY(-1px);
        }

        .btn-secondary {
            background-color: transparent;
            color: var(--text-main);
            border: 1px solid var(--card-border);
        }

        .btn-secondary:hover {
            background-color: rgba(255, 255, 255, 0.05);
            border-color: var(--text-muted);
        }

        .history-item {
            background: rgba(11, 19, 43, 0.5);
            border: 1px solid var(--card-border);
            padding: 12px 16px;
            border-radius: 10px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.95rem;
        }

        .alert-box {
            background: rgba(230, 57, 70, 0.15);
            border: 1px solid rgba(230, 57, 70, 0.4);
            border-radius: 14px;
            padding: 16px 20px;
            margin-bottom: 24px;
            color: #ffb703;
            font-size: 0.95rem;
            line-height: 1.6;
        }

        @media (max-width: 600px) {
            .subjects-grid {
                grid-template-columns: 1fr;
            }
            .subject-inputs {
                flex-direction: column;
                gap: 8px;
            }
            .actions {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>مهام يوسف اليومية</h1>
        <div class="date-badge" id="currentDate">2026</div>
    </header>

    <!-- تنبيه النواقص من اليوم السابق -->
    <div id="alertBox" class="alert-box" style="display: none;">
        <strong>⚠️ تنبيه نواقص الأمس:</strong> <span id="alertText"></span>
        <button onclick="carryOverTasks()" style="margin-top:12px; padding:8px 14px; font-size:0.85rem;" class="btn-secondary">ترحيل النواقص لليوم</button>
    </div>

    <!-- مؤشر التقدم الإجمالي -->
    <div class="progress-container">
        <div style="display: flex; justify-content: space-between; font-weight: 700; font-size: 1.1rem;">
            <span>نسبة الإنجاز اليومي</span>
            <span id="progressText" style="color: var(--accent);">0%</span>
        </div>
        <div class="progress-bar-bg">
            <div id="progressBar" class="progress-bar-fill"></div>
        </div>
    </div>

    <!-- المهمات اليومية -->
    <div class="card">
        <div class="card-title">📌 المهمات اليومية</div>
        <div class="tasks-container" id="tasksList"></div>
    </div>

    <!-- متابعة المواد -->
    <div class="card">
        <div class="card-title">📚 متابعة المواد الدراسية</div>
        <div class="subjects-grid" id="subjectsList"></div>
    </div>

    <!-- الأزرار -->
    <div class="actions">
        <button onclick="saveAndResetDay()">حفظ اليوم والانتقال للجديد</button>
        <button class="btn-secondary" onclick="resetToday()">إعادة ضبط اليوم</button>
    </div>

    <!-- السجل السابق -->
    <div class="card" style="margin-top: 24px;">
        <div class="card-title">🕒 سجل الأيام السابقة</div>
        <div id="historyList">
            <p style="color: var(--text-muted); font-size: 0.95rem;">لا يوجد سجل سابق بعد.</p>
        </div>
    </div>
</div>

<script>
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

    let state = JSON.parse(localStorage.getItem('youssef_daily_state')) || {
        date: new Date().toLocaleDateString('ar-SA'),
        tasks: defaultTasks,
        subjects: defaultSubjects,
        history: []
    };

    document.getElementById('currentDate').innerText = "التاريخ: " + state.date + " (2026)";

    function render() {
        const tasksContainer = document.getElementById('tasksList');
        tasksContainer.innerHTML = '';
        state.tasks.forEach((task, index) => {
            tasksContainer.innerHTML += `
                <div class="task-item ${task.done ? 'completed' : ''}">
                    <label class="task-label">
                        <input type="checkbox" ${task.done ? 'checked' : ''} onclick="toggleTask(${index})">
                        <span>${task.text}</span>
                    </label>
                </div>
            `;
        });

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
                            <span>الدروس:</span>
                            <input type="number" value="${sub.lessonsDone}" min="0" max="${sub.lessonsTotal}" onchange="updateSub(${index}, 'lessonsDone', this.value)">
                            <span>/ ${sub.lessonsTotal}</span>
                        </div>
                        <div class="input-group">
                            <span>الصفحات:</span>
                            <input type="number" value="${sub.pagesDone}" min="0" max="${sub.pagesTotal}" onchange="updateSub(${index}, 'pagesDone', this.value)">
                            <span>/ ${sub.pagesTotal}</span>
                        </div>
                    </div>
                </div>
            `;
        });

        let totalItems = state.tasks.length + state.subjects.length * 2;
        let completedItems = state.tasks.filter(t => t.done).length;
        state.subjects.forEach(sub => {
            if (sub.lessonsDone >= sub.lessonsTotal) completedItems++;
            if (sub.pagesDone >= sub.pagesTotal) completedItems++;
        });

        let percent = Math.round((completedItems / totalItems) * 100);
        document.getElementById('progressBar').style.width = percent + '%';
        document.getElementById('progressText').innerText = percent + '%';

        const historyContainer = document.getElementById('historyList');
        if (state.history.length === 0) {
            historyContainer.innerHTML = '<p style="color: var(--text-muted); font-size: 0.95rem;">لا يوجد سجل سابق بعد.</p>';
        } else {
            historyContainer.innerHTML = '';
            state.history.forEach((h, hIdx) => {
                historyContainer.innerHTML += `
                    <div class="history-item">
                        <span>📅 ${h.date} - نسبة الإنجاز: <strong>${h.percent}%</strong></span>
                        <button onclick="deleteHistory(${hIdx})" style="background:var(--danger); color:white; padding:4px 10px; font-size:0.8rem; border-radius:6px; flex:none;">حذف</button>
                    </div>
                `;
            });
        }

        localStorage.setItem('youssef_daily_state', JSON.stringify(state));
    }

    function toggleTask(index) {
        state.tasks[index].done = !state.tasks[index].done;
        render();
    }

    function updateSub(index, field, val) {
        state.subjects[index][field] = Number(val);
        render();
    }

    function resetToday() {
        state.tasks.forEach(t => t.done = false);
        state.subjects.forEach(s => { s.lessonsDone = 0; s.pagesDone = 0; });
        render();
    }

    function saveAndResetDay() {
        let totalItems = state.tasks.length + state.subjects.length * 2;
        let completedItems = state.tasks.filter(t => t.done).length;
        state.subjects.forEach(sub => {
            if (sub.lessonsDone >= sub.lessonsTotal) completedItems++;
            if (sub.pagesDone >= sub.pagesTotal) completedItems++;
        });
        let percent = Math.round((completedItems / totalItems) * 100);

        state.history.unshift({
            date: state.date,
            percent: percent,
            tasks: JSON.parse(JSON.stringify(state.tasks))
        });

        let unfinished = state.tasks.filter(t => !t.done).map(t => t.text);
        if(unfinished.length > 0) {
            localStorage.setItem('youssef_unfinished', JSON.stringify(unfinished));
        }

        state.date = new Date().toLocaleDateString('ar-SA');
        resetToday();
    }

    window.onload = function() {
        let unfs = JSON.parse(localStorage.getItem('youssef_unfinished'));
        if(unfs && unfs.length > 0) {
            document.getElementById('alertBox').style.display = 'block';
            document.getElementById('alertText').innerText = unfs.join('، ');
        }
        render();
    }

    function carryOverTasks() {
        let unfs = JSON.parse(localStorage.getItem('youssef_unfinished'));
        if(unfs) {
            unfs.forEach(text => {
                state.tasks.push({ id: Date.now(), text: text + " (مرحل)", done: false });
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
</script>

</body>
</html>
