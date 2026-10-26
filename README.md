<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Verity Bank - Luxury Biometric Banking</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Inter Font -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        gold: {
                            400: '#FBBF24',
                            500: '#F59E0B',
                            600: '#D97706',
                            700: '#B45309',
                        },
                        dark: {
                            950: '#090A0F',
                            900: '#0F1117',
                            800: '#171A23',
                            700: '#232736',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #090A0F;
            color: #F8FAFC;
        }

        /* Face Scan Laser Animation */
        @keyframes scan-laser-gold {
            0% { top: 0%; opacity: 0.8; }
            50% { top: 95%; opacity: 1; }
            100% { top: 0%; opacity: 0.8; }
        }

        .scan-line-gold {
            position: absolute;
            width: 100%;
            height: 3px;
            background: linear-gradient(90deg, transparent, #FBBF24, #F59E0B, #FBBF24, transparent);
            box-shadow: 0 0 15px #FBBF24, 0 0 8px #F59E0B;
            animation: scan-laser-gold 2.2s ease-in-out infinite;
        }

        @keyframes pulse-ring-gold {
            0% { transform: scale(0.97); opacity: 0.8; }
            50% { transform: scale(1.03); opacity: 0.4; }
            100% { transform: scale(0.97); opacity: 0.8; }
        }

        .pulse-border-gold {
            animation: pulse-ring-gold 3s ease-in-out infinite;
        }

        /* Luxury Glassmorphism effects */
        .glass-panel {
            background: rgba(23, 26, 35, 0.75);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(251, 191, 36, 0.12);
        }

        .glass-card {
            background: linear-gradient(135deg, rgba(251,191,36,0.12), rgba(255,255,255,0.02));
            backdrop-filter: blur(20px);
            border: 1px solid rgba(251, 191, 36, 0.25);
        }

        .gold-glow {
            box-shadow: 0 0 25px rgba(245, 158, 11, 0.25);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(9, 10, 15, 0.8);
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(245, 158, 11, 0.4);
            border-radius: 4px;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-gold-500 selection:text-black">

    <!-- Top Navigation Header -->
    <header class="glass-panel sticky top-0 z-30 border-b border-gold-500/20 px-4 lg:px-8 py-3.5 flex items-center justify-between">
        <div class="flex items-center space-x-3 cursor-pointer" onclick="showAuthLanding()">
            <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-amber-600 via-gold-500 to-yellow-300 flex items-center justify-center shadow-lg shadow-gold-500/20">
                <i class="fa-solid font-bold fa-crown text-black text-lg"></i>
            </div>
            <div>
                <span class="text-xl font-extrabold tracking-wider bg-gradient-to-r from-yellow-200 via-gold-400 to-amber-500 bg-clip-text text-transparent">VERITY</span>
                <span class="text-[10px] text-gold-400 font-semibold block tracking-widest uppercase -mt-1">Luxury Biometric Bank</span>
            </div>
        </div>

        <!-- Auth Status & Action Button -->
        <div class="flex items-center space-x-3">
            <div id="authStatusBadge" class="hidden sm:flex items-center space-x-2 px-3 py-1.5 rounded-full bg-dark-800 border border-gold-500/30 text-xs text-amber-200">
                <span class="w-2.5 h-2.5 rounded-full bg-gold-400 animate-pulse"></span>
                <span id="authBadgeRole">VIP Member</span>
            </div>
            
            <button id="authHeaderBtn" onclick="handleHeaderAuthAction()" class="flex items-center space-x-2 bg-gradient-to-r from-amber-500 to-gold-400 hover:from-amber-600 hover:to-gold-500 text-black font-semibold px-4 py-2 rounded-xl text-xs transition-all duration-200 gold-glow active:scale-95">
                <i class="fa-solid fa-right-to-bracket"></i>
                <span id="authHeaderBtnText">Sign In</span>
            </button>
        </div>
    </header>

    <!-- MAIN INTERFACE VIEWPORT -->
    <div id="mainViewport" class="max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 flex-1 flex flex-col justify-center">
        
        <!-- ========================================== -->
        <!-- VIEW 1: AUTHENTICATION (LANDING / LOGIN / SIGNUP) -->
        <!-- ========================================== -->
        <section id="authSection" class="w-full max-w-md mx-auto py-4">
            <div class="glass-panel rounded-3xl p-6 sm:p-8 shadow-2xl border border-gold-500/20 relative">
                
                <!-- Auth Tabs: Sign In vs Sign Up -->
                <div class="flex bg-dark-900 p-1 rounded-xl mb-6 border border-gold-500/10">
                    <button id="tabSigninBtn" onclick="toggleAuthTab('signin')" class="w-1/2 py-2.5 text-xs font-bold rounded-lg transition-all text-black bg-gold-400">
                        Sign In
                    </button>
                    <button id="tabSignupBtn" onclick="toggleAuthTab('signup')" class="w-1/2 py-2.5 text-xs font-bold rounded-lg transition-all text-slate-400 hover:text-slate-200">
                        Create Account
                    </button>
                </div>

                <!-- SIGN IN FORM -->
                <form id="signInForm" onsubmit="handlePasswordLogin(event)" class="space-y-4">
                    <div class="text-center mb-4">
                        <h2 class="text-xl font-bold text-white">Welcome Back</h2>
                        <p class="text-xs text-slate-400 mt-1">Access your secure Verity vault</p>
                    </div>

                    <div>
                        <label class="block text-xs font-medium text-slate-300 mb-1">Username or Email</label>
                        <div class="relative">
                            <span class="absolute left-3.5 top-3 text-gold-400/70"><i class="fa-solid fa-user"></i></span>
                            <input type="text" id="loginUsername" required placeholder="e.g. Tommy Pham" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl pl-10 pr-4 py-2.5 text-sm text-slate-100 outline-none transition">
                        </div>
                    </div>

                    <div>
                        <label class="block text-xs font-medium text-slate-300 mb-1">Password</label>
                        <div class="relative">
                            <span class="absolute left-3.5 top-3 text-gold-400/70"><i class="fa-solid fa-lock"></i></span>
                            <input type="password" id="loginPassword" required placeholder="••••••••" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl pl-10 pr-4 py-2.5 text-sm text-slate-100 outline-none transition">
                        </div>
                    </div>

                    <button type="submit" class="w-full bg-gradient-to-r from-amber-500 to-gold-400 hover:from-amber-600 hover:to-gold-500 text-black font-bold py-3 rounded-xl shadow-lg gold-glow text-sm transition active:scale-[0.99] flex items-center justify-center space-x-2">
                        <span>Sign In Securely</span>
                        <i class="fa-solid fa-arrow-right"></i>
                    </button>

                    <div class="relative my-4 text-center">
                        <div class="absolute inset-0 flex items-center"><div class="w-full border-t border-slate-800"></div></div>
                        <span class="relative bg-dark-800 px-3 text-[10px] text-slate-400 uppercase tracking-widest">or biometrics</span>
                    </div>

                    <button type="button" onclick="openFaceModal('login')" class="w-full bg-dark-900 hover:bg-dark-800 text-gold-400 border border-gold-500/30 font-semibold py-2.5 rounded-xl text-xs transition flex items-center justify-center space-x-2">
                        <i class="fa-solid fa-face-smile text-base"></i>
                        <span>Sign In with Face ID</span>
                    </button>
                </form>

                <!-- SIGN UP FORM -->
                <form id="signUpForm" onsubmit="handleSignUp(event)" class="space-y-4 hidden">
                    <div class="text-center mb-4">
                        <h2 class="text-xl font-bold text-white">Create Account</h2>
                        <p class="text-xs text-amber-400/90 font-medium mt-1"><i class="fa-solid fa-sparkles"></i> New accounts start with $100.00 Initial Deposit</p>
                    </div>

                    <div>
                        <label class="block text-xs font-medium text-slate-300 mb-1">Full Name</label>
                        <input type="text" id="regFullName" required placeholder="e.g. Sarah Jenkins" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl px-4 py-2.5 text-sm text-slate-100 outline-none transition">
                    </div>

                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block text-xs font-medium text-slate-300 mb-1">Username</label>
                            <input type="text" id="regUsername" required placeholder="sjenkins" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl px-3 py-2.5 text-sm text-slate-100 outline-none transition">
                        </div>
                        <div>
                            <label class="block text-xs font-medium text-slate-300 mb-1">Account Type</label>
                            <select id="regAccType" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl px-3 py-2.5 text-sm text-slate-100 outline-none transition">
                                <option value="Checking">Checking Vault ($100)</option>
                                <option value="Savings">Savings</option>
                            </select>
                        </div>
                    </div>

                    <div>
                        <label class="block text-xs font-medium text-slate-300 mb-1">Email Address</label>
                        <input type="email" id="regEmail" required placeholder="sarah@example.com" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl px-4 py-2.5 text-sm text-slate-100 outline-none transition">
                    </div>

                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block text-xs font-medium text-slate-300 mb-1">Password</label>
                            <input type="password" id="regPassword" required placeholder="••••••••" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl px-3 py-2.5 text-sm text-slate-100 outline-none transition">
                        </div>
                        <div>
                            <label class="block text-xs font-medium text-slate-300 mb-1">Confirm Password</label>
                            <input type="password" id="regConfirmPassword" required placeholder="••••••••" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl px-3 py-2.5 text-sm text-slate-100 outline-none transition">
                        </div>
                    </div>

                    <!-- Enrolled Baseline Status in Register -->
                    <div id="signupFaceStatus" class="p-3 bg-dark-950 rounded-xl border border-gold-500/20 flex items-center justify-between text-xs">
                        <span id="signupFaceText" class="text-slate-400"><i class="fa-solid fa-camera text-gold-400 mr-1.5"></i> Face ID optional</span>
                        <button type="button" onclick="openFaceModal('enroll')" class="px-2.5 py-1 bg-gold-500/10 hover:bg-gold-500/20 text-gold-400 border border-gold-500/30 rounded-lg text-[11px] font-semibold">
                            Scan Face
                        </button>
                    </div>

                    <button type="submit" class="w-full bg-gradient-to-r from-amber-500 to-gold-400 hover:from-amber-600 hover:to-gold-500 text-black font-bold py-3 rounded-xl shadow-lg gold-glow text-sm transition active:scale-[0.99]">
                        Register & Claim $100 Initial Balance
                    </button>
                </form>

            </div>
        </section>


        <!-- ========================================== -->
        <!-- VIEW 2: BANKING DASHBOARD                  -->
        <!-- ========================================== -->
        <div id="dashboardApp" class="hidden grid grid-cols-1 lg:grid-cols-12 gap-6 w-full">

            <!-- Sidebar Navigation -->
            <aside class="lg:col-span-3 glass-panel rounded-2xl p-4 flex flex-row lg:flex-col justify-between items-center lg:items-stretch gap-2">
                <div class="w-full">
                    <!-- Profile Card -->
                    <div class="hidden lg:flex items-center space-x-3 p-3 mb-4 rounded-xl bg-dark-950/80 border border-gold-500/20">
                        <div class="relative">
                            <img id="userAvatar" src="https://placehold.co/150x150/171a23/fbbf24?text=VRTY" class="w-11 h-11 rounded-full object-cover border-2 border-gold-400" alt="Avatar">
                            <span id="enrolledStatusDot" class="absolute bottom-0 right-0 w-3 h-3 bg-amber-500 border-2 border-dark-950 rounded-full"></span>
                        </div>
                        <div class="overflow-hidden">
                            <h4 id="userNameDisplay" class="font-bold text-sm text-amber-100 truncate">User Name</h4>
                            <p id="userRoleDisplay" class="text-[11px] text-gold-400 truncate">Account Holder</p>
                            <p id="userAccountNo" class="text-[10px] text-slate-400 font-mono truncate">VRTY-0000-0000</p>
                        </div>
                    </div>

                    <!-- Nav Links -->
                    <nav class="flex lg:flex-col w-full gap-1 justify-around lg:justify-start">
                        <button onclick="switchTab('dashboard')" id="nav-dashboard" class="nav-tab active flex items-center space-x-3 px-4 py-3 rounded-xl text-xs font-bold transition-colors w-full bg-gold-400/10 text-gold-400 border border-gold-500/30">
                            <i class="fa-solid fa-chart-pie text-base"></i>
                            <span class="hidden lg:inline">Dashboard</span>
                        </button>
                        <button onclick="switchTab('transfer')" id="nav-transfer" class="nav-tab flex items-center space-x-3 px-4 py-3 rounded-xl text-xs font-semibold text-slate-400 hover:bg-dark-800 hover:text-amber-200 transition-colors w-full">
                            <i class="fa-solid fa-paper-plane text-base"></i>
                            <span class="hidden lg:inline">Send Money</span>
                        </button>
                        <button onclick="switchTab('statements')" id="nav-statements" class="nav-tab flex items-center space-x-3 px-4 py-3 rounded-xl text-xs font-semibold text-slate-400 hover:bg-dark-800 hover:text-amber-200 transition-colors w-full">
                            <i class="fa-solid fa-receipt text-base"></i>
                            <span class="hidden lg:inline">Activity Logs</span>
                        </button>
                        <button onclick="switchTab('security')" id="nav-security" class="nav-tab flex items-center space-x-3 px-4 py-3 rounded-xl text-xs font-semibold text-slate-400 hover:bg-dark-800 hover:text-amber-200 transition-colors w-full">
                            <i class="fa-solid fa-shield-halved text-base"></i>
                            <span class="hidden lg:inline">Face ID Settings</span>
                        </button>
                    </nav>
                </div>

                <!-- Admin Status Banner -->
                <div class="hidden lg:block pt-4 border-t border-gold-500/10">
                    <div id="adminNoticeCard" class="p-3 bg-dark-950 border border-gold-500/20 rounded-xl text-xs text-amber-300">
                        <div class="flex items-center justify-between mb-1">
                            <span class="font-bold text-[11px]"><i class="fa-solid fa-crown text-gold-400 mr-1"></i> Verity Protection</span>
                        </div>
                        <p class="text-[11px] text-slate-400 leading-relaxed">Transactions biometrically encrypted with Face ID AI engine.</p>
                    </div>
                </div>
            </aside>

            <!-- Dynamic Content Main -->
            <main class="lg:col-span-9 space-y-6">

                <!-- TAB 1: DASHBOARD -->
                <section id="tab-dashboard" class="tab-content space-y-6">
                    <!-- Balance Cards -->
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-5">
                        
                        <!-- Checking Card -->
                        <div class="glass-panel rounded-2xl p-5 relative overflow-hidden group hover:border-gold-500/40 transition-all">
                            <div class="flex justify-between items-start mb-4">
                                <div>
                                    <p class="text-[11px] font-bold text-gold-400 uppercase tracking-wider">Checking Account</p>
                                    <h3 id="checkingBalance" class="text-2xl font-black text-white mt-1">$100.00</h3>
                                </div>
                                <span class="p-2.5 bg-gold-500/10 text-gold-400 rounded-xl border border-gold-500/20">
                                    <i class="fa-solid fa-vault"></i>
                                </span>
                            </div>
                            <div class="flex items-center text-xs text-amber-400/80 font-medium">
                                <span>Verity Vault Active</span>
                            </div>
                        </div>

                        <!-- Savings Card -->
                        <div class="glass-panel rounded-2xl p-5 relative overflow-hidden group hover:border-gold-500/40 transition-all">
                            <div class="flex justify-between items-start mb-4">
                                <div>
                                    <p class="text-[11px] font-bold text-gold-400 uppercase tracking-wider">Savings Account</p>
                                    <h3 id="savingsBalance" class="text-2xl font-black text-white mt-1">$0.00</h3>
                                </div>
                                <span class="p-2.5 bg-gold-500/10 text-gold-400 rounded-xl border border-gold-500/20">
                                    <i class="fa-solid fa-piggy-bank"></i>
                                </span>
                            </div>
                            <div class="flex items-center text-xs text-slate-400 font-medium">
                                <span>5.15% APY High Yield</span>
                            </div>
                        </div>

                        <!-- Quick Actions Widget -->
                        <div class="glass-panel rounded-2xl p-5 flex flex-col justify-between">
                            <p class="text-[11px] font-bold text-gold-400 uppercase tracking-wider mb-2">Fund Operations</p>
                            <div class="grid grid-cols-2 gap-3">
                                <button onclick="triggerDepositModal()" class="flex items-center justify-center space-x-2 bg-gradient-to-r from-amber-500 to-gold-400 hover:from-amber-600 hover:to-gold-500 text-black p-2.5 rounded-xl text-xs font-bold transition-all active:scale-95 shadow-md">
                                    <i class="fa-solid fa-circle-plus"></i>
                                    <span>Add Funds</span>
                                </button>
                                <button onclick="triggerWithdrawModal()" class="flex items-center justify-center space-x-2 bg-dark-900 hover:bg-dark-800 text-rose-400 border border-rose-500/30 p-2.5 rounded-xl text-xs font-bold transition-all active:scale-95">
                                    <i class="fa-solid fa-circle-minus"></i>
                                    <span>Withdraw</span>
                                </button>
                            </div>
                        </div>
                    </div>

                    <!-- Digital Card & Recent Activity Row -->
                    <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                        <!-- Black & Gold Card Visual -->
                        <div class="lg:col-span-5 glass-panel rounded-2xl p-5 flex flex-col justify-between">
                            <div class="flex justify-between items-center mb-4">
                                <h3 class="font-bold text-slate-200 text-xs tracking-wider uppercase">Verity Gold Card</h3>
                                <button id="freezeToggleBtn" onclick="toggleCardFreeze()" class="text-[11px] px-2.5 py-1 rounded-lg bg-dark-950 text-slate-300 border border-gold-500/20 hover:bg-dark-800 transition">
                                    <i class="fa-solid fa-snowflake text-amber-400 mr-1"></i> Active
                                </button>
                            </div>

                            <!-- Card Graphic -->
                            <div id="virtualCard" class="glass-card rounded-2xl p-5 text-white shadow-2xl relative overflow-hidden transition-all duration-300 bg-gradient-to-tr from-black via-dark-900 to-dark-800 border border-gold-500/40">
                                <div class="absolute -right-8 -bottom-8 w-40 h-40 bg-gold-500/10 rounded-full blur-2xl"></div>
                                
                                <div class="flex justify-between items-start mb-8">
                                    <i class="fa-solid fa-microchip text-gold-400 text-3xl"></i>
                                    <span class="font-black tracking-widest text-[11px] text-gold-400 uppercase">VERITY PRIVATE</span>
                                </div>

                                <div class="space-y-1 mb-6">
                                    <p class="text-[10px] text-slate-400 tracking-wider">CARD NUMBER</p>
                                    <p class="font-mono text-base tracking-widest text-amber-200">5942 •••• •••• 1092</p>
                                </div>

                                <div class="flex justify-between items-end text-xs">
                                    <div>
                                        <p class="text-slate-400 text-[9px]">CARD HOLDER</p>
                                        <p id="cardHolderName" class="font-bold tracking-wider text-slate-100 uppercase">USER NAME</p>
                                    </div>
                                    <div>
                                        <p class="text-slate-400 text-[9px]">EXPIRES</p>
                                        <p class="font-mono text-slate-200">12/29</p>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Recent Quick Activity -->
                        <div class="lg:col-span-7 glass-panel rounded-2xl p-5">
                            <div class="flex justify-between items-center mb-4">
                                <h3 class="font-bold text-slate-200 text-xs tracking-wider uppercase">Recent Activity</h3>
                                <button onclick="switchTab('statements')" class="text-xs text-gold-400 hover:underline">View All</button>
                            </div>
                            <div id="dashboardActivityList" class="space-y-3">
                                <!-- Populated dynamically -->
                            </div>
                        </div>
                    </div>
                </section>

                <!-- TAB 2: TRANSFER MONEY (SEND PEOPLE MONEY) -->
                <section id="tab-transfer" class="tab-content hidden space-y-6">
                    <div class="glass-panel rounded-2xl p-6 max-w-2xl mx-auto">
                        <div class="flex items-center space-x-3 mb-6 pb-4 border-b border-gold-500/10">
                            <div class="w-10 h-10 rounded-xl bg-gold-500/10 border border-gold-500/30 flex items-center justify-center text-gold-400">
                                <i class="fa-solid fa-paper-plane"></i>
                            </div>
                            <div>
                                <h2 class="text-base font-bold text-slate-100">Send Money to Anyone</h2>
                                <p class="text-xs text-slate-400">Instant peer-to-peer transfers to any Verity Bank member</p>
                            </div>
                        </div>

                        <form id="transferForm" onsubmit="initiateTransfer(event)" class="space-y-4">
                            <!-- Recipient Picker -->
                            <div>
                                <label class="block text-xs font-medium text-slate-300 mb-1">Select Recipient</label>
                                <select id="recipientSelect" required class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl px-4 py-2.5 text-sm text-slate-100 outline-none transition">
                                    <option value="">-- Choose Member --</option>
                                    <!-- Options populated dynamically -->
                                </select>
                            </div>

                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                                <div>
                                    <label class="block text-xs font-medium text-slate-300 mb-1">Source Account</label>
                                    <select id="transferSourceAccount" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl px-4 py-2.5 text-sm text-slate-100 outline-none transition">
                                        <option value="checking">Checking Vault</option>
                                        <option value="savings">Savings Account</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="block text-xs font-medium text-slate-300 mb-1">Amount ($ USD)</label>
                                    <div class="relative">
                                        <span class="absolute left-3.5 top-2.5 text-gold-400">$</span>
                                        <input type="number" id="transferAmount" min="0.01" step="0.01" required placeholder="0.00" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl pl-8 pr-4 py-2.5 text-sm text-slate-100 outline-none transition">
                                    </div>
                                </div>
                            </div>

                            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                                <div>
                                    <label class="block text-xs font-medium text-slate-300 mb-1">Category</label>
                                    <select id="transferCategory" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl px-4 py-2.5 text-sm text-slate-100 outline-none transition">
                                        <option value="Personal">Personal Transfer</option>
                                        <option value="Business">Business Payment</option>
                                        <option value="Gift">Gift / Bonus</option>
                                        <option value="Investment">Investment</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="block text-xs font-medium text-slate-300 mb-1">Memo / Note (Optional)</label>
                                    <input type="text" id="transferMemo" placeholder="e.g. Dinner split, gift" class="w-full bg-dark-950 border border-gold-500/20 focus:border-gold-400 rounded-xl px-4 py-2.5 text-sm text-slate-100 outline-none transition">
                                </div>
                            </div>

                            <div class="p-3 rounded-xl bg-dark-950 border border-gold-500/20 text-xs text-amber-300/80 flex items-center justify-between">
                                <span><i class="fa-solid fa-shield-halved text-gold-400 mr-1.5"></i> Step-up Face ID triggered for transfers > $500.00</span>
                            </div>

                            <div class="pt-2">
                                <button type="submit" class="w-full bg-gradient-to-r from-amber-500 to-gold-400 hover:from-amber-600 hover:to-gold-500 text-black font-bold py-3 rounded-xl shadow-lg gold-glow flex items-center justify-center space-x-2 transition active:scale-[0.99]">
                                    <i class="fa-solid fa-paper-plane"></i>
                                    <span>Send Funds Instantly</span>
                                </button>
                            </div>
                        </form>
                    </div>
                </section>

                <!-- TAB 3: STATEMENTS -->
                <section id="tab-statements" class="tab-content hidden space-y-6">
                    <div class="glass-panel rounded-2xl p-6">
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-6 pb-4 border-b border-gold-500/10">
                            <div>
                                <h2 class="text-base font-bold text-slate-100">Transaction History Log</h2>
                                <p class="text-xs text-slate-400">Complete record of biometrically verified actions</p>
                            </div>
                            <button onclick="clearActivityLogs()" class="text-xs bg-rose-500/10 text-rose-400 border border-rose-500/20 px-3 py-1.5 rounded-lg hover:bg-rose-500/20 transition">
                                Clear Log History
                            </button>
                        </div>

                        <div class="overflow-x-auto">
                            <table class="w-full text-left text-sm">
                                <thead class="text-xs text-slate-400 uppercase bg-dark-950">
                                    <tr>
                                        <th class="px-4 py-3 rounded-l-lg">Transaction</th>
                                        <th class="px-4 py-3">Category</th>
                                        <th class="px-4 py-3">Date</th>
                                        <th class="px-4 py-3">Status</th>
                                        <th class="px-4 py-3 rounded-r-lg text-right">Amount</th>
                                    </tr>
                                </thead>
                                <tbody id="fullActivityTable" class="divide-y divide-dark-800">
                                    <!-- Populated dynamically -->
                                </tbody>
                            </table>
                        </div>
                    </div>
                </section>

                <!-- TAB 4: SECURITY SETTINGS -->
                <section id="tab-security" class="tab-content hidden space-y-6">
                    <div class="glass-panel rounded-2xl p-6 max-w-3xl mx-auto space-y-6">
                        <div>
                            <h2 class="text-base font-bold text-slate-100">Face ID & Biometric Settings</h2>
                            <p class="text-xs text-slate-400">Manage your facial baseline scan for instant sign-ins and high-value transfers</p>
                        </div>

                        <div class="bg-dark-950 border border-gold-500/20 rounded-2xl p-5 flex flex-col sm:flex-row items-center justify-between gap-4">
                            <div class="flex items-center space-x-4">
                                <div class="relative w-20 h-20 rounded-2xl overflow-hidden border-2 border-gold-400 bg-dark-900 flex items-center justify-center">
                                    <img id="enrolledFacePreview" src="" class="w-full h-full object-cover hidden" alt="Baseline Face">
                                    <i id="enrolledFacePlaceholder" class="fa-solid fa-user-shield text-gold-400 text-3xl"></i>
                                </div>
                                <div>
                                    <h4 class="font-bold text-slate-200 text-sm">Registered Face Baseline</h4>
                                    <p id="enrollmentMeta" class="text-xs text-slate-400 mt-0.5">Status: Not Enrolled</p>
                                    <p class="text-[11px] text-gold-400 mt-1"><i class="fa-solid fa-shield-check"></i> AES-256 Encrypted Profile</p>
                                </div>
                            </div>

                            <button onclick="openFaceModal('enroll')" class="w-full sm:w-auto px-4 py-2.5 bg-gradient-to-r from-amber-500 to-gold-400 hover:from-amber-600 hover:to-gold-500 text-black font-bold rounded-xl text-xs transition active:scale-95 shadow-md">
                                <i class="fa-solid fa-camera mr-1"></i> Update Face Baseline
                            </button>
                        </div>
                    </div>
                </section>

            </main>
        </div>

    </div>

    <!-- Footer -->
    <footer class="glass-panel border-t border-gold-500/10 py-4 px-6 text-center text-xs text-slate-500 mt-auto">
        <p>© 2026 Verity Financial Corp. Encrypted Biometric Banking Systems.</p>
    </footer>


    <!-- ========================================== -->
    <!-- FACE ID SCANNER MODAL WITH HUD OVERLAY     -->
    <!-- ========================================== -->
    <div id="faceModal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-md flex items-center justify-center p-4 hidden">
        <div class="glass-panel max-w-sm w-full rounded-3xl p-6 border border-gold-500/30 shadow-2xl relative flex flex-col items-center text-center">
            
            <button onclick="closeFaceModal()" class="absolute top-4 right-4 text-slate-400 hover:text-white p-2 rounded-full">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>

            <h3 id="modalTitle" class="text-lg font-bold text-slate-100 mb-1">Face ID Scan</h3>
            <p id="modalSubtitle" class="text-xs text-slate-400 mb-5">Align your face inside the golden ring</p>

            <div class="relative w-56 h-56 rounded-full overflow-hidden border-4 border-gold-400 shadow-inner bg-dark-950 mb-5 pulse-border-gold flex items-center justify-center">
                <video id="webcamVideo" autoplay playsinline muted class="w-full h-full object-cover transform -scale-x-100"></video>
                <canvas id="snapshotCanvas" class="hidden"></canvas>

                <!-- Scanning Laser -->
                <div id="scanLaser" class="scan-line-gold"></div>

                <!-- Facial AI Landmarks Grid Graphic Overlay -->
                <svg class="absolute inset-0 w-full h-full pointer-events-none opacity-60" viewBox="0 0 200 200">
                    <circle cx="100" cy="90" r="45" stroke="#FBBF24" stroke-width="1" stroke-dasharray="3,3" fill="none" />
                    <circle cx="82" cy="80" r="4" fill="#F59E0B" />
                    <circle cx="118" cy="80" r="4" fill="#F59E0B" />
                    <path d="M 100 85 L 100 100 L 93 105" stroke="#FBBF24" stroke-width="1.5" fill="none" />
                    <path d="M 85 118 Q 100 128 115 118" stroke="#FBBF24" stroke-width="1.5" fill="none" />
                </svg>

                <div class="absolute inset-0 border-2 border-dashed border-gold-400/50 rounded-full pointer-events-none"></div>

                <!-- Status Overlay -->
                <div id="scanStatusOverlay" class="absolute inset-0 bg-dark-950/80 flex flex-col items-center justify-center space-y-2 hidden">
                    <i id="scanStatusIcon" class="fa-solid fa-spinner fa-spin text-gold-400 text-3xl"></i>
                    <p id="scanStatusText" class="text-xs font-semibold text-slate-200 px-4">Analyzing Face...</p>
                </div>
            </div>

            <div id="scanFeedback" class="w-full text-xs font-medium py-2 px-3 rounded-xl bg-dark-900 text-gold-300 border border-gold-500/20 mb-4">
                <i class="fa-solid fa-camera mr-1"></i> <span id="scanFeedbackText">Camera active. Scanning...</span>
            </div>

            <button id="triggerScanBtn" onclick="executeFaceScan()" class="w-full bg-gradient-to-r from-amber-500 to-gold-400 hover:from-amber-600 hover:to-gold-500 text-black font-bold py-3 rounded-xl text-sm shadow-lg gold-glow transition active:scale-95">
                Scan & Verify
            </button>
        </div>
    </div>


    <!-- ========================================== -->
    <!-- ADD FUNDS / WITHDRAW MODAL                 -->
    <!-- ========================================== -->
    <div id="quickFundsModal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-sm flex items-center justify-center p-4 hidden">
        <div class="glass-panel max-w-md w-full rounded-2xl p-6 border border-gold-500/30 shadow-2xl relative">
            <button onclick="closeFundsModal()" class="absolute top-4 right-4 text-slate-400 hover:text-white">
                <i class="fa-solid fa-xmark"></i>
            </button>

            <h3 id="fundsModalTitle" class="text-base font-bold text-slate-100 mb-4">Deposit Money</h3>
            
            <div class="space-y-4">
                <div>
                    <label class="block text-xs text-slate-400 mb-1">Select Target Account</label>
                    <select id="fundsAccountSelect" class="w-full bg-dark-950 border border-gold-500/20 rounded-xl px-3 py-2 text-sm text-slate-200 outline-none">
                        <option value="checking">Checking Vault</option>
                        <option value="savings">Savings Account</option>
                    </select>
                </div>
                <div>
                    <label class="block text-xs text-slate-400 mb-1">Amount ($ USD)</label>
                    <input type="number" id="fundsAmountInput" min="1" step="0.01" placeholder="100.00" class="w-full bg-dark-950 border border-gold-500/20 rounded-xl px-3 py-2 text-sm text-slate-200 outline-none">
                </div>
                <button onclick="processQuickFunds()" class="w-full bg-gradient-to-r from-amber-500 to-gold-400 text-black font-bold py-2.5 rounded-xl text-xs gold-glow transition">
                    Confirm Transaction
                </button>
            </div>
        </div>
    </div>


    <!-- APP LOGIC & SYSTEM CONTROLLER -->
    <script>
        /* ==========================================
           HARDCODED ADMIN & DEFAULT DATABASE SETUP
           ========================================== */
        const ADMIN_ACCOUNT = {
            id: 'admin_tommy',
            fullName: 'Tommy Pham',
            username: 'Tommy Pham',
            email: 'tommypham@verity.com',
            password: 'tommy2013',
            checkingBalance: 999999999.00,
            savingsBalance: 50000000.00,
            accountNo: 'VRTY-8888-9999',
            role: 'Admin / VIP Member',
            faceBaseline: null,
            activities: [
                { id: 101, title: 'VIP Capital Deposit', category: 'Investment', date: 'Oct 26, 2026', amount: 999999999.00, verified: true }
            ]
        };

        const DEMO_USER_SARAH = {
            id: 'usr_demo_1',
            fullName: 'Sarah Jenkins',
            username: 'sjenkins',
            email: 'sarah@verity.com',
            password: 'password123',
            checkingBalance: 100.00, // Starts at $100
            savingsBalance: 0.00,
            accountNo: 'VRTY-1001-2002',
            role: 'Standard Member',
            faceBaseline: null,
            activities: [
                { id: 201, title: 'Welcome Bonus Deposit', category: 'Initial Bonus', date: 'Oct 26, 2026', amount: 100.00, verified: true }
            ]
        };

        let systemState = {
            users: [],
            activeUser: null
        };

        let activeScanPurpose = 'login';
        let pendingTransferData = null;
        let mediaStream = null;
        let tempSignupFace = null;

        // Sound Synthesis Engine
        const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        function playTone(type) {
            try {
                const osc = audioCtx.createOscillator();
                const gain = audioCtx.createGain();
                osc.connect(gain);
                gain.connect(audioCtx.destination);

                if (type === 'success') {
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(587.33, audioCtx.currentTime); 
                    osc.frequency.exponentialRampToValueAtTime(880, audioCtx.currentTime + 0.15); 
                    gain.gain.setValueAtTime(0.15, audioCtx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
                    osc.start();
                    osc.stop(audioCtx.currentTime + 0.3);
                } else if (type === 'error') {
                    osc.type = 'triangle';
                    osc.frequency.setValueAtTime(250, audioCtx.currentTime);
                    osc.frequency.setValueAtTime(150, audioCtx.currentTime + 0.1);
                    gain.gain.setValueAtTime(0.2, audioCtx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.25);
                    osc.start();
                    osc.stop(audioCtx.currentTime + 0.25);
                }
            } catch (e) { console.error(e); }
        }

        // Initialize Database
        window.onload = function() {
            initDatabase();
        };

        function initDatabase() {
            const raw = localStorage.getItem('verity_bank_db');
            if (raw) {
                try {
                    systemState = JSON.parse(raw);
                } catch(e) { console.error(e); }
            }

            // Ensure Admin Tommy Pham exists
            let adminIndex = systemState.users.findIndex(u => u.username.toLowerCase() === 'tommy pham' || u.username.toLowerCase() === 'tommypham');
            if (adminIndex === -1) {
                systemState.users.push(ADMIN_ACCOUNT);
            }

            // Ensure Demo User exists for recipient testing
            let demoIndex = systemState.users.findIndex(u => u.username.toLowerCase() === 'sjenkins');
            if (demoIndex === -1) {
                systemState.users.push(DEMO_USER_SARAH);
            }

            saveDatabase();

            // Restore persistent active session if valid
            if (systemState.activeUser) {
                const refreshed = systemState.users.find(u => u.id === systemState.activeUser.id);
                if (refreshed) {
                    systemState.activeUser = refreshed;
                    showDashboard();
                } else {
                    showAuthLanding();
                }
            } else {
                showAuthLanding();
            }
        }

        function saveDatabase() {
            if (systemState.activeUser) {
                const idx = systemState.users.findIndex(u => u.id === systemState.activeUser.id);
                if (idx !== -1) {
                    systemState.users[idx] = systemState.activeUser;
                }
            }
            localStorage.setItem('verity_bank_db', JSON.stringify(systemState));
            if (systemState.activeUser) renderDashboardUI();
        }

        /* ==========================================
           AUTHENTICATION & SCREEN SWITCHING
           ========================================== */
        function showAuthLanding() {
            document.getElementById('authSection').classList.remove('hidden');
            document.getElementById('dashboardApp').classList.add('hidden');
            document.getElementById('authStatusBadge').classList.add('hidden');
            document.getElementById('authHeaderBtnText').innerText = 'Sign In';
        }

        function showDashboard() {
            document.getElementById('authSection').classList.add('hidden');
            document.getElementById('dashboardApp').classList.remove('hidden');
            document.getElementById('authStatusBadge').classList.remove('hidden');
            document.getElementById('authHeaderBtnText').innerText = 'Sign Out';
            populateRecipientOptions();
            renderDashboardUI();
        }

        function toggleAuthTab(tab) {
            const signinBtn = document.getElementById('tabSigninBtn');
            const signupBtn = document.getElementById('tabSignupBtn');
            const signinForm = document.getElementById('signInForm');
            const signupForm = document.getElementById('signUpForm');

            if (tab === 'signin') {
                signinBtn.className = 'w-1/2 py-2.5 text-xs font-bold rounded-lg transition-all text-black bg-gold-400';
                signupBtn.className = 'w-1/2 py-2.5 text-xs font-bold rounded-lg transition-all text-slate-400 hover:text-slate-200';
                signinForm.classList.remove('hidden');
                signupForm.classList.add('hidden');
            } else {
                signupBtn.className = 'w-1/2 py-2.5 text-xs font-bold rounded-lg transition-all text-black bg-gold-400';
                signinBtn.className = 'w-1/2 py-2.5 text-xs font-bold rounded-lg transition-all text-slate-400 hover:text-slate-200';
                signupForm.classList.remove('hidden');
                signinForm.classList.add('hidden');
            }
        }

        function handleHeaderAuthAction() {
            if (systemState.activeUser) {
                // Sign Out
                systemState.activeUser = null;
                saveDatabase();
                showAuthLanding();
                alertToast('Successfully signed out.');
            } else {
                showAuthLanding();
            }
        }

        // Standard Password Login
        function handlePasswordLogin(e) {
            e.preventDefault();
            const inputUser = document.getElementById('loginUsername').value.trim();
            const inputPass = document.getElementById('loginPassword').value;

            const userMatch = systemState.users.find(u => 
                u.username.toLowerCase() === inputUser.toLowerCase() || 
                u.email.toLowerCase() === inputUser.toLowerCase()
            );

            if (userMatch && userMatch.password === inputPass) {
                systemState.activeUser = userMatch;
                saveDatabase();
                showDashboard();
                playTone('success');
                alertToast(`Welcome back, ${userMatch.fullName}!`);
            } else {
                playTone('error');
                alertToast('Invalid credentials. Check username or password.');
            }
        }

        // Register Account (EVERY DEFAULT NEW ACCOUNT GETS $100.00 STARTING BALANCE)
        function handleSignUp(e) {
            e.preventDefault();
            const fullName = document.getElementById('regFullName').value.trim();
            const username = document.getElementById('regUsername').value.trim();
            const email = document.getElementById('regEmail').value.trim();
            const pass = document.getElementById('regPassword').value;
            const confirmPass = document.getElementById('regConfirmPassword').value;

            if (pass !== confirmPass) {
                alertToast('Passwords do not match!');
                playTone('error');
                return;
            }

            const existing = systemState.users.find(u => u.username.toLowerCase() === username.toLowerCase());
            if (existing) {
                alertToast('Username already taken.');
                playTone('error');
                return;
            }

            const newUser = {
                id: 'usr_' + Date.now(),
                fullName,
                username,
                email,
                password: pass,
                checkingBalance: 100.00, // DEFAULT $100 STARTING BALANCE
                savingsBalance: 0.00,
                accountNo: 'VRTY-' + Math.floor(1000 + Math.random() * 9000) + '-' + Math.floor(1000 + Math.random() * 9000),
                role: 'Standard Member',
                faceBaseline: tempSignupFace,
                activities: [
                    { id: Date.now(), title: 'Initial Welcome Bonus', category: 'Bonus', date: 'Just now', amount: 100.00, verified: true }
                ]
            };

            systemState.users.push(newUser);
            systemState.activeUser = newUser;
            tempSignupFace = null;
            saveDatabase();
            showDashboard();
            playTone('success');
            alertToast(`Account registered! $100.00 initial balance added for ${fullName}.`);
        }

        /* ==========================================
           RENDER DASHBOARD STATE & RECIPIENT SELECT
           ========================================== */
        function renderDashboardUI() {
            const user = systemState.activeUser;
            if (!user) return;

            // Header/Sidebar user info
            document.getElementById('userNameDisplay').innerText = user.fullName;
            document.getElementById('userRoleDisplay').innerText = user.role || 'Member';
            document.getElementById('userAccountNo').innerText = user.accountNo;
            document.getElementById('cardHolderName').innerText = user.fullName;
            document.getElementById('authBadgeRole').innerText = user.role;

            // Dynamic Balances
            document.getElementById('checkingBalance').innerText = `$${user.checkingBalance.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
            document.getElementById('savingsBalance').innerText = `$${user.savingsBalance.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;

            // Face Image Settings
            const faceImg = document.getElementById('enrolledFacePreview');
            const facePlaceholder = document.getElementById('enrolledFacePlaceholder');
            const enrollMeta = document.getElementById('enrollmentMeta');
            const statusDot = document.getElementById('enrolledStatusDot');
            const avatar = document.getElementById('userAvatar');

            if (user.faceBaseline) {
                faceImg.src = user.faceBaseline;
                avatar.src = user.faceBaseline;
                faceImg.classList.remove('hidden');
                facePlaceholder.classList.add('hidden');
                enrollMeta.innerText = 'Status: Enrolled & Active';
                statusDot.className = 'absolute bottom-0 right-0 w-3 h-3 bg-amber-400 border-2 border-dark-950 rounded-full';
            } else {
                faceImg.classList.add('hidden');
                facePlaceholder.classList.remove('hidden');
                enrollMeta.innerText = 'Status: No Face Scan Baseline';
                statusDot.className = 'absolute bottom-0 right-0 w-3 h-3 bg-rose-500 border-2 border-dark-950 rounded-full';
            }

            renderActivityLists(user.activities || []);
        }

        function populateRecipientOptions() {
            const recipientSelect = document.getElementById('recipientSelect');
            if (!recipientSelect) return;

            recipientSelect.innerHTML = '<option value="">-- Select Member --</option>';

            systemState.users.forEach(user => {
                if (systemState.activeUser && user.id === systemState.activeUser.id) return; // Skip self
                const opt = document.createElement('option');
                opt.value = user.id;
                opt.innerText = `${user.fullName} (${user.accountNo}) - @${user.username}`;
                recipientSelect.appendChild(opt);
            });
        }

        function renderActivityLists(activities) {
            const dashList = document.getElementById('dashboardActivityList');
            const fullTable = document.getElementById('fullActivityTable');

            dashList.innerHTML = '';
            fullTable.innerHTML = '';

            if (activities.length === 0) {
                dashList.innerHTML = `<p class="text-xs text-slate-500 py-4 text-center">No transactions logged yet.</p>`;
                return;
            }

            activities.forEach(item => {
                const isPos = item.amount >= 0;
                const amtFormatted = `${isPos ? '+' : ''}$${Math.abs(item.amount).toLocaleString('en-US', {minimumFractionDigits: 2})}`;
                
                const dashRow = document.createElement('div');
                dashRow.className = 'flex items-center justify-between p-3 rounded-xl bg-dark-950 border border-gold-500/10';
                dashRow.innerHTML = `
                    <div class="flex items-center space-x-3">
                        <div class="w-8 h-8 rounded-lg ${isPos ? 'bg-gold-500/10 text-gold-400' : 'bg-dark-800 text-slate-300'} flex items-center justify-center text-xs">
                            <i class="fa-solid ${isPos ? 'fa-arrow-down' : 'fa-arrow-up'}"></i>
                        </div>
                        <div>
                            <p class="text-xs font-bold text-slate-200">${item.title}</p>
                            <p class="text-[10px] text-slate-400">${item.date}</p>
                        </div>
                    </div>
                    <span class="text-xs font-bold ${isPos ? 'text-gold-400' : 'text-slate-200'}">${amtFormatted}</span>
                `;
                dashList.appendChild(dashRow);

                const tr = document.createElement('tr');
                tr.className = 'hover:bg-dark-900 transition';
                tr.innerHTML = `
                    <td class="px-4 py-3 font-semibold text-slate-200">${item.title}</td>
                    <td class="px-4 py-3 text-slate-400 text-xs">${item.category}</td>
                    <td class="px-4 py-3 text-slate-400 text-xs">${item.date}</td>
                    <td class="px-4 py-3">
                        <span class="inline-flex items-center px-2 py-0.5 rounded text-[10px] font-bold bg-gold-500/10 text-gold-400 border border-gold-500/20">
                            <i class="fa-solid fa-face-smile mr-1"></i> Verified
                        </span>
                    </td>
                    <td class="px-4 py-3 text-right font-bold ${isPos ? 'text-gold-400' : 'text-slate-200'}">${amtFormatted}</td>
                `;
                fullTable.appendChild(tr);
            });
        }

        /* ==========================================
           TAB NAVIGATION
           ========================================== */
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.nav-tab').forEach(el => {
                el.classList.remove('bg-gold-400/10', 'text-gold-400', 'border', 'border-gold-500/30');
                el.classList.add('text-slate-400');
            });

            document.getElementById(`tab-${tabId}`).classList.remove('hidden');
            const navBtn = document.getElementById(`nav-${tabId}`);
            if (navBtn) {
                navBtn.classList.add('bg-gold-400/10', 'text-gold-400', 'border', 'border-gold-500/30');
                navBtn.classList.remove('text-slate-400');
            }

            if (tabId === 'transfer') {
                populateRecipientOptions();
            }
        }

        /* ==========================================
           FACIAL RECOGNITION CAMERA & SCANNER
           ========================================== */
        async function openFaceModal(purpose) {
            activeScanPurpose = purpose;
            const modal = document.getElementById('faceModal');
            const title = document.getElementById('modalTitle');
            const sub = document.getElementById('modalSubtitle');
            const btn = document.getElementById('triggerScanBtn');

            if (purpose === 'enroll') {
                title.innerText = 'Enroll Face ID Baseline';
                sub.innerText = 'Capture clear facial geometry baseline';
                btn.innerText = 'Save Face Profile';
            } else if (purpose === 'login') {
                title.innerText = 'Face ID Authentication';
                sub.innerText = 'Verify face scan to unlock account';
                btn.innerText = 'Authenticate Face ID';
            } else if (purpose === 'transfer') {
                title.innerText = 'Biometric Authorization Required';
                sub.innerText = `High-value transfer over $500 ($${pendingTransferData?.amount.toFixed(2)})`;
                btn.innerText = 'Biometrically Authorize';
            }

            document.getElementById('scanStatusOverlay').classList.add('hidden');
            modal.classList.remove('hidden');

            try {
                mediaStream = await navigator.mediaDevices.getUserMedia({ video: { width: 400, height: 400, facingMode: 'user' } });
                const video = document.getElementById('webcamVideo');
                video.srcObject = mediaStream;
                document.getElementById('scanFeedbackText').innerText = 'Camera feed active.';
            } catch (err) {
                console.error('Camera Access Error:', err);
                document.getElementById('scanFeedbackText').innerText = 'Webcam simulated. Click scan to complete verification.';
            }
        }

        function closeFaceModal() {
            document.getElementById('faceModal').classList.add('hidden');
            if (mediaStream) {
                mediaStream.getTracks().forEach(track => track.stop());
            }
        }

        function executeFaceScan() {
            const overlay = document.getElementById('scanStatusOverlay');
            const overlayIcon = document.getElementById('scanStatusIcon');
            const overlayText = document.getElementById('scanStatusText');

            overlay.classList.remove('hidden');
            overlayIcon.className = 'fa-solid fa-spinner fa-spin text-gold-400 text-3xl';
            overlayText.innerText = 'Matching Facial Geometry...';

            // Capture Snapshot
            const video = document.getElementById('webcamVideo');
            const canvas = document.getElementById('snapshotCanvas');
            canvas.width = 300;
            canvas.height = 300;
            const ctx = canvas.getContext('2d');
            ctx.drawImage(video, 0, 0, 300, 300);
            const snapshotData = canvas.toDataURL('image/jpeg', 0.85);

            setTimeout(() => {
                if (activeScanPurpose === 'enroll') {
                    if (systemState.activeUser) {
                        systemState.activeUser.faceBaseline = snapshotData;
                        saveDatabase();
                    } else {
                        tempSignupFace = snapshotData;
                        document.getElementById('signupFaceText').innerHTML = `<i class="fa-solid fa-circle-check text-gold-400 mr-1.5"></i> Face ID Captured!`;
                    }
                    overlayIcon.className = 'fa-solid fa-circle-check text-gold-400 text-4xl';
                    overlayText.innerText = 'Face Baseline Registered!';
                    playTone('success');
                } 
                else if (activeScanPurpose === 'login') {
                    const match = systemState.users.find(u => u.faceBaseline) || systemState.users[0];
                    if (match) {
                        systemState.activeUser = match;
                        saveDatabase();
                        showDashboard();
                        overlayIcon.className = 'fa-solid fa-circle-check text-gold-400 text-4xl';
                        overlayText.innerText = `Verified: Welcome ${match.fullName}!`;
                        playTone('success');
                    } else {
                        overlayIcon.className = 'fa-solid fa-circle-xmark text-rose-400 text-4xl';
                        overlayText.innerText = 'No face profile found';
                        playTone('error');
                    }
                }
                else if (activeScanPurpose === 'transfer') {
                    executeTransferAction();
                    overlayIcon.className = 'fa-solid fa-circle-check text-gold-400 text-4xl';
                    overlayText.innerText = 'Face ID Verified & Sent!';
                    playTone('success');
                }

                setTimeout(() => {
                    closeFaceModal();
                }, 1200);

            }, 1400);
        }

        /* ==========================================
           P2P MONEY TRANSFER SYSTEM (SEND MONEY)
           ========================================== */
        function initiateTransfer(e) {
            e.preventDefault();
            const recipientId = document.getElementById('recipientSelect').value;
            const sourceAcc = document.getElementById('transferSourceAccount').value;
            const amount = parseFloat(document.getElementById('transferAmount').value);
            const category = document.getElementById('transferCategory').value;
            const memo = document.getElementById('transferMemo').value.trim();

            if (!systemState.activeUser) return;
            if (!recipientId) {
                alertToast('Please select a recipient account.');
                playTone('error');
                return;
            }

            const recipientUser = systemState.users.find(u => u.id === recipientId);
            if (!recipientUser) {
                alertToast('Selected recipient not found.');
                playTone('error');
                return;
            }

            const currentBalance = sourceAcc === 'checking' ? systemState.activeUser.checkingBalance : systemState.activeUser.savingsBalance;

            if (amount > currentBalance) {
                alertToast(`Insufficient funds! Your ${sourceAcc} balance is $${currentBalance.toFixed(2)}.`);
                playTone('error');
                return;
            }

            pendingTransferData = {
                recipientId,
                recipientUser,
                sourceAcc,
                amount,
                category,
                memo
            };

            // TRIGGER STEP-UP FACE ID FOR TRANSFERS OVER $500
            if (amount > 500) {
                openFaceModal('transfer');
            } else {
                executeTransferAction();
            }
        }

        function executeTransferAction() {
            if (!pendingTransferData || !systemState.activeUser) return;

            const sender = systemState.activeUser;
            const receiver = pendingTransferData.recipientUser;
            const amount = pendingTransferData.amount;
            const sourceAcc = pendingTransferData.sourceAcc;
            const category = pendingTransferData.category;
            const memo = pendingTransferData.memo ? ` (${pendingTransferData.memo})` : '';

            // Deduct from sender
            if (sourceAcc === 'checking') {
                sender.checkingBalance -= amount;
            } else {
                sender.savingsBalance -= amount;
            }

            // Add to receiver checking balance by default
            const receiverIdx = systemState.users.findIndex(u => u.id === receiver.id);
            if (receiverIdx !== -1) {
                systemState.users[receiverIdx].checkingBalance += amount;
                
                // Log activity for Receiver
                systemState.users[receiverIdx].activities.unshift({
                    id: Date.now() + 1,
                    title: `Received from ${sender.fullName}${memo}`,
                    category: category,
                    date: 'Just now',
                    amount: amount,
                    verified: true
                });
            }

            // Log activity for Sender
            sender.activities.unshift({
                id: Date.now(),
                title: `Sent to ${receiver.fullName}${memo}`,
                category: category,
                date: 'Just now',
                amount: -amount,
                verified: true
            });

            pendingTransferData = null;
            document.getElementById('transferForm').reset();
            saveDatabase();
            switchTab('dashboard');
            playTone('success');
            alertToast(`Successfully sent $${amount.toFixed(2)} to ${receiver.fullName}!`);
        }

        /* ==========================================
           QUICK DEPOSITS & WITHDRAWALS
           ========================================== */
        function triggerDepositModal() {
            document.getElementById('fundsModalTitle').innerText = 'Deposit Money';
            document.getElementById('quickFundsModal').classList.remove('hidden');
        }

        function triggerWithdrawModal() {
            document.getElementById('fundsModalTitle').innerText = 'Withdraw Money';
            document.getElementById('quickFundsModal').classList.remove('hidden');
        }

        function closeFundsModal() {
            document.getElementById('quickFundsModal').classList.add('hidden');
        }

        function processQuickFunds() {
            const isDeposit = document.getElementById('fundsModalTitle').innerText.includes('Deposit');
            const accountType = document.getElementById('fundsAccountSelect').value;
            const amount = parseFloat(document.getElementById('fundsAmountInput').value);

            if (!amount || amount <= 0 || !systemState.activeUser) return;

            if (!isDeposit) {
                const currentBal = accountType === 'checking' ? systemState.activeUser.checkingBalance : systemState.activeUser.savingsBalance;
                if (amount > currentBal) {
                    alertToast('Withdrawal exceeds account balance.');
                    playTone('error');
                    return;
                }
            }

            if (accountType === 'checking') {
                systemState.activeUser.checkingBalance += isDeposit ? amount : -amount;
            } else {
                systemState.activeUser.savingsBalance += isDeposit ? amount : -amount;
            }

            systemState.activeUser.activities.unshift({
                id: Date.now(),
                title: `${isDeposit ? 'Deposit' : 'Withdrawal'} (${accountType})`,
                category: 'Adjustment',
                date: 'Just now',
                amount: isDeposit ? amount : -amount,
                verified: true
            });

            closeFundsModal();
            saveDatabase();
            playTone('success');
            alertToast(`${isDeposit ? 'Deposited' : 'Withdrew'} $${amount.toFixed(2)} successfully!`);
        }

        function toggleCardFreeze() {
            const card = document.getElementById('virtualCard');
            const btn = document.getElementById('freezeToggleBtn');
            const isFrozen = card.classList.toggle('opacity-40');
            card.classList.toggle('grayscale');

            if (isFrozen) {
                btn.innerHTML = '<i class="fa-solid fa-lock text-rose-400 mr-1"></i> Frozen';
            } else {
                btn.innerHTML = '<i class="fa-solid fa-snowflake text-amber-400 mr-1"></i> Active';
            }
        }

        function clearActivityLogs() {
            if (systemState.activeUser) {
                systemState.activeUser.activities = [];
                saveDatabase();
                alertToast('Activity history cleared.');
            }
        }

        function alertToast(msg) {
            const toast = document.createElement('div');
            toast.className = 'fixed bottom-5 right-5 z-50 glass-panel border border-gold-400/50 bg-dark-950/90 text-amber-100 text-xs font-semibold px-4 py-3 rounded-xl shadow-2xl flex items-center space-x-2.5 animate-bounce';
            toast.innerHTML = `<i class="fa-solid fa-circle-info text-gold-400 text-base"></i><span>${msg}</span>`;
            document.body.appendChild(toast);
            setTimeout(() => toast.remove(), 3200);
        }
    </script>
</body>
</html>
