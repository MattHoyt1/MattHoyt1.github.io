
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Matthew Hoyt — App Support</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      --ink: #0f0e0d;
      --ink-2: #3a3632;
      --ink-3: #8a847d;
      --cream: #faf7f2;
      --warm: #f0ebe2;
      --warm-2: #e0d9ce;
      --accent: #c9603a;
      --accent-light: #f5ede8;
      --gold: #c4a35a;
      --radius: 16px;
      --radius-sm: 8px;
    }
    html { scroll-behavior: smooth; }
    body {
      font-family: 'DM Sans', sans-serif;
      background: transparent;
      color: var(--ink);
      overflow-x: hidden;
    }
    /* ─── BACKGROUND SYSTEM ─── */
    /* The page scrolls over a fixed gradient+lines+specks backdrop.
       Light sections are transparent so the backdrop shows through.
       Dark sections (hero, faq, footer) have their own solid bg. */
    html {
      /* The gradient lives on html so it scrolls with the page height,
         giving a top-light → bottom-dark effect as you scroll */
      background: linear-gradient(
        to bottom,
        #fdf6e3 0%,
        #f5e6d0 25%,
        #e8d0b5 55%,
        #d4b59c 80%,
        #c4a08a 100%
      );
    }
    body { background: transparent; }
    /* Diagonal line pattern — fixed, always behind content */
    #diag-lines {
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      pointer-events: none;
      z-index: 0;
      overflow: hidden;
      opacity: 0.13;
    }
    #diag-lines svg { width: 100%; height: 100%; }
    /* Specks canvas — fixed, above lines, below content */
    #specks {
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      pointer-events: none;
      z-index: 1;
      mix-blend-mode: screen;
    }
    /* All page content sits above the backdrop */
    nav, section, footer, .modal-overlay { position: relative; z-index: 2; }
    /* Light sections: transparent bg so gradient shows through */
    #apps    { background: transparent; }
    #contact { background: transparent; }
    /* Dark sections keep their solid backgrounds */
    .hero { background: var(--ink); }
    #faq  { background: var(--ink); }
    footer { background: var(--ink); }
    /* Cards on transparent sections need their own white bg */
    .app-card { background: rgba(255,255,255,0.82); backdrop-filter: blur(8px); }
    .contact-card { background: rgba(255,255,255,0.82); backdrop-filter: blur(8px); }
    /* ─── NAV ─── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      padding: 0 2rem;
      height: 64px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      background: rgba(250, 247, 242, 0.85);
      backdrop-filter: blur(20px);
      -webkit-backdrop-filter: blur(20px);
      border-bottom: 1px solid rgba(160, 140, 120, 0.15);
      transition: background 0.3s;
    }
    .nav-logo {
      font-family: 'DM Serif Display', serif;
      font-size: 1.2rem;
      color: var(--ink);
      letter-spacing: -0.01em;
    }
    .nav-links {
      display: flex;
      align-items: center;
      gap: 2rem;
    }
    .nav-links a, .nav-links button {
      font-size: 0.85rem;
      font-weight: 400;
      color: var(--ink-2);
      text-decoration: none;
      background: none;
      border: none;
      cursor: pointer;
      letter-spacing: 0.04em;
      text-transform: uppercase;
      transition: color 0.2s;
    }
    .nav-links a:hover, .nav-links button:hover { color: var(--accent); }
    .hamburger {
      display: none;
      flex-direction: column;
      gap: 5px;
      background: none;
      border: none;
      cursor: pointer;
      padding: 4px;
    }
    .hamburger span {
      display: block;
      width: 22px;
      height: 1.5px;
      background: var(--ink);
      transition: all 0.3s;
    }
    .mobile-nav {
      display: none;
      position: fixed;
      top: 64px; left: 0; right: 0;
      background: var(--cream);
      border-bottom: 1px solid var(--warm-2);
      padding: 1.5rem 2rem;
      z-index: 99;
      flex-direction: column;
      gap: 1.25rem;
    }
    .mobile-nav.open { display: flex; }
    .mobile-nav a, .mobile-nav button {
      font-size: 0.9rem;
      color: var(--ink-2);
      text-decoration: none;
      background: none;
      border: none;
      cursor: pointer;
      text-align: left;
      letter-spacing: 0.04em;
      text-transform: uppercase;
    }
    /* ─── HERO ─── */
    .hero {
      min-height: 100vh;
      display: grid;
      grid-template-columns: 1fr 1fr;
      align-items: center;
      padding: 0 6vw;
      padding-top: 64px;
      position: relative;
      overflow: hidden;
      background: var(--ink);
    }
    .hero-bg {
      position: absolute;
      inset: 0;
      background:
        radial-gradient(ellipse 60% 80% at 80% 50%, rgba(201,96,58,0.18) 0%, transparent 70%),
        radial-gradient(ellipse 40% 60% at 20% 80%, rgba(196,163,90,0.1) 0%, transparent 60%);
    }
    .hero-grid {
      position: absolute;
      inset: 0;
      background-image:
        linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
      background-size: 60px 60px;
    }
    .hero-left {
      position: relative;
      z-index: 1;
    }
    .hero-eyebrow {
      font-size: 0.75rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--gold);
      margin-bottom: 1.5rem;
      display: flex;
      align-items: center;
      gap: 0.75rem;
    }
    .hero-eyebrow::before {
      content: '';
      display: block;
      width: 32px;
      height: 1px;
      background: var(--gold);
    }
    .hero h1 {
      font-family: 'DM Serif Display', serif;
      font-size: clamp(3rem, 6vw, 5.5rem);
      line-height: 1.05;
      color: #faf7f2;
      letter-spacing: -0.02em;
      margin-bottom: 1.5rem;
    }
    .hero h1 em {
      font-style: italic;
      color: var(--accent);
    }
    .hero-sub {
      font-size: 1.05rem;
      color: rgba(250,247,242,0.55);
      line-height: 1.7;
      max-width: 420px;
      margin-bottom: 2.5rem;
    }
    .hero-cta {
      display: inline-flex;
      align-items: center;
      gap: 0.75rem;
      background: var(--accent);
      color: white;
      font-size: 0.85rem;
      font-weight: 500;
      letter-spacing: 0.05em;
      text-transform: uppercase;
      text-decoration: none;
      padding: 0.85rem 1.75rem;
      border-radius: 100px;
      transition: all 0.25s;
    }
    .hero-cta:hover {
      background: #b85530;
      transform: translateY(-2px);
      box-shadow: 0 12px 32px rgba(201,96,58,0.35);
    }
    .hero-cta svg { width: 14px; height: 14px; }
    .hero-right {
      position: relative;
      z-index: 1;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .hero-orb {
      width: clamp(260px, 35vw, 420px);
      aspect-ratio: 1;
      border-radius: 50%;
      background: radial-gradient(circle at 35% 35%, rgba(201,96,58,0.5), rgba(196,163,90,0.2) 50%, transparent 70%);
      border: 1px solid rgba(255,255,255,0.08);
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
      animation: float 6s ease-in-out infinite;
    }
    .hero-orb::before {
      content: '';
      position: absolute;
      inset: 20px;
      border-radius: 50%;
      border: 1px solid rgba(255,255,255,0.06);
    }
    .hero-orb-text {
      font-family: 'DM Serif Display', serif;
      font-size: clamp(3rem, 5vw, 5rem);
      color: rgba(250,247,242,0.15);
      text-align: center;
      line-height: 1;
      user-select: none;
    }
    @keyframes float {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-16px); }
    }
    .hero-stats {
      position: absolute;
      bottom: 3rem;
      left: 6vw;
      right: 6vw;
      display: flex;
      gap: 3rem;
      z-index: 1;
      border-top: 1px solid rgba(255,255,255,0.08);
      padding-top: 2rem;
    }
    .stat-item { }
    .stat-num {
      font-family: 'DM Serif Display', serif;
      font-size: 2rem;
      color: var(--cream);
      line-height: 1;
    }
    .stat-label {
      font-size: 0.75rem;
      color: rgba(250,247,242,0.4);
      text-transform: uppercase;
      letter-spacing: 0.08em;
      margin-top: 0.25rem;
    }
    /* ─── SECTION LABELS ─── */
    .section-label {
      font-size: 0.7rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--ink-3);
      display: flex;
      align-items: center;
      gap: 0.75rem;
      margin-bottom: 1rem;
    }
    .section-label::after {
      content: '';
      flex: 1;
      height: 1px;
      background: var(--warm-2);
      max-width: 60px;
    }
    /* ─── APPS SECTION ─── */
    #apps {
      padding: 8rem 6vw;
      background: transparent;
    }
    .section-header {
      margin-bottom: 4rem;
    }
    .section-title {
      font-family: 'DM Serif Display', serif;
      font-size: clamp(2rem, 4vw, 3.5rem);
      letter-spacing: -0.02em;
      line-height: 1.1;
      margin-bottom: 1rem;
    }
    .section-desc {
      font-size: 1rem;
      color: var(--ink-3);
      max-width: 480px;
      line-height: 1.7;
    }
    .apps-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
      gap: 1.5rem;
    }
    .app-card {
      background: rgba(255,255,255,0.72);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border: 1px solid rgba(255,255,255,0.6);
      border-radius: var(--radius);
      padding: 2rem;
      cursor: pointer;
      transition: all 0.35s cubic-bezier(0.175, 0.885, 0.32, 1.275);
      display: flex;
      flex-direction: column;
      gap: 1rem;
      position: relative;
      overflow: hidden;
    }
    .app-card::before {
      content: '';
      position: absolute;
      inset: 0;
      opacity: 0;
      transition: opacity 0.35s;
    }
    .app-card:hover {
      transform: translateY(-6px);
      box-shadow: 0 24px 48px rgba(15,14,13,0.12);
      border-color: transparent;
    }
    .app-card:hover::before { opacity: 1; }
    /* Card accent colors */
    .card-hygge { --card-accent: #c9603a; --card-bg: #fdf1ec; }
    .card-bormes { --card-accent: #2a6eb5; --card-bg: #eef4fb; }
    .card-danish { --card-accent: #b33535; --card-bg: #faeaea; }
    .card-ring { --card-accent: #3a8c5c; --card-bg: #eaf4ee; }
    .card-gift { --card-accent: #7a55b5; --card-bg: #f3eefb; }
    .app-card::before {
      background: linear-gradient(135deg, var(--card-bg), white);
    }
    .app-icon {
      width: 52px;
      height: 52px;
      border-radius: 14px;
      background: var(--card-bg);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.5rem;
      position: relative;
      z-index: 1;
      flex-shrink: 0;
    }
    .app-card-header {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 1rem;
      position: relative;
      z-index: 1;
    }
    .app-card-meta { flex: 1; }
    .app-name {
      font-family: 'DM Serif Display', serif;
      font-size: 1.3rem;
      letter-spacing: -0.01em;
      color: var(--ink);
      margin-bottom: 0.35rem;
    }
    .app-tag {
      font-size: 0.7rem;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      color: var(--card-accent);
      background: var(--card-bg);
      padding: 0.2rem 0.6rem;
      border-radius: 100px;
      display: inline-block;
    }
    .app-desc {
      font-size: 0.9rem;
      color: var(--ink-3);
      line-height: 1.65;
      position: relative;
      z-index: 1;
    }
    .app-arrow {
      color: var(--card-accent);
      font-size: 1.2rem;
      transition: transform 0.2s;
      position: relative;
      z-index: 1;
    }
    .app-card:hover .app-arrow { transform: translate(3px, -3px); }
    /* ─── FAQ ─── */
    #faq {
      padding: 8rem 6vw;
      background: var(--ink);
      color: var(--cream);
    }
    #faq .section-label { color: rgba(250,247,242,0.35); }
    #faq .section-label::after { background: rgba(255,255,255,0.1); }
    #faq .section-title { color: var(--cream); }
    .faq-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1px;
      background: rgba(255,255,255,0.08);
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: var(--radius);
      overflow: hidden;
      margin-top: 3rem;
    }
    .faq-item {
      background: var(--ink);
      padding: 2.5rem;
      transition: background 0.25s;
    }
    .faq-item:hover { background: #1a1917; }
    .faq-q {
      font-family: 'DM Serif Display', serif;
      font-size: 1.1rem;
      color: var(--cream);
      margin-bottom: 0.75rem;
      line-height: 1.3;
    }
    .faq-a {
      font-size: 0.9rem;
      color: rgba(250,247,242,0.5);
      line-height: 1.7;
    }
    .faq-a button {
      color: var(--gold);
      background: none;
      border: none;
      cursor: pointer;
      font-size: 0.9rem;
      padding: 0;
      text-decoration: underline;
      text-decoration-color: rgba(196,163,90,0.4);
      text-underline-offset: 2px;
    }
    /* ─── CONTACT ─── */
    #contact {
      padding: 8rem 6vw;
      background: transparent;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 6rem;
      align-items: center;
    }
    .contact-title {
      font-family: 'DM Serif Display', serif;
      font-size: clamp(2rem, 3.5vw, 3rem);
      letter-spacing: -0.02em;
      line-height: 1.15;
      margin-bottom: 1.25rem;
    }
    .contact-sub {
      font-size: 1rem;
      color: var(--ink-3);
      line-height: 1.7;
      margin-bottom: 2rem;
    }
    .contact-email-link {
      display: inline-flex;
      align-items: center;
      gap: 0.75rem;
      background: var(--ink);
      color: var(--cream);
      font-size: 0.85rem;
      font-weight: 500;
      letter-spacing: 0.05em;
      text-transform: uppercase;
      text-decoration: none;
      padding: 0.9rem 2rem;
      border-radius: 100px;
      transition: all 0.25s;
    }
    .contact-email-link:hover {
      background: var(--accent);
      transform: translateY(-2px);
      box-shadow: 0 12px 32px rgba(201,96,58,0.3);
    }
    .contact-card {
      background: rgba(255,255,255,0.72);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border: 1px solid rgba(255,255,255,0.6);
      border-radius: var(--radius);
      padding: 2.5rem;
    }
    .contact-card-label {
      font-size: 0.75rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--ink-3);
      margin-bottom: 0.5rem;
    }
    .contact-card-email {
      font-family: 'DM Serif Display', serif;
      font-size: 1.3rem;
      color: var(--accent);
      margin-bottom: 1.5rem;
    }
    .contact-card-note {
      font-size: 0.85rem;
      color: var(--ink-3);
      line-height: 1.6;
      padding-top: 1.25rem;
      border-top: 1px solid var(--warm-2);
    }
    /* ─── FOOTER ─── */
    footer {
      background: var(--ink);
      color: rgba(250,247,242,0.35);
      padding: 2rem 6vw;
      display: flex;
      align-items: center;
      justify-content: space-between;
      font-size: 0.8rem;
      letter-spacing: 0.05em;
    }
    footer .foot-logo {
      font-family: 'DM Serif Display', serif;
      font-size: 1rem;
      color: rgba(250,247,242,0.6);
    }
    footer .foot-links {
      display: flex;
      gap: 1.5rem;
    }
    footer button {
      background: none;
      border: none;
      color: rgba(250,247,242,0.35);
      font-size: 0.8rem;
      cursor: pointer;
      letter-spacing: 0.05em;
      transition: color 0.2s;
    }
    footer button:hover { color: var(--gold); }
    /* ─── MODAL ─── */
    .modal-overlay {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(15,14,13,0.7);
      backdrop-filter: blur(8px);
      z-index: 200;
      align-items: center;
      justify-content: center;
      padding: 2rem;
    }
    .modal-overlay.active { display: flex; }
    .modal-box {
      background: rgba(250,247,242,0.96);
      border-radius: var(--radius);
      padding: 3rem;
      width: 100%;
      max-width: 680px;
      max-height: 85vh;
      overflow-y: auto;
      position: relative;
      animation: modalIn 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }
    @keyframes modalIn {
      from { opacity: 0; transform: scale(0.96) translateY(8px); }
      to { opacity: 1; transform: scale(1) translateY(0); }
    }
    .modal-close {
      position: absolute;
      top: 1.25rem;
      right: 1.25rem;
      width: 32px;
      height: 32px;
      border-radius: 50%;
      background: var(--warm);
      border: none;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      color: var(--ink-3);
      font-size: 1rem;
      transition: all 0.2s;
    }
    .modal-close:hover { background: var(--warm-2); color: var(--ink); }
    .modal-eyebrow {
      font-size: 0.7rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 0.75rem;
    }
    .modal-title {
      font-family: 'DM Serif Display', serif;
      font-size: 2rem;
      letter-spacing: -0.02em;
      color: var(--ink);
      margin-bottom: 1.5rem;
      line-height: 1.15;
    }
    .modal-body p {
      font-size: 0.95rem;
      color: var(--ink-2);
      line-height: 1.8;
      margin-bottom: 1rem;
    }
    .modal-body h3 {
      font-family: 'DM Serif Display', serif;
      font-size: 1.2rem;
      color: var(--ink);
      margin: 1.5rem 0 0.5rem;
    }
    .modal-body ul {
      padding-left: 1.2rem;
    }
    .modal-body li {
      font-size: 0.9rem;
      color: var(--ink-2);
      line-height: 1.8;
      margin-bottom: 0.4rem;
    }
    .modal-link {
      color: var(--accent);
      text-decoration: none;
    }
    .modal-link:hover { text-decoration: underline; }
    /* ─── SCROLL REVEAL ─── */
    .reveal {
      opacity: 0;
      transform: translateY(24px);
      transition: opacity 0.6s ease, transform 0.6s ease;
    }
    .reveal.visible {
      opacity: 1;
      transform: none;
    }
    /* ─── RESPONSIVE ─── */
    @media (max-width: 900px) {
      .hero {
        grid-template-columns: 1fr;
        padding: 100px 6vw 180px;
        text-align: center;
      }
      .hero-eyebrow { justify-content: center; }
      .hero-sub { margin: 0 auto 2.5rem; }
      .hero-right { display: none; }
      .hero-stats { flex-wrap: wrap; gap: 2rem; }
      .nav-links { display: none; }
      .hamburger { display: flex; }
      .faq-grid { grid-template-columns: 1fr; }
      #contact { grid-template-columns: 1fr; gap: 3rem; }
      .apps-grid { grid-template-columns: 1fr; }
    }
    @media (max-width: 600px) {
      .modal-box { padding: 2rem 1.5rem; }
      #faq { padding: 5rem 5vw; }
      #apps { padding: 5rem 5vw; }
      #contact { padding: 5rem 5vw; }
    }
  </style>
</head>
<body>
<!-- ── DIAGONAL LINE PATTERN ── -->
<div id="diag-lines">
  <svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%">
    <defs>
      <pattern id="diamond-lines" x="0" y="0" width="260" height="260" patternUnits="userSpaceOnUse">
        <!-- Two crossing diagonals forming a diamond grid, matching the screenshot -->
        <line x1="0" y1="0" x2="260" y2="260" stroke="#7a5c40" stroke-width="1"/>
        <line x1="260" y1="0" x2="0" y2="260" stroke="#7a5c40" stroke-width="1"/>
      </pattern>
    </defs>
    <rect width="100%" height="100%" fill="url(#diamond-lines)"/>
  </svg>
</div>
<!-- ── FLOATING SPECKS ── -->
<canvas id="specks"></canvas>
<!-- ── NAV ── -->
<nav>
  <div class="nav-logo">Matthew Hoyt</div>
  <div class="nav-links">
    <a href="#apps">Apps</a>
    <a href="#faq">FAQ</a>
    <a href="#contact">Contact</a>
    <button onclick="openModal('privacy-modal')">Privacy</button>
    <button onclick="openModal('terms-modal')">Terms</button>
  </div>
  <button class="hamburger" id="hamburger" aria-label="Menu">
    <span></span><span></span><span></span>
  </button>
</nav>

<div class="mobile-nav" id="mobile-nav">
  <a href="#apps" onclick="closeMobile()">Apps</a>
  <a href="#faq" onclick="closeMobile()">FAQ</a>
  <a href="#contact" onclick="closeMobile()">Contact</a>
  <button onclick="closeMobile(); openModal('privacy-modal')">Privacy</button>
  <button onclick="closeMobile(); openModal('terms-modal')">Terms</button>
</div>

<!-- ── HERO ── -->
<section class="hero" id="home">
  <div class="hero-bg"></div>
  <div class="hero-grid"></div>

  <div class="hero-left">
    <div class="hero-eyebrow">App Support Center</div>
    <h1>Thoughtful apps<br>for <em>everyday</em><br>living</h1>
    <p class="hero-sub">Discover tools built around the moments that matter — connection, coziness, culture, and care.</p>
    <a href="#apps" class="hero-cta">
      Explore the apps
      <svg viewBox="0 0 14 14" fill="none" stroke="currentColor" stroke-width="2"><path d="M2 7h10M7 2l5 5-5 5"/></svg>
    </a>
  </div>

  <div class="hero-right">
    <div class="hero-orb">
      <div class="hero-orb-text">MH</div>
    </div>
  </div>
</section>

<!-- ── APPS ── -->
<section id="apps">
  <div class="section-header reveal">
    <div class="section-label">Our collection</div>
    <h2 class="section-title">Five apps.<br>One philosophy.</h2>
    <p class="section-desc">Each app solves a real problem with elegance — nothing superfluous, nothing missing.</p>
  </div>

  <div class="apps-grid">
    <div class="app-card card-hygge reveal" onclick="openModal('hygge-modal')">
      <div class="app-card-header">
        <div class="app-icon">🕯️</div>
        <div class="app-arrow">↗</div>
      </div>
      <div class="app-card-meta">
        <div class="app-name">Hygge Detector</div>
        <span class="app-tag">AI · Interior</span>
      </div>
      <p class="app-desc">Discover the coziness in your space with AI-powered visual analysis and a personalised hygge score.</p>
    </div>
    <div class="app-card card-bormes reveal" onclick="openModal('bormes-modal')">
      <div class="app-card-header">
        <div class="app-icon">🌿</div>
        <div class="app-arrow">↗</div>
      </div>
      <div class="app-card-meta">
        <div class="app-name">Bormes Apartment</div>
        <span class="app-tag">Travel · Local</span>
      </div>
      <p class="app-desc">Your personal guide to Bormes-les-Mimosas — hidden gems, local charm, all in one beautiful app.</p>
    </div>
    <div class="app-card card-danish reveal" onclick="openModal('danish-modal')">
      <div class="app-card-header">
        <div class="app-icon">🇩🇰</div>
        <div class="app-arrow">↗</div>
      </div>
      <div class="app-card-meta">
        <div class="app-name">Danish Idioms Quiz</div>
        <span class="app-tag">Language · Culture</span>
      </div>
      <p class="app-desc">Go beyond the textbook. Test your knowledge of Danish slang and think like a local.</p>
    </div>
    <div class="app-card card-ring reveal" onclick="openModal('ring-modal')">
      <div class="app-card-header">
        <div class="app-icon">📞</div>
        <div class="app-arrow">↗</div>
      </div>
      <div class="app-card-meta">
        <div class="app-name">Ring Log</div>
        <span class="app-tag">Relationships</span>
      </div>
      <p class="app-desc">Never lose touch. Set your own call rhythm and get gentle reminders to reach the people who matter.</p>
    </div>
    <div class="app-card card-gift reveal" onclick="openModal('gift-modal')">
      <div class="app-card-header">
        <div class="app-icon">🎁</div>
        <div class="app-arrow">↗</div>
      </div>
      <div class="app-card-meta">
        <div class="app-name">Gift Ideas</div>
        <span class="app-tag">AI · Lifestyle</span>
      </div>
      <p class="app-desc">From blank screen to perfect gift. AI that understands the person, not just the occasion.</p>
    </div>
  </div>
</section>

<!-- ── FAQ ── -->
<section id="faq">
  <div class="reveal">
    <div class="section-label">Common questions</div>
    <h2 class="section-title">Got questions?<br>We have answers.</h2>
  </div>

  <div class="faq-grid">
    <div class="faq-item reveal">
      <div class="faq-q">How do I get support for an app?</div>
      <p class="faq-a">Select any app above to read about it in detail, then reach out via the contact section below. We aim to respond within 24 hours.</p>
    </div>
    <div class="faq-item reveal">
      <div class="faq-q">How do I report a bug or issue?</div>
      <p class="faq-a">Email our support team directly at Matthewhoytapps@gmail.com with a brief description and your device model. Screenshots are always helpful.</p>
    </div>
    <div class="faq-item reveal">
      <div class="faq-q">Is my data and privacy protected?</div>
      <p class="faq-a">Yes — we take it seriously. Read our <button onclick="openModal('privacy-modal')">full privacy policy</button> for how we handle your data. Short version: we don't sell it, ever.</p>
    </div>
    <div class="faq-item reveal">
      <div class="faq-q">Can I get a refund on an in-app purchase?</div>
      <p class="faq-a">All purchases go through Apple's system. Refund requests are handled directly through your Apple account or Apple Support.</p>
    </div>
  </div>
</section>

<!-- ── CONTACT ── -->
<section id="contact">
  <div class="reveal">
    <div class="section-label">Get in touch</div>
    <h2 class="contact-title">We're here<br>to help.</h2>
    <p class="contact-sub">Have a question, found a bug, or just want to share feedback? Drop us a line — every message is read personally.</p>
    <a href="mailto:Matthewhoytapps@gmail.com" class="contact-email-link">
      <svg width="14" height="14" viewBox="0 0 14 14" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="1" y="3" width="12" height="9" rx="1.5"/><path d="M1 4l6 5 6-5"/></svg>
      Email support
    </a>
  </div>
  <div class="contact-card reveal">
    <div class="contact-card-label">Direct email</div>
    <div class="contact-card-email">Matthewhoytapps@gmail.com</div>
    <div class="contact-card-note">
      We typically respond within one business day. For in-app purchase refunds, please use your Apple account settings directly.
    </div>
  </div>
</section>

<!-- ── FOOTER ── -->
<footer>
  <div class="foot-logo">Matthew Hoyt</div>
  <div class="foot-links">
    <button onclick="openModal('privacy-modal')">Privacy</button>
    <button onclick="openModal('terms-modal')">Terms</button>
  </div>
  <div>© 2024 Matthew Hoyt</div>
</footer>

<!-- ════ MODALS ════ -->

<!-- Hygge -->
<div class="modal-overlay" id="hygge-modal">
  <div class="modal-box">
    <button class="modal-close" onclick="closeModal('hygge-modal')">✕</button>
    <div class="modal-eyebrow">AI · Interior</div>
    <h2 class="modal-title">Hygge Detector</h2>
    <div class="modal-body">
      <p>You might be wondering — what is hygge? It's the Danish art of creating a space that feels warm, inviting, and perfectly cozy. Until now, understanding hygge was subjective, elusive — a feeling. Not anymore.</p>
      <p>With Hygge Detector, we bring the power of advanced AI and computer vision together to give you a tool that doesn't just look at your room — it <em>understands</em> it.</p>
      <p>Take a photo or upload one. In seconds, the app analyses the lighting, colours, and objects — the very soul of your space — and gives you a simple, elegant Hygge Score. Then it tells you exactly how to improve it. Need more warmth? Add a candle. Too much clutter? Simplify. Missing harmony? We'll guide you.</p>
      <p>Technology should enhance your humanity. Hygge Detector helps you enhance your home, your mood, and your connection to what matters most. This isn't just an app — it's hygge, in your pocket.</p>
    </div>
  </div>
</div>

<!-- Bormes -->
<div class="modal-overlay" id="bormes-modal">
  <div class="modal-box">
    <button class="modal-close" onclick="closeModal('bormes-modal')">✕</button>
    <div class="modal-eyebrow">Travel · Local</div>
    <h2 class="modal-title">Bormes Apartment</h2>
    <div class="modal-body">
      <p>Technology should amplify the best parts of life — not complicate them. And that's exactly what this app does. It's a beautifully designed, intuitive gateway to one of the most breathtaking places on Earth: Bormes-les-Mimosas.</p>
      <p>With just a few taps, you're immersed in the charm of the village, its hidden gems, and its stunning landscapes. The app doesn't just give you information — it guides you, inspires you, and helps you experience the magic of this place effortlessly.</p>
      <p>Elegant. Seamless. It just works. That's what great technology is all about.</p>
    </div>
  </div>
</div>

<!-- Danish -->
<div class="modal-overlay" id="danish-modal">
  <div class="modal-box">
    <button class="modal-close" onclick="closeModal('danish-modal')">✕</button>
    <div class="modal-eyebrow">Language · Culture</div>
    <h2 class="modal-title">Danish Idioms Quiz</h2>
    <div class="modal-body">
      <p>Language isn't just about words — it's about culture, personality, and expression. In Denmark, nothing captures that better than its rich, quirky slang.</p>
      <p>With the Danish Idioms Quiz, we've created a way to not just learn Danish — but to <em>think</em> Danish. It's fun, unpredictable, and challenges you to go beyond the textbook and speak like a local.</p>
      <p>Choose your level. Step into the game. See how many you can get right before the language gets you. This isn't just a quiz — it's an experience. One idiom at a time.</p>
    </div>
  </div>
</div>

<!-- Ring Log -->
<div class="modal-overlay" id="ring-modal">
  <div class="modal-box">
    <button class="modal-close" onclick="closeModal('ring-modal')">✕</button>
    <div class="modal-eyebrow">Relationships</div>
    <h2 class="modal-title">Ring Log</h2>
    <div class="modal-body">
      <p>Staying connected is everything. But life gets busy. Days turn into weeks, weeks into months, and before you know it — you've lost touch with the people who matter most.</p>
      <p>Ring Log is a beautifully simple way to never forget to check in again. It remembers the last time you called someone and gently reminds you when it's time to reach out. No spreadsheets, no mental notes — just seamless, thoughtful connection.</p>
      <p>Want to call your best friend every two weeks? Done. Need to follow up with a client every month? Easy. It's your relationships, your way, effortlessly managed.</p>
      <p>Because the best calls are the ones you never forget to make.</p>
      <p><a href="https://apps.apple.com/us/app/ringlog/id6741731973" target="_blank" class="modal-link">Download on the App Store →</a></p>
    </div>
  </div>
</div>

<!-- Gift -->
<div class="modal-overlay" id="gift-modal">
  <div class="modal-box">
    <button class="modal-close" onclick="closeModal('gift-modal')">✕</button>
    <div class="modal-eyebrow">AI · Lifestyle</div>
    <h2 class="modal-title">Gift Ideas</h2>
    <div class="modal-body">
      <p>We've all been there. A birthday, an anniversary, the holidays are coming up, and you find yourself staring at a blank screen thinking: <em>what do I get them?</em></p>
      <p>Gift Ideas doesn't give you random suggestions — it understands the person you're shopping for. It learns from preferences, occasions, and subtle hints, then surfaces the perfect gift like magic. No more endless searching, no more last-minute panic.</p>
      <p>Simple. Thoughtful. It just works. Because at the heart of it, gift-giving isn't about the thing — it's about the feeling. This app helps you give something that truly matters.</p>
    </div>
  </div>
</div>

<!-- Privacy -->
<div class="modal-overlay" id="privacy-modal">
  <div class="modal-box">
    <button class="modal-close" onclick="closeModal('privacy-modal')">✕</button>
    <div class="modal-eyebrow">Legal</div>
    <h2 class="modal-title">Privacy Policy</h2>
    <div class="modal-body">
      <h3>Information We Collect</h3>
      <p><strong>In-App Purchases:</strong> All payments are processed securely through Apple's in-app purchase system. We do not collect or store payment information.</p>
      <p><strong>Usage Data:</strong> We may collect anonymous data on app usage to improve functionality.</p>
      <p><strong>Images:</strong> Any images uploaded are processed locally on your device. We do not store or share these images.</p>
      <h3>How We Use Your Data</h3>
      <ul>
        <li>To enable premium features or subscriptions</li>
        <li>To improve the app through anonymous usage analysis</li>
      </ul>
      <h3>Data Sharing</h3>
      <p>We do not sell or share your personal information with third parties. Payment data is handled securely by Apple.</p>
      <h3>Your Rights</h3>
      <ul>
        <li>You can manage or cancel subscriptions via your Apple account</li>
        <li>For data concerns, contact us at Matthewhoytapps@gmail.com</li>
      </ul>
      <h3>Updates</h3>
      <p>We may update this policy from time to time. Changes will be posted within the app and on our website.</p>
      <h3>Contact</h3>
      <p>Questions? Email us at <strong>Matthewhoytapps@gmail.com</strong></p>
    </div>
  </div>
</div>

<!-- Terms -->
<div class="modal-overlay" id="terms-modal">
  <div class="modal-box">
    <button class="modal-close" onclick="closeModal('terms-modal')">✕</button>
    <div class="modal-eyebrow">Legal</div>
    <h2 class="modal-title">Terms of Service</h2>
    <div class="modal-body">
      <h3>Acceptance of Terms</h3>
      <p>By downloading, installing, or using our applications, you agree to be bound by these Terms of Service.</p>
      <h3>License to Use</h3>
      <ul>
        <li>We grant a limited, non-exclusive, non-transferable license for personal, non-commercial use</li>
        <li>You must be at least 13 years old; under 18 requires parental consent</li>
      </ul>
      <h3>In-App Purchases</h3>
      <ul>
        <li>All purchases are processed securely through Apple's in-app purchase system</li>
        <li>Purchased features are non-transferable and non-refundable unless required by applicable law</li>
      </ul>
      <h3>Intellectual Property</h3>
      <p>All content, logos, and materials are owned by us and protected by copyright law. You may not copy, modify, distribute, or sell any part of the app.</p>
      <h3>API Use</h3>
      <p>Some apps use OpenAI's API to generate content. All usage complies with OpenAI's terms and privacy policies.</p>
      <h3>Disclaimer</h3>
      <ul>
        <li>Apps are provided "as is" without warranties of any kind</li>
        <li>We do not guarantee the accuracy or suitability of results</li>
      </ul>
      <h3>Governing Law</h3>
      <p>These terms are governed by the laws of the United States of America.</p>
      <h3>Contact</h3>
      <p>Questions? Email <strong>Matthewhoytapps@gmail.com</strong></p>
    </div>
  </div>
</div>

<script>
  // ── Modal ──
  function openModal(id) {
    document.getElementById(id).classList.add('active');
    document.body.style.overflow = 'hidden';
  }
  function closeModal(id) {
    document.getElementById(id).classList.remove('active');
    document.body.style.overflow = '';
  }
  document.querySelectorAll('.modal-overlay').forEach(el => {
    el.addEventListener('click', e => {
      if (e.target === el) closeModal(el.id);
    });
  });
  document.addEventListener('keydown', e => {
    if (e.key === 'Escape') {
      document.querySelectorAll('.modal-overlay.active').forEach(el => closeModal(el.id));
    }
  });

  // ── Mobile nav ──
  const hamburger = document.getElementById('hamburger');
  const mobileNav = document.getElementById('mobile-nav');
  hamburger.addEventListener('click', () => mobileNav.classList.toggle('open'));
  function closeMobile() { mobileNav.classList.remove('open'); }

  // ── Scroll reveal ──
  const revealEls = document.querySelectorAll('.reveal');
  const io = new IntersectionObserver((entries) => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        setTimeout(() => entry.target.classList.add('visible'), 60);
        io.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1 });
  revealEls.forEach(el => io.observe(el));

  // ── Stagger cards ──
  document.querySelectorAll('.apps-grid .app-card').forEach((card, i) => {
    card.style.transitionDelay = (i * 80) + 'ms';
  });
  document.querySelectorAll('.faq-item').forEach((item, i) => {
    item.style.transitionDelay = (i * 60) + 'ms';
  });

  // ── Smooth nav on scroll ──
  document.querySelectorAll('a[href^="#"]').forEach(a => {
    a.addEventListener('click', e => {
      const target = document.querySelector(a.getAttribute('href'));
      if (target) { e.preventDefault(); target.scrollIntoView({ behavior: 'smooth' }); }
    });
  });
</script>

<script>
  // ── Floating Specks ──
  const canvas = document.getElementById('specks');
  const ctx = canvas.getContext('2d');

  function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  resizeCanvas();
  window.addEventListener('resize', resizeCanvas);

  const paths = [{
    points: function(t) {
      const cellSize = 300;
      const cornerRadius = 50;
      const gridX = Math.floor(t * canvas.width / cellSize) * cellSize;
      const gridY = Math.floor(t * canvas.height / cellSize) * cellSize;
      const localT = (t * canvas.width) % cellSize / cellSize;

      if (localT < 0.2) {
        const angle = localT * Math.PI / 0.4;
        return { x: gridX + cornerRadius * (1 - Math.cos(angle)), y: gridY + cornerRadius * (1 - Math.sin(angle)) };
      } else if (localT < 0.8) {
        const progress = (localT - 0.2) / 0.6;
        return { x: gridX + cornerRadius + progress * (cellSize - 2 * cornerRadius), y: gridY + cornerRadius + progress * (cellSize - 2 * cornerRadius) };
      } else {
        const angle = (localT - 0.8) * Math.PI / 0.4 + Math.PI / 2;
        return { x: gridX + cellSize - cornerRadius + cornerRadius * Math.cos(angle), y: gridY + cellSize - cornerRadius + cornerRadius * Math.sin(angle) };
      }
    }
  }];

  const specks = [];
  for (let i = 0; i < 200; i++) {
    specks.push({
      pathIndex: 0,
      pathProgress: Math.random(),
      speed: Math.random() * 0.0002 + 0.0001,
      radius: Math.random() * 4 + 1.5,
      opacity: Math.random() * 0.35 + 0.2,
      pulse: Math.random() * Math.PI * 2,
      pulseSpeed: Math.random() * 0.02 + 0.01
    });
  }

  function drawSpecks() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    specks.forEach(speck => {
      speck.pathProgress += speck.speed;
      if (speck.pathProgress > 1) speck.pathProgress = 0;

      const pos = paths[speck.pathIndex].points(speck.pathProgress);
      speck.pulse += speck.pulseSpeed;
      const currentOpacity = speck.opacity + Math.sin(speck.pulse) * 0.15;

      // Larger bright core for the star-glint look in the screenshot
      const g = ctx.createRadialGradient(pos.x, pos.y, 0, pos.x, pos.y, speck.radius * 4);
      g.addColorStop(0,   `rgba(255,250,230,${Math.min(currentOpacity * 1.8, 0.9)})`);
      g.addColorStop(0.3, `rgba(255,240,200,${currentOpacity})`);
      g.addColorStop(0.7, `rgba(255,220,160,${currentOpacity * 0.4})`);
      g.addColorStop(1,   'rgba(255,200,120,0)');

      ctx.beginPath();
      ctx.fillStyle = g;
      ctx.arc(pos.x, pos.y, speck.radius * 4, 0, Math.PI * 2);
      ctx.fill();

      // Sharp bright centre for the star-glint sparkle
      if (speck.radius > 3) {
        ctx.beginPath();
        ctx.fillStyle = `rgba(255,255,255,${Math.min(currentOpacity * 2, 0.95)})`;
        ctx.arc(pos.x, pos.y, speck.radius * 0.6, 0, Math.PI * 2);
        ctx.fill();
      }
    });
    requestAnimationFrame(drawSpecks);
  }
  drawSpecks();
</script>
</body>
</html>

