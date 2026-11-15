<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>BINGO TACTICS Ver4.3</title>

<style>
body{
    margin:0;
    background:#1c1c1c;
    color:white;
    font-family:Arial,sans-serif;
    text-align:center;
}

.screen{
    padding:20px;
}

.mainBtn{
    width:260px;
    padding:15px;
    margin:10px;
    font-size:20px;
    border:none;
    border-radius:10px;
    cursor:pointer;
    color:white;
}

.quickBtn{
    background:#2196F3;
}

.privateBtn{
    background:#4CAF50;
}

.helpBtn{
    width:55px;
    height:55px;

    border:3px solid white;
    border-radius:50%;

    background:#ff3333;
    color:white;

    font-size:30px;
    font-weight:bold;

    cursor:pointer;

    box-shadow:0 0 20px #ff3333;
}

.subBtn{
    width:220px;
    padding:12px;

    border:none;
    border-radius:10px;

    margin:10px;

    font-size:18px;

    cursor:pointer;
}

.createBtn{
    background:#00BCD4;
    color:white;
}

.joinBtn{
    background:#FF9800;
    color:white;
}

.backBtn{
    padding:10px 20px;

    background:#666;
    color:white;

    border:none;
    border-radius:10px;

    cursor:pointer;
}

.card{
    background:#2a2a2a;

    width:320px;

    margin:15px auto;

    padding:15px;

    border-radius:15px;
}

.roomCard{

    background:#333;

    width:320px;

    margin:12px auto;

    padding:15px;

    border-radius:10px;

    cursor:pointer;

    border:2px solid #666;
}

.roomCard:hover{

    border:2px solid #2196F3;
}

.roomNo{

    font-size:30px;

    color:#FFD700;

    font-weight:bold;
}

.startBtn{

    width:240px;

    padding:15px;

    font-size:22px;

    border:none;
    border-radius:10px;

    background:red;
    color:white;

    cursor:pointer;
}

.popup{

    display:none;

    position:fixed;

    top:50%;
    left:50%;

    transform:translate(-50%,-50%);

    background:#2a2a2a;

    border:2px solid white;

    border-radius:15px;

    width:300px;

    padding:20px;

    z-index:1000;
}

.overlay{

    display:none;

    position:fixed;

    top:0;
    left:0;

    width:100%;
    height:100%;

    background:rgba(0,0,0,0.7);

    z-index:999;
}

input{

    padding:10px;

    width:180px;

    font-size:20px;

    text-align:center;
}
#board{
    width:350px;
    margin:auto;
    display:grid;
    grid-template-columns:repeat(5,65px);
    gap:5px;
    justify-content:center;
}

.cell{
    width:65px;
    height:65px;
    border:2px solid #444;
    border-radius:8px;
    display:flex;
    justify-content:center;
    align-items:center;
    background:white;

    color:black;

    font-size:24px;
    font-weight:bold;
    cursor:pointer;
    user-select:none;
}

.self{
    background:#4d94ff;
    color:white;
}

.self-pending{
background:#b3d1ff;
color:white;
}

.enemy{

background:#ff6666;
color:white;
}

#resultMessage{
position:fixed;
top:50%;
left:50%;
transform:translate(-50%,-50%);
font-size:100px;
font-weight:bold;
color:gold;
text-shadow:
-3px -3px 0 #cc0000,
3px -3px 0 #cc0000,
-3px 3px 0 #cc0000,
3px 3px 0 #cc0000;
z-index:9999;
pointer-events:none;
}

@keyframes joinFlash{
0%{
opacity:1;
transform:scale(1);
}
50%{
opacity:0.5;
transform:scale(1.15);
}
100%{
opacity:1;
transform:scale(1);
}
}

</style>
</head>

<body>

<!-- TOP MENU -->

<div id="menuScreen" class="screen">

<h1>BINGO TACTICS</h1>

<div>

<button
class="mainBtn quickBtn"
onclick="showQuickMatch()">

QUICK MATCH


</button>

<button
class="helpBtn"
onclick="showHelp('quick')">

?

</button>

</div>

<div>

<button
class="mainBtn privateBtn"
onclick="showPrivateMatch()">

PRIVATE MATCH

</button>

<button
class="helpBtn"
onclick="showHelp('private')">

?

</button>

</div>

</div>

<!-- QUICK MATCH -->

<div
id="quickScreen"
class="screen"
style="display:none;">

<h2>QUICK MATCH</h2>

<div
class="roomCard"
onclick="joinQuickRoom('4582')">

<div class="roomNo">
4582
</div>

HOST : Shoshi

<br>

Waiting...

</div>

<div
class="roomCard"
onclick="joinQuickRoom('7124')">

<div class="roomNo">
7124
</div>

HOST : ZEN

<br>

Waiting...

</div>

<div
class="roomCard"
onclick="joinQuickRoom('9011')">

<div class="roomNo">
9011
</div>

