<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width" />
  <title>__________</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <h1>__________</h1>
  <div id="test"></div>

  <script src="script.js"></script>
</body>
</html>

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>짱깨뽀 엽전 교환기</title>

<style>
    body {
    margin: 0;
    padding: 0;
    height: 100vh;
    width: 100vw;
    overflow: hidden;
    background: url("https://drive.google.com/uc?export=view&id=11QOUwsHNzAz37-Gma0ybnf0hANwomZ0f") center/cover no-repeat fixed;
    background-size: cover !important;
    font-family: "NanumSquare", sans-serif;
    position: relative;
}

    /* 상단 타이틀 */
    .title-box {
        margin-top: 12px;
        text-align: center;
        color: white;
        text-shadow: 0 3px 6px rgba(0,0,0,0.8);
    }
    .title-box h1 { font-size: 26px; margin: 0; }
    .title-box p { font-size: 11px; opacity: 0.9; }

    /* 코인 UI */
    .coin-box, .total-coin-box {
        position: absolute; right: 12px;
        background: rgba(0,0,0,0.55);
        padding: 8px 12px; border-radius: 8px;
        border: 2px solid #000; z-index: 10;
    }
    .coin-box { top: 12px; color: #F7D93A; font-size: 15px; }
    .total-coin-box { top: 55px; color: #00eaff; font-size: 14px; }

    /* 동전 투입구 */
    .coin-slot {
        position: absolute; right: 18px; top: 105px;
        width: 58px; height: 98px;
        background: linear-gradient(145deg, #d9d9d9, #9c9c9c);
        border: 3px solid black; border-radius: 10px;
        box-shadow: inset 0 0 6px #000;
    }
    .coin-line { width: 70%; height: 8px; background: #000; margin: 20px auto; border-radius: 4px; }

    .side-note {
        position: absolute; right: 12px; top: 220px;
        background: rgba(0,0,0,0.45);
        padding: 10px 14px; border-radius: 8px;
        border: 2px solid #000; color: white; font-size: 12px; line-height: 1.5;
        z-index: 10;
    }

    /* 중앙 원형판 */
    .circle-area {
        position: absolute;
        top: 24%;
        left: 50%;
        transform: translateX(-50%);
        width: 74%;
        aspect-ratio: 1/1;
        background: radial-gradient(circle, #2d2d2d, #0c0c0c);
        border-radius: 50%;
        box-shadow: inset 0 0 40px rgba(255,255,255,0.15), 0 0 25px rgba(255,255,255,0.4);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .rewards { position: relative; width: 92%; height: 92%; }
    .reward {
        width: 22%; aspect-ratio: 1/1;
        background: radial-gradient(circle, #ffffff, #d9d9d9);
        border-radius: 50%;
        position: absolute;
        display: flex; justify-content: center; align-items: center;
        font-size: 1.4rem; font-weight: 700; color: #333;
        box-shadow:
            0 0 18px rgba(255,255,255,0.9),
            inset 0 0 10px rgba(255,255,255,0.9),
            0 0 8px rgba(255,255,255,0.8);
    }

    /* 위치 유지 */
    .reward:nth-child(1) { top: 0%; left: 50%; transform: translate(-50%, -20%); }
    .reward:nth-child(2) { top: 17%; left: 84%; transform: translate(-50%, -50%); }
    .reward:nth-child(3) { top: 50%; left: 100%; transform: translate(-60%, -50%); }
    .reward:nth-child(4) { top: 83%; left: 84%; transform: translate(-50%, -50%); }
    .reward:nth-child(5) { top: 100%; left: 50%; transform: translate(-50%, -80%); }
    .reward:nth-child(6) { top: 83%; left: 16%; transform: translate(-50%, -50%); }
    .reward:nth-child(7) { top: 50%; left: 0%; transform: translate(-40%, -50%); }
    .reward:nth-child(8) { top: 17%; left: 16%; transform: translate(-50%, -50%); }

    /* LED */
    .led-box {
        position: absolute;
        top: 50%; left: 50%;
        transform: translate(-50%, -50%);
    }
    .led-icon {
        font-size: 80px;
        color: red;
        text-shadow: 0 0 8px red, 0 0 18px red, 0 0 38px red;
        animation: ledBlink 0.25s infinite alternate;
    }
    @keyframes ledBlink { from { opacity: 0.5; } to { opacity: 1; } }

    /* 버튼 */
    .buttons {
        position: absolute;
        bottom: 45px;
        width: 100%;
        display: flex; justify-content: center; gap: 25px;
    }
    .btn {
        width: 95px; height: 95px;
        border-radius: 50%;
        border: 4px solid black;
        display: flex; justify-content: center; align-items: center;
        font-size: 20px; font-weight: 700;
        box-shadow: 0 5px 0 black;
        cursor: pointer;
        color: #000;
    }
    .red { background: #ff3e3e; }
    .green { background: #3fd85b; }
    .yellow { background: #f8e44e; }

    .start-label {
        position: absolute;
        bottom: 20px;
        width: 100%;
        text-align: center;
        color: white;
        text-shadow: 0 2px 4px black;
    }

    /* ★★★ 여기부터 "결과 강조" 수정 ★★★ */

    #resultText {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 100%;
        text-align: center;
        font-size: 85px;
        font-weight: 900;
        letter-spacing: 4px;
        opacity: 0;
        text-shadow:
            0 0 15px black,
            0 0 25px black,
            0 0 40px rgba(0,0,0,0.8);
        transition: 0.25s ease-out;
        animation: resultPulse 0.6s infinite alternate ease-in-out;
        pointer-events: none;
        z-index: 9999;
    }

    @keyframes resultPulse {
        from { transform: translate(-50%, -50%) scale(1); }
        to   { transform: translate(-50%, -50%) scale(1.15); }
    }

    /* 상태별 문방구 글씨 느낌 */
    .flash-win  { color: #00ff95; text-shadow: 0 0 18px #00ff95, 0 0 28px #00ff95; }
    .flash-draw { color: #ffe14b; text-shadow: 0 0 18px #ffe14b, 0 0 28px #ffe14b; }
    .flash-lose { color: #ff5454; text-shadow: 0 0 18px #ff5454, 0 0 28px #ff5454; }

</style>
</head>

<body>

<div class="title-box">
    <h1>짱깨뽀 엽전 교환기</h1>
    <p>본 링크는 이벤트용으로 제작되었습니다.</p>
</div>

<div class="coin-box" id="coinBox">엽전 : 10개</div>
<div class="total-coin-box" id="totalCoinBox">누적 : 0개</div>

<div class="coin-slot"><div class="coin-line"></div></div>
<div class="side-note">과한 연타 금지<br>결과는 랜덤입니다<br>운이 좋으면 고보상!</div>

<!-- ★ 결과 표시 ★ -->
<div id="resultText"></div>

<div class="circle-area">
    <div class="rewards">
        <div class="reward">1</div><div class="reward">2</div><div class="reward">3</div><div class="reward">4</div>
        <div class="reward">5</div><div class="reward">6</div><div class="reward">7</div><div class="reward">8</div>
    </div>
    <div class="led-box"><div id="ledIcon" class="led-icon">✊</div></div>
</div>

<div class="buttons">
    <div class="btn red" onclick="startGame('scissors')">가위</div>
    <div class="btn green" onclick="startGame('rock')">바위</div>
    <div class="btn yellow" onclick="startGame('paper')">보</div>
</div>

<div class="start-label">게임 시작</div>

<script>
let coins = 10;
let totalCoins = 0;

const reward = { win: 3, draw: 1, lose: 0 };
const LUCKY_PROB = 0.06;

const coinBox = document.getElementById("coinBox");
const totalCoinBox = document.getElementById("totalCoinBox");
const ledIcon = document.getElementById("ledIcon");
const resultText = document.getElementById("resultText");

/* LED 애니메이션용 */
const sequence = ["✌️","✊","🖐️"];
const mapToRPS = { "✌️":"scissors", "✊":"rock", "🖐️":"paper" };

let spinning = false;

/* 승패 판단 */
function judge(player, machine){
    if(player === machine) return "draw";
    if(player === "rock" && machine === "scissors") return "win";
    if(player === "scissors" && machine === "paper") return "win";
    if(player === "paper" && machine === "rock") return "win";
    return "lose";
}

function flashResult(type){
    resultText.classList.remove("flash-win","flash-draw","flash-lose");
    resultText.classList.add(
        type === "win"  ? "flash-win" :
        type === "draw" ? "flash-draw" : "flash-lose"
    );
    resultText.style.opacity = "1";

    setTimeout(()=> resultText.style.opacity = "0.85", 200);
}

function startGame(playerChoice){
    if(coins <= 0) return alert("엽전이 부족합니다!");
    if(spinning) return;

    coins--;
    totalCoins++;
    coinBox.innerText = `엽전 : ${coins}개`;
    totalCoinBox.innerText = `누적 : ${totalCoins}개`;

    resultText.style.opacity = "0";
    spinning = true;

    let idx = 0;
    let speed = 60;

    function spin(){
        ledIcon.innerText = sequence[idx];
        idx = (idx + 1) % 3;
        speed += 45;

        if(speed < 550){
            setTimeout(spin, speed);
        } else {

            const final = sequence[Math.floor(Math.random() * 3)];
            ledIcon.innerText = final;

            const machine = mapToRPS[final];
            const outcome = judge(playerChoice, machine);

            let gained = reward[outcome];
            const lucky = Math.random() < LUCKY_PROB;
            if(lucky) gained += 5;

            coins += gained;
            coinBox.innerText = `엽전 : ${coins}개`;

            resultText.innerText =
                outcome === "win"  ? `이겼다! +${gained}` :
                outcome === "draw" ? `비겼다..! +${gained}` :
                                     `졌다ㅜ +${gained}`;

            flashResult(outcome);
            spinning = false;
        }
    }

    spin();
}
</script>

</body>
</html>
