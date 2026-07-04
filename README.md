# Galext Enterprises
Here's the full source code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GALEXT — Connect Beyond Limits</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg:        #050d1a;
    --surface:   #0b1a2e;
    --card:      #0f2236;
    --border:    rgba(0,210,200,0.15);
    --accent:    #00d4c8;
    --accent2:   #7b61ff;
    --gold:      #f0b429;
    --text:      #e8f4f8;
    --muted:     #7a9bb5;
    --danger:    #ff4d6d;
    --success:   #00c48c;
    --radius:    14px;
    --font-head: 'Space Grotesk', sans-serif;
    --font-body: 'Inter', sans-serif;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-body);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ─── PAGE SYSTEM ─── */
  .page { display: none; min-height: 100vh; }
  .page.active { display: flex; flex-direction: column; }

  /* ─── NAV ─── */
  nav {
    display: flex; align-items: center; justify-content: space-between;
    padding: 18px 32px;
    background: rgba(5,13,26,0.85);
    backdrop-filter: blur(14px);
    border-bottom: 1px solid var(--border);
    position: sticky; top: 0; z-index: 100;
  }
  .nav-logo {
    font-family: var(--font-head);
    font-size: 1.5rem; font-weight: 700;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    letter-spacing: 2px;
  }
  .nav-tabs { display: flex; gap: 4px; background: var(--surface); border-radius: 10px; padding: 4px; }
  .nav-tab {
    padding: 8px 20px; border: none; background: transparent;
    color: var(--muted); font-family: var(--font-body); font-size: 0.875rem;
    border-radius: 7px; cursor: pointer; transition: all 0.2s;
  }
  .nav-tab.active, .nav-tab:hover { background: var(--card); color: var(--accent); }

  /* ─── HERO ─── */
  .hero {
    flex: 1; display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    padding: 60px 24px;
    position: relative; overflow: hidden;
  }
  .hero-glow {
    position: absolute; width: 600px; height: 600px; border-radius: 50%;
    background: radial-gradient(circle, rgba(0,212,200,0.08) 0%, transparent 70%);
    top: 50%; left: 50%; transform: translate(-50%, -50%);
    pointer-events: none;
  }
  .avatar-wrap { position: relative; margin-bottom: 32px; }
  .avatar-ring {
    width: 130px; height: 130px; border-radius: 50%;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    padding: 3px; animation: spin-ring 6s linear infinite;
  }
  @keyframes spin-ring {
    0%   { filter: hue-rotate(0deg); }
    100% { filter: hue-rotate(360deg); }
  }
  .avatar-inner {
    width: 100%; height: 100%; border-radius: 50%;
    background: var(--surface);
    display: flex; align-items: center; justify-content: center;
    font-size: 3rem; overflow: hidden;
  }
  .status-dot {
    position: absolute; bottom: 6px; right: 6px;
    width: 18px; height: 18px; border-radius: 50%;
    background: var(--success);
    border: 3px solid var(--bg);
    animation: pulse-dot 2s infinite;
  }
  @keyframes pulse-dot {
    0%, 100% { box-shadow: 0 0 0 0 rgba(0,196,140,0.4); }
    50%       { box-shadow: 0 0 0 8px rgba(0,196,140,0); }
  }
  .hero h1 {
    font-family: var(--font-head); font-size: clamp(2rem, 6vw, 3.5rem);
    font-weight: 700; text-align: center; line-height: 1.1; margin-bottom: 12px;
  }
  .hero h1 span {
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  }
  .hero-sub {
    color: var(--muted); font-size: 1.05rem; text-align: center;
    max-width: 480px; line-height: 1.6; margin-bottom: 40px;
  }
  .hero-cta { display: flex; gap: 12px; flex-wrap: wrap; justify-content: center; }

  /* ─── BUTTONS ─── */
  .btn {
    padding: 12px 28px; border-radius: 10px; font-size: 0.9rem;
    font-weight: 600; cursor: pointer; border: none;
    font-family: var(--font-body); transition: all 0.2s; letter-spacing: 0.3px;
  }
  .btn-primary {
    background: linear-gradient(135deg, var(--accent), var(--accent2)); color: #fff;
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(0,212,200,0.3); }
  .btn-ghost { background: transparent; color: var(--text); border: 1px solid var(--border); }
  .btn-ghost:hover { border-color: var(--accent); color: var(--accent); }
  .btn-danger { background: var(--danger); color: #fff; }
  .btn-danger:hover { opacity: 0.85; }
  .btn-full { width: 100%; }

  /* ─── FEATURE CARDS ─── */
  .features {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 16px; padding: 40px 32px; max-width: 1100px; margin: 0 auto; width: 100%;
  }
  .feat-card {
    background: var(--card); border: 1px solid var(--border);
    border-radius: var(--radius); padding: 24px; transition: all 0.25s;
  }
  .feat-card:hover {
    border-color: var(--accent); transform: translateY(-3px);
    box-shadow: 0 12px 32px rgba(0,212,200,0.1);
  }
  .feat-icon {
    width: 44px; height: 44px; border-radius: 10px;
    background: linear-gradient(135deg, rgba(0,212,200,0.15), rgba(123,97,255,0.15));
    display: flex; align-items: center; justify-content: center;
    font-size: 1.3rem; margin-bottom: 14px;
  }
  .feat-card h3 { font-family: var(--font-head); font-size: 0.95rem; font-weight: 600; margin-bottom: 6px; }
  .feat-card p { color: var(--muted); font-size: 0.82rem; line-height: 1.6; }

  /* ─── FORM ─── */
  .form-page {
    flex: 1; display: flex; align-items: center; justify-content: center; padding: 40px 24px;
  }
  .form-card {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 20px; padding: 40px; width: 100%; max-width: 480px;
    box-shadow: 0 24px 64px rgba(0,0,0,0.4);
  }
  .form-header { text-align: center; margin-bottom: 32px; }
  .form-header h2 { font-family: var(--font-head); font-size: 1.6rem; font-weight: 700; margin-bottom: 6px; }
  .form-header p { color: var(--muted); font-size: 0.875rem; }
  .form-group { margin-bottom: 20px; }
  .form-label {
    display: block; font-size: 0.8rem; font-weight: 500;
    color: var(--muted); margin-bottom: 7px; letter-spacing: 0.3px; text-transform: uppercase;
  }
  .form-input {
    width: 100%; padding: 12px 16px; border-radius: 10px;
    background: var(--surface); border: 1px solid var(--border);
    color: var(--text); font-family: var(--font-body); font-size: 0.9rem;
    transition: all 0.2s; outline: none;
  }
  .form-input:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(0,212,200,0.1); }
  .form-input.error { border-color: var(--danger); }
  .error-msg { color: var(--danger); font-size: 0.75rem; margin-top: 5px; display: none; }
  .error-msg.show { display: block; }
  .gender-group { display: flex; gap: 10px; }
  .gender-opt { flex: 1; }
  .gender-opt input { display: none; }
  .gender-opt label {
    display: flex; align-items: center; justify-content: center; gap: 8px;
    padding: 11px; border-radius: 10px; border: 1px solid var(--border);
    background: var(--surface); cursor: pointer; font-size: 0.875rem;
    transition: all 0.2s; color: var(--muted);
  }
  .gender-opt input:checked + label {
    border-color: var(--accent); color: var(--accent); background: rgba(0,212,200,0.08);
  }
  .terms-row { display: flex; align-items: flex-start; gap: 10px; margin-bottom: 24px; }
  .terms-row input[type="checkbox"] { margin-top: 2px; accent-color: var(--accent); width: 16px; height: 16px; }
  .terms-row label { font-size: 0.82rem; color: var(--muted); line-height: 1.5; }
  .terms-row a { color: var(--accent); text-decoration: none; }
  .progress-bar {
    height: 3px; background: var(--surface); border-radius: 3px; margin-bottom: 28px; overflow: hidden;
  }
  .progress-fill {
    height: 100%; width: 0%;
    background: linear-gradient(90deg, var(--accent), var(--accent2)); transition: width 0.4s ease;
  }

  /* ─── DASHBOARD ─── */
  .dash-body { flex: 1; display: flex; overflow: hidden; }
  .sidebar {
    width: 72px; background: var(--surface); border-right: 1px solid var(--border);
    display: flex; flex-direction: column; align-items: center; padding: 20px 0; gap: 8px;
  }
  .sidebar-btn {
    width: 44px; height: 44px; border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.2rem; cursor: pointer; border: none;
    background: transparent; color: var(--muted); transition: all 0.2s;
  }
  .sidebar-btn.active, .sidebar-btn:hover { background: rgba(0,212,200,0.1); color: var(--accent); }
  .sidebar-spacer { flex: 1; }
  .main-content { flex: 1; display: flex; flex-direction: column; overflow: hidden; }
  .conn-panel { flex: 1; display: grid; grid-template-columns: 280px 1fr; overflow: hidden; }
  .conn-list { border-right: 1px solid var(--border); overflow-y: auto; padding: 16px; }
  .conn-list h3 {
    font-size: 0.7rem; font-weight: 600; color: var(--muted);
    text-transform: uppercase; letter-spacing: 1px; margin-bottom: 12px; padding: 0 4px;
  }
  .conn-item {
    display: flex; align-items: center; gap: 12px;
    padding: 10px 12px; border-radius: 10px; cursor: pointer;
    transition: all 0.15s; margin-bottom: 4px;
  }
  .conn-item:hover, .conn-item.active { background: var(--card); }
  .conn-avatar {
    width: 38px; height: 38px; border-radius: 50%;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    display: flex; align-items: center; justify-content: center;
    font-size: 1rem; font-weight: 600; flex-shrink: 0; color: #fff; font-family: var(--font-head);
  }
  .conn-info { flex: 1; min-width: 0; }
  .conn-name { font-size: 0.875rem; font-weight: 500; }
  .conn-status { font-size: 0.75rem; color: var(--muted); }
  .conn-dot { width: 8px; height: 8px; border-radius: 50%; background: var(--success); flex-shrink: 0; }
  .conn-dot.offline { background: var(--muted); }
  .chat-area {
    display: flex; flex-direction: column; padding: 24px;
    justify-content: center; align-items: center; color: var(--muted);
    font-size: 0.9rem; gap: 12px;
  }
  .chat-area.has-chat { justify-content: flex-start; }
  .chat-empty-icon { font-size: 3rem; opacity: 0.3; }
  .msg-input-bar { padding: 16px 24px; border-top: 1px solid var(--border); display: flex; gap: 10px; }
  .msg-input-bar .form-input { flex: 1; }
  .send-btn {
    padding: 12px 20px; border-radius: 10px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    border: none; color: #fff; cursor: pointer; font-size: 1rem; transition: all 0.2s;
  }
  .send-btn:hover { transform: scale(1.05); }
  .stats-bar {
    display: flex; gap: 16px; padding: 16px 24px;
    border-bottom: 1px solid var(--border); flex-wrap: wrap;
  }
  .stat-pill {
    display: flex; align-items: center; gap: 8px;
    background: var(--card); border: 1px solid var(--border);
    border-radius: 20px; padding: 6px 14px; font-size: 0.78rem; color: var(--muted);
  }
  .stat-pill strong { color: var(--text); font-size: 0.85rem; }

  /* ─── TOAST ─── */
  .toast-wrap { position: fixed; bottom: 28px; right: 28px; z-index: 999; display: flex; flex-direction: column; gap: 10px; }
  .toast {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 12px; padding: 14px 20px;
    font-size: 0.875rem; min-width: 240px;
    display: flex; align-items: center; gap: 10px;
    box-shadow: 0 8px 32px rgba(0,0,0,0.4);
    animation: toast-in 0.35s ease;
  }
  .toast.success { border-color: var(--success); }
  .toast.error   { border-color: var(--danger); }
  @keyframes toast-in {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* ─── MODAL ─── */
  .modal-overlay {
    display: none; position: fixed; inset: 0;
    background: rgba(0,0,0,0.6); backdrop-filter: blur(4px);
    z-index: 200; align-items: center; justify-content: center;
  }
  .modal-overlay.open { display: flex; }
  .modal {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 20px; padding: 32px; max-width: 420px; width: 90%;
    animation: modal-in 0.3s ease;
  }
  @keyframes modal-in {
    from { opacity: 0; transform: scale(0.95); }
    to   { opacity: 1; transform: scale(1); }
  }
  .modal h3 { font-family: var(--font-head); font-size: 1.2rem; margin-bottom: 8px; }
  .modal p  { color: var(--muted); font-size: 0.875rem; line-height: 1.6; margin-bottom: 20px; }
  .modal-btns { display: flex; gap: 10px; justify-content: flex-end; }

  /* ─── SCROLLBAR ─── */
  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }

  /* ─── RESPONSIVE ─── */
  @media (max-width: 640px) {
    nav { padding: 14px 16px; }
    .nav-tab { padding: 7px 12px; font-size: 0.78rem; }
    .features { padding: 24px 16px; }
    .conn-panel { grid-template-columns: 1fr; }
    .conn-list { display: none; }
    .form-card { padding: 28px 20px; }
    .stats-bar { padding: 12px 16px; }
  }
