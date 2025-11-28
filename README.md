
<!doctype html>
<html lang="hi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>BRAND_NAME — Join & Earn</title>
  <style>
    :root{--bg:#fff7ed;--accent:#ff7a18;--muted:#666}
    *{box-sizing:border-box}
    body{font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial; margin:0; background:linear-gradient(180deg,var(--bg),#fff); color:#111}
    .wrap{max-width:460px;margin:0 auto;padding:18px}
    .card{background:#fff;border-radius:14px;box-shadow:0 8px 20px rgba(15,15,15,0.08);overflow:hidden}
    header{display:flex;align-items:center;padding:18px;gap:12px}
    header img{width:56px;height:56px;object-fit:contain;border-radius:10px}
    header h1{font-size:18px;margin:0}
    .hero{padding:18px;border-top:1px solid #faf0e6}
    .hero h2{margin:0 0 8px;font-size:20px}
    .benefits{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:12px}
    .chip{background:#fff9f5;border:1px solid rgba(255,122,24,0.08);padding:8px 10px;border-radius:999px;font-size:13px}
    .amount{font-weight:700;color:var(--accent);font-size:26px}

    form{padding:0 18px 18px}
    label{display:block;font-size:13px;color:var(--muted);margin-bottom:6px}
    input[type=text], input[type=tel]{width:100%;padding:12px;border-radius:10px;border:1px solid #eee;font-size:15px}
    .row{display:flex;gap:10px}
    .btn{display:inline-block;width:100%;padding:12px;border-radius:10px;background:linear-gradient(90deg,var(--accent),#ffb06b);color:white;border:0;font-weight:700;font-size:16px;cursor:pointer;margin-top:12px}
    .small{font-size:13px;color:#777;margin-top:10px}
    .footer{padding:14px;text-align:center;font-size:13px;color:#999}

    /* referral banner */
    .ref-banner{background:#fff5eb;border-left:4px solid var(--accent);padding:12px;border-radius:8px;display:flex;justify-content:space-between;align-items:center;margin:10px 18px}
    .ref-code{font-weight:700}

    /* responsive */
    @media(min-width:780px){body{background:#f6f7fb}.wrap{margin-top:36px}}
  </style>
</head>
<body>
  <div class="wrap">
    <div class="card">
      <header>
        <img src="logo.png" alt="BRAND logo" id="brandLogo" />
        <div>
          <h1 id="brandName">BRAND_NAME</h1>
          <div style="font-size:13px;color:#888">Sign up & get instant rewards</div>
        </div>
      </header>

      <div class="hero">
        <h2>Get a bonus of <span class="amount">₹220</span> on registration</h2>
        <div class="benefits">
          <div class="chip">Quick payouts</div>
          <div class="chip">No fees</div>
          <div class="chip">Refer friends</div>
        </div>
        <div class="small">Limited time offer. Simple KYC after signup.</div>
      </div>

      <div class="ref-banner" id="refBanner" style="display:none">
        <div>Referral code:</div>
        <div class="ref-code" id="refCode">-</div>
      </div>

      <form id="regForm" onsubmit="return handleSubmit(event)">
        <label for="name">Full name</label>
        <input type="text" id="name" placeholder="Ram Kumar" required />

        <label for="phone">Mobile number</label>
        <input type="tel" id="phone" placeholder="98XXXXXXXX" pattern="[0-9]{7,15}" required />

        <div class="row">
          <input type="text" id="city" placeholder="City (optional)" />
        </div>

        <button class="btn" type="submit">Register & Claim ₹220</button>

        <div class="small">By continuing you agree to our Terms & Privacy Policy.</div>
      </form>

      <div class="footer">Already registered? <a href="#" onclick="goLogin(event)">Login</a></div>
    </div>

    <div style="text-align:center;margin-top:12px;color:#666;font-size:13px">Download the app later — or use the web version now.</div>
  </div>

  <script>
    // Simple brand variables (edit these or set dynamically)
    const BRAND_NAME = 'TUMHARA_APP';
    const BRAND_LOGO = 'logo.png'; // replace with your logo file

    document.getElementById('brandName').textContent = BRAND_NAME;
    document.getElementById('brandLogo').src = BRAND_LOGO;

    // Parse referral code from URL (example: ?ref=YE4BZH)
    function getParam(name){
      const url = new URL(window.location.href);
      return url.searchParams.get(name) || url.searchParams.get('channelId') || '';
    }

    const ref = getParam('ref') || getParam('channelId') || '';
    if(ref){
      document.getElementById('refCode').textContent = ref;
      document.getElementById('refBanner').style.display = 'flex';
    }

    // Fake submit handler - replace with actual API call
    function handleSubmit(e){
      e.preventDefault();
      const name = document.getElementById('name').value.trim();
      const phone = document.getElementById('phone').value.trim();
      const city = document.getElementById('city').value.trim();

      // Basic validation
      if(!name || !phone){ alert('Name and phone required'); return false; }

      // Simulate request
      const payload = { name, phone, city, ref };
      console.log('Register payload', payload);

      // Show success
      alert('Registration successful! Bonus ₹220 will be credited after verification.');

      // Redirect to success or app store
      // window.location.href = 'success.html';
      return false;
    }

    function goLogin(e){ e.preventDefault(); alert('Show login screen (to be implemented)'); }
  </script>
</body>
</html>
