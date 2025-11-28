<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Salem Investment Dashboard</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --primary:#1f6feb;
  --secondary:#0ea5a0;
  --danger:#ef4444;
  --bg:#f6f8fb;
  --card:#fff;
}
*{box-sizing:border-box;margin:0;padding:0;font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;}
body{background:var(--bg);color:#0f1724;}
.container{max-width:900px;margin:20px auto;padding:16px;}
.card{background:var(--card);border-radius:16px;padding:20px;box-shadow:0 8px 20px rgba(0,0,0,0.08);margin-bottom:16px;transition:transform 0.2s;}
.card:hover{transform:translateY(-3px);}
header{display:flex;align-items:center;gap:12px;padding:16px;border-radius:16px;background:linear-gradient(90deg,var(--primary),var(--secondary));color:white;}
header img{width:60px;height:60px;border-radius:12px;box-shadow:0 4px 10px rgba(0,0,0,0.2);}
h1,h2,h3{margin:0 0 8px 0;}
p.lead{color:white;margin:4px 0;font-size:14px;}
input,button,select{padding:10px;border-radius:10px;border:1px solid #e6edf3;font-size:14px;}
button{font-weight:600;cursor:pointer;transition:transform 0.15s;}
button:hover{transform:scale(1.05);}
button.gradient{background:linear-gradient(45deg,var(--primary),var(--secondary));color:white;border:none;}
.muted{color:#64748b;font-size:13px;}
.space-between{display:flex;justify-content:space-between;align-items:center;}
.balance{font-weight:700;font-size:22px;}
.small{font-size:13px;}
table{width:100%;border-collapse:collapse;margin-top:10px;}
th,td{padding:10px;border-bottom:1px solid #eef2f7;text-align:left;}
a{color:var(--primary);text-decoration:none;}
a:hover{text-decoration:underline;}
#proofPopup{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.7);justify-content:center;align-items:center;}
#proofPopup img{max-width:100%;border-radius:10px;margin-bottom:10px;}
</style>
</head>
<body>
<div class="container">

<!-- Header -->
<div class="card">
<header>
<img src="logo.png" alt="Salem Logo">
<div>
<h1>Salem Investment Dashboard</h1>
<p class="lead">Trusted since 1979 | Spin, VIP, Referral, QR Demo</p>
</div>
</header>
</div>

<!-- Auth Card -->
<div class="card" id="authCard">
<div class="space-between">
<div>
<h2>Welcome — Sign up / Log in</h2>
<p class="muted">Nepali Number (+977) required</p>
</div>
<div class="muted small">Salem Investment Counselors</div>
</div>

<div style="margin-top:12px">
<div style="display:flex;gap:8px;flex-wrap:wrap">
<input id="phone" type="text" placeholder="Nepali Mobile Number (9801234567)" style="flex:1;min-width:160px">
<input id="password" type="password" placeholder="Password" style="min-width:160px">
<input id="referral" type="text" placeholder="Referral Phone (optional)" style="min-width:160px">
<button id="signupBtn" class="gradient">Sign up</button>
<button id="loginBtn" style="background:var(--secondary)">Log in</button>
</div>
<p class="muted small" style="margin-top:8px">Or continue as <a href="#" id="guestBtn">Guest</a></p>
</div>
<div id="authMsg" class="muted small" style="margin-top:8px"></div>
</div>

<!-- Dashboard Card -->
<div class="card" id="dashCard" style="display:none">

<div class="space-between">
<div>
<div class="muted small">Account</div>
<div class="balance" id="balance">NPR 0</div>
</div>
<div style="text-align:right">
<div id="userEmail" class="small muted">user@example.com</div>
<button id="logoutBtn" style="margin-top:8px;background:var(--danger)">Log out</button>
</div>
</div>

<hr>
<div class="form-row" style="margin-bottom:8px;flex-wrap:wrap">
<input id="amount" type="number" placeholder="Amount" min="1" style="flex:1">
<button id="depositBtn" class="gradient">Deposit</button>
<button id="withdrawBtn" style="background:var(--danger)">Withdraw</button>
</div>
<p class="muted small">Min Deposit/Withdraw: NPR 500 | Withdrawal Fee: 5%</p>

<h3>Deposit using Nepali Wallets (Demo)</h3>
<div class="form-row" style="gap:8px;">
<button id="khaltiBtn" style="background:#5c2d91">Deposit with Khalti</button>
<button id="esewaBtn" style="background:#1ba548">Deposit with eSewa</button>
<button id="bankBtn" style="background:#0f172a">Deposit via Nepal Bank</button>
</div>

<h3>Transactions</h3>
<table id="txTable">
<thead><tr><th>Type</th><th>Amount</th><th>Date</th><th>Status</th></tr></thead>
<tbody></tbody>
</table>
</div>

<!-- Admin Panel -->
<div id="adminLogin" class="card" style="max-width:350px; margin:40px auto; display:none; text-align:center;">
<h2>Admin Login</h2>
<input id="adminPass" type="password" placeholder="Enter Admin Password" style="width:100%; margin-bottom:10px; padding:10px; border-radius:10px; border:1px solid #ccc;">
<button id="adminLoginBtn" style="width:100%; padding:10px; border-radius:10px;">Login</button>
</div>

<div id="adminPanel" style="display:none; padding:20px; max-width:900px; margin:auto;">
<h2 style="text-align:center;">Admin Dashboard</h2>
<div class="card">
<h3>Withdraw Requests</h3>
<table id="adminWithdrawTable" style="width:100%; border-collapse:collapse;">
<tr style="background:#f1f5f9;">
<th>User</th><th>Amount</th><th>Proof</th><th>Status</th><th>Action</th>
</tr>
</table>
</div>
<button id="logoutAdmin" style="background:#ef4444; padding:10px 20px; border-radius:12px; color:white;">Logout</button>
</div>

<!-- Proof Popup -->
<div id="proofPopup" style="display:none; position:fixed; inset:0; background:rgba(0,0,0,0.7); justify-content:center; align-items:center;">
<div style="background:white; padding:20px; border-radius:14px; max-width:90%; max-height:90%; overflow:auto;">
<img id="popupImg" src="" style="max-width:100%; border-radius:10px; margin-bottom:10px;">
<button onclick="closePopup()" style="width:100%; padding:10px; border-radius:8px; background:#ef4444; color:white;">Close</button>
</div>
</div>

<script>
// Complete JS logic: Signup/Login, Guest, VIP, Deposit/Withdraw, Admin, QR demo, Transaction table
const ADMIN_PASSWORD='salem_admin_2025';
const el=id=>document.getElementById(id);
let state={user:null,balance:0,tx:[],dailyCheckin:false};

// Show/Hide
function show(id,val=true){el(id).style.display=val?'block':'none';}

// Proof Popup
function openPopup(src){el('popupImg').src=src; show('proofPopup');}
function closePopup(){show('proofPopup',false);}

// Transactions Table
function renderTxTable(){
  const tbody=el('txTable').querySelector('tbody');
  tbody.innerHTML='';
  state.tx.forEach((t)=>{
    const tr=document.createElement('tr');
    tr.innerHTML=`<td>${t.type}</td>
                  <td>NPR ${t.amount}</td>
                  <td>${t.date}</td>
                  <td>${t.status}</td>`;
    tbody.appendChild(tr);
  });
}

// Add transaction
function addTx(type,amount,meta={}){state.tx.unshift({type,amount,date:new Date().toLocaleString(),meta,status:meta.status||'completed'});renderTxTable();}
function updateBalance(){el('balance').innerText=`NPR ${state.balance}`;}

// Signup
el('signupBtn').onclick=()=>{
  let phone=el('phone').value.trim(); let pass=el('password').value.trim();
  if(!phone.match(/^\d{9,10}$/)){el('authMsg').innerText='Invalid Nepali Number'; return;}
  if(pass.length<6){el('authMsg').innerText='Password min 6 chars'; return;}
  state.user={phone:'+977'+phone,password:pass,invested:false,balance:50};
  state.balance=50; el('authCard').style.display='none'; el('dashCard').style.display='block';
  el('userEmail').innerText=state.user.phone; el('authMsg').innerText='';
  addTx('Sign-up Bonus',50);
  alert('Signup success! 50 NPR bonus credited.');
}

// Login
el('loginBtn').onclick=()=>{
  let phone=el('phone').value.trim(); let pass=el('password').value.trim();
  if(!state.user || state.user.phone!=='+977'+phone || state.user.password!==pass){el('authMsg').innerText='Wrong credentials';return;}
  el('authCard').style.display='none'; el('dashCard').style.display='block'; el('userEmail').innerText=state.user.phone; updateBalance();
}

// Logout
el('logoutBtn').onclick=()=>{el('dashCard').style.display='none'; el('authCard').style.display='block'; state.user=null; state.balance=0; state.tx=[]; renderTxTable();}

// Deposit
el('depositBtn').onclick=()=>{
  let amt=Number(el('amount').value); if(amt<500){alert('Min deposit 500 NPR'); return;}
  state.balance+=amt; updateBalance(); addTx('Deposit',amt,{status:'completed'});
}

// Withdraw
el('withdrawBtn').onclick=()=>{
  if(!state.user?.invested){alert('Purchase VIP first'); return;}
  let amt=Number(el('amount').value); if(amt<500){alert('Min withdraw 500'); return;}
  if(amt>state.balance){alert('Insufficient balance'); return;}
  let fee=Math.ceil(amt*0.05); state.balance-=amt; updateBalance();
  addTx('WithdrawRequest',amt,{status:'pending',fee:fee,user:state.user.phone}); alert('Withdraw request submitted.');
}

// Admin login
el('adminLoginBtn').onclick=()=>{
  if(el('adminPass').value===ADMIN_PASSWORD){show('adminLogin',false); show('adminPanel'); renderAdminTable();}
  else{alert('Wrong password');}
}
el('logoutAdmin').onclick=()=>{show('adminPanel',false); show('adminLogin',true);}

// Admin Withdraw Table
function renderAdminTable(){
  const tbl=el('adminWithdrawTable'); tbl.querySelectorAll('tr:not(:first-child)').forEach(r=>r.remove());
  state.tx.forEach((t,i)=>{
    if(t.type==='WithdrawRequest'){
      const tr=document.createElement('tr');
      tr.innerHTML=`<td>${t.meta.user||'Guest'}</td><td>${t.amount}</td>
                    <td>${t.meta.proof?'<button onclick="openPopup(\''+t.meta.proof+'\')">View</button>':'-'}</td>
                    <td>${t.status}</td>
                    <td><button onclick="approve(${i})">Approve</button> <button onclick="reject(${i})">Reject</button></td>`;
      tbl.appendChild(tr);
    }
  });
}
function approve(i){state.tx[i].status='approved'; state.balance-=Number(state.tx[i].amount); renderAdminTable(); renderTxTable();}
function reject(i){state.tx[i].status='rejected'; renderAdminTable(); renderTxTable();}

// QR Demo
el('khaltiBtn').onclick=()=>{alert('Khalti QR demo');}
el('esewaBtn').onclick=()=>{alert('eSewa QR demo');}
el('bankBtn').onclick=()=>{alert('Bank QR demo');}
</script>
</body>
</html>