</style>
</head>
<body>

<!-- ══ WELCOME PAGE ══ -->
<div class="page active" id="page-welcome">
  <nav>
    <div class="nav-logo">GALEXT</div>
    <div class="nav-tabs">
      <button class="nav-tab active" onclick="showPage('welcome')">Home</button>
      <button class="nav-tab" onclick="showPage('register')">Join</button>
      <button class="nav-tab" onclick="showPage('interface')">Dashboard</button>
    </div>
  </nav>
  <div class="hero">
    <div class="hero-glow"></div>
    <div class="avatar-wrap">
      <div class="avatar-ring">
        <div class="avatar-inner">👤</div>
      </div>
      <div class="status-dot"></div>
    </div>
    <h1>Connect <span>Beyond Limits</span></h1>
    <p class="hero-sub">GALEXT gives you encrypted, peer-to-peer communication across Bluetooth, Wi-Fi, and cables — no middleman, no compromise.</p>
    <div class="hero-cta">
      <button class="btn btn-primary" onclick="showPage('register')">Get Started Free</button>
      <button class="btn btn-ghost" onclick="showPage('interface')">See Dashboard →</button>
    </div>
  </div>
  <div class="features">
    <div class="feat-card">
      <div class="feat-icon">🔒</div>
      <h3>End-to-End Encrypted</h3>
      <p>Every message and call is secured with military-grade encryption. Only you and your contact can read it.</p>
    </div>
    <div class="feat-card">
      <div class="feat-icon">📡</div>
      <h3>Multi-Protocol</h3>
      <p>Connect via Bluetooth, Wi-Fi, or USB cables. GALEXT adapts to whatever network you have available.</p>
    </div>
    <div class="feat-card">
      <div class="feat-icon">⚡</div>
      <h3>Fast Connectivity</h3>
      <p>Ultra-low latency calls and instant message delivery, even on constrained networks.</p>
    </div>
    <div class="feat-card">
      <div class="feat-icon">🌐</div>
      <h3>Mesh Network</h3>
      <p>Each user strengthens the network. Your connection helps others stay online — decentralized by design.</p>
    </div>
  </div>
