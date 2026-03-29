<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<title>Рандомайзер команды</title>

<!-- библиотека конфетти -->
<script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

<style>
body {
    font-family: Arial;
    text-align: center;
    background: linear-gradient(135deg, #87CEFA, #FFD700);
}

h1 {
    margin-top: 20px;
}

#wheel {
    width: 300px;
    height: 300px;
    border-radius: 50%;
    border: 10px solid white;
    margin: 20px auto;
    position: relative;
    overflow: hidden;
    transform: rotate(0deg);
    transition: transform 4s cubic-bezier(0.33, 1, 0.68, 1);
}

.segment {
    position: absolute;
    width: 50%;
    height: 50%;
    background: red;
    transform-origin: 100% 100%;
}

#pointer {
    width: 0;
    height: 0;
    border-left: 20px solid transparent;
    border-right: 20px solid transparent;
    border-bottom: 30px solid red;
    margin: auto;
}

button {
    padding: 12px 20px;
    margin: 10px;
    border-radius: 10px;
    border: none;
    background: #ff5722;
    color: white;
    cursor: pointer;
}

.characters button {
    margin: 5px;
}

.result {
    font-size: 24px;
    margin: 10px;
}
</style>
</head>

<body>

<h1>🎰 Рандомайзер</h1>

<div id="pointer"></div>
<div id="wheel"></div>

<div class="result" id="player">—</div>
<button onclick="spin()">Крутить</button>

<h2>Выбор персонажа</h2>
<div class="result" id="character">—</div>
<div class="characters" id="characters"></div>

<!-- звук -->
<audio id="spinSound" src="https://actions.google.com/sounds/v1/ambiences/slot_machine.ogg"></audio>

<script>
const players = [
"Участник 1","Участник 2","Участник 3","Участник 4",
"Участник 5","Участник 6","Участник 7","Участник 8"
];

let availablePlayers = [...players];

const characters = [
"Кар-Карыч 🧠 Стратег",
"Бараш 💭 Размышлял",
"Лосяш 📊 Метрик",
"Крош ⚡ Хаос",
"Нюша 💖 UX",
"Копатыч 💼 Бизнес",
"Совунья 🩺 QA",
"Ёжик ⚠️ Риски"
];

let takenCharacters = [];

const wheel = document.getElementById("wheel");
const playerDiv = document.getElementById("player");
const charDiv = document.getElementById("character");
const charContainer = document.getElementById("characters");
const sound = document.getElementById("spinSound");

// создаем колесо
function createWheel() {
    wheel.innerHTML = "";
    const angle = 360 / players.length;

    players.forEach((p, i) => {
        const seg = document.createElement("div");
        seg.className = "segment";
        seg.style.background = `hsl(${i * 45}, 70%, 60%)`;
        seg.style.transform = `rotate(${i * angle}deg) skewY(${90 - angle}deg)`;
        wheel.appendChild(seg);
    });
}

// крутилка
function spin() {
    if (availablePlayers.length === 0) {
        playerDiv.innerText = "Все выбраны!";
        return;
    }

    sound.play();

    const randomIndex = Math.floor(Math.random() * availablePlayers.length);
    const selected = availablePlayers[randomIndex];

    const angle = 360 / players.length;
    const spins = 5;
    const finalDeg = (360 * spins) + (randomIndex * angle);

    wheel.style.transform = `rotate(${finalDeg}deg)`;

    setTimeout(() => {
        playerDiv.innerText = selected;

        // удаляем игрока
        availablePlayers = availablePlayers.filter(p => p !== selected);

        // конфетти 🎉
        confetti({
            particleCount: 150,
            spread: 70,
            origin: { y: 0.6 }
        });

    }, 4000);
}

// персонажи
function renderCharacters() {
    charContainer.innerHTML = "";

    characters.forEach(c => {
        const btn = document.createElement("button");
        btn.innerText = c;

        if (takenCharacters.includes(c)) {
            btn.disabled = true;
        }

        btn.onclick = () => {
            charDiv.innerText = c;
            takenCharacters.push(c);

            confetti({
                particleCount: 100,
                spread: 60
            });

            renderCharacters();
        };

        charContainer.appendChild(btn);
    });
}

createWheel();
renderCharacters();
</script>

</body>
</html>
