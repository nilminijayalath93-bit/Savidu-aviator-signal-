# Savidu-aviator-signal-
1xbet aviator signal 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Savindu Aviator Signal</title>
<style>
body {
    font-family: Arial;
    background:#f0f2f5;
    display:flex;
    justify-content:center;
    padding:20px;
}
.container {
    max-width:600px;
    background:white;
    padding:20px;
    border-radius:12px;
    box-shadow:0 0 10px rgba(0,0,0,0.2);
    text-align:center;
}
h1,h2 { text-align:center; }
table {
    width:100%;
    border-collapse: collapse;
    margin-top:15px;
}
th,td { border:1px solid #ccc; padding:8px; text-align:center; }
.signal-box { background:#e0ffe0; padding:15px; border-radius:10px; margin-bottom:20px; }
button {
    display:block;
    margin:auto;
    padding:10px 20px;
    font-size:16px;
    border:none;
    border-radius:8px;
    background:#0066ff;
    color:white;
    cursor:pointer;
}
input { width:80%; padding:10px; margin-top:10px; border-radius:8px; border:1px solid #ccc; }
</style>
</head>
<body>

<div class="container" id="loginBox">
    <h1>Savindu Aviator</h1>
    <p>Enter your 1xBet ID to continue</p>
    <input type="number" id="userid" placeholder="1xBet ID" required>
    <button onclick="login()">Login</button>
</div>

<div class="container" id="dashboard" style="display:none;">
    <h1>Savindu Aviator Signal</h1>
    <p id="welcome"></p>
    <div class="signal-box">
        <h2>Next Signal</h2>
        <p>Multiplier: <span id="multiplier">-</span>x</p>
        <p>Odd/Even: <span id="odd_even">-</span></p>
        <p>Confidence: <span id="confidence">-</span>%</p>
    </div>

    <h2>Past Games</h2>
    <table>
        <thead>
            <tr>
                <th>Time</th>
                <th>Crash</th>
                <th>Odd/Even</th>
                <th>Probability %</th>
            </tr>
        </thead>
        <tbody id="past_table">
        </tbody>
    </table>
</div>

<script>
let pastGames = [];

// Login function
function login() {
    const id = document.getElementById("userid").value;
    if(id.length < 5){ alert("Invalid ID!"); return; }
    localStorage.setItem("userID", id);
    startDashboard();
}

// Check if already logged in
if(localStorage.getItem("userID")){
    startDashboard();
}

function startDashboard(){
    document.getElementById("loginBox").style.display="none";
    document.getElementById("dashboard").style.display="block";
    const user = localStorage.getItem("userID");
    document.getElementById("welcome").innerText = "Welcome, 1xBet ID: " + user;
    generateSignal();
    setInterval(generateSignal,5000);
}

// Generate random crash
function generateCrash() {
    const crash = (Math.random()*4+1).toFixed(2);
    const odd_even = (Math.floor(crash*10)%2===0)?"Even":"Odd";
    const prob = Math.floor(Math.random()*40+50);
    const time = new Date().toLocaleTimeString();
    const game = {time, crash, odd_even, prob};
    pastGames.push(game);
    if(pastGames.length>20) pastGames.shift();
    return game;
}

// Generate next signal
function generateSignal(){
    const multiplier = (Math.random()*1.8+1.2).toFixed(2);
    const odd_even = (Math.floor(multiplier*10)%2===0)?"Even":"Odd";
    const confidence = Math.floor(Math.random()*25+60);

    document.getElementById("multiplier").innerText=multiplier;
    document.getElementById("odd_even").innerText=odd_even;
    document.getElementById("confidence").innerText=confidence;

    generateCrash();
    updateTable();
}

// Update table
function updateTable(){
    const tbody = document.getElementById("past_table");
    tbody.innerHTML="";
    pastGames.forEach(game=>{
        tbody.innerHTML += `<tr>
        <td>${game.time}</td>
        <td>${game.crash}x</td>
        <td>${game.odd_even}</td>
        <td>${game.prob}%</td>
        </tr>`;
    });
}
</script>

</body>
</html>