</div>

<!-- ══ REGISTER PAGE ══ -->
<div class="page" id="page-register">
  <nav>
    <div class="nav-logo">GALEXT</div>
    <div class="nav-tabs">
      <button class="nav-tab" onclick="showPage('welcome')">Home</button>
      <button class="nav-tab active" onclick="showPage('register')">Join</button>
      <button class="nav-tab" onclick="showPage('interface')">Dashboard</button>
    </div>
  </nav>
  <div class="form-page">
    <div class="form-card">
      <div class="form-header">
        <h2>Create your account</h2>
        <p>Fill in your details to join the GALEXT network</p>
      </div>
      <div class="progress-bar"><div class="progress-fill" id="reg-progress"></div></div>
      <div class="form-group">
        <label class="form-label">Full Name</label>
        <input class="form-input" id="f-name" type="text" placeholder="e.g. Alex Johnson" oninput="updateProgress()">
        <div class="error-msg" id="err-name">Please enter your full name</div>
      </div>
      <div class="form-group">
        <label class="form-label">Phone Number</label>
        <input class="form-input" id="f-phone" type="tel" placeholder="+234 9123456789" oninput="updateProgress()">
        <div class="error-msg" id="err-phone">Enter a valid phone number</div>
      </div>
      <div class="form-group">
        <label class="form-label">Gender</label>
        <div class="gender-group">
          <div class="gender-opt">
            <input type="radio" name="gender" id="g-male" value="male" onchange="updateProgress()">
            <label for="g-male">♂ Male</label>
          </div>
          <div class="gender-opt">
            <input type="radio" name="gender" id="g-female" value="female" onchange="updateProgress()">
            <label for="g-female">♀ Female</label>
          </div>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Date of Birth</label>
        <input class="form-input" id="f-dob" type="date" oninput="updateProgress()">
        <div class="error-msg" id="err-dob">Please enter your date of birth</div>
      </div>
      <div class="form-group">
        <label class="form-label">House Address</label>
        <input class="form-input" id="f-addr" type="text" placeholder="123 Main Street, City" oninput="updateProgress()">
        <div class="error-msg" id="err-addr">Please enter your address</div>
      </div>
      <div class="terms-row">
        <input type="checkbox" id="terms" onchange="updateProgress()">
        <label for="terms">I agree to GALEXT's <a href="#">Terms of Service</a> and <a href="#">Privacy Policy</a></label>
      </div>
      <button class="btn btn-primary btn-full" onclick="submitForm()">Create Account</button>
    </div>
  </div>
