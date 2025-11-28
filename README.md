<!--
Filename: kukaapp_like_landing.html
Purpose: Mobile-first single-file HTML/CSS/JS implementing the dark "Marvel"-style app UI from your screenshots.
Branding: Company name set to "APPLE Company" (replace logo.png with your logo file if you have one).
How to use: Save as HTML and open on mobile or desktop. For backend, replace the fake submit handlers with your API endpoints.
-->

<!doctype html>
<html lang="hi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
  <title>APPLE Company — Mobile</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=Caveat&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#22252a; --card:#2b2f35; --muted:#bdbdbd; --accent:#ff2b2b; --soft:#3a3e44;
      --radius:12px; --gap:14px; --font-hand: 'Caveat', cursive; --ui: 'Inter', system-ui, -apple-system, Arial;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{margin:0;font-family:var(--ui);background:var(--bg);color:#fff;-webkit-font-smoothing:antialiased}
    .container{max-width:460px;margin:0 auto;padding:16px}

    /* HEADER */
    .topbar{display:flex;align-items:center;gap:12px;padding:8px 0}
    .topbar .close{font-size:28px;padding-right:6px;opacity:0.9}
    .brand{font-weight:700;font-size:20px}
    .sub{font-size:12px;color:var(--muted);margin-top:2px}

    /* MAIN CARD */
    .card{background:linear-gradient(180deg,var(--card),#232629);border-radius:18px;padding:18px;margin-top:8px}
    .logo-wrap{text-align:center;padding:18px}
    .logo{width:120px;height:120px;object-fit:contain;border-radius:12px;background:#111;display:inline-flex;align-items:center;justify-content:center}
    .logo img{max-width:100%;max-height:100%}
    .logo h1{margin:0;font-family:var(--font-hand);font-size:22px;color:#fff}

    .form{margin-top:10px}
    label{display:block;font-size:15px;color:var(--muted);margin-bottom:6px;font-family:var(--font-hand)}
    .inputs{display:flex;gap:10px}
    .country{min-width:74px;padding:12px;border-radius:10px;border:1px solid rgba(255,255,255,0.08);background:transparent;text-align:center}
    input[type=tel], input[type=password], input[type=text]{flex:1;padding:14px;border-radius:10px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:#ddd;font-size:16px}

    .big-input{padding:16px;border-radius:12px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:#ddd}

    .btn{width:100%;padding:14px;border-radius:12px;border:0;background:linear-gradient(90deg,var(--accent),#ff6b6b);color:#111;font-weight:700;font-size:18px;margin-top:12px;cursor:pointer}
    .btn.secondary{background:#ff2b2b;opacity:0.95}

    .link-btn{width:100%;padding:14px;border-radius:12px;border:0;background:transparent;color:var(--accent);border:1px solid rgba(255,43,43,0.15);margin-top:12px}

    .ref{margin-top:10px;padding:12px;border-radius:12px;border-left:4px solid var(--accent);background:#2b2b2b;color:var(--muted);display:flex;justify-content:space-between;align-items:center}

    .small{font-size:13px;color:var(--muted);margin-top:10px}

    /* HOME / GRID */
    .hero-image{width:100%;height:150px;border-radius:12px;overflow:hidden;background:#333;margin-top:12px}
    .icons{display:flex;gap:18px;justify-content:space-around;padding:12px 6px}
    .icon{display:flex;flex-direction:column;align-items:center;gap:8px}
    .icon i{width:54px;height:54px;border-radius:12px;background:var(--accent);display:flex;align-items:center;justify-content:center}
    .icon span{font-size:13px;color:var(--muted);font-family:var(--font-hand)}

    .list{margin-top:14px}
    .plan{background:linear-gradient(180deg,#2b2f35,#23272b);padding:14px;border-radius:12px;display:flex;justify-content:space-between;align-items:center;margin-bottom:12px;border:1px solid rgba(255,255,255,0.02)}
    .plan .info{max-width:62%}
    .plan h3{margin:0;font-family:var(--font-hand);font-size:18px}
    .plan p{margin:6px 0 0;color:var(--muted);font-size:13px}
    .plan .price{background:#1f2124;padding:10px 12px;border-radius:10px;text-align:center}
    .plan .price strong{display:block;font-size:22px}
    .plan .cta{margin-top:8px;display:block;padding:8px 10px;border-radius:8px;background:var(--accent);color:#111;font-weight:700;text-align:center}

    /* bottom nav */
    .bottom-nav{position:fixed;left:0;right:0;bottom:12px;max-width:460px;margin:0 auto;padding:8px;display:flex;gap:8px;justify-content:space-around}
    .nav-item{background:#1f2124;padding:10px 14px;border-radius:10px;color:#999;text-align:center;flex:1}
    .nav-item.active{background:#111;color:var(--accent)}

    /* small screens tweaks */
    @media(min-width:780px){.container{margin-top:36px}}
  </style>
</head>
<body>
  <div class="container" id="app">

    <div class="topbar">
      <div class="close">✕</div>
      <div>
        <div class="brand">APPLE Company</div>
        <div class="sub">apple.company/login</div>
      </div>
    </div>

    <!-- LOGIN / REGISTER CARD -->
    <div class="card" id="authCard">
      <div class="logo-wrap">
        <div class="logo" id="logoBox"><img src="logo.png" alt="APPLE logo" onerror="this.style.display='none'"/></div>
        <h1 style="margin-top:8px;font-size:20px">APPLE Company</h1>
      </div>

      <div class="form" id="loginForm">
        <label>Mobile Number</label>
        <div class="inputs">
          <div class="country">+977</div>
          <input type="tel" id="loginPhone" placeholder="Mobile number" />
        </div>

        <label style="margin-top:12px">Password</label>
        <input type="password" id="loginPass" placeholder="Password" class="big-input" />

        <button class="btn" onclick="doLogin()">Log-in</button>
        <button class="btn secondary" onclick="showRegister()">Register</button>
      </div>

      <!-- REGISTER (hidden by default) -->
      <div class="form" id="registerForm" style="display:none">
        <label>Mobile Number</label>
        <div class="inputs">
          <div class="country">+977</div>
          <input type="tel" id="regPhone" placeholder="Mobile number" />
        </div>
        <label>Password</label>
        <input type="password" id="regPass" placeholder="Password" class="big-input" />
        <label>Confirm Password</label>
        <input type="password" id="regPass2" placeholder="Confirm password" class="big-input" />
        <label>Invitation code</label>
        <input type="text" id="invCode" value="bb20c9f9" class="big-input" />

        <button class="btn" onclick="doRegister()">Register</button>
        <button class="link-btn" onclick="showLogin()">Already Have Account? Log-in</button>
      </div>

    </div>

    <!-- Home / dashboard preview -->
    <div class="card" id="homeCard" style="display:none;margin-top:12px">
      <div class="hero-image">
        <!-- sample hero image area -->
        <img src="hero.jpg" alt="hero" style="width:100%;height:100%;object-fit:cover" onerror="this.style.background='#3a3a3a'"/>
      </div>

      <div class="icons">
        <div class="icon"><i></i><span>Check-In</span></div>
        <div class="icon"><i></i><span>Recharge</span></div>
        <div class="icon"><i></i><span>Official Channel</span></div>
        <div class="icon"><i></i><span>Treasure</span></div>
      </div>

      <div class="list">
        <div class="plan">
          <div class="info">
            <h3>Marvel-1</h3>
            <p>Period: 200 days • Daily Profit: NPR330 • Total Profit: NPR66,000</p>
          </div>
          <div style="text-align:right">
            <div class="price"><strong>1000</strong><div style="font-size:12px;color:var(--muted)">NPR</div></div>
            <a class="cta" href="#">Invest now</a>
          </div>
        </div>

        <div class="plan">
          <div class="info">
            <h3>Marvel-2</h3>
            <p>Period: 200 days • Daily Profit: NPR1,000 • Total Profit: NPR200,000</p>
          </div>
          <div style="text-align:right">
            <div class="price"><strong>3000</strong><div style="font-size:12px;color:var(--muted)">NPR</div></div>
            <a class="cta" href="#">Invest now</a>
          </div>
        </div>
      </div>

    </div>

    <div class="bottom-nav">
      <div class="nav-item active" onclick="navTo('home')">Home</div>
      <div class="nav-item" onclick="navTo('products')">My products</div>
      <div class="nav-item" onclick="navTo('share')">Share</div>
      <div class="nav-item" onclick="navTo('mine')">Mine</div>
    </div>

  </div>

  <script>
    // Simple UI state handlers
    function showRegister(){ document.getElementById('loginForm').style.display='none'; document.getElementById('registerForm').style.display='block'; }
    function showLogin(){ document.getElementById('loginForm').style.display='block'; document.getElementById('registerForm').style.display='none'; }
    function doLogin(){
      const phone = document.getElementById('loginPhone').value.trim();
      const pass = document.getElementById('loginPass').value.trim();
      if(!phone || !pass){ alert('Mobile aur password daaliye'); return }
      // fake success -> show home
      alert('Login successful (demo)');
      document.getElementById('authCard').style.display='none';
      document.getElementById('homeCard').style.display='block';
    }
    function doRegister(){
      const phone = document.getElementById('regPhone').value.trim();
      const p1 = document.getElementById('regPass').value;
      const p2 = document.getElementById('regPass2').value;
      if(!phone || !p1){ alert('Number aur password chahiye'); return }
      if(p1!==p2){ alert('Password match nahi kar raha'); return }
      alert('Registration successful (demo). Verification ke baad bonus milega.');
      showLogin();
    }

    function navTo(page){
      // simple demo: only Home toggles content
      const items = document.querySelectorAll('.nav-item'); items.forEach(i=>i.classList.remove('active'));
      event.currentTarget.classList.add('active');
      if(page==='home'){ document.getElementById('homeCard').style.display='block'; document.getElementById('authCard').style.display='none'; }
      if(page==='mine'){ document.getElementById('homeCard').style.display='none'; document.getElementById('authCard').style.display='block'; showLogin(); }
    }
</body>
</html>
