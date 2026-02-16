# Math-game-2G-New-Vision
Math game for children
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🧮 Считалочка: Соревнование с автовводом</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, sans-serif;
        }
        body {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .game-container {
            max-width: 1300px;
            width: 100%;
        }

        .main-menu {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 25px;
        }
        .menu-btn {
            background: rgba(255,255,255,0.15);
            border: 3px solid white;
            color: white;
            font-size: 1.6rem;
            font-weight: 800;
            padding: 18px 35px;
            border-radius: 60px;
            cursor: pointer;
            backdrop-filter: blur(10px);
            box-shadow: 0 8px 0 rgba(0,0,0,0.3);
        }
        .menu-btn.active {
            background: #f6e58d;
            color: #1e3c72;
            transform: translateY(4px);
            box-shadow: 0 4px 0 rgba(0,0,0,0.3);
        }

        .game-panel {
            background: rgba(255,255,255,0.95);
            backdrop-filter: blur(8px);
            border-radius: 70px;
            padding: 30px;
            border: 6px solid white;
            box-shadow: 0 30px 40px rgba(0,0,0,0.4);
        }

        .global-settings {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 20px;
            background: #dfe9f3;
            padding: 20px 25px;
            border-radius: 60px;
            margin-bottom: 25px;
        }
        .badge {
            background: #34495e;
            color: white;
            font-weight: 700;
            font-size: 1.2rem;
            padding: 8px 22px;
            border-radius: 50px;
        }
        .digits-group, .ops-group {
            display: flex;
            gap: 12px;
            flex-wrap: wrap;
        }
        .digit-btn, .op-btn {
            background: white;
            border: 3px solid #2980b9;
            font-size: 1.3rem;
            font-weight: 700;
            padding: 8px 20px;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 5px 0 #a0bccf;
        }
        .op-btn {
            font-size: 2rem;
            width: 70px;
            height: 70px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .digit-btn.active, .op-btn.active {
            background: #f1c40f;
            border-color: #e67e22;
            transform: translateY(2px);
            box-shadow: 0 3px 0 #b85e0a;
        }
        .multi-toggle {
            background: #9b59b6;
            color: white;
            font-size: 1.3rem;
            padding: 12px 28px;
            border-radius: 50px;
            border: 3px solid white;
            font-weight: 700;
            cursor: pointer;
            box-shadow: 0 6px 0 #6c3483;
            margin-left: auto;
        }
        .multi-toggle.active {
            background: #e67e22;
            transform: translateY(3px);
            box-shadow: 0 3px 0 #a04000;
        }

        /* Режимы */
        .classic-area, .competition-area, .blitz-area {
            display: none;
        }
        .classic-area.active, .competition-area.active, .blitz-area.active {
            display: block;
        }

        /* Классика */
        .example-box {
            background: #2c3e50;
            color: white;
            font-size: 5rem;
            text-align: center;
            padding: 25px;
            border-radius: 70px;
            border: 6px solid #f1c40f;
            margin-bottom: 25px;
        }
        .input-block {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-bottom: 20px;
        }
        .big-input {
            font-size: 3rem;
            width: 250px;
            text-align: center;
            border: 6px solid #3498db;
            border-radius: 70px;
            padding: 15px;
        }
        .big-btn {
            background: #2ecc71;
            border: none;
            border-radius: 70px;
            font-size: 2.2rem;
            padding: 15px 40px;
            color: white;
            border: 5px solid white;
            box-shadow: 0 8px 0 #1e8b4c;
            cursor: pointer;
        }

        /* СОРЕВНОВАНИЕ */
        .competition-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }
        .player-card {
            background: #ecf0f1;
            border-radius: 60px;
            padding: 25px;
            border: 6px solid white;
        }
        .player1 .player-card {
            border-top: 15px solid #e74c3c;
        }
        .player2 .player-card {
            border-top: 15px solid #3498db;
        }
        .player-title {
            font-size: 2.5rem;
            font-weight: 700;
            text-align: center;
            margin-bottom: 15px;
        }
        .comp-example {
            font-size: 4rem;
            text-align: center;
            background: white;
            padding: 25px;
            border-radius: 50px;
            margin: 15px 0;
            border: 4px solid #7f8c8d;
        }
        .comp-input {
            font-size: 3rem;
            width: 100%;
            text-align: center;
            border: 5px solid #2c3e50;
            border-radius: 50px;
            padding: 15px;
            margin: 15px 0;
        }
        .comp-input:focus {
            outline: 4px solid #f1c40f;
        }
        .player-start-btn {
            background: #f39c12;
            color: white;
            font-size: 2rem;
            padding: 20px;
            border-radius: 60px;
            border: 4px solid white;
            font-weight: 700;
            cursor: pointer;
            box-shadow: 0 8px 0 #b85e0a;
            width: 100%;
            margin: 10px 0;
        }
        .comp-progress {
            font-size: 2rem;
            text-align: center;
            margin: 15px 0;
            font-weight: 600;
        }
        .player-timer {
            font-size: 2.5rem;
            font-family: monospace;
            background: #2c3e50;
            color: white;
            padding: 10px 20px;
            border-radius: 50px;
            text-align: center;
            margin: 10px 0;
        }
        .comp-winner {
            grid-column: span 2;
            background: #f9ca24;
            font-size: 2.5rem;
            padding: 25px;
            border-radius: 60px;
            text-align: center;
            font-weight: 800;
            margin-top: 20px;
        }

        .links {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
        }
        .links a {
            background: #2c3e50;
            color: white;
            padding: 15px 35px;
            border-radius: 60px;
            text-decoration: none;
            font-weight: 700;
            border: 3px solid white;
        }
    </style>
</head>
<body>
<div class="game-container">
    <div class="main-menu">
        <div class="menu-btn active" data-mode="classic">📚 Классика</div>
        <div class="menu-btn" data-mode="competition">🏆 Соревнование</div>
        <div class="menu-btn" data-mode="blitz">⚡ Блиц</div>
    </div>

    <div class="game-panel">
        <!-- Общие настройки -->
        <div class="global-settings">
            <span class="badge">Числа</span>
            <div class="digits-group">
                <span class="digit-btn active" data-digits="1">1 цифра</span>
                <span class="digit-btn" data-digits="2">двузнач</span>
                <span class="digit-btn" data-digits="3">трёхзнач</span>
            </div>
            <span class="badge">Действия</span>
            <div class="ops-group">
                <span class="op-btn active" data-op="+">+</span>
                <span class="op-btn" data-op="-">−</span>
                <span class="op-btn" data-op="×">×</span>
                <span class="op-btn" data-op="÷">÷</span>
            </div>
            <span class="multi-toggle" id="multiToggle">🌈 мульти</span>
        </div>

        <!-- Классика -->
        <div id="classicMode" class="classic-area active">
            <div class="example-box" id="classicExample">5 + 3</div>
            <div class="input-block">
                <input type="number" id="classicAnswer" class="big-input" placeholder="?" autofocus>
                <button class="big-btn" id="classicCheck">✅ Проверить</button>
            </div>
        </div>

        <!-- Соревнование -->
        <div id="competitionMode" class="competition-area">
            <div class="competition-grid">
                <!-- Игрок 1 -->
                <div class="player-card player1">
                    <div class="player-title">🔴 ИГРОК 1</div>
                    <div class="comp-example" id="p1Example">5 + 3</div>
                    <input type="number" id="p1Input" class="comp-input" placeholder="ответ" disabled>
                    <button class="player-start-btn" id="p1StartBtn">🚀 СТАРТ</button>
                    <div class="comp-progress" id="p1Progress">0/10</div>
                    <div class="player-timer" id="p1Timer">0.0 с</div>
                </div>
                <!-- Игрок 2 -->
                <div class="player-card player2">
                    <div class="player-title">🔵 ИГРОК 2</div>
                    <div class="comp-example" id="p2Example">7 - 2</div>
                    <input type="number" id="p2Input" class="comp-input" placeholder="ответ" disabled>
                    <button class="player-start-btn" id="p2StartBtn">🚀 СТАРТ</button>
                    <div class="comp-progress" id="p2Progress">0/10</div>
                    <div class="player-timer" id="p2Timer">0.0 с</div>
                </div>
                <div class="comp-winner" id="compWinner">🏆 Нажмите СТАРТ, чтобы начать</div>
            </div>
        </div>

        <!-- Блиц (упрощённо) -->
        <div id="blitzMode" class="blitz-area">
            <div style="text-align:center; font-size:2rem; padding:50px;">⚡ Блиц-турнир будет здесь</div>
        </div>

        <div class="links">
            <a href="https://pages.github.com/" target="_blank">GitHub Pages</a>
            <a href="https://app.netlify.com/drop" target="_blank">Netlify Drop</a>
        </div>
    </div>
</div>

<script>
    (function() {
        // ========== ОБЩЕЕ ==========
        let currentDigits = 1;
        let selectedOps = new Set(['+']);
        let multiMode = false;

        // Состояние соревнования
        let compState = {
            p1: { active: false, tasks: [], currentIdx: 0, time: 0, timer: null, done: false },
            p2: { active: false, tasks: [], currentIdx: 0, time: 0, timer: null, done: false }
        };

        // Элементы
        const digitBtns = document.querySelectorAll('.digit-btn');
        const opBtns = document.querySelectorAll('.op-btn');
        const multiToggle = document.getElementById('multiToggle');

        // ========== ФУНКЦИИ ==========
        function getRandomInt(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + min;
        }

        function generateNumber(digits) {
            if (digits === 1) return getRandomInt(1, 9);
            if (digits === 2) return getRandomInt(10, 99);
            return getRandomInt(100, 999);
        }

        function getRandomOp() {
            if (selectedOps.size === 0) return '+';
            const arr = Array.from(selectedOps);
            return arr[Math.floor(Math.random() * arr.length)];
        }

        function generateExample() {
            let op = multiMode ? getRandomOp() : Array.from(selectedOps)[0] || '+';
            let a, b, answer;

            if (op === '+') {
                a = generateNumber(currentDigits);
                b = generateNumber(currentDigits);
                answer = a + b;
            } else if (op === '-') {
                a = generateNumber(currentDigits);
                b = generateNumber(currentDigits);
                if (a < b) [a, b] = [b, a];
                answer = a - b;
            } else if (op === '×') {
                a = generateNumber(currentDigits);
                b = (currentDigits === 3) ? getRandomInt(2, 15) : (currentDigits === 2) ? getRandomInt(2, 12) : getRandomInt(2, 9);
                answer = a * b;
            } else { // ÷
                if (currentDigits === 1) {
                    b = getRandomInt(2, 9);
                    answer = getRandomInt(2, 9);
                } else if (currentDigits === 2) {
                    b = getRandomInt(3, 12);
                    answer = getRandomInt(3, 12);
                } else {
                    b = getRandomInt(5, 20);
                    answer = getRandomInt(5, 20);
                }
                a = b * answer;
            }
            return { text: `${a} ${op} ${b}`, answer, op };
        }

        // Генерация 10 задач для игрока
        function generateTasks() {
            let tasks = [];
            for (let i = 0; i < 10; i++) {
                tasks.push(generateExample());
            }
            return tasks;
        }

        // Обновить UI настроек
        function updateSettingsUI() {
            digitBtns.forEach(btn => btn.classList.toggle('active', parseInt(btn.dataset.digits) === currentDigits));
            opBtns.forEach(btn => btn.classList.toggle('active', selectedOps.has(btn.dataset.op)));
            multiToggle.classList.toggle('active', multiMode);
        }

        // Запуск игрока
        function startPlayer(playerNum) {
            if (playerNum === 1) {
                if (compState.p1.active || compState.p1.done) return;
                compState.p1.tasks = generateTasks();
                compState.p1.currentIdx = 0;
                compState.p1.time = 0;
                compState.p1.active = true;
                compState.p1.done = false;

                document.getElementById('p1Example').innerText = compState.p1.tasks[0].text;
                document.getElementById('p1Input').disabled = false;
                document.getElementById('p1Input').value = '';
                document.getElementById('p1Input').focus();
                document.getElementById('p1StartBtn').disabled = true;
                document.getElementById('p1Progress').innerText = `1/10`;

                if (compState.p1.timer) clearInterval(compState.p1.timer);
                compState.p1.timer = setInterval(() => {
                    compState.p1.time += 0.1;
                    document.getElementById('p1Timer').innerText = compState.p1.time.toFixed(1) + ' с';
                }, 100);
            } else {
                if (compState.p2.active || compState.p2.done) return;
                compState.p2.tasks = generateTasks();
                compState.p2.currentIdx = 0;
                compState.p2.time = 0;
                compState.p2.active = true;
                compState.p2.done = false;

                document.getElementById('p2Example').innerText = compState.p2.tasks[0].text;
                document.getElementById('p2Input').disabled = false;
                document.getElementById('p2Input').value = '';
                document.getElementById('p2Input').focus();
                document.getElementById('p2StartBtn').disabled = true;
                document.getElementById('p2Progress').innerText = `1/10`;

                if (compState.p2.timer) clearInterval(compState.p2.timer);
                compState.p2.timer = setInterval(() => {
                    compState.p2.time += 0.1;
                    document.getElementById('p2Timer').innerText = compState.p2.time.toFixed(1) + ' с';
                }, 100);
            }
        }

        // Обработка ответа игрока
        function handlePlayerAnswer(playerNum) {
            if (playerNum === 1) {
                if (!compState.p1.active) return;
                const input = document.getElementById('p1Input');
                const val = parseInt(input.value);
                if (isNaN(val)) return;

                const task = compState.p1.tasks[compState.p1.currentIdx];
                if (val === task.answer) {
                    // Правильно - следующая задача
                    compState.p1.currentIdx++;
                    if (compState.p1.currentIdx >= 10) {
                        // Игрок закончил
                        compState.p1.active = false;
                        compState.p1.done = true;
                        clearInterval(compState.p1.timer);
                        document.getElementById('p1Input').disabled = true;
                        document.getElementById('p1Progress').innerText = `10/10 ✅`;
                        document.getElementById('p1StartBtn').disabled = false;
                    } else {
                        document.getElementById('p1Example').innerText = compState.p1.tasks[compState.p1.currentIdx].text;
                        document.getElementById('p1Progress').innerText = `${compState.p1.currentIdx+1}/10`;
                    }
                } else {
                    // Неправильно - ничего не меняем, просто очищаем поле
                }
                input.value = '';
                input.focus(); // сохраняем фокус
            } else {
                if (!compState.p2.active) return;
                const input = document.getElementById('p2Input');
                const val = parseInt(input.value);
                if (isNaN(val)) return;

                const task = compState.p2.tasks[compState.p2.currentIdx];
                if (val === task.answer) {
                    compState.p2.currentIdx++;
                    if (compState.p2.currentIdx >= 10) {
                        compState.p2.active = false;
                        compState.p2.done = true;
                        clearInterval(compState.p2.timer);
                        document.getElementById('p2Input').disabled = true;
                        document.getElementById('p2Progress').innerText = `10/10 ✅`;
                        document.getElementById('p2StartBtn').disabled = false;
                    } else {
                        document.getElementById('p2Example').innerText = compState.p2.tasks[compState.p2.currentIdx].text;
                        document.getElementById('p2Progress').innerText = `${compState.p2.currentIdx+1}/10`;
                    }
                }
                input.value = '';
                input.focus();
            }

            // Проверяем, закончили ли оба
            if (compState.p1.done && compState.p2.done) {
                let winner = '';
                if (compState.p1.time < compState.p2.time) winner = '🏆 Победил Игрок 1 (быстрее)!';
                else if (compState.p2.time < compState.p1.time) winner = '🏆 Победил Игрок 2 (быстрее)!';
                else winner = '🤝 Ничья!';
                document.getElementById('compWinner').innerHTML = `${winner}<br>⏱️ Игрок1: ${compState.p1.time.toFixed(1)}с | Игрок2: ${compState.p2.time.toFixed(1)}с`;
            }
        }

        // ========== ИНИЦИАЛИЗАЦИЯ ==========
        window.addEventListener('load', () => {
            updateSettingsUI();

            // Переключение режимов
            document.querySelectorAll('.menu-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    document.querySelectorAll('.menu-btn').forEach(b => b.classList.remove('active'));
                    btn.classList.add('active');
                    document.querySelectorAll('.classic-area, .competition-area, .blitz-area').forEach(el => {
                        el.classList.remove('active');
                    });
                    document.getElementById(btn.dataset.mode + 'Mode').classList.add('active');
                    
                    // Автофокус для классики
                    if (btn.dataset.mode === 'classic') {
                        document.getElementById('classicAnswer').focus();
                    }
                });
            });

            // Настройки
            digitBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    currentDigits = parseInt(btn.dataset.digits);
                    updateSettingsUI();
                    document.getElementById('classicExample').innerText = generateExample().text;
                });
            });

            opBtns.forEach(btn => {
                btn.addEventListener('click', () => {
                    const op = btn.dataset.op;
                    if (multiMode) {
                        if (selectedOps.has(op)) {
                            if (selectedOps.size > 1) selectedOps.delete(op);
                        } else selectedOps.add(op);
                    } else {
                        selectedOps.clear();
                        selectedOps.add(op);
                    }
                    updateSettingsUI();
                    document.getElementById('classicExample').innerText = generateExample().text;
                });
            });

            multiToggle.addEventListener('click', () => {
                multiMode = !multiMode;
                if (!multiMode && selectedOps.size > 1) {
                    const first = Array.from(selectedOps)[0];
                    selectedOps.clear();
                    selectedOps.add(first);
                }
                updateSettingsUI();
                document.getElementById('classicExample').innerText = generateExample().text;
            });

            // Классика
            document.getElementById('classicCheck').addEventListener('click', () => {
                document.getElementById('classicExample').innerText = generateExample().text;
                document.getElementById('classicAnswer').value = '';
                document.getElementById('classicAnswer').focus();
            });
            document.getElementById('classicAnswer').addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    document.getElementById('classicExample').innerText = generateExample().text;
                    document.getElementById('classicAnswer').value = '';
                    document.getElementById('classicAnswer').focus();
                }
            });

            // Соревнование: кнопки СТАРТ
            document.getElementById('p1StartBtn').addEventListener('click', () => startPlayer(1));
            document.getElementById('p2StartBtn').addEventListener('click', () => startPlayer(2));

            // Соревнование: обработка ввода (Enter)
            document.getElementById('p1Input').addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    handlePlayerAnswer(1);
                }
            });
            document.getElementById('p2Input').addEventListener('keypress', (e) => {
                if (e.key === 'Enter') {
                    e.preventDefault();
                    handlePlayerAnswer(2);
                }
            });

            // Также можно отвечать кнопкой (на случай сенсорных устройств)
            // Добавим невидимые кнопки-обработчики (опционально)
        });
    })();
</script>
</body>
</html>