</div>

<!-- ══ DASHBOARD PAGE ══ -->
<div class="page" id="page-interface">
  <nav>
    <div class="nav-logo">GALEXT</div>
    <div class="nav-tabs">
      <button class="nav-tab" onclick="showPage('welcome')">Home</button>
      <button class="nav-tab" onclick="showPage('register')">Join</button>
      <button class="nav-tab active" onclick="showPage('interface')">Dashboard</button>
    </div>
  </nav>
  <div class="stats-bar">
    <div class="stat-pill">🟢 <strong>Online</strong> · 3 connections</div>
    <div class="stat-pill">📡 <strong>Wi-Fi</strong> · 24 Mbps</div>
    <div class="stat-pill">🔒 <strong>Encrypted</strong> · AES-256</div>
    <div class="stat-pill" id="stat-time">🕐 <strong>--:--</strong></div>
  </div>
  <div class="dash-body">
    <div class="sidebar">
      <button class="sidebar-btn active" title="Connections" onclick="setTab(this,'conn')">💬</button>
      <button class="sidebar-btn" title="Calls" onclick="setTab(this,'calls')">📞</button>
      <button class="sidebar-btn" title="Network" onclick="setTab(this,'net')">🌐</button>
      <div class="sidebar-spacer"></div>
      <button class="sidebar-btn" title="Settings" onclick="showModal()">⚙️</button>
    </div>
    <div class="main-content">
      <div id="tab-conn" class="conn-panel">
        <div class="conn-list">
          <h3>Connections</h3>
          <div class="conn-item active" onclick="openChat('Jordan Lee','🟢 Online')">
            <div class="conn-avatar">JL</div>
            <div class="conn-info">
              <div class="conn-name">Jordan Lee</div>
              <div class="conn-status">🟢 Online</div>
            </div>
            <div class="conn-dot"></div>
          </div>
          <div class="conn-item" onclick="openChat('Mia Patel','🟢 Online')">
            <div class="conn-avatar" style="background:linear-gradient(135deg,#f0b429,#ff4d6d)">MP</div>
            <div class="conn-info">
              <div class="conn-name">Mia Patel</div>
              <div class="conn-status">🟢 Online</div>
            </div>
            <div class="conn-dot"></div>
          </div>
          <div class="conn-item" onclick="openChat('Carlos Vega','⚫ Offline')">
            <div class="conn-avatar" style="background:linear-gradient(135deg,#7b61ff,#ff4d6d)">CV</div>
            <div class="conn-info">
              <div class="conn-name">Carlos Vega</div>
              <div class="conn-status">⚫ Offline</div>
            </div>
            <div class="conn-dot offline"></div>
          </div>
        </div>
        <div class="chat-area" id="chat-area">
          <div class="chat-empty-icon">💬</div>
          <span>Select a connection to start chatting</span>
        </div>
      </div>
      <div id="tab-calls" style="display:none; flex:1; align-items:center; justify-content:center; flex-direction:column; gap:12px; color:var(--muted);">
        <div style="font-size:3rem; opacity:0.3">📞</div>
        <span>No recent calls</span>
        <button class="btn btn-primary" onclick="showToast('📞 Starting a call...','success')">New Call</button>
      </div>
      <div id="tab-net" style="display:none; flex:1; padding:28px; flex-direction:column; gap:16px;">
        <h3 style="font-family:var(--font-head); font-size:1.1rem;">Network Status</h3>
        <div style="display:grid; grid-template-columns:repeat(auto-fit,minmax(180px,1fr)); gap:12px;">
          <div class="feat-card"><div class="feat-icon">📶</div><h3>Wi-Fi</h3><p>Connected · 24 Mbps · Low latency</p></div>
          <div class="feat-card"><div class="feat-icon">🔵</div><h3>Bluetooth</h3><p>Active · 3 paired devices nearby</p></div>
          <div class="feat-card"><div class="feat-icon">🔌</div><h3>Cable</h3><p>Not connected</p></div>
        </div>
      </div>
    </div>
  </div>
  <div class="msg-input-bar" id="msg-bar" style="display:none">
    <input class="form-input" id="msg-input" placeholder="Type a message..." onkeydown="if(event.key==='Enter') sendMsg()">
    <button class="send-btn" onclick="sendMsg()">➤</button>
  </div>
