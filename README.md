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
            --gradient: linear-gradient(135deg, #1e40af 0%, #1e3a8a 100%);
        }
        
        [data-theme="dark"] {
            --primary: #3b82f6;
            --secondary: #ef4444;
            --accent: #f59e0b;
            --success: #10b981;
            --dark: #f8fafc;
            --light: #1f2937;
            --gradient: linear-gradient(135deg, #1e3a8a 0%, #1e40af 100%);
        }
        
        body { 
            background: var(--gradient);
            color: var(--dark);
            min-height: 100vh;
            transition: all 0.3s ease;
        }
        
        .container { 
            max-width: 1200px; 
            margin: 0 auto; 
            padding: 20px; 
        }
        
        /* Header Styling */
        .header {
            background: var(--light);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        
        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--primary), var(--secondary), var(--accent));
        }
        
        .logo {
            font-size: 3em;
            font-weight: bold;
            color: var(--primary);
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }
        
        .logo span {
            color: var(--secondary);
        }
        
        .tagline {
            color: var(--dark);
            font-size: 1.2em;
            opacity: 0.9;
            font-weight: 500;
        }
        
        .theme-toggle {
            position: absolute;
            top: 20px;
            right: 20px;
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 50%;
            width: 45px;
            height: 45px;
            cursor: pointer;
            font-size: 1.2em;
            transition: all 0.3s ease;
        }
        
        .theme-toggle:hover {
            transform: rotate(30deg);
        }

        /* Card Styling */
        .card { 
            background: var(--light); 
            border-radius: 20px; 
            padding: 30px; 
            margin: 25px 0; 
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
            border-left: 5px solid var(--primary);
            display: none;
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* Button Styling */
        .btn { 
            padding: 14px 28px; 
            border: none; 
            border-radius: 12px; 
            cursor: pointer; 
            margin: 10px;
            font-weight: bold;
            font-size: 15px;
            transition: all 0.3s ease;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }
        
        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.15);
        }
        
        .btn-primary { 
            background: var(--primary); 
            color: white; 
        }
        
        .btn-success { 
            background: var(--success); 
            color: white; 
        }
        
        .btn-danger { 
            background: var(--secondary); 
            color: white; 
        }
        
        .btn-warning { 
            background: var(--accent); 
            color: white; 
        }
        
        /* Form Styling */
        .form-group {
            margin: 20px 0;
        }
        
        input, select { 
            width: 100%; 
            padding: 15px; 
            margin: 10px 0; 
            border: 2px solid #e2e8f0; 
            border-radius: 12px; 
            font-size: 16px;
            transition: all 0.3s ease;
            background: var(--light);
            color: var(--dark);
        }
        
        input:focus, select:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 4px rgba(30, 64, 175, 0.1);
            transform: translateY(-2px);
        }
        
        /* Navigation */
        .nav { 
            background: var(--light); 
            padding: 20px 25px; 
            border-radius: 15px; 
            margin-bottom: 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .user-info {
            font-weight: bold;
            color: var(--primary);
            font-size: 1.1em;
        }
        
        /* Balance Display */
        .balance-card {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            text-align: center;
            padding: 40px 30px;
            border-radius: 20px;
            margin: 25px 0;
            position: relative;
            overflow: hidden;
        }
        
        .balance-card::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 1%, transparent 1%);
            background-size: 20px 20px;
            animation: float 6s ease-in-out infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }
        
        .balance-amount {
            font-size: 3.5em;
            font-weight: bold;
            margin: 15px 0;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }
        
        /* Quick Actions */
        .quick-actions {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }
        
        .action-card {
            background: var(--light);
            padding: 25px 20px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            transition: all 0.3s ease;
            cursor: pointer;
            border: 2px solid transparent;
        }
        
        .action-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 12px 30px rgba(0,0,0,0.15);
            border-color: var(--primary);
        }
        
        .action-icon {
            font-size: 2.5em;
            margin-bottom: 15px;
            color: var(--primary);
        }
        
        /* Investment Plans Grid */
        .plans-grid { 
            display: grid; 
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); 
            gap: 25px; 
            margin: 35px 0;
        }
        
        .plan-card { 
            background: var(--light); 
            padding: 30px 25px; 
            border-radius: 20px; 
            text-align: center;
            border: 3px solid #e2e8f0;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .plan-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 6px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
        }
        
        .plan-card:hover { 
            border-color: var(--primary); 
            transform: translateY(-10px) scale(1.02); 
            box-shadow: 0 15px 40px rgba(0,0,0,0.2);
        }
        
        .plan-amount { 
            font-size: 2.2em; 
            font-weight: bold; 
            color: var(--primary); 
            margin: 15px 0;
        }
        
        .plan-daily { 
            font-size: 1.4em; 
            color: var(--success); 
            font-weight: bold;
        }
        
        .plan-badge {
            background: var(--accent);
            color: white;
            padding: 8px 20px;
            border-radius: 25px;
            font-size: 0.9em;
            position: absolute;
            top: 20px;
            right: 20px;
            font-weight: bold;
        }
        
        /* Payment Methods */
        .payment-methods {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 15px;
            margin: 25px 0;
        }
        
        .payment-card {
            background: var(--light);
            padding: 20px;
            border-radius: 12px;
            text-align: center;
            border: 2px solid #e2e8f0;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .payment-card:hover {
            border-color: var(--primary);
            transform: translateY(-3px);
        }
        
        .payment-card.active {
            border-color: var(--success);
            background: rgba(16, 185, 129, 0.1);
        }
        
        /* Transaction Table */
        .transaction-section {
            background: var(--light);
            border-radius: 20px;
            padding: 30px;
            margin: 30px 0;
        }
        
        table { 
            width: 100%; 
            border-collapse: collapse; 
            margin: 25px 0; 
        }
        
        th, td { 
            padding: 18px; 
            text-align: left; 
            border-bottom: 1px solid #e2e8f0; 
        }
        
        th { 
            background: var(--light); 
            font-weight: bold;
            color: var(--dark);
            font-size: 1.1em;
        }
        
        tr:hover {
            background: rgba(30, 64, 175, 0.05);
        }
        
        /* Footer */
        .footer {
            text-align: center;
            color: white;
            padding: 40px 0;
            margin-top: 50px;
        }
        
        .footer-links {
            margin: 25px 0;
        }
        
        .footer-links a {
            color: white;
            margin: 0 20px;
            text-decoration: none;
            transition: all 0.3s ease;
        }
        
        .footer-links a:hover {
            color: var(--accent);
        }
        
        /* Popup */
        .popup-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            backdrop-filter: blur(5px);
        }
        
        .popup-content {
            background: var(--light);
            padding: 35px;
            border-radius: 20px;
            max-width: 500px;
            width: 90%;
            text-align: center;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            animation: popIn 0.4s ease;
        }
        
        @keyframes popIn {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
        }
        
        /* Loading Spinner */
        .loader {
            border: 4px solid #f3f3f3;
            border-top: 4px solid var(--primary);
            border-radius: 50%;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
            margin: 20px auto;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* Responsive */
        @media (max-width: 768px) {
            .container {
                padding: 15px;
            }
            
            .quick-actions {
                grid-template-columns: 1fr;
            }
            
            .plans-grid {
                grid-template-columns: 1fr;
            }
            
            .nav {
                flex-direction: column;
                gap: 15px;
                text-align: center;
            }
            
            .balance-amount {
                font-size: 2.5em;
            }
            
            .logo {
                font-size: 2.2em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <button class="theme-toggle" id="themeToggle">
                <i class="fas fa-moon"></i>
            </button>
            <div class="logo">SALIM<span>INVESTMENT</span></div>
            <div class="tagline">Secure Your Financial Future With Trusted Investments</div>
        </div>

        <!-- Authentication Card -->
        <div class="card" id="authCard" style="display: block;">
            <h2 style="text-align: center; color: var(--primary); margin-bottom: 25px;">
                <i class="fas fa-lock"></i> Welcome to Salim Investment
            </h2>
            
            <div class="form-group">
                <label style="display: block; margin-bottom: 10px; font-weight: bold; color: var(--dark);">
                    <i class="fas fa-mobile-alt"></i> Nepali Mobile Number:
                </label>
                <div style="display: flex; align-items: center;">
                    <span style="background: var(--light); padding: 15px; border-radius: 12px 0 0 12px; border: 2px solid #e2e8f0; font-weight: bold; border-right: none;">
                        +977
                    </span>
                    <input type="tel" id="phone" placeholder="9841234567" maxlength="10" 
                           style="border-radius: 0 12px 12px 0; margin: 0; border-left: none;">
                </div>
                <small style="color: #666;">Enter your 10-digit Nepali number (98/97/96...)</small>
            </div>
            
            <div class="form-group">
                <label style="display: block; margin-bottom: 10px; font-weight: bold; color: var(--dark);">
                    <i class="fas fa-key"></i> Password:
                </label>
                <input type="password" id="password" placeholder="Create strong password (min 6 characters)">
            </div>
            
            <div style="text-align: center; margin: 30px 0;">
                <button class="btn btn-primary" id="signupBtn">
                    <i class="fas fa-gift"></i> Sign Up - Get 50 NPR Bonus
                </button>
                <button class="btn btn-success" id="loginBtn">
                    <i class="fas fa-sign-in-alt"></i> Login
                </button>
            </div>
            
            <p id="authMsg" style="color: var(--secondary); margin-top: 20px; font-weight: bold; text-align: center;"></p>
        </div>

        <!-- Dashboard Card -->
        <div class="card" id="dashCard">
            <!-- Navigation -->
            <div class="nav">
                <div class="user-info">
                    <i class="fas fa-user"></i> Welcome, <span id="userEmail"></span>
                </div>
                <div>
                    <button class="btn btn-warning" onclick="showSection('investmentSection')">
                        <i class="fas fa-briefcase"></i> Investments
                    </button>
                    <button class="btn btn-primary" onclick="showSection('transactionSection')">
                        <i class="fas fa-chart-bar"></i> Transactions
                    </button>
                    <button class="btn btn-danger" id="logoutBtn">
                        <i class="fas fa-sign-out-alt"></i> Logout
                    </button>
                </div>
            </div>
            
            <!-- Balance Card -->
            <div class="balance-card">
                <div style="font-size: 1.3em; opacity: 0.9;">Your Balance</div>
                <div class="balance-amount" id="balance">NPR 0</div>
                <div style="opacity: 0.8;">Available for withdrawal</div>
            </div>
            
            <!-- Quick Actions -->
            <div class="quick-actions">
                <div class="action-card" onclick="showSection('depositSection')">
                    <div class="action-icon"><i class="fas fa-credit-card"></i></div>
                    <div style="font-weight: bold; font-size: 1.1em;">Deposit</div>
                    <small>Add funds to your account</small>
                </div>
                <div class="action-card" onclick="showSection('withdrawSection')">
                    <div class="action-icon"><i class="fas fa-university"></i></div>
                    <div style="font-weight: bold; font-size: 1.1em;">Withdraw</div>
                    <small>Get your earnings</small>
                </div>
                <div class="action-card" onclick="dailyCheckin()">
                    <div class="action-icon"><i class="fas fa-calendar-check"></i></div>
                    <div style="font-weight: bold; font-size: 1.1em;">Daily Check-in</div>
                    <small>+5 NPR Bonus</small>
                </div>
                <div class="action-card" onclick="spinWheel()">
                    <div class="action-icon"><i class="fas fa-dharmachakra"></i></div>
                    <div style="font-weight: bold; font-size: 1.1em;">Spin Wheel</div>
                    <small>Win up to 40 NPR</small>
                </div>
            </div>

            <!-- Deposit Section -->
            <div class="card" id="depositSection">
                <h3 style="color: var(--primary); margin-bottom: 25px;">
                    <i class="fas fa-credit-card"></i> Deposit Funds
                </h3>
                <input type="number" id="amount" placeholder="Enter amount (minimum 500 NPR)" min="500">
                
                <div style="margin: 25px 0;">
                    <h4 style="margin-bottom: 20px; color: var(--dark);">Select Payment Method:</h4>
                    <div class="payment-methods">
                        <div class="payment-card active" onclick="selectPayment('khalti')">
                            <i class="fas fa-wallet" style="font-size: 2em; color: #5C2D91; margin-bottom: 10px;"></i>
                            <div style="font-weight: bold;">Khalti</div>
                        </div>
                        <div class="payment-card" onclick="selectPayment('esewa')">
                            <i class="fas fa-mobile-alt" style="font-size: 2em; color: #53BEE6; margin-bottom: 10px;"></i>
                            <div style="font-weight: bold;">eSewa</div>
                        </div>
                        <div class="payment-card" onclick="selectPayment('bank')">
                            <i class="fas fa-university" style="font-size: 2em; color: var(--dark); margin-bottom: 10px;"></i>
                            <div style="font-weight: bold;">Bank Transfer</div>
                        </div>
                    </div>
 