HOST : Player

<br>

Waiting...

</div>

<button
class="subBtn createBtn"
onclick="createQuickRoom()">

CREATE ROOM

</button>

<br>

<button
class="backBtn"
onclick="showMenu()">

BACK

</button>

</div>

<!-- PRIVATE MATCH -->

<div
id="privateScreen"
class="screen"
style="display:none;">

<h2>PRIVATE MATCH</h2>

<button
class="subBtn createBtn"
onclick="createPrivateRoom()">

CREATE ROOM

</button>

<br><br>

Room Number

<br><br>

<input
id="privateRoomInput"
placeholder="1234">

<br><br>

<button
class="subBtn joinBtn"
onclick="joinPrivateRoom()">

JOIN

</button>

<br><br>

<button
class="backBtn"
onclick="showMenu()">

BACK

</button>

</div>

<!-- WAIT ROOM -->

<div
id="gameScreen"
class="screen"
style="display:none;"
>
<h1>GAME START</h1>

<h2 id="orderLabel"></h2>

<h2 id="turnLabelGame"></h2>

<div id="resultMessage"></div>

<div id="board"></div>

<br><br>

<button
id="resetBtn"
class="backBtn">
RESET
</button>

<p id="resetStatus" style="display:none;">
HOST RESET ❌<br>
GUEST RESET ❌
</p>

<div id="rematchBox" style="display:none;">

<h2>もう一戦？</h2>

<button id="yesBtn">
〇 YES
</button>

<button id="noBtn">
✕ NO
</button>

</div>

</div>

<div
id="waitScreen"
class="screen"
style="display:none;">

<h2 id="waitTitle"></h2>

<div class="card">

<p>ROOM NUMBER</p>

<div
class="roomNo"
id="waitRoomNo">

0000

</div>

<hr>

<h3>HOST</h3>
<p id="hostLabel">
Shoshi
</p>

<hr>

<h3>GUEST</h3>
<p id="guestLabel">
Waiting...
</p>

<hr>
<h3>HOST READY</h3>
<p id="hostReadyLabel">
NO
</p>

<hr>

<h3>GUEST READY</h3>
<p id="guestReadyLabel">
NO
</p>

<hr>

<h3>CONNECTION</h3>
<p id="readyStatus">
🟡 相手待機中
</p>

<hr>


<h3 id="roleLabel"></h3>

<p id="turnLabel"></p>

</div>

<button
class="startBtn"
onclick="readyUp()">

READY

</button>

<br><br>

<button
class="backBtn"
onclick="showMenu()">

BACK

</button>

</div>

<!-- HELP -->

<div
id="overlay"
class="overlay"
onclick="closeHelp()">
</div>

<div
id="helpPopup"
class="popup">

<h2 id="helpTitle"></h2>

<p id="helpText"></p>

<br>

<button
class="backBtn"
onclick="closeHelp()">

CLOSE

</button>

</div>

<script type="module">

import { initializeApp }
from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";

import {
getFirestore,
doc,
getDoc,
setDoc,
updateDoc,
onSnapshot
}
from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";