</div>

<!-- ══ MODAL ══ -->
<div class="modal-overlay" id="settings-modal">
  <div class="modal">
    <h3>Settings</h3>
    <p>Manage your GALEXT account, privacy preferences, and connection settings here.</p>
    <div class="modal-btns">
      <button class="btn btn-ghost" onclick="closeModal()">Close</button>
      <button class="btn btn-danger" onclick="closeModal(); showToast('Logged out','error')">Sign Out</button>
    </div>
  </div>
</div>

<!-- ══ TOASTS ══ -->
<div class="toast-wrap" id="toasts"></div>

<script>
function showPage(name) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-' + name).classList.add('active');
}

function updateProgress() {
  const fields = ['f-name','f-phone','f-dob','f-addr'];
  const gender = document.querySelector('input[name="gender"]:checked');
  const terms  = document.getElementById('terms').checked;
  let done = fields.filter(id => document.getElementById(id).value.trim()).length;
  if (gender) done++;
  if (terms)  done++;
  const pct = Math.round((done / (fields.length + 2)) * 100);
  document.getElementById('reg-progress').style.width = pct + '%';
}

function submitForm() {
  let ok = true;
  const checks = [
    { id: 'f-name',  err: 'err-name',  test: v => v.trim().length > 1 },
    { id: 'f-phone', err: 'err-phone', test: v => /[\d\s\+\-]{7,}/.test(v) },
    { id: 'f-dob',   err: 'err-dob',   test: v => v !== '' },
    { id: 'f-addr',  err: 'err-addr',  test: v => v.trim().length > 3 },
  ];
  checks.forEach(c => {
    const inp = document.getElementById(c.id);
    const err = document.getElementById(c.err);
    if (!c.test(inp.value)) {
      inp.classList.add('error'); err.classList.add('show'); ok = false;
    } else {
      inp.classList.remove('error'); err.classList.remove('show');
    }
  });
  if (!document.querySelector('input[name="gender"]:checked')) {
    showToast('Please select your gender','error'); ok = false;
  }
  if (!document.getElementById('terms').checked) {
    showToast('Please accept the terms','error'); ok = false;
  }
  if (ok) {
    showToast('🎉 Account created! Welcome to GALEXT','success');
    setTimeout(() => showPage('interface'), 1500);
  }
}

