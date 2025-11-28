<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Register</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f5f5f5;
      padding: 20px;
    }
    .container {
      max-width: 400px;
      margin: auto;
      background: #fff;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    h2 {
      text-align: center;
      margin-bottom: 20px;
    }
    input {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      border-radius: 8px;
      border: 1px solid #ccc;
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
    }
    button:hover {
      background: #005fcc;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Create Account</h2>
    <input type="text" placeholder="Full Name" />
    <input type="text" placeholder="Mobile Number" />
    <input type="password" placeholder="Password" />
    <input type="password" placeholder="Confirm Password" />
    <button id="submitBtn">Register</button>
  </div>

  <script>
    document.getElementById("submitBtn").addEventListener("click", function () {
      const name = document.querySelector('input[placeholder="Full Name"]').value;
      const mobile = document.querySelector('input[placeholder="Mobile Number"]').value;
      const password = document.querySelector('input[placeholder="Password"]').value;
      const confirmPassword = document.querySelector('input[placeholder="Confirm Password"]').value;

      // सभी fields check
      if (!name || !mobile || !password || !confirmPassword) {
        alert("कृपया सभी fields भरें!");
        return;
      }

      // Password match check
      if (password !== confirmPassword) {
        alert("Passwords मेल नहीं खाते!");
        return;
      }

      // User data save करना localStorage में
      const users = JSON.parse(localStorage.getItem("users") || "[]");
      users.push({ name, mobile, password });
      localStorage.setItem("users", JSON.stringify(users));

      alert("Registration Successful!");
      // Form साफ करना
      document.querySelectorAll('input').forEach(input => input.value = "");
    });
  </script>
</body>
</html>
