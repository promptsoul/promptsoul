<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#09090b">
  <meta name="description" content="Nimbus Developer Hub">
  <title>Nimbus — Developer Hub</title>

  <style>
    :root {
      --bg: #09090b;
      --card: #111113;
      --card2: #151518;
      --border: #27272a;
      --text: #f4f4f5;
      --muted: #a1a1aa;
      --dim: #71717a;
      --green: #22c55e;
      --green-soft: #14532d;
      --blue: #60a5fa;
      --purple: #a78bfa;
      --yellow: #facc15;
      --red: #f87171;
    }

    * {
      box-sizing: border-box;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      margin: 0;
      background: var(--bg);
      color: var(--text);
      font-family:
        Inter,
        ui-sans-serif,
        system-ui,
        -apple-system,
        BlinkMacSystemFont,
        "Segoe UI",
        sans-serif;
      min-height: 100vh;
    }

    button,
    input {
      font: inherit;
    }

    button {
      cursor: pointer;
    }

    a {
      color: inherit;
      text-decoration: none;
    }

    /* HEADER */

    .header {
      position: sticky;
      top: 0;
      z-index: 100;
      height: 64px;
      background: rgba(9, 9, 11, 0.94);
      border-bottom: 1px solid var(--border);
      backdrop-filter: blur(16px);
    }

    .header-inner {
      width: min(1400px, calc(100% - 32px));
      height: 100%;
      margin: 0 auto;
      display: flex;
      align-items: center;
      gap: 22px;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 20px;
      font-weight: 800;
      letter-spacing: -0.04em;
      min-width: 145px;
    }

    .brand-mark {
      width: 32px;
      height: 32px;
      display: grid;
      place-items: center;
      border-radius: 9px;
      background: linear-gradient(135deg, #4ade80, #16a34a);
      color: #052e16;
      font-weight: 900;
      box-shadow: 0 0 30px rgba(34, 197, 94, 0.2);
    }

    .search {
      position: relative;
      width: min(520px, 100%);
    }

    .search input {
      width: 100%;
      height: 38px;
      padding: 0 75px 0 39px;
      border: 1px solid var(--border);