function setTab(btn, tab) {
  document.querySelectorAll('.sidebar-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  ['conn','calls','net'].forEach(t => {
    const el = document.getElementById('tab-'+t);
    if (el) el.style.display = t === tab ? (t==='conn' ? 'grid' : 'flex') : 'none';
  });
  document.getElementById('msg-bar').style.display = tab === 'conn' ? 'flex' : 'none';
}

let currentChat = null;
const chatHistory = {};

function openChat(name) {
  currentChat = name;
  if (!chatHistory[name]) chatHistory[name] = [];
  document.querySelectorAll('.conn-item').forEach(i => i.classList.remove('active'));
  event.currentTarget.classList.add('active');
  renderChat();
  document.getElementById('msg-bar').style.display = 'flex';
  document.getElementById('msg-input').focus();
}

function renderChat() {
  const area = document.getElementById('chat-area');
  if (!currentChat) return;
  const msgs = chatHistory[currentChat];
  if (msgs.length === 0) {
    area.innerHTML = `<div style="font-size:2rem;opacity:0.3">👋</div><span>Start a conversation with ${currentChat}</span>`;
    area.className = 'chat-area';
    return;
  }
  area.className = 'chat-area has-chat';
  area.innerHTML = msgs.map(m => `
    <div style="display:flex;justify-content:${m.me?'flex-end':'flex-start'};margin-bottom:8px;width:100%">
      <div style="max-width:68%;padding:10px 14px;border-radius:${m.me?'14px 14px 4px 14px':'14px 14px 14px 4px'};
        background:${m.me?'linear-gradient(135deg,var(--accent),var(--accent2))':'var(--card)'};
        border:1px solid ${m.me?'transparent':'var(--border)'};font-size:0.875rem;line-height:1.5;
        color:${m.me?'#fff':'var(--text)'}">
        ${m.text}
        <div style="font-size:0.65rem;opacity:0.6;margin-top:4px;text-align:right">${m.time}</div>
      </div>
    </div>
  `).join('');
  area.scrollTop = area.scrollHeight;
}

