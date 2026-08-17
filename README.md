<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">

<title>AKONRUNER</title>

<style>
*{
  box-sizing:border-box;
  -webkit-tap-highlight-color:transparent;
}

html,body{
  margin:0;
  width:100%;
  height:100%;
  overflow:hidden;
  background:#07101d;
  font-family:Arial,sans-serif;
}

body{
  touch-action:none;
}

#game{
  position:absolute;
  inset:0;
  width:100%;
  height:100%;
  display:block;
  background:#07101d;
}

/* LOADING */
#loading{
  position:absolute;
  inset:0;
  z-index:20;
  display:flex;
  justify-content:center;
  align-items:center;
  background:
    radial-gradient(circle at center,#17345b,#07101d 70%);
  color:white;
  text-align:center;
}

.loadingBox{
  width:90%;
  max-width:420px;
}

.logo{
  font-size:48px;
  font-weight:900;
  letter-spacing:4px;
  text-shadow:0 0 25px #42d9ff;
}

.subtitle{
  color:#9bb0c7;
  font-size:11px;
  letter-spacing:4px;
  margin:8px 0 25px;
}

.loader{
  width:100%;
  height:7px;
  background:#ffffff18;
  border-radius:20px;
  overflow:hidden;
}

#bar{
  width:0%;
  height:100%;
  background:linear-gradient(90deg,#42d9ff,#ffd35a);
}

#loadingText{
  margin-top:10px;
  color:#9bb0c7;
  font-size:12px;
}

/* MENU */
#menu{
  position:absolute;
  inset:0;
  z-index:15;
  display:none;
  align-items:center;
  justify-content:center;
  padding:20px;
  background:#02060bd9;
}

.card{
  width:min(420px,92vw);
  padding:25px;
  border-radius:22px;
  text-align:center;
  color:white;
  background:linear-gradient(145deg,#12243b,#091321);
  border:1px solid #ffffff20;
  box-shadow:0 20px 70px #000b;
}

.card h1{
  margin:0;
  font-size:45px;
  letter-spacing:3px;
}

.card p{
  color:#91a6bd;
  font-size:13px;
  line-height:1.6;
}

select{
  width:100%;
  padding:13px;
  margin:7px 0;
  border:0;
  border-radius:10px;
  background:#eef5fb;
  color:#111;
  font-weight:bold;
}

#start{
  width:100%;
  margin-top:15px;
  padding:15px;
  border:0;
  border-radius:12px;
  background:linear-gradient(135deg,#ffd35a,#ff852c);
  color:#111;
  font-size:17px;
  font-weight:900;
}

/* HUD */
#hud{
  position:absolute;
  top:10px;
  left:10px;
  z-index:5;
  display:none;
  padding:8px 12px;
  border-radius:10px;
  background:#07101dcc;
  border:1px solid #ffffff20;
  color:white;
}

#hud small{
  display:block;
  color:#91a6bd;
  font-size:9px;
}

#hud b{
  font-size:19px;
}

/* PAUSE */
#pause{
  position:absolute;
  right:10px;
  top:10px;
  z-index:6;
  display:none;
  padding:9px 13px;
  border:1px solid #ffffff25;
  border-radius:10px;
  background:#07101ddd;
  color:white;
  font-weight:bold;
}

/* JUMP */
#jump{
  position:absolute;
  right:15px;
  bottom:15px;
  z-index:6;
  display:none;
  width:78px;
  height:78px;
  border:0;
  border-radius:50%;
  background:linear-gradient(145deg,#ffd35a,#ff852c);
  color:#111;
  font-weight:900;
  box-shadow:0 8px 25px #0008;
}

/* PAUSE SCREEN */
#pauseScreen{
  position:absolute;
  inset:0;
  z-index:12;
  display:none;
  align-items:center;
  justify-content:center;
  background:#0009;
}

#resume{
  border:0;
  padding:12px 25px;
  border-radius:10px;
  background:#ffd35a;
  color:#111;
  font-weight:900;
}

