# Evening_thoughts Login page

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Evening Thoughts – Login</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Young+Serif&family=Figtree:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --sky-top: #ece3f4;
    --sky-bottom: #f6d9c9;
    --card: rgba(255, 255, 255, 0.72);
    --card-border: rgba(80, 60, 120, 0.18);
    --ink: #2a2147;
    --ink-soft: #63587f;
    --field: #ffffff;
    --field-border: #bfb4d6;
    --accent: #4b3a8f;
    --accent-ink: #ffffff;
    --glow: #f2a65a;
    --error: #a3243b;
    --ok: #1f6b4a;
    box-sizing: border-box;
    padding-top: env(safe-area-inset-top, 0px);
    padding-bottom: env(safe-area-inset-bottom, 0px);
  }
  @media (prefers-color-scheme: dark) {
    :root:not([data-theme="light"]) {
      --sky-top: #14152e;
      --sky-bottom: #4a2c58;
      --card: rgba(24, 22, 48, 0.72);
      --card-border: rgba(242, 200, 121, 0.22);
      --ink: #f3ece2;
      --ink-soft: #b9afcf;
      --field: rgba(255, 255, 255, 0.07);
      --field-border: rgba(243, 236, 226, 0.28);
      --accent: #f2c879;
      --accent-ink: #1d1a38;
      --glow: #f2a65a;
      --error: #ff9aa8;
      --ok: #8fe0b5;
    }
  }
  :root[data-theme="dark"] {
    --sky-top: #14152e;
    --sky-bottom: #4a2c58;
    --card: rgba(24, 22, 48, 0.72);
    --card-border: rgba(242, 200, 121, 0.22);
    --ink: #f3ece2;
    --ink-soft: #b9afcf;
    --field: rgba(255, 255, 255, 0.07);
    --field-border: rgba(243, 236, 226, 0.28);
    --accent: #f2c879;
    --accent-ink: #1d1a38;
    --glow: #f2a65a;
    --error: #ff9aa8;
    --ok: #8fe0b5;
  }

  html { scroll-padding-top: env(safe-area-inset-top, 0px); }
  *, *::before, *::after { box-sizing: border-box; }
  html, body { min-height: 100%; margin: 0; }
  body {
    background: linear-gradient(180deg, var(--sky-top) 0%, var(--sky-bottom) 100%) fixed;
    color: var(--ink);
    font-family: "Figtree", system-ui, -apple-system, "Segoe UI", sans-serif;
    font-size: 16px;
    line-height: 1.5;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 24px 16px;
    position: relative;
    overflow-x: hidden;
  }

  /* the one memorable element: a low sun on the horizon behind the card */
  .sun {
    position: fixed;
    left: 50%;
    bottom: -140px;
    width: 420px;
    height: 420px;
    max-width: 90vw;
    max-height: 90vw;
    transform: translateX(-50%);
    border-radius: 50%;
    background: radial-gradient(circle, var(--glow) 0%, rgba(242,166,90,0.45) 38%, rgba(242,166,90,0) 70%);
    pointer-events: none;
  }

  .card {
    position: relative;
    width: 100%;
    max-width: 400px;
    background: var(--card);
    border: 1px solid var(--card-border);
    border-radius: 18px;
    padding: 40px 32px 32px;
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
  }

  .brand {
    font-family: "Young Serif", Georgia, "Times New Roman", serif;
    font-weight: 400;
    font-size: 2.1rem;
    line-height: 1.15;
    letter-spacing: 0.005em;
    margin: 0 0 6px;
  }
  .sub { margin: 0 0 28px; color: var(--ink-soft); }

  .field { margin-bottom: 18px; }
  label { display: block; font-weight: 500; margin-bottom: 6px; }
  input {
    width: 100%;
    font: inherit;
    color: var(--ink);
    background: var(--field);
    border: 1px solid var(--field-border);
    border-radius: 10px;
    padding: 12px 14px;
  }
  input::placeholder { color: var(--ink-soft); opacity: 0.8; }
  input:focus-visible, button:focus-visible {
    outline: 3px solid var(--accent);
    outline-offset: 2px;
  }
  input[aria-invalid="true"] { border-color: var(--error); }

  .pw-row { position: relative; }
  .pw-row input { padding-right: 76px; }
  .toggle {
    position: absolute;
    right: 6px;
    top: 50%;
    transform: translateY(-50%);
    background: none;
    border: 0;
    color: var(--ink-soft);
    font: inherit;
    font-size: 0.9rem;
    padding: 6px 10px;
    border-radius: 8px;
    cursor: pointer;
  }

  .submit {
    width: 100%;
    margin-top: 6px;
    font: inherit;
    font-weight: 600;
    background: var(--accent);
    color: var(--accent-ink);
    border: 0;
    border-radius: 10px;
    padding: 13px 16px;
    cursor: pointer;
    transition: transform 0.12s ease, filter 0.12s ease;
  }
  .submit:hover { filter: brightness(1.08); }
  .submit:active { transform: translateY(1px); }

  .msg { min-height: 1.5em; margin: 16px 0 0; font-size: 0.95rem; }
  .msg.error { color: var(--error); }
  .msg.ok { color: var(--ok); }

  @media (prefers-reduced-motion: reduce) {
    * { transition: none !important; }
  }