const replies = [
  "Got it, thanks! 👍","Sounds good to me.","Sure, let's connect soon!",
  "Interesting! Tell me more.","On it 🚀","Let me check and get back to you.",
];

function sendMsg() {
  const inp = document.getElementById('msg-input');
  const txt = inp.value.trim();
  if (!txt || !currentChat) return;
  const time = new Date().toLocaleTimeString([], {hour:'2-digit', minute:'2-digit'});
  chatHistory[currentChat].push({ me: true, text: txt, time });
  inp.value = '';
  renderChat();
  setTimeout(() => {
    const reply = replies[Math.floor(Math.random() * replies.length)];
    chatHistory[currentChat].push({
      me: false, text: reply,
      time: new Date().toLocaleTimeString([], {hour:'2-digit', minute:'2-digit'})
    });
    renderChat();
  }, 900 + Math.random() * 800);
}

function showModal() { document.getElementById('settings-modal').classList.add('open'); }
function closeModal() { document.getElementById('settings-modal').classList.remove('open'); }
document.getElementById('settings-modal').addEventListener('click', e => {
  if (e.target === e.currentTarget) closeModal();
});

function showToast(msg, type = 'success') {
  const wrap = document.getElementById('toasts');
  const el = document.createElement('div');
  el.className = 'toast ' + type;
  el.innerHTML = `<span>${type === 'success' ? '✅' : '❌'}</span><span>${msg}</span>`;
  wrap.appendChild(el);
  setTimeout(() => el.remove(), 3500);
}

function updateClock() {
  const t = new Date().toLocaleTimeString([], {hour:'2-digit', minute:'2-digit'});
  document.getElementById('stat-time').innerHTML = `🕐 <strong>${t}</strong>`;
}
updateClock();
setInterval(updateClock, 10000);
</script>
</body>
</html>
