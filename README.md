<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Salim Investment - Secure Your Financial Future</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * { 
            box-sizing: border-box; 
            margin: 0; 
            padding: 0; 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
        }
        
        :root {
            --primary: #1e40af;
            --secondary: #dc2626;
            --accent: #f59e0b;
            --success: #10b981;
            --dark: #1f2937;
            --light: #f8fafc;
        }
        
        body { 
            background: linear-gradient(135deg, #1e40af 0%, #1e3a8a 100%);
            color: #333; 
            min-height: 100vh;
            padding: 20px;
        }
        
        .container { 
            max-width: 400px; 
            margin: 50px auto; 
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        
        .logo {
            text-align: center;
            font-size: 2.5em;
            font-weight: bold;
            color: var(--primary);
            margin-bottom: 10px;
        }
        
        .logo span {
            color: var(--secondary);
        }
        
        .tagline {
            text-align: center;
            color: #666;
            margin-bottom: 30px;
        }
        
        .form-group {
            margin: 20px 0;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: var(--dark);
        }
        
        input {
            width: 100%;
            padding: 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: border 0.3s ease;
        }
        
        input:focus {
            border-color: var(--primary);
            outline: none;
        }
        
        .btn {
            width: 100%;
            padding: 15px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 10px 0;
        }
        
        .btn-primary {
            background: var(--primary);
            color: white;
        }
        
        .btn-success {
            background: var(--success);
            color: white;
        }
        
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        
        .message {
            text-align: center;
            margin: 15px 0;
            padding: 10px;
            border-radius: 5px;
            font-weight: bold;
        }
        
        .error {
            background: #fee2e2;
            color: var(--secondary);
            border: 1px solid #fecaca;
        }
        
        .success {
            background: #d1fae5;
            color: var(--success);
            border: 1px solid #a7f3d0;
        }
        
        .phone-input {
            display: flex;
        }
        
        .phone-prefix {
            background: #f3f4f6;
            padding: 15px;
            border: 2px solid #ddd;
            border-right: none;
            border-radius: 8px 0 0 8px;
            font-weight: bold;
        }
        
        .phone-input input {
            border-radius: 0 8px 8px 0;
            border-left: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="logo">SALIM<span>INVESTMENT</span></div>
        <div class="tagline">Secure Your Financial Future</div>
        
        <!-- Authentication Form -->
        <div id="authForm">
            <div class="form-group">
                <label><i class="fas fa-mobile-alt"></i> Nepali Mobile Number</label>
                <div class="phone-input">
                    <div class="phone-prefix">+977</div>
                    <input type="tel" id="phone" placeholder="9841234567" maxlength="10">
                </div>
                <small style="color: #666;">Enter 10-digit number (98/97/96...)</small>
            </div>
            
            <div class="form-group">
                <label><i class="fas fa-lock"></i> Password</label>
                <input type="password" id="password" placeholder="Enter password (min 6 characters)">
            </div>
            
            <button class="btn btn-primary" id="signupBtn">
                <i class="fas fa-user-plus"></i> Sign Up - Get 50 NPR Bonus
            </button>
            
            <button class="btn btn-success" id="loginBtn">
                <i class="fas fa-sign-in-alt"></i> Login to Account
            </button>
            
            <div id="authMsg" class="message"></div>
        </div>
    </div>

    <script>
        // Simple Working Authentication System
        const el = id => document.getElementById(id);
        
        // Load users from localStorage
        function getUsers() {
            return JSON.parse(localStorage.getItem('salimUsers')) || [];
        }
        
        // Save users to localStorage
        function saveUsers(users) {
            localStorage.setItem('salimUsers', JSON.stringify(users));
        }
        
        // Validate Nepali number
        function isValidNepaliNumber(phone) {
            return /^(98|97|96)\d{8}$/.test(phone);
        }
        
        // Show message
        function showMessage(message, type = 'error') {
            const msgEl = el('authMsg');
            msgEl.textContent = message;
            msgEl.className = 'message ' + (type === 'error' ? 'error' : 'success');
        }
        
        // Sign Up Function
        el('signupBtn').onclick = function() {
            const phone = el('phone').value.trim();
            const password = el('password').value.trim();
            
            // Validation
            if (!isValidNepaliNumber(phone)) {
                showMessage('Please enter valid Nepali number (98XXXXXXXX)');
                return;
            }
            
            if (password.length < 6) {
                showMessage('Password must be at least 6 characters');
                return;
            }
            
            const users = getUsers();
            const userExists = users.find(user => user.phone === phone);
            
            if (userExists) {
                showMessage('This number is already registered');
                return;
            }
            
            // Create new user
            const newUser = {
                phone: phone,
                password: password,
                balance: 50, // Signup bonus
                joined: new Date().toISOString(),
                invested: false
            };
            
            users.push(newUser);
            saveUsers(users);
            
            // Save current user session
            localStorage.setItem('currentUser', JSON.stringify(newUser));
            
            showMessage('Account created successfully! 50 NPR bonus added.', 'success');
            
            // Redirect to dashboard after 2 seconds
            setTimeout(() => {
                window.location.href = 'dashboard.html';
            }, 2000);
        };
        
        // Login Function
        el('loginBtn').onclick = function() {
            const phone = el('phone').value.trim();
            const password = el('password').value.trim();
            
            if (!isValidNepaliNumber(phone)) {
                showMessage('Please enter valid Nepali number');
                return;
            }
            
            const users = getUsers();
            const user = users.find(u => u.phone === phone && u.password === password);
            
            if (user) {
                // Save current user session
                localStorage.setItem('currentUser', JSON.stringify(user));
                showMessage('Login successful! Redirecting...', 'success');
                
                // Redirect to dashboard
                setTimeout(() => {
                    window.location.href = 'dashboard.html';
                }, 1500);
            } else {
                showMessage('Invalid phone number or password');
            }
        };
        
        // Enter key support
        el('password').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                el('loginBtn').click();
            }
        });
    </script>
</body>
</html>