</style>
</head>
<body>
<script>
  // The whole page is built from JavaScript.
  (function () {
    function h(tag, attrs, children) {
      var el = document.createElement(tag);
      Object.keys(attrs || {}).forEach(function (k) {
        if (k === 'class') el.className = attrs[k];
        else if (k === 'text') el.textContent = attrs[k];
        else el.setAttribute(k, attrs[k]);
      });
      (children || []).forEach(function (c) { el.appendChild(c); });
      return el;
    }

    var sun = h('div', { 'class': 'sun', 'aria-hidden': 'true' });

    var title = h('h1', { 'class': 'brand', text: 'Evening Thoughts' });
    var sub = h('p', { 'class': 'sub', text: 'Log in to continue.' });

    var userInput = h('input', {
      id: 'username', name: 'username', type: 'text',
      autocomplete: 'username', placeholder: 'Enter your username', required: ''
    });
    var userField = h('div', { 'class': 'field' }, [
      h('label', { 'for': 'username', text: 'Username' }), userInput
    ]);

    var passInput = h('input', {
      id: 'password', name: 'password', type: 'password',
      autocomplete: 'current-password', placeholder: 'Enter your password', required: ''
    });
    var toggle = h('button', { 'class': 'toggle', type: 'button', 'aria-label': 'Show password', text: 'Show' });
    toggle.addEventListener('click', function () {
      var show = passInput.type === 'password';
      passInput.type = show ? 'text' : 'password';
      toggle.textContent = show ? 'Hide' : 'Show';
      toggle.setAttribute('aria-label', show ? 'Hide password' : 'Show password');
    });
    var passField = h('div', { 'class': 'field' }, [
      h('label', { 'for': 'password', text: 'Password' }),
      h('div', { 'class': 'pw-row' }, [passInput, toggle])
    ]);

    var button = h('button', { 'class': 'submit', type: 'submit', text: 'Log in' });
    var message = h('p', { 'class': 'msg', role: 'status', 'aria-live': 'polite' });

    var form = h('form', { novalidate: '' }, [userField, passField, button, message]);
    form.addEventListener('submit', function (e) {
      e.preventDefault();
      var user = userInput.value.trim();
      var pass = passInput.value;
      userInput.removeAttribute('aria-invalid');
      passInput.removeAttribute('aria-invalid');
      message.className = 'msg';

      if (!user) {
        userInput.setAttribute('aria-invalid', 'true');
        message.className = 'msg error';
        message.textContent = 'Enter your username.';
        userInput.focus();
        return;
      }
      if (!pass) {
        passInput.setAttribute('aria-invalid', 'true');
        message.className = 'msg error';
        message.textContent = 'Enter your password.';
        passInput.focus();
        return;
      }
      // Demo only: there is no server, so nothing is checked or sent.
      message.className = 'msg ok';
      message.textContent = 'Welcome back, ' + user + '.';
    });

    var card = h('main', { 'class': 'card' }, [title, sub, form]);
    document.body.appendChild(sun);
    document.body.appendChild(card);
    userInput.focus();
  })();
</script>
</body>
</html>

