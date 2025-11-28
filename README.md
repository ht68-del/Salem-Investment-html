<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dark Mode Game Wallet + Dashboard</title>
<style>
body{margin:0;font-family:Arial,sans-serif;background:#111;color:#eee;}
.container{max-width:600px;margin:20px auto;background:#1c1c1c;padding:20px;border-radius:10px;box-shadow:0 5px 15px rgba(0,0,0,0.7);}
h2,h3,h4{text-align:center;margin-bottom:15px;color:#fff;}
button{padding:10px 15px;margin:5px;border:none;border-radius:6px;cursor:pointer;transition:0.2s;background:#007bff;color:#fff;}
button:hover{opacity:0.9;}
input,select{padding:8px;width:100%;margin:5px 0;border-radius:5px;border:1px solid #555;background:#222;color:#fff;}
#spinWheel{width:200px;height:200px;border-radius:50%;border:5px solid #0f0;margin:15px auto;display:flex;justify-content:center;align-items:center;font-size:24px;font-weight:bold;cursor:pointer;color:#fff;background:radial-gradient(circle,#333,#111);}
#spinResult{color:#0f0;font-weight:bold;text-align:center;}
.bottomNav{position:fixed;bottom:0;width:100%;background:#1c1c1c;display:flex;justify-content:space-around;padding:10px 0;border-top:1px solid #555;}
.bottomNav button{flex:1;margin:0;border-radius:0;}
table{width:100%;border-collapse:collapse;margin-top:10px;background:#222;}
table,th,td{border:1px solid #555;}
th,td{padding:8px;text-align:center;color:#fff;}
.status-pending{color:orange;font-weight:bold;}
.status-approved{color:#0f0;font-weight:bold;}
.status-rejected{color:red;font-weight:bold;}
</style>
</head>
<body>

<!-- Registration/Login -->
<div class="container" id="registerForm">
<h2>Register</h2>
<input type="text" placeholder="Full Name" id="regName">
<input type="text" placeholder="Mobile Number" id="regMobile">
<input type="password" placeholder="Password" id="regPass">
<input type="password" placeholder="Confirm Password" id="regConfirm">
<button onclick="registerUser()">Register</button>
<p style="text-align:center;margin-top:10px;">Already registered? <span style="color:#0f0;cursor:pointer;" onclick="showLogin()">Login</span></p>
</div>

<div class="container" id="loginForm" style="display:none;">
<h2>Login</h2>
<input type="text" placeholder="Mobile Number" id="loginMobile">
<input type="password" placeholder="Password" id="loginPass">
<button onclick="loginUser()">Login</button>
<p style="text-align:center;margin-top:10px;">Admin? <span style="color:#0f0;cursor:pointer;" onclick="showAdminLogin()">Admin Login</span></p>
<p style="text-align:center;margin-top:10px;">New user? <span style="color:#0f0;cursor:pointer;" onclick="showRegister()">Register</span></p>
</div>

<!-- User Dashboard -->
<div class="container" id="userDashboard" style="display:none;">
<h2>Welcome, <span id="uName"></span></h2>
<p>Wallet: <span id="wallet">0</span> NPR</p>

<!-- Action Buttons -->
<div style="display:flex;flex-direction:column;gap:10px;">
<button onclick="depositSection()">💰 Deposit</button>
<button onclick="withdrawSection()">💸 Withdraw</button>
<button onclick="customerSupport()">📞 Customer Support</button>
<button id="spinWheel" onclick="spinWheel()">🎡 Spin Wheel</button>
<p id="spinResult"></p>
<button onclick="checkIn()">✅ Daily Check In (+5 NPR)</button>
</div>

<!-- Deposit Form -->
<div id="depositDiv" style="display:none;margin-top:10px;">
<h3>Deposit</h3>
<select id="depositAmount">
<option value="">Select Amount</option>
<option value="500">500</option>
<option value="1000">1000</option>
<option value="2000">2000</option>
<option value="3000">3000</option>
<option value="4000">4000</option>
<option value="5000">5000</option>
</select>
<input type="file" id="depositProof">
<button onclick="requestDeposit()">Submit Deposit</button>
<p id="depositTimer" style="text-align:center;color:#0f0;"></p>
</div>

<!-- Withdraw Form -->
<div id="withdrawDiv" style="display:none;margin-top:10px;">
<h3>Withdraw</h3>
<input type="number" id="withdrawAmount" placeholder="Amount 500-10000">
<select id="withdrawMethod">
<option value="">Select Method</option>
<option value="Esewa">Esewa</option>
<option value="Khalti">Khalti</option>
<option value="Bank">Bank</option>
</select>
<button onclick="requestWithdraw()">Submit Withdraw</button>
</div>

<h3>My Requests</h3>
<div id="myRequests"></div>

<!-- My Product Section -->
<div class="container" id="myProduct" style="display:none;">
  <h2>My Product / Plan</h2>
  <div style="display:flex;flex-wrap:wrap;gap:15px;justify-content:center;">
    <!-- VIP Plan Card -->
    <div style="border:1px solid #555;padding:15px;border-radius:10px;background:#222;width:200px;text-align:center;">
      <h3 style="color:#0f0;margin-bottom:5px;">VIP Plan</h3>
      <p style="color:#fff;margin-bottom:10px;">Price: 500 NPR</p>
      <ul style="text-align:left;color:#eee;padding-left:15px;margin-bottom:10px;">
        <li>Exclusive Feature 1</li>
        <li>Exclusive Feature 2</li>
        <li>Exclusive Feature 3</li>
      </ul>
      <button style="width:100%;padding:10px;background:#007bff;color:#fff;border:none;border-radius:5px;cursor:pointer;"
        onclick="purchasePlan('VIP Plan',500)">
        Buy / View
      </button>
    </div>
  </div>
</div>

<button onclick="logoutUser()">Logout</button>
</div>

<!-- Admin Login -->
<div class="container" id="adminLogin" style="display:none;">
<h2>Admin Login</h2>
<input type="password" placeholder="Enter Admin Password" id="adminPass">
<button onclick="loginAdmin()">Login</button>
</div>

<!-- Admin Panel -->
<div class="container" id="adminPanel" style="display:none;">
<h2>Admin Panel</h2>
<button onclick="logoutAdmin()">Logout Admin</button>

<h3>Pending Deposits</h3>
<div id="pendingDeposits"></div>

<h3>Pending Withdrawals</h3>
<div id="pendingWithdrawals"></div>
</div>

<!-- Bottom Navigation Bar -->
<div class="bottomNav">
<button onclick="showDashboard()">Home</button>
<button onclick="showMyProduct()">My Product</button>
<button>Team</button>
<button>My Account</button>
</div>

<script>
// Local Storage Init
if(!localStorage.getItem("users")) localStorage.setItem("users",JSON.stringify([]));
let currentUser=null;
let lastDepositTime = 0;
let depositInterval = null;

// Show Forms
function showRegister(){document.getElementById("registerForm").style.display="block";document.getElementById("loginForm").style.display="none";document.getElementById("userDashboard").style.display="none";document.getElementById("adminLogin").style.display="none";}
function showLogin(){document.getElementById("registerForm").style.display="none";document.getElementById("loginForm").style.display="block";}
function showAdminLogin(){document.getElementById("loginForm").style.display="none";document.getElementById("adminLogin").style.display="block";}

// Dashboard Toggle
function showDashboard(){
  document.getElementById("userDashboard").style.display="block";
  document.getElementById("myProduct").style.display="none";
}
function showMyProduct(){
  document.getElementById("userDashboard").style.display="none";
  document.getElementById("myProduct").style.display="block";
}

// Register
function registerUser(){
const name=document.getElementById("regName").value.trim();
const mobile=document.getElementById("regMobile").value.trim();
const pass=document.getElementById("regPass").value;
const conf=document.getElementById("regConfirm").value;
if(!name||!mobile||!pass||!conf){alert("Fill all fields"); return;}
if(pass!==conf){alert("Passwords do not match"); return;}
let users=JSON.parse(localStorage.getItem("users"));
if(users.find(u=>u.mobile===mobile)){alert("Mobile already registered"); return;}
const newUser={name,mobile,password:pass,wallet:50,deposits:[],withdrawals:[],lastCheckIn:null};
users.push(newUser);
localStorage.setItem("users",JSON.stringify(users));
alert("Registered successfully! 🎉 50 NPR signup bonus added");
showLogin();
}

// Login
function loginUser(){
const mobile=document.getElementById("loginMobile").value.trim();
const pass=document.getElementById("loginPass").value;
let users=JSON.parse(localStorage.getItem("users"));
const user=users.find(u=>u.mobile===mobile && u.password===pass);
if(user){currentUser=user; localStorage.setItem("currentUser",JSON.stringify(user)); showUserDashboard();}
else{alert("Invalid credentials");}
}

function showUserDashboard(){
document.getElementById("registerForm").style.display="none";
document.getElementById("loginForm").style.display="none";
document.getElementById("userDashboard").style.display="block";
document.getElementById("myProduct").style.display="none";
document.getElementById("uName").innerText=currentUser.name;
document.getElementById("depositDiv").style.display="none";
document.getElementById("withdrawDiv").style.display="none";
updateWallet();
displayRequests();
updateDepositTimer();
}

// Toggle Sections
function depositSection(){document.getElementById("depositDiv").style.display="block";document.getElementById("withdrawDiv").style.display="none";}
function withdrawSection(){document.getElementById("withdrawDiv").style.display="block";document.getElementById("depositDiv").style.display="none";}
function customerSupport(){alert("Customer Support: Contact admin via Email/Phone.");}

// Check In
function checkIn(){
if(currentUser.lastCheckIn===new Date().toDateString()){alert("Already checked in today"); return;}
currentUser.wallet+=5;
saveCurrentUser();
updateWallet();
alert("✅ Daily 5 NPR added to wallet");
}

// Spin Wheel
function spinWheel(){
const wheel = document.getElementById("spinWheel");
const pointsArr=[5,10,15,20,25,30,35];
const win=pointsArr[Math.floor(Math.random()*pointsArr.length)];
const segment = 360 / pointsArr.length;
const randomSpin = 360*5 + segment*pointsArr.indexOf(win) + Math.random()*segment;
wheel.style.transition = "transform 4s cubic-bezier(0.33, 1, 0.68, 1)";
wheel.style.transform = `rotate(${randomSpin}deg)`;
setTimeout(()=>{
    currentUser.wallet+=win;
    saveCurrentUser();
    updateWallet();
    document.getElementById("spinResult").innerText=`You won ${win} NPR!`;
},4000);
}

// Deposit
function requestDeposit(){
const now = Date.now();
if(now - lastDepositTime < 30*60*1000){ 
    const remaining = Math.ceil((30*60*1000 - (now - lastDepositTime))/1000);
    alert(`Next deposit available in ${Math.floor(remaining/60)}m ${remaining%60}s`);
    return;
}
const amt=parseInt(document.getElementById("depositAmount").value);
const proof=document.getElementById("depositProof").files[0];
if(!amt||!proof){alert("Select amount and proof"); return;}
lastDepositTime = now;
const deposit={id:Date.now(),amount:amt,proof:proof.name,status:"Pending",timestamp:new Date().toLocaleString()};
currentUser.deposits.push(deposit);
saveCurrentUser();
alert("Deposit request submitted");
document.getElementById("depositAmount").value="";
document.getElementById("depositProof").value="";
displayRequests();
updateDepositTimer();
}

// Deposit Timer
function updateDepositTimer(){
    const timerEl = document.getElementById("depositTimer");
    if(depositInterval) clearInterval(depositInterval);
    depositInterval = setInterval(()=>{
        const now = Date.now();
        const diff = 30*60*1000 - (now - lastDepositTime);
        if(diff>0){
            const m = Math.floor(diff/60000);
            const s = Math.floor((diff%60000)/1000);
            timerEl.innerText=`Next deposit in ${m}m ${s}s`;
        } else {
            timerEl.innerText="";
            clearInterval(depositInterval);
            depositInterval = null;
        }
    },1000);
}

// Withdraw
function requestWithdraw(){
const amt=parseInt(document.getElementById("withdrawAmount").value);
const method=document.getElementById("withdrawMethod").value;
if(!amt||!method){alert("Enter amount & method"); return;}
if(amt<500||amt>10000){alert("Amount 500-10000 allowed"); return;}
const withdraw={id:Date.now(),amount:amt,fee:Math.round(amt*0.1),method,status:"Pending",timestamp:new Date().toLocaleString()};
currentUser.withdrawals.push(withdraw);
saveCurrentUser();
alert("Withdraw request submitted");
document.getElementById("withdrawAmount").value="";
document.getElementById("withdrawMethod").value="";
displayRequests();
}

// Display Requests
function displayRequests(){
let html="<h4>Deposits</h4><table><tr><th>Amount</th><th>Status</th></tr>";
currentUser.deposits.forEach(d=>{html+=`<tr><td>${d.amount}</td><td class="status-${d.status.toLowerCase()}">${d.status}</td></tr>`;});
html+="</table><h4>Withdrawals</h4><table><tr><th>Amount</th><th>Fee</th><th>Status</th></tr>";
currentUser.withdrawals.forEach(w=>{html+=`<tr><td>${w.amount}</td><td>${w.fee}</td><td class="status-${w.status.toLowerCase()}">${w.status}</td></tr>`;});
html+="</table>";
document.getElementById("myRequests").innerHTML=html;
updateWallet();
}

// Save current user
function saveCurrentUser(){
let users=JSON.parse(localStorage.getItem("users"));
const idx=users.findIndex(u=>u.mobile===currentUser.mobile);
users[idx]=currentUser;
localStorage.setItem("users",JSON.stringify(users));
}

// Update Wallet
function updateWallet(){document.getElementById("wallet").innerText=currentUser.wallet;}

// Logout
function logoutUser(){localStorage.removeItem("currentUser");location.reload();}

// Purchase VIP Plan
function purchasePlan(planName, planPrice){
  if(currentUser.wallet >= planPrice){
    currentUser.wallet -= planPrice;
    saveCurrentUser();
    updateWallet();
    alert(`You have purchased ${planName}!`);
  } else {
    alert("Please Deposit into Your Account");
  }
}

// Auto-login demo user
window.onload=function(){const storedUser=JSON.parse(localStorage.getItem("currentUser")); if(storedUser){currentUser=storedUser; showUserDashboard();}}
</script>

</body>
</html>
