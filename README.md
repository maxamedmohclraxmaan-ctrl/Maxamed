# Maxamed
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Login • Demo</title>
  <style>
    :root {
      --bg: #0f172a;   /* slate-900 */
      --card: #111827; /* gray-900 */
      --muted: #94a3b8;/* slate-400 */
      --text: #e5e7eb; /* gray-200 */
      --accent: #22d3ee; /* cyan-400 */
      --accent-2: #a78bfa; /* violet-400 */
      --error: #fca5a5; /* red-300 */
      --ok: #86efac; /* green-300 */
    }
    * { box-sizing: border-box; }
    html, body { height: 100%; }
    body {
      margin: 0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial;
      color: var(--text);
      background:
        radial-gradient(40rem 40rem at 10% 10%, #0ea5e922, transparent 60%),
        radial-gradient(40rem 40rem at 90% 20%, #8b5cf622, transparent 60%),
        radial-gradient(50rem 50rem at 50% 120%, #22d3ee22, transparent 60%),
        var(--bg);
      display: grid;
      place-items: center;
      padding: 24px;
    }
    .card {
      width: 100%;
      max-width: 380px;
      background: color-mix(in srgb, var(--card) 88%, #000);
      border: 1px solid #334155aa;
      border-radius: 16px;
      padding: 22px;
      box-shadow: 0 20px 50px #0008, inset 0 1px 0 #ffffff10;
      backdrop-filter: blur(6px);
    }
    h1 {
      margin: 0 0 4px;
      font-size: 1.35rem;
      letter-spacing: 0.2px;
    }
    .sub {
      margin: 0 0 18px;
      color: var(--muted);
      font-size: 0.95rem;
    }
    label {
      display: block;
      font-size: 0.9rem;
      margin: 10px 0 6px;
    }
    .field {
      position: relative;
    }
    input[type="email"],
    input[type="text"],
    input[type="password"] {
      width: 100%;
      padding: 12px 44px 12px 12px;
      border: 1px solid #334155;
      background: #0b1220;
      color: var(--text);
      border-radius: 10px;
      outline: none;
      font-size: 0.98rem;
      transition: border-color .15s ease, box-shadow .15s ease;
    }
    input:focus {
      border-color: var(--accent);
      box-shadow: 0 0 0 3px #22d3ee33;
    }
    .toggle {
      position: absolute;
      right: 8px;
      top: 50%;
      transform: translateY(-50%);
      font-size: 0.85rem;
      background: transparent;
      border: 0;
      color: var(--muted);
      cursor: pointer;
      padding: 6px 8px;
    }
    .row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      margin: 10px 0 16px;
      font-size: 0.9rem;
    }
    .row a { color: var(--accent); text-decoration: none; }
    .row a:hover { text-decoration: underline; }
    .checkbox {
      display: inline-flex;
      align-items: center; gap: 8px;
      color: var(--muted);
      user-select: none;
    }
    .btn {
      width: 100%;
      padding: 12px 14px;
      border-radius: 10px;
      border: 0;
      background: linear-gradient(135deg, var(--accent), var(--accent-2));
      color: #0b1220;
      font-weight: 700;
      letter-spacing: 0.2px;
      cursor: pointer;
      transition: transform .08s ease, filter .15s ease;
    }
    .btn:active { transform: translateY(1px); }
    .msg {
      margin-top: 12px;
      min-height: 22px;
      font-size: 0.92rem;
    }
    .msg.error { color: var(--error); }
    .msg.ok { color: var(--ok); }
    .or {
      display: grid; grid-template-columns: 1fr auto 1fr; align-items: center; gap: 10px;
      color: var(--muted); font-size: 0.85rem; margin: 12px 0;
    }
    .or::before, .or::after { content: ""; height: 1px; background: #334155; }
    .social { display: grid; gap: 10px; }
    .social button {
      width: 100%;
      border: 1px solid #334155;
      background: #0b1220;
      color: var(--text);
      padding: 10px 12px;
      border-radius: 10px;
      cursor: pointer;
    }
    footer {
      margin-top: 18px;
      color: var(--muted);
      font-size: 0.8rem;
      text-align: center;
    }
  </style>
</head>
<body>
  <main class="card" role="main" aria-labelledby="title">
    <h1 id="title">Welcome back</h1>
    <p class="sub">Sign in to continue.</p>

    <form id="loginForm" novalidate>
      <label for="identity">Email or Username</label>
      <div class="field">
        <input id="identity" name="identity" type="text" inputmode="email"
               placeholder="e.g. demo@site.com or demo"
               autocomplete="username" required aria-required="true" />
      </div>

      <label for="password">Password</label>
      <div class="field">
        <input id="password" name="password" type="password"
               placeholder="••••••••" minlength="6"
               autocomplete="current-password" required aria-required="true" />
        <button type="button" class="toggle" id="togglePw" aria-label="Show password">Show</button>
      </div>

      <div class="row">
        <label class="checkbox">
          <input type="checkbox" id="remember" /> Remember me
        </label>
        <a href="#" aria-label="Forgot password link">Forgot password?</a>
      </div>

      <button class="btn" type="submit" id="submitBtn">Sign In</button>
      <div id="msg" class="msg" role="status" aria-live="polite"></div>

      <div class="or">OR</div>
      <div class="social">
        <button type="button" aria-label="Continue with Google">Continue with Google</button>
        <button type="button" aria-label="Continue with GitHub">Continue with GitHub</button>
      </div>
    </form>

    <footer>Demo only • Do not use real passwords.</footer>
  </main>

  <script>
    // --- Demo "auth" (front-end only) ---
    const DEMO_USERS = [
      { identity: "demo@site.com", password: "demo1234" },
      { identity: "demo", password: "demo1234" }
    ];

    const form = document.getElementById("loginForm");
    const msg = document.getElementById("msg");
    const toggle = document.getElementById("togglePw");
    const pw = document.getElementById("password");

    toggle.addEventListener("click", () => {
      const isPwd = pw.type === "password";
      pw.type = isPwd ? "text" : "password";
      toggle.textContent = isPwd ? "Hide" : "Show";
      toggle.setAttribute("aria-label", isPwd ? "Hide password" : "Show password");
      pw.focus();
    });

    form.addEventListener("submit", (e) => {
      e.preventDefault();
      msg.textContent = "";
      msg.className = "msg";

      const identity = document.getElementById("identity").value.trim();
      const password = pw.value;

      // Client-side checks
      if (!identity || !password) {
        showError("Please fill in all required fields.");
        return;
      }
      if (password.length < 6) {
        showError("Password must be at least 6 characters.");
        return;
      }

      // Fake check (replace with real request)
      const ok = DEMO_USERS.some(u =>
        u.identity.toLowerCase() === identity.toLowerCase() && u.password === password
      );

      if (ok) {
        showOk("Logged in! Redirecting…");
        // Example: window.location.href = "/dashboard";
      } else {
        showError("Invalid credentials (try demo@site.com / demo1234 or demo / demo1234).");
      }
    });

    function showError(text) { msg.textContent = text; msg.className = "msg error"; }
    function showOk(text) { msg.textContent = text; msg.className = "msg ok"; }
  </script>
</body>
</html>