/* GAME OVER */
#gameOver{
  position:absolute;
  inset:0;
  z-index:13;
  display:none;
  align-items:center;
  justify-content:center;
  background:#02060bd9;
}

#gameOver h2{
  font-size:30px;
}

#finalScore{
  color:#ffd35a;
  font-size:50px;
  font-weight:900;
}

#again{
  border:0;
  padding:13px 25px;
  border-radius:10px;
  background:linear-gradient(135deg,#ffd35a,#ff852c);
  font-weight:900;
}
</style>
</head>

<body>

<canvas id="game"></canvas>

<!-- LOADING SCREEN -->
<div id="loading">
  <div class="loadingBox">

    <div class="logo">
      AKONRUNER
    </div>

    <div class="subtitle">
      ENDLESS RUNNER
    </div>

    <div class="loader">
      <div id="bar"></div>
    </div>

    <div id="loadingText">
      Loading game...
    </div>

  </div>
</div>


<!-- START MENU -->
<div id="menu">

  <div class="card">

    <h1>AKONRUNER</h1>

    <p>
      Run as far as you can.<br>
      Jump over obstacles and beat your best score.
    </p>

    <select id="difficulty">
      <option value="easy">Easy</option>
      <option value="normal" selected>Normal</option>
      <option value="hard">Hard</option>
    </select>

    <select id="music">
      <option value="on" selected>Sweet Music ON</option>
      <option value="off">Music OFF</option>
    </select>

    <button id="start">
      START GAME
    </button>

    <p>
      Tap the screen or press JUMP to jump.
    </p>

  </div>

</div>


<!-- SCORE -->
<div id="hud">
  <small>SCORE</small>
  <b id="score">0</b>
</div>


<!-- PAUSE -->
<button id="pause">
  Ⅱ PAUSE
</button>


<!-- JUMP -->
<button id="jump">
  JUMP
</button>


<!-- PAUSE SCREEN -->
<div id="pauseScreen">

  <div class="card">

    <h2>GAME PAUSED</h2>

    <p>
      Your run is waiting.
    </p>

    <button id="resume">
      RESUME
    </button>

  </div>

</div>


<!-- GAME OVER -->
<div id="gameOver">

  <div class="card">

    <h2>GAME OVER</h2>

    <p>Your Score</p>

    <div id="finalScore">
      0
    </div>

    <p id="bestScore">
      Best score: 0
    </p>

    <button id="again">
      PLAY AGAIN
    </button>

  </div>

</div>


<script>

/* =========================
   GAME SETUP
========================= */

const canvas =
  document.getElementById("game");

const ctx =
  canvas.getContext("2d");

let W = 1000;
let H = 600;

canvas.width = W;
canvas.height = H;

const ground = 485;


/* =========================
   PLAYER
========================= */

const player = {

  x:100,

  y:385,

  width:90,

  height:90,

  velocityY:0,

  jumping:false

};


/* =========================
   SETTINGS
========================= */

const settings = {

  easy:{
    speed:4,
    gravity:.55,
    jump:-13,
    spawn:100
  },

  normal:{
    speed:6,
    gravity:.65,
    jump:-14,
    spawn:78
  },

  hard:{
    speed:8,
    gravity:.75,
    jump:-15,
    spawn:58
  }

};


let difficulty = "normal";

let speed = 6;

let gravity = .65;

let jumpPower = -14;

let spawnTime = 78;

let spawnCounter = 78;

let running = false;

let paused = false;

let score = 0;

let best =
  Number(
    localStorage.getItem("akonrunnerBest") || 0
  );

let frame = 0;

let obstacles = [];

let coins = [];


/* =========================
   PLAYER IMAGE
========================= */

const playerImage =
  new Image();

/*
  This is a simple built-in
  character. You can replace
  this with your own image later.
*/

playerImage.src =
  "data:image/svg+xml;charset=UTF-8," +
  encodeURIComponent(`
  <svg xmlns="http://www.w3.org/2000/svg"
       width="200"
       height="200">

    <circle cx="100"
            cy="100"
            r="96"
            fill="#ffd35a"/>

    <circle cx="70"
            cy="75"
            r="10"
           