const firebaseConfig = {
apiKey: "AIzaSyAfLxgAzWA8ozZOJJHRS795H4u5aBwXE9c",
authDomain: "bt-mobile-f126a.firebaseapp.com",
projectId: "bt-mobile-f126a",
storageBucket: "bt-mobile-f126a.firebasestorage.app",
messagingSenderId: "779653776766",
appId: "1:779653776766:web:230aac9341a4b9bc229f2f",
measurementId: "G-QTSHMQK53V"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
window.db = db;
window.doc = doc;
window.getDoc = getDoc;
window.setDoc = setDoc;
window.updateDoc = updateDoc;
window.onSnapshot = onSnapshot;

console.log("Firebase OK");

</script>

<script>

let roomId = "";
let roomRef = null;
let playerId = "";
let isHost = false;
let pendingIndex = null;
let pendingTimer = null;
let opponentJoined = false;
let gameStartedFlag = false;
let cells = [];
let states = [];
let lastCalledCell = null;
let gameEnded = false;
let resetTimer = null;
let rematchAnnounced = false;
let rematchTimer = null;


async function readyUp(){

    console.log("READY押下");

    if(isHost){

        await updateDoc(roomRef,{
            hostReady:true
 
        });

    }else{

        await updateDoc(roomRef,{
            guestReady:true,

        });

    }

}

function hideAll(){

document.getElementById("menuScreen").style.display="none";
document.getElementById("quickScreen").style.display="none";
document.getElementById("privateScreen").style.display="none";
document.getElementById("waitScreen").style.display="none";
document.getElementById("gameScreen").style.display="none";

}

function showMenu(){

hideAll();

document.getElementById("menuScreen").style.display="block";

}

function showPrivateMatch(){

hideAll();

document.getElementById("privateScreen").style.display="block";

}

function generateRoomNo(){

return Math.floor(1000 + Math.random()*9000);

}

function openWaitRoom(roomNo,isHost){

hideAll();

document.getElementById("waitScreen").style.display="block";

document.getElementById("waitRoomNo").innerText=roomNo;

if(isHost){

document.getElementById("roleLabel").innerText=
"YOU ARE HOST";

document.getElementById("turnLabel").innerText=
"FIRST PLAYER";

document.getElementById("guestLabel").innerText=
"Waiting...";

}else{

document.getElementById("roleLabel").innerText=
"YOU ARE GUEST";

document.getElementById("turnLabel").innerText=
"SECOND PLAYER";

document.getElementById("guestLabel").innerText=
"Shoshi";

}

}

function createQuickRoom(){

document.getElementById("waitTitle").innerText=
"QUICK MATCH";

openWaitRoom(
generateRoomNo(),
true
);

}
async function createPrivateRoom()
{
console.log(db);
console.log(doc);
console.log(setDoc);

roomId = generateRoomNo().toString();

isHost = true;

roomRef = doc(db,"rooms",roomId);

await setDoc(roomRef,{
host:"A",
guest:"",
playerCount:1,
hostReady:false,
guestReady:false,
currentTurn:"HOST",
lastCall:0,
lastCaller:"",
hostFirstCallDone:false,
guestFirstCallDone:false,
winner:"",
hostReset:false,
guestReset:false,

hostRematch:false,
guestRematch:false

});

alert("作成番号:"+roomId);

document.getElementById("waitTitle").innerText =
"PRIVATE MATCH";

openWaitRoom(
roomId,
true
);

onSnapshot(roomRef,async (docSnap)=>{

const data = docSnap.data();

if(!data){
return;
}

console.log(
"HOST SNAPSHOT RAW",
JSON.stringify(data)
);

console.log(
"受信lastCall=",
data.lastCall
);

if(
(isHost && data.lastCaller==="HOST") ||
(!isHost && data.lastCaller==="GUEST")
){
    console.log("自分送信なので赤化スキップ");
}else{

    for(let i=0;i<cells.length;i++){

        if(
            parseInt(cells[i].innerText)
            === data.lastCall
        ){

            states[i] = 3;
            updateCell(i);

let unused = 0;

for(let j=0;j<25;j++){
    if(states[j] === 0){
        unused++;
    }
}

console.log("unused=", unused);
   
 const enemyLines = checkBingo(3);

console.log(
"enemyLines=",
enemyLines
);

/*
if(gameEnded){
    console.log("HOST gameEnded return 発動");
    return;
}
*/

if(
    enemyLines > 0 &&
    !gameEnded &&
    !data.winner
){

    gameEnded = true;

    const result =
    document.getElementById(
    "resultMessage"
    );

    result.innerText =
    "YOU WIN";

    result.style.color =
    "#00ff66";

    if(!rematchTimer){

        rematchTimer = setTimeout(()=>{

            document.getElementById(
                "rematchBox"
            ).style.display = "block";

            rematchTimer = null;

        },3000);

    }

    console.log(
        "HOST WIN WRITE START",
        Date.now(),
        "lastCall=",
        data.lastCall
    );

    await updateDoc(roomRef,{
        winner:"HOST"
    });

    console.log(
        "HOST WIN WRITE END",
        Date.now()
    );

}
else if(unused === 1){

    const result =
    document.getElementById("resultMessage");

    result.innerText = "DRAW";
    result.style.color = "#00BFFF";
    result.style.fontSize = "140px";
    result.style.fontWeight = "bold";
    result.style.webkitTextStroke = "2px black";

    gameEnded = true;

    await updateDoc(roomRef,{
        winner:"DRAW"
    });


}

            if(lastCalledCell){
                lastCalledCell.style.border =
                "2px solid #444";
            }

            cells[i].style.border =
            "5px solid yellow";

            lastCalledCell = cells[i];
        }
    }
}
if(
    data.hostReady &&
    data.guestReady &&
    !data.gameStarted &&
    isHost
){

    updateDoc(roomRef,{
        gameStarted:true
    });

}

if(
data.playerCount >= 2 &&
!opponentJoined
){

 opponentJoined = true;

    const guestLabel =
    document.getElementById(
    "guestLabel"
    );

    guestLabel.innerText =
    "⚡ PLAYER JOINED! ⚡";

    guestLabel.style.color =
    "#00ff66";

    guestLabel.style.fontSize =
    "32px";

    guestLabel.style.fontWeight =
    "bold";

    guestLabel.style.textShadow =
    "0 0 10px #00ff66";

    guestLabel.style.animation =
    "joinFlash 1s infinite";

    alert("相手が参加しました");

}

const readyStatus =
document.getElementById("readyStatus");

if(data.playerCount < 2){

    readyStatus.innerText =
    "🟡 相手待機中";

}else{

    if(data.hostReady &&
       data.guestReady){

        readyStatus.innerText =
        "✅ 対戦可能";

    }else{

        const opponentReady =
        data.guestReady;

        if(opponentReady){

            readyStatus.innerText =
            "🟢 相手準備完了";

        }else{

            readyStatus.innerText =
            "🔴 相手未準備";

        }

    }

}


if(data.hostReady){

document.getElementById(
"hostReadyLabel"
).innerText = "READY";

}

const winner = data.winner;

console.log(
"LOSE CHECK",
winner,
isHost,
gameEnded
);

if(winner === "DRAW"){

    const result =
    document.getElementById("resultMessage");

    result.innerText = "DRAW";
    result.style.color = "#00BFFF";
    result.style.fontSize = "18vw";
    result.style.fontWeight = "bold";
    result.style.webkitTextStroke = "2px black";

    gameEnded = true;

    if(!rematchTimer){
        rematchTimer = setTimeout(()=>{
            document.getElementById(
                "rematchBox"
            ).style.display = "block";

            rematchTimer = null;
        },3000);
    }

    console.log("DRAW処理終了");
    
}


else if(
winner &&
winner !== (isHost ? "HOST" : "GUEST")
){

console.log(
"LOSE受信詳細",
winner,
data.lastCall,
data.currentTurn,
data.hostReset,
data.guestReset
);

    if(!gameEnded){

        console.log(
        "LOSE処理突入",
        winner,
        isHost,
        gameEnded
        );

        gameEnded = true;

        const result =
        document.getElementById(
        "resultMessage"
        );

        result.innerText = "YOU LOSE";
        result.style.color = "#A020F0";

        if(!rematchTimer){

            rematchTimer = setTimeout(()=>{

                console.log(
                "REMATCH BOX OPEN",
                Date.now()
                );

                document.getElementById(
                "rematchBox"
                ).style.display = "block";

                rematchTimer = null;

            },3000);

        }

    }

}
const currentTurn = data.currentTurn;

console.log("HOST SNAPSHOT");
console.log(data);

console.log(
    "currentTurn=",
    currentTurn,
    "isHost=",
    isHost
);
console.log(
"RESET STATUS",
data.hostReset,
data.guestReset
);
document.getElementById(
"resetStatus"
).innerHTML =
"HOST RESET " +
(data.hostReset ? "✅" : "❌")
+
"<br>" +
"GUEST RESET " +
(data.guestReset ? "✅" : "❌");

if(
    data.hostReset &&
    data.guestReset
){

if(rematchTimer){
    clearTimeout(rematchTimer);
    rematchTimer = null;
    console.log("REMATCH TIMER STOP");
}

console.log("両者RESET成立");

    document.getElementById(
    "resetStatus"
    ).style.display = "none";

    document.getElementById(
    "resetBtn"
    ).style.display = "none";

    document.getElementById(
    "rematchBox"
    ).style.display = "none";

    rematchAnnounced = false;
console.log(
"UI CHECK",
document.getElementById("rematchBox").style.display,
document.getElementById("resetBtn").style.display
);
}

if(
    data.hostReset &&
    data.guestReset &&
    isHost
){

console.log("HOST RESET条件到達");

console.log(
"HOST RESET DATA",
JSON.stringify(data)
);

console.log("両者RESET成立");

document.getElementById(
"resetStatus"
).style.display = "none";

document.getElementById(
"resetBtn"
).style.display = "none";

document.getElementById(
"rematchBox"
).style.display = "none";

rematchAnnounced = false;

if(lastCalledCell){
    lastCalledCell.style.border =
    "2px solid #444";
}

createBoard();

console.log(
"HOST RESET後 enemyLines=",
checkBingo(3)
);

lastCalledCell = null;
pendingIndex = null;

document.getElementById(
"resultMessage"
).innerText = "";


console.log("RESET COMPLETE HOST");

console.log("RESET書込み開始");

await updateDoc(roomRef,{
    hostReset:false,
    guestReset:false,
    hostRematch:false,
    guestRematch:false,

    hostFirstCallDone:false,
    guestFirstCallDone:false,

    lastCall:0,
    lastCaller:"",
    winner:"",
    currentTurn:"HOST"
});

const snap = await getDoc(roomRef);

console.log(
"RESET後確認",
JSON.stringify(snap.data())
);

console.log("RESET書込み完了");

setTimeout(()=>{

    gameEnded = false;

    console.log(
    "gameEnded解除"
    );

},1000);

return;

}

console.log(
"REMATCH STATUS",
data.hostRematch,
data.guestRematch,
rematchAnnounced,
"winner=",
data.winner,
"hostReset=",
data.hostReset,
"guestReset=",
data.guestReset
);

console.log(
"再戦判定",
data.hostRematch,
data.guestRematch,
rematchAnnounced,
gameEnded
);

if(
data.hostRematch &&
data.guestRematch &&
!rematchAnnounced
){
console.log("再戦成立ブロック実行");
if(
data.hostReset ||
data.guestReset
){
    return;
}

if(gameEnded === false){
    return;
}

console.log("再戦成立ブロック実行");

    rematchAnnounced = true;

    alert("再戦成立");

    document.getElementById(
    "resetBtn"
    ).style.display = "inline-block";

    document.getElementById(
    "resetStatus"
    ).style.display = "block";

    document.getElementById(
    "resetStatus"
    ).innerHTML =
    "HOST RESET ❌<br>GUEST RESET ❌";
}

/*
if(
data.hostRematch ||
data.guestRematch
){

document.getElementById(
"resetStatus"
).innerHTML =
"HOST REMATCH " +
(data.hostRematch ? "✅" : "❌")
+
"<br>"
+
"GUEST REMATCH " +
(data.guestRematch ? "✅" : "❌");


}
*/

document.getElementById(
"resetStatus"
).innerHTML =
"HOST RESET " +
(data.hostReset ? "✅" : "❌")
+
"<br>GUEST RESET " +
(data.guestReset ? "✅" : "❌");


if(
    data.hostReset &&
    data.guestReset
){

console.log("RESET COMPLETE前");

console.log("GUEST RESET処理開始");

    document.getElementById(
    "resetStatus"
    ).style.display = "none";

    document.getElementById(
    "resetBtn"
    ).style.display = "none";

    document.getElementById(
    "rematchBox"
    ).style.display = "none";

    rematchAnnounced = false;

    if(lastCalledCell){
        lastCalledCell.style.border =
        "2px solid #444";
    }

    createBoard();

console.log(
"GUEST RESET後 enemyLines=",
checkBingo(3)
);

lastCalledCell = null;
pendingIndex = null;
   
    document.getElementById(
    "resultMessage"
    ).innerText = "";

    gameEnded = false;

console.log(
"RESET COMPLETE",
rematchAnnounced
);

console.log(
"GUEST RESET COMPLETE",
JSON.stringify(data)
);

setTimeout(()=>{

console.log(
"3秒後UI確認",
document.getElementById(
"rematchBox"
).style.display,
document.getElementById(
"resetBtn"
).style.display
);

},3500);

}

if(
    data.hostFirstCallDone &&
    data.guestFirstCallDone
){

    document.getElementById(
    "orderLabel"
).innerText =
"🟢 Connected";

}

console.log("currentTurn=", currentTurn);

if(currentTurn){

    if(isHost){

        document.getElementById(
            "turnLabelGame"
        ).innerText =
        currentTurn==="HOST"
        ? "あなたのターン"
        : "相手のターン";

    }else{

        document.getElementById(
            "turnLabelGame"
        ).innerText =
        currentTurn==="GUEST"
        ? "あなたのターン"
        : "相手のターン";
    }

    console.log(
        "currentTurn=",
        currentTurn
    );

    console.log(
        "turnLabelGame=",
        document.getElementById("turnLabelGame").innerText
    );

}

if(data.guestReady){

document.getElementById(
"guestReadyLabel"
).innerText = "READY";

}

if(
    data.gameStarted &&
    !gameStartedFlag
){

    gameStartedFlag = true;

    console.log("START GAME実行");

    startGame();

}
});
}

function joinQuickRoom(roomNo){

document.getElementById("waitTitle").innerText=
"QUICK MATCH";

openWaitRoom(
roomNo,
false
);

}

async function joinPrivateRoom(){

isHost = false;

roomId =
document.getElementById("privateRoomInput").value;

if(roomId===""){
alert("ルーム番号を入力してください");
return;
}

roomRef = doc(db,"rooms",roomId);

const snap = await getDoc(roomRef);

if(!snap.exists()){

alert("ルームが存在しません");

return;

}

await updateDoc(roomRef,{
guest:"B",
playerCount:2
});

document.getElementById("waitTitle").innerText=
"PRIVATE MATCH";

openWaitRoom(
roomId,
false
);

onSnapshot(roomRef,async (docSnap)=>{
const data = docSnap.data();

if(!data){
return;
}


console.log("GUEST SNAPSHOT");
console.log(data);

console.log(
"受信lastCall=",
data.lastCall
);


if(
(isHost && data.lastCaller==="HOST") ||
(!isHost && data.lastCaller==="GUEST")
){
    console.log("自分送信なので赤化スキップ");
}else{

    for(let i=0;i<cells.length;i++){

        if(
            parseInt(cells[i].innerText)
            === data.lastCall
        ){
states[i] = 3;
updateCell(i);

let unused = 0;

for(let j=0;j<25;j++){
    if(states[j] === 0){
        unused++;
    }
}

const enemyLines = checkBingo(3);

console.log(
"enemyLines=",
enemyLines
);

console.log(
"敵ライン判定",
enemyLines,
"lastCall=",
data.lastCall,
"winner=",
data.winner
);

/*
if(gameEnded){
    return;
}

*/
if(
    enemyLines > 0 &&
    !gameEnded &&
    !data.winner
){

    console.log(
    "GUEST winner書込み実行",
    Date.now(),
    "lastCall=",
    data.lastCall,
    "gameEnded=",
    gameEnded
    );

    gameEnded = true;

    const result =
    document.getElementById("resultMessage");

    result.innerText = "YOU WIN";

    result.style.color = "#00ff66";

    if(!rematchTimer){

        rematchTimer = setTimeout(()=>{

            document.getElementById(
            "rematchBox"
            ).style.display = "block";

            rematchTimer = null;

        },3000);

    }

    console.log(
    "winner:GUEST 書込み"
    );

console.log(
"★★★★★ GUEST WIN WRITE ★★★★★",
Date.now(),
"enemyLines=",
enemyLines,
"winnerBefore=",
data.winner,
"lastCall=",
data.lastCall,
"gameEnded=",
gameEnded
);

console.log(
"★★★★★ GUEST WIN WRITE START ★★★★★",
Date.now(),
"lastCall=",
data.lastCall
);

await updateDoc(roomRef,{
    winner:"GUEST"
});

console.log(
"★★★★★ GUEST WIN WRITE END ★★★★★",
Date.now()
);

}

else if(unused === 1){

    const result =
    document.getElementById("resultMessage");

    result.innerText = "DRAW";

    result.style.color = "#00BFFF";

    gameEnded = true;

    await updateDoc(roomRef,{
        winner:"DRAW"
    });

}

console.log("WIN処理終了");

}

if(lastCalledCell){

            
                lastCalledCell.style.border =
                "2px solid #444";
            }

            cells[i].style.border =
            "5px solid yellow";

            lastCalledCell = cells[i];
        }
    }



if(data.hostReady){
console.log("turn更新処理へ");
document.getElementById(
"hostReadyLabel"
).innerText="READY";
}

if(data.guestReady){
document.getElementById(
"guestReadyLabel"
).innerText="READY";
}

const readyStatus =
document.getElementById("readyStatus");

if(data.playerCount < 2){

    readyStatus.innerText =
    "🟡 HOST待機中";

}else{

    if(data.hostReady &&
       data.guestReady){

        readyStatus.innerText =
        "✅ 対戦可能";

    }else{

        const opponentReady =
        data.hostReady;

        if(opponentReady){

            readyStatus.innerText =
            "🟢 HOST準備完了";

        }else{

            readyStatus.innerText =
            "🔴 HOST未準備";

        }

    }

}

const winner = data.winner;

console.log(
"WINNER WATCH",
winner,
"lastCall=",
data.lastCall,
"hostReset=",
data.hostReset,
"guestReset=",
data.guestReset
);

console.log(
"LOSE CHECK",
winner,
isHost,
gameEnded
);


if(winner === "DRAW"){

    const result =
    document.getElementById("resultMessage");

    result.innerText = "DRAW";
    result.style.color = "#00BFFF";
    result.style.fontSize = "18vw";
    result.style.fontWeight = "bold";
    result.style.webkitTextStroke = "2px black";

    gameEnded = true;

    if(!rematchTimer){
        rematchTimer = setTimeout(()=>{
            document.getElementById(
                "rematchBox"
            ).style.display = "block";

            rematchTimer = null;
        },3000);
    }

    console.log("DRAW処理終了");
    
}

else if(
winner &&
winner !== (isHost ? "HOST" : "GUEST")
){

    if(!gameEnded){

        console.log(
        "LOSE処理突入",
        winner,
        isHost,
        gameEnded
        );

        gameEnded = true;

        const result =
        document.getElementById(
        "resultMessage"
        );

        result.innerText = "YOU LOSE";
        result.style.color = "#A020F0";

        if(!rematchTimer){

            rematchTimer = setTimeout(()=>{

                console.log(
                "REMATCH BOX OPEN",
                Date.now()
                );

                document.getElementById(
                "rematchBox"
                ).style.display = "block";

                rematchTimer = null;

            },3000);

        }

    }

}
const currentTurn = data.currentTurn;

console.log(
data.hostReset,
data.guestReset
);

console.log(
"RESET STATUS",
data.hostReset,
data.guestReset
);
document.getElementById(
"resetStatus"
).innerHTML =
"HOST RESET " +
(data.hostReset ? "✅" : "❌")
+
"<br>" +
"GUEST RESET " +
(data.guestReset ? "✅" : "❌");

if(
    data.hostReset &&
    data.guestReset
){

if(rematchTimer){
    clearTimeout(rematchTimer);
    rematchTimer = null;
    console.log("REMATCH TIMER STOP");
}

    document.getElementById(
    "resetStatus"
    ).style.display = "none";

    document.getElementById(
    "resetBtn"
    ).style.display = "none";

    document.getElementById(
    "rematchBox"
    ).style.display = "none";

    rematchAnnounced = false;

    if(lastCalledCell){
        lastCalledCell.style.border =
        "2px solid #444";
    }

    createBoard();

    lastCalledCell = null;
    pendingIndex = null;

    document.getElementById(
    "resultMessage"
    ).innerText = "";

    gameEnded = false;

console.log(
"RESET COMPLETE",
rematchAnnounced
);

setTimeout(()=>{

console.log(
"3秒後UI確認",
document.getElementById(
"rematchBox"
).style.display,
document.getElementById(
"resetBtn"
).style.display
);

},3500);

}

console.log(
"REMATCH STATUS",
data.hostRematch,
data.guestRematch,
rematchAnnounced,
"winner=",
data.winner,
"hostReset=",
data.hostReset,
"guestReset=",
data.guestReset
);

console.log(
"GUEST REMATCH CHECK",
data.hostRematch,
data.guestRematch,
rematchAnnounced,
"winner=",
data.winner,
"hostReset=",
data.hostReset,
"guestReset=",
data.guestReset
);

console.log(
"再戦判定",
data.hostRematch,
data.guestRematch,
rematchAnnounced,
gameEnded
);

if(
data.hostRematch &&
data.guestRematch &&
!rematchAnnounced
){

if(
data.hostReset ||
data.guestReset
){
    return;
}

if(gameEnded === false){
    return;
}

console.log("再戦成立ブロック実行");

    rematchAnnounced = true;

    alert("再戦成立");

    document.getElementById(
    "resetBtn"
    ).style.display = "inline-block";

    document.getElementById(
    "resetStatus"
    ).style.display = "block";

    document.getElementById(
    "resetStatus"
    ).innerHTML =
    "HOST RESET ❌<br>GUEST RESET ❌";
}

if(
    data.hostFirstCallDone &&
    data.guestFirstCallDone
){

    document.getElementById(
    "orderLabel"
).innerText =
"🟢 Connected";

}

if(currentTurn){

    if(isHost){

        document.getElementById(
            "turnLabelGame"
        ).innerText =
        currentTurn==="HOST"
        ? "あなたのターン"
        : "相手のターン";

    }else{

        document.getElementById(
            "turnLabelGame"
        ).innerText =
        currentTurn==="GUEST"
        ? "あなたのターン"
        : "相手のターン";

    }

}

if(
    data.gameStarted &&
    !gameStartedFlag
){

    gameStartedFlag = true;

    console.log("START GAME実行");

    startGame();

}
});
}

async function nextTurn(){

    console.log("① NEXT TURN押下");

    const snap = await getDoc(roomRef);

    console.log("② SNAP取得成功");

    const data = snap.data();

    console.log("③ DATA取得", data);

    if(!data){
        console.log("④ dataなし");
        return;
    }

    const nextTurn =
        data.currentTurn === "HOST"
        ? "GUEST"
        : "HOST";

    console.log("⑤ nextTurn=", nextTurn);

    await updateDoc(roomRef,{
        currentTurn: nextTurn
    });

    console.log("⑥ Firestore更新完了");

}

function startGame(){

console.log("startGame開始");

hideAll();

console.log("hideAll後");

document.getElementById(
"gameScreen"
).style.display="block";

console.log("gameScreen表示後");

if(isHost){

document.getElementById(
"orderLabel"
).innerText =
"あなたが先攻";

document.getElementById(
"turnLabelGame"
).innerText =
"あなたのターン";

}else{

document.getElementById(
"orderLabel"
).innerText =
"あなたが後攻";

document.getElementById(
"turnLabelGame"
).innerText =
"相手のターン";

}

createBoard();

document.getElementById(
"resetBtn"
).style.display = "none";

document.getElementById(
"resetBtn"
).onclick =
resetBoard;

document.getElementById(
"rematchBox"
).style.display = "none";

document.getElementById(
"resetStatus"
).style.display = "none";

document.getElementById(
"resetBtn"
).style.display = "none";

rematchAnnounced = false;

document.getElementById(
"resetStatus"
).innerHTML =

"HOST RESET ❌<br>GUEST RESET ❌";

}

function updateCell(index){

const cell = cells[index];

cell.className = "cell";

switch(states[index]){

case 2:
cell.classList.add("self-pending");
break;

case 3:
cell.classList.add("enemy");
break;

case 4:
cell.classList.add("self");
break;

}

}

function checkBingo(type){

const lines = [

[0,1,2,3,4],
[5,6,7,8,9],
[10,11,12,13,14],
[15,16,17,18,19],
[20,21,22,23,24],

[0,5,10,15,20],
[1,6,11,16,21],
[2,7,12,17,22],
[3,8,13,18,23],
[4,9,14,19,24],

[0,6,12,18,24],
[4,8,12,16,20]

];

let completedLines = 0;

for(const line of lines){

let bingo = true;

for(const index of line){

if(states[index] !== type){

bingo = false;
break;

}

}

if(bingo){

completedLines++;

}

}

return completedLines;

}
async function confirmCell(index){

states[index] = 4;
updateCell(index);

if(lastCalledCell){
    lastCalledCell.style.border =
    "2px solid #444";
}

cells[index].style.border =
"5px solid yellow";

lastCalledCell = cells[index];

const number =
parseInt(cells[index].innerText);


  await updateDoc(roomRef,{
    lastCall:number,
    lastCaller:isHost ? "HOST" : "GUEST",
    currentTurn:isHost ? "GUEST" : "HOST"
});

if(isHost){

    await updateDoc(roomRef,{
        hostFirstCallDone:true
    });

}else{

    await updateDoc(roomRef,{
        guestFirstCallDone:true
    });

}
/*
const myLines = checkBingo(4);

console.log(
"myLines=",
myLines
);

if(myLines > 0){

const result =
document.getElementById(
"resultMessage"
);

result.innerText =
"YOU WIN";

result.style.color =
"#00ff66";


await updateDoc(roomRef,{
    winner:isHost ? "HOST" : "GUEST"
});

}
*/
const snap = await getDoc(roomRef);

console.log(
    "保存確認 currentTurn=",
    snap.data().currentTurn
);
    console.log(
        "lastCall送信 =",
        number
    );

    pendingIndex = null;

}

async function resetBoard(){

if(!gameEnded){
    alert("勝敗決定後のみリセット可能");
    return;
}
/*
createBoard();

lastCalledCell = null;
pendingIndex = null;

rematchAnnounced = false;

console.log(
"rematchAnnounced reset"
);

document.getElementById(
"rematchBox"
).style.display = "none";

document.getElementById(
"resetStatus"
).style.display = "none";

document.getElementById(
"resetBtn"
).style.display = "none";

document.getElementById(
"resultMessage"
).innerText = "";

gameEnded = false;

*/

if(isHost){

    await updateDoc(roomRef,{
        hostReset:true
    });

}else{

    await updateDoc(roomRef,{
        guestReset:true
    });

}

}

function createBoard(){

const board =
document.getElementById("board");

board.innerHTML = "";

cells = [];
states = [];

let numbers = [];

for(let i=1;i<=25;i++){
    numbers.push(i);
}

for(let i=numbers.length-1;i>0;i--){

    const j =
    Math.floor(Math.random()*(i+1));

    [numbers[i],numbers[j]] =
    [numbers[j],numbers[i]];
}

for(let i=0;i<25;i++){

    const cell =
    document.createElement("div");

    cell.className = "cell";

    cell.innerText =
    numbers[i];

    cells.push(cell);

    states.push(0);

   cell.onclick = function(){
     handleTap(i);
};

board.appendChild(cell);

}

}

async function handleTap(index){

    console.log(
        "現在表示=",
        document.getElementById("turnLabelGame").innerText
    );

    if(
        document.getElementById("turnLabelGame").innerText
        !== "あなたのターン"
    ){
        console.log("ターン外なので停止");
        return;
    }

    const number =
    parseInt(cells[index].innerText);

    console.log("CALL =",number);

    if(pendingIndex !== null){

        clearTimeout(pendingTimer);

        if(pendingIndex !== index){

            states[pendingIndex] = 0;
            updateCell(pendingIndex);

        }
    }

if(states[index] === 0){

states[index] = 2;
updateCell(index);

pendingIndex = index;

pendingTimer = setTimeout(()=>{
    confirmCell(index);
},2000);

}else if(states[index] === 2){

states[index] = 0;
updateCell(index);

pendingIndex = null;

}

}

function showHelp(type){

document.getElementById("overlay").style.display="block";
document.getElementById("helpPopup").style.display="block";

if(type==="quick"){

document.getElementById("helpTitle").innerText=
"QUICK MATCH";

document.getElementById("helpText").innerText=
"公開ルームに参加するモードです。ルーム番号をタップして参加できます。";

}else{

document.getElementById("helpTitle").innerText=
"PRIVATE MATCH";

document.getElementById("helpText").innerText=
"ルーム番号を共有した相手と対戦できます。";

}

}

function closeHelp(){

document.getElementById("overlay").style.display="none";
document.getElementById("helpPopup").style.display="none";

}

document.getElementById(
"yesBtn"
).onclick = async function(){

console.log(
"YES CLICK",
new Date().getTime()
);

console.log("YES押下");

if(isHost){

console.log("HOST送信開始");
await updateDoc(roomRef,{
hostRematch:true
});

console.log("HOST送信成功");

}else{

console.log("GUEST送信開始");

await updateDoc(roomRef,{
guestRematch:true
});

console.log("GUEST送信成功");

}

alert("YES送信");

};

document.getElementById(
"noBtn"
).onclick = function(){

alert("NO");

};


</script>

</body>
</html>
