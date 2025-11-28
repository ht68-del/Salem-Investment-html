<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Register, Login & Dashboard (Spin Wheel + Check In)</title>
  <style>
    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: linear-gradient(to right, #6a11cb, #2575fc);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      padding: 10px;
    }
    .container {
      width: 100%;
      max-width: 400px;
      background: #fff;
      padding: 25px;
      border-radius: 15px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.2);
    }
    h2 {
      text-align: center;
      margin-bottom: 20px;
      color: #333;
      font-size: 24px;
    }
    .input-group {
      position: relative;
      margin-bottom: 15px;
    }
    input {
      width: 100%;
      padding: 12px 40px 12px 12px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 16px;
    }
    .toggle-pass {
      position: absolute;
      right: 10px;
      top: 50%;
      transform: translateY(-50%);
      cursor: pointer;
      color: #007bff;
      font-weight: bold;
      font-size: 14px;
    }
    button {
      width: 100%;
      padding: 12px;
      background: #007bff;
      color: white;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
      margin-top: 10px;
    }
    button:hover {
      background: #005fcc;
    }
    .toggle {
      text-align: center;
      margin-top: 15px;
      color: #007bff;
      cursor: pointer;
      font-size: 14px;
    }

    /* Dashboard Styles */
    #dashboard {
      display: none;
      text-align: center;
      color: #fff;
    }
    #dashboard p {
      font-size: 16px;
      margin: 5px 0 20px;
    }
    .dashboard-buttons {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      margin-top: 10px;
    }
    .dashboard-buttons button {
      flex: 48%;
      padding: 15px;
      margin-bottom: 15px;
      font-size: 16px;
      border-radius: 10px;
      background: #ff9800;
      color: white;
      border: none;
      cursor: pointer;
    }
    .dashboard-buttons button:hover {
      background: #e68900;
    }

    @media(max-width:480px){
      .dashboard-buttons { flex-direction: column; }
      .dashboard-buttons button { flex: 100%; }
      h2 { font-size: 20px; }
      input { font-size: 14px; padding: 10px 35px 10px 10px; }
      button { font-size: 14px; padding: 10px; }
      .toggle-pass { font-size: 12px; }
      .toggle { font-size: 12px; }
    }
  </style>
</head>
<body>

  <!-- Register Form -->
  <div class="container" id="registerForm">
    <h2>Create Account</h2>
    <div class="input-group"><input type="text" placeholder="Full Name" /></div>
    <div class="input-group"><input type="text" placeholder="Mobile Number" /></div>
    <div class="input-group">
      <input type="password" placeholder="Password" class="pass-input" />
      <span class="toggle-pass" onclick="togglePass(this)">Show</span>
    </div>
    <div class="input-group">
      <input type="password" placeholder="Confirm Password" class="pass-input" />
      <span class="toggle-pass" onclick="togglePass(this)">Show</span>
    </div>
    <button id="registerBtn">Register</button>
    <div class="toggle" onclick="showLogin()">Already have an account? Login</div>
  </div>

  <!-- Login Form -->
  <div class="container" id="loginForm" style="display:none;">
    <h2>Login</h2>
    <div class="input-group"><input type="text" placeholder="Mobile Number" /></div>
    <div class="input-group">
      <input type="password" placeholder="Password" class="pass-input" />
      <span class="toggle-pass" onclick="togglePass(this)">Show</span>
    </div>
    <button id="loginBtn">Login</button>
    <div class="toggle" onclick="showRegister()">Don't have an account? Register</div>
  </div>

  <!-- Dashboard -->
  <div class="container" id="dashboard">
    <h2>Welcome, <span id="userName"></span>!</h2>
    <p>Mobile Number: <span id="userMobile"></span></p>
    <div class="dashboard-buttons">
      <button onclick="deposit()">💰 Deposit</button>
      <button onclick="withdraw()">💸 Withdraw</button>
      <button onclick="customerSupport()">📞 Customer Support</button>
      <button onclick="spinWheel()">🎡 Spin Wheel</button>
      <button onclick="checkIn()">✅ Check In</button>
    </div>
    <button onclick="logout()" style="margin-top:20px;background:#ff4d4d;">Logout</button>
  </div>

  <script>
    const registerForm = document.getElementById("registerForm");
    const loginForm = document.getElementById("loginForm");
    const dashboard = document.getElementById("dashboard");
    const userName = document.getElementById("userName");
    const userMobile = document.getElementById("userMobile");

    function showLogin() { registerForm.style.display="none"; loginForm.style.display="block"; dashboard.style.display="none"; }
    function showRegister() { loginForm.style.display="none"; registerForm.style.display="block"; dashboard.style.display="none"; }
    function togglePass(span){ const input=span.previousElementSibling; if(input.type==="password"){ input.type="text"; span.innerText="Hide"; } else{ input.type="password"; span.innerText="Show"; }}

    // Check session on load
    window.onload = function(){
      const currentUser = JSON.parse(localStorage.getItem("currentUser"));
      if(currentUser){ showDashboard(currentUser); }
    }

    function showDashboard(user){
      registerForm.style.display="none";
      loginForm.style.display="none";
      dashboard.style.display="block";
      userName.innerText=user.name;
      userMobile.innerText=user.mobile;
    }

    // Register
    document.getElementById("registerBtn").addEventListener("click", function(){
      const name=registerForm.querySelector('input[placeholder="Full Name"]').value;
      const mobile=registerForm.querySelector('input[placeholder="Mobile Number"]').value;
      const password=registerForm.querySelector('input[placeholder="Password"]').value;
      const confirmPassword=registerForm.querySelector('input[placeholder="Confirm Password"]').value;
      if(!name||!mobile||!password||!confirmPassword){ alert("कृपया सभी fields भरें!"); return; }
      if(password!==confirmPassword){ alert("Passwords मेल नहीं खाते!"); return; }
      const users=JSON.parse(localStorage.getItem("users")||"[]");
      if(users.find(u=>u.mobile===mobile)){ alert("ये Mobile Number पहले से register है!"); return; }
      const newUser={name,mobile,password};
      users.push(newUser);
      localStorage.setItem("users",JSON.stringify(users));
      localStorage.setItem("currentUser",JSON.stringify(newUser));
      alert("Registration Successful!");
      registerForm.querySelectorAll('input').forEach(i=>i.value="");
      showDashboard(newUser);
    });

    // Login
    document.getElementById("loginBtn").addEventListener("click", function(){
      const mobile=loginForm.querySelector('input[placeholder="Mobile Number"]').value;
      const password=loginForm.querySelector('input[placeholder="Password"]').value;
      if(!mobile||!password){ alert("कृपया सभी fields भरें!"); return; }
      const users=JSON.parse(localStorage.getItem("users")||"[]");
      const user=users.find(u=>u.mobile===mobile && u.password===password);
      if(user){ localStorage.setItem("currentUser",JSON.stringify(user)); showDashboard(user); }
      else{ alert("Invalid Mobile Number or Password!"); }
    });

    function logout(){ localStorage.removeItem("currentUser"); showLogin(); }

    // Dashboard button functions
    function deposit(){ alert("Deposit clicked!"); }
    function withdraw(){ alert("Withdraw clicked!"); }
    function customerSupport(){ alert("Customer Support clicked!"); }
    function spinWheel(){ alert("Spin Wheel clicked!"); }
    function checkIn(){ alert("Check In clicked!"); }
  </script>
</body>
</html>
