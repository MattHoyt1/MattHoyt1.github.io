
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
    html { scroll-behavior: auto; }
    body {
      font-family: 'DM Sans', sans-serif;
      background: transparent;
      color: var(--ink);
      overflow-x: hidden;
    }
    body.preloading { overflow: hidden; height: 100vh; }
    /* ─── BACKGROUND SYSTEM ─── */
    html {
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
      opacity: 0.1;
    }
    #diag-lines svg { width: 100%; height: 100%; }
    /* WebGL 3D backdrop — fixed, above lines, below content */
    #webgl-bg {
      position: fixed;
      top: 0; left: 0; width: 100%; height: 100%;
      pointer-events: none;
      z-index: 1;
    }
    #webgl-bg canvas { display: block; width: 100%; height: 100%; }
    /* All page content sits above the backdrop */
    nav, section, footer, .modal-overlay { position: relative; z-index: 2; }
    /* Light sections: transparent bg so gradient + 3D show through */
    #apps    { background: transparent; }
    #contact { background: transparent; }
    /* Dark sections keep their solid backgrounds */
    .hero { background: var(--ink); }
    #faq  { background: var(--ink); }
    footer { background: var(--ink); }
    /* Cards on transparent sections need their own translucent bg */
    .app-card { background: rgba(255,255,255,0.78); backdrop-filter: blur(10px); }
    .contact-card { background: rgba(255,255,255,0.78); backdrop-filter: blur(10px); }

    /* ─── SCROLL PROGRESS BAR ─── */
    #scroll-progress {
      position: fixed;
      top: 0; left: 0;
      height: 2.5px;
      width: 0%;
      background: linear-gradient(90deg, var(--accent), var(--gold));
      z-index: 300;
      box-shadow: 0 0 12px rgba(201,96,58,0.5);
    }

    /* ─── PRELOADER ─── */
    #preloader {
      position: fixed;
      inset: 0;
      z-index: 999;
      background: var(--ink);
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      gap: 1.5rem;
    }
    .preloader-mark {
      font-family: 'DM Serif Display', serif;
      font-size: 2.75rem;
      color: var(--cream);
      letter-spacing: 0.08em;
      opacity: 0;
      animation: fadeInMark 0.9s ease forwards 0.1s;
    }
    .preloader-bar {
      width: 160px; height: 2px;
      background: rgba(255,255,255,0.1);
      overflow: hidden;
      border-radius: 2px;
    }
    .preloader-bar span {
      display: block; height: 100%; width: 0%;
      background: linear-gradient(90deg, var(--accent), var(--gold));
      animation: barFill 1.2s ease forwards 0.25s;
    }
    @keyframes fadeInMark { to { opacity: 1; } }
    @keyframes barFill { to { width: 100%; } }
    #preloader.done {
      opacity: 0;
      visibility: hidden;
      pointer-events: none;
      transition: opacity 0.7s ease, visibility 0.7s;
    }

    /* ─── CUSTOM CURSOR (native pointer + trailing ring) ─── */
    #cursor-ring {
      position: fixed;
      top: 0; left: 0;
      pointer-events: none;
      border-radius: 50%;
      z-index: 9999;
      will-change: transform;
      width: 32px; height: 32px;
      border: 1px solid rgba(201,96,58,0.45);
      transform: translate(-50%,-50%);
      transition: width 0.25s ease, height 0.25s ease, border-color 0.25s ease, background 0.25s ease;
    }
    #cursor-ring.active {
      width: 56px; height: 56px;
      border-color: var(--accent);
      background: rgba(201,96,58,0.08);
    }

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
      perspective: 1000px;
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
      background: radial-gradient(circle at 35% 35%, rgba(201,96,58,0.35), rgba(196,163,90,0.12) 50%, transparent 70%);
      border: 1px solid rgba(255,255,255,0.08);
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
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
      color: rgba(250,247,242,0.12);
      text-align: center;
      line-height: 1;
      user-select: none;
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
      perspective: 1400px;
    }
    .app-card {
      background: rgba(255,255,255,0.72);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border: 1px solid rgba(255,255,255,0.6);
      border-radius: var(--radius);
      padding: 2rem;
      cursor: pointer;
      transition: box-shadow 0.35s ease, border-color 0.35s ease, transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
      transform-style: preserve-3d;
      will-change: transform;
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
      box-shadow: 0 24px 48px rgba(15,14,13,0.16);
      border-color: transparent;
    }
    .app-card:hover::before { opacity: 1; }
    /* Card accent colors */
    .card-hygge { --card-accent: #c9603a; --card-bg: #fdf1ec; --glimmer-rgb: 201,96,58; }
    .card-bormes { --card-accent: #2a6eb5; --card-bg: #eef4fb; --glimmer-rgb: 42,110,181; }
    .card-danish { --card-accent: #b33535; --card-bg: #faeaea; --glimmer-rgb: 179,53,53; }
    .card-ring { --card-accent: #3a8c5c; --card-bg: #eaf4ee; --glimmer-rgb: 58,140,92; }
    .card-gift { --card-accent: #7a55b5; --card-bg: #f3eefb; --glimmer-rgb: 122,85,181; }
    .app-card::before {
      background: linear-gradient(135deg, var(--card-bg), white);
    }
    /* Faint diagonal glimmer sweep — lower-right to upper-left, once every 10s */
    .app-card::after, .modal-box::after {
      content: '';
      position: absolute;
      inset: -60%;
      background: linear-gradient(115deg, transparent 42%, rgba(var(--glimmer-rgb, 201,96,58), 0.5) 50%, transparent 58%);
      transform: translate(70%, 70%);
      opacity: 0;
      pointer-events: none;
      z-index: 2;
      animation: glimmerSweep 10s ease-in-out infinite;
    }
    @keyframes glimmerSweep {
      0% { transform: translate(70%, 70%); opacity: 0; }
      8% { opacity: 0.55; }
      38% { opacity: 0.55; }
      48%, 100% { transform: translate(-70%, -70%); opacity: 0; }
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
    /* Modal accent colors (feeds the glimmer sweep, matched to each app's card) */
    .modal-hygge   { --glimmer-rgb: 201,96,58; }
    .modal-bormes  { --glimmer-rgb: 42,110,181; }
    .modal-danish  { --glimmer-rgb: 179,53,53; }
    .modal-ring    { --glimmer-rgb: 58,140,92; }
    .modal-gift    { --glimmer-rgb: 122,85,181; }
    .modal-privacy { --glimmer-rgb: 196,163,90; }
    .modal-terms   { --glimmer-rgb: 107,124,135; }
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
    /* ─── SCROLL REVEAL (CSS fallback, used only if GSAP fails to load) ─── */
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
    @media (prefers-reduced-motion: reduce) {
      #webgl-bg { display: none; }
      .reveal { opacity: 1 !important; transform: none !important; }
    }
  </style>
</head>
<body class="preloading">

<!-- ── PRELOADER ── -->
<div id="preloader">
  <div class="preloader-mark">MH</div>
  <div class="preloader-bar"><span></span></div>
</div>

<!-- ── SCROLL PROGRESS ── -->
<div id="scroll-progress"></div>

<!-- ── DIAGONAL LINE PATTERN ── -->
<div id="diag-lines">
  <svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%">
    <defs>
      <pattern id="diamond-lines" x="0" y="0" width="260" height="260" patternUnits="userSpaceOnUse">
        <line x1="0" y1="0" x2="260" y2="260" stroke="#7a5c40" stroke-width="1"/>
        <line x1="260" y1="0" x2="0" y2="260" stroke="#7a5c40" stroke-width="1"/>
      </pattern>
    </defs>
    <rect width="100%" height="100%" fill="url(#diamond-lines)"/>
  </svg>
</div>

<!-- ── 3D WEBGL BACKDROP ── -->
<div id="webgl-bg"></div>

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

  <div class="hero-stats">
    <div class="stat-item">
      <div class="stat-num">24h</div>
      <div class="stat-label">Support response</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">0</div>
      <div class="stat-label">Data ever sold</div>
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
  <div class="modal-box modal-hygge">
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
  <div class="modal-box modal-bormes">
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
  <div class="modal-box modal-danish">
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
  <div class="modal-box modal-ring">
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
  <div class="modal-box modal-gift">
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
  <div class="modal-box modal-privacy">
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
  <div class="modal-box modal-terms">
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

<!-- ── Third-party libraries (GSAP + ScrollTrigger + Lenis smooth scroll) ── -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script src="https://unpkg.com/lenis@1.1.18/dist/lenis.min.js"></script>

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

  // ── Scroll reveal fallback (only runs if GSAP failed to load) ──
  if (!window.gsap) {
    const revealEls = document.querySelectorAll('.reveal');
    const io = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          setTimeout(() => entry.target.classList.add('visible'), 60);
          io.unobserve(entry.target);
        }
      });
    }, { threshold: 0.1 });
    revealEls.forEach(el => io.observe(el));
    document.querySelectorAll('.apps-grid .app-card').forEach((card, i) => {
      card.style.transitionDelay = (i * 80) + 'ms';
    });
    document.querySelectorAll('.faq-item').forEach((item, i) => {
      item.style.transitionDelay = (i * 60) + 'ms';
    });
  }

  // ── Smooth nav-link scrolling (Lenis takes over the physical scroll if present) ──
  document.querySelectorAll('a[href^="#"]').forEach(a => {
    a.addEventListener('click', e => {
      const target = document.querySelector(a.getAttribute('href'));
      if (target) {
        e.preventDefault();
        if (window.__lenis) window.__lenis.scrollTo(target, { duration: 1.4 });
        else target.scrollIntoView({ behavior: 'smooth' });
      }
    });
  });

  // ── Preloader ──
  window.addEventListener('load', () => {
    setTimeout(() => {
      document.getElementById('preloader').classList.add('done');
      document.body.classList.remove('preloading');
      window.dispatchEvent(new Event('site:ready'));
    }, 850);
  });
</script>

<!-- ── GSAP-driven reveals, cursor, card tilt, smooth scroll ── -->
<script>
  (function () {
    const hasGSAP = !!window.gsap && !!window.ScrollTrigger;

    // Smooth scroll (Lenis) — purely cosmetic; scroll position stays native so
    // the WebGL layer can always read window.scrollY directly.
    let lenis = null;
    if (window.Lenis) {
      lenis = new Lenis({
        duration: 1.05,
        easing: (t) => 1 - Math.pow(1 - t, 3),
        smoothWheel: true
      });
      window.__lenis = lenis;
      function raf(time) {
        lenis.raf(time);
        requestAnimationFrame(raf);
      }
      requestAnimationFrame(raf);
    }

    if (hasGSAP) {
      gsap.registerPlugin(ScrollTrigger);
      if (lenis) lenis.on('scroll', ScrollTrigger.update);

      // Hero entrance timeline
      const heroTl = gsap.timeline({ delay: 0.15, defaults: { ease: 'power3.out' } });
      heroTl
        .from('.hero-eyebrow', { opacity: 0, y: 16, duration: 0.7 })
        .from('.hero h1', { opacity: 0, y: 46, rotateX: 18, transformPerspective: 700, transformOrigin: '50% 100%', duration: 1, ease: 'power4.out' }, '-=0.45')
        .from('.hero-sub', { opacity: 0, y: 20, duration: 0.7 }, '-=0.55')
        .from('.hero-cta', { opacity: 0, y: 16, duration: 0.6 }, '-=0.45')
        .from('.hero-orb', { opacity: 0, scale: 0.7, duration: 1.1 }, '-=0.7')
        .from('.hero-stats .stat-item', { opacity: 0, y: 16, stagger: 0.08, duration: 0.6 }, '-=0.5');

      // Generic reveal for section headers / faq / contact (cards handled separately below)
      gsap.set('.reveal:not(.app-card)', { opacity: 0, y: 34 });
      gsap.utils.toArray('.reveal:not(.app-card)').forEach((el) => {
        gsap.to(el, {
          opacity: 1, y: 0, duration: 0.9, ease: 'power3.out',
          scrollTrigger: { trigger: el, start: 'top 87%' }
        });
      });

      // App cards: staggered 3D tilt-up entrance
      gsap.set('.app-card', { opacity: 0, y: 56, rotateX: 12, transformPerspective: 800, transformOrigin: '50% 100%' });
      ScrollTrigger.batch('.app-card', {
        start: 'top 88%',
        onEnter: (batch) => gsap.to(batch, { opacity: 1, y: 0, rotateX: 0, stagger: 0.1, duration: 0.85, ease: 'power3.out' })
      });
    }

    // 3D pointer-tilt on app cards (desktop only)
    const isFinePointer = window.matchMedia('(pointer: fine)').matches;
    if (isFinePointer) {
      document.querySelectorAll('.app-card').forEach((card) => {
        card.addEventListener('mousemove', (e) => {
          const r = card.getBoundingClientRect();
          const px = (e.clientX - r.left) / r.width - 0.5;
          const py = (e.clientY - r.top) / r.height - 0.5;
          const rx = (py * -14).toFixed(2);
          const ry = (px * 14).toFixed(2);
          card.style.transform = `perspective(900px) rotateX(${rx}deg) rotateY(${ry}deg) translateY(-6px) scale(1.015)`;
        });
        card.addEventListener('mouseleave', () => { card.style.transform = ''; });
      });

      // Custom cursor ring (native pointer stays visible; the ring trails behind it)
      const ring = document.createElement('div'); ring.id = 'cursor-ring';
      document.body.appendChild(ring);
      let mx = window.innerWidth / 2, my = window.innerHeight / 2, rx = mx, ry = my;
      window.addEventListener('mousemove', (e) => {
        mx = e.clientX; my = e.clientY;
      });
      (function ringLoop() {
        rx += (mx - rx) * 0.18;
        ry += (my - ry) * 0.18;
        ring.style.transform = `translate(${rx}px, ${ry}px) translate(-50%,-50%)`;
        requestAnimationFrame(ringLoop);
      })();
      document.querySelectorAll('a, button, .app-card').forEach((el) => {
        el.addEventListener('mouseenter', () => ring.classList.add('active'));
        el.addEventListener('mouseleave', () => ring.classList.remove('active'));
      });
    }

    // Scroll progress bar
    const progressBar = document.getElementById('scroll-progress');
    function updateProgress() {
      const max = document.documentElement.scrollHeight - window.innerHeight;
      const p = max > 0 ? Math.min(1, Math.max(0, window.scrollY / max)) : 0;
      progressBar.style.width = (p * 100) + '%';
      requestAnimationFrame(updateProgress);
    }
    requestAnimationFrame(updateProgress);
  })();
</script>

<!-- ── 3D WebGL background scene (Three.js) ── -->
<script type="module">
  import * as THREE from 'https://unpkg.com/three@0.160.0/build/three.module.js';

  const mount = document.getElementById('webgl-bg');
  if (!mount || window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    // respect reduced-motion; do nothing further
  } else {
    const isMobile = window.innerWidth < 760;

    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 100);
    camera.position.set(0, 0, 9);

    const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    renderer.setSize(window.innerWidth, window.innerHeight);
    mount.appendChild(renderer.domElement);

    // The shatter effect below is anchored to these two transparent sections
    // (rather than a raw scroll %) so it always plays out while the canvas is
    // actually visible — #faq in between is solid/opaque and would otherwise
    // hide the entire transition.
    const appsEl = document.getElementById('apps');
    const contactEl = document.getElementById('contact');

    // ── Lights ──
    scene.add(new THREE.AmbientLight(0xfff2e0, 0.55));
    const keyLight = new THREE.DirectionalLight(0xffe4c4, 1.15);
    keyLight.position.set(5, 6, 4);
    scene.add(keyLight);
    const rimLight = new THREE.PointLight(0xc4a35a, 1.3, 24);
    rimLight.position.set(-6, -2, 3);
    scene.add(rimLight);

    // ── Hero centerpiece: noise-displaced glassy blob ──
    const noiseGLSL = `
      vec3 mod289(vec3 x){return x - floor(x * (1.0/289.0)) * 289.0;}
      vec4 mod289(vec4 x){return x - floor(x * (1.0/289.0)) * 289.0;}
      vec4 permute(vec4 x){return mod289(((x*34.0)+1.0)*x);}
      vec4 taylorInvSqrt(vec4 r){return 1.79284291400159 - 0.85373472095314 * r;}
      float snoise(vec3 v){
        const vec2 C = vec2(1.0/6.0, 1.0/3.0);
        const vec4 D = vec4(0.0, 0.5, 1.0, 2.0);
        vec3 i  = floor(v + dot(v, C.yyy));
        vec3 x0 = v - i + dot(i, C.xxx);
        vec3 g = step(x0.yzx, x0.xyz);
        vec3 l = 1.0 - g;
        vec3 i1 = min(g.xyz, l.zxy);
        vec3 i2 = max(g.xyz, l.zxy);
        vec3 x1 = x0 - i1 + C.xxx;
        vec3 x2 = x0 - i2 + C.yyy;
        vec3 x3 = x0 - D.yyy;
        i = mod289(i);
        vec4 p = permute(permute(permute(
                   i.z + vec4(0.0, i1.z, i2.z, 1.0))
                 + i.y + vec4(0.0, i1.y, i2.y, 1.0))
                 + i.x + vec4(0.0, i1.x, i2.x, 1.0));
        float n_ = 0.142857142857;
        vec3 ns = n_ * D.wyz - D.xzx;
        vec4 j = p - 49.0 * floor(p * ns.z * ns.z);
        vec4 x_ = floor(j * ns.z);
        vec4 y_ = floor(j - 7.0 * x_);
        vec4 x = x_ * ns.x + ns.yyyy;
        vec4 y = y_ * ns.x + ns.yyyy;
        vec4 h = 1.0 - abs(x) - abs(y);
        vec4 b0 = vec4(x.xy, y.xy);
        vec4 b1 = vec4(x.zw, y.zw);
        vec4 s0 = floor(b0) * 2.0 + 1.0;
        vec4 s1 = floor(b1) * 2.0 + 1.0;
        vec4 sh = -step(h, vec4(0.0));
        vec4 a0 = b0.xzyw + s0.xzyw * sh.xxyy;
        vec4 a1 = b1.xzyw + s1.xzyw * sh.zzww;
        vec3 p0 = vec3(a0.xy, h.x);
        vec3 p1 = vec3(a0.zw, h.y);
        vec3 p2 = vec3(a1.xy, h.z);
        vec3 p3 = vec3(a1.zw, h.w);
        vec4 norm = taylorInvSqrt(vec4(dot(p0,p0), dot(p1,p1), dot(p2,p2), dot(p3,p3)));
        p0 *= norm.x; p1 *= norm.y; p2 *= norm.z; p3 *= norm.w;
        vec4 m = max(0.6 - vec4(dot(x0,x0), dot(x1,x1), dot(x2,x2), dot(x3,x3)), 0.0);
        m = m * m;
        return 42.0 * dot(m * m, vec4(dot(p0,x0), dot(p1,x1), dot(p2,x2), dot(p3,x3)));
      }
    `;

    const blobGeo = new THREE.IcosahedronGeometry(1.9, isMobile ? 3 : 5);
    const blobMat = new THREE.ShaderMaterial({
      transparent: true,
      uniforms: {
        uTime: { value: 0 },
        uAmp: { value: 0.22 },
        uOpacity: { value: 1 },
        uColorA: { value: new THREE.Color(0xc9603a) },
        uColorB: { value: new THREE.Color(0xc4a35a) }
      },
      vertexShader: `
        uniform float uTime;
        uniform float uAmp;
        varying vec3 vNormal;
        varying float vNoise;
        ${noiseGLSL}
        void main() {
          float n = snoise(position * 1.35 + uTime * 0.15);
          vec3 displaced = position + normal * n * uAmp;
          vNoise = n;
          vNormal = normalize(normalMatrix * normal);
          gl_Position = projectionMatrix * modelViewMatrix * vec4(displaced, 1.0);
        }
      `,
      fragmentShader: `
        uniform vec3 uColorA;
        uniform vec3 uColorB;
        uniform float uOpacity;
        varying vec3 vNormal;
        varying float vNoise;
        void main() {
          float fresnel = pow(1.0 - abs(vNormal.z), 2.4);
          vec3 base = mix(uColorA, uColorB, vNoise * 0.5 + 0.5);
          vec3 color = base + fresnel * 0.65;
          gl_FragColor = vec4(color, 0.8 * uOpacity);
        }
      `
    });
    const heroBlob = new THREE.Mesh(blobGeo, blobMat);
    heroBlob.position.set(2.4, 0.1, -1.2);
    scene.add(heroBlob);

    // ── Five floating shapes, one per app, color-matched to card accents ──
    const appDefs = [
      { color: 0xc9603a, geo: () => new THREE.IcosahedronGeometry(0.85, 0), pos: [-4.3, 1.6, -2] },
      { color: 0x2a6eb5, geo: () => new THREE.TorusGeometry(0.62, 0.24, 16, 60), pos: [4.6, -0.9, -3.4] },
      { color: 0xb33535, geo: () => new THREE.OctahedronGeometry(0.9, 0), pos: [-3.6, -2.5, -1.2] },
      { color: 0x3a8c5c, geo: () => new THREE.DodecahedronGeometry(0.78, 0), pos: [3.9, 2.7, -3.8] },
      { color: 0x7a55b5, geo: () => new THREE.SphereGeometry(0.72, 24, 24), pos: [0.2, -3.5, -2.3] }
    ];
    const shapesGroup = new THREE.Group();
    const fragCount = 42;
    const shapes = appDefs.map((def, i) => {
      const mat = new THREE.MeshStandardMaterial({
        color: def.color, emissive: def.color, emissiveIntensity: 0.35,
        metalness: 0.35, roughness: 0.3, transparent: true, opacity: 0.92
      });
      const geo = def.geo();
      const mesh = new THREE.Mesh(geo, mat);
      mesh.position.set(...def.pos);
      shapesGroup.add(mesh);

      // Sample points across the shape's surface — these become the shattered
      // "dust" fragments once the page is scrolled past the halfway mark.
      const posAttr = geo.attributes.position;
      const fragBase = new Float32Array(fragCount * 3);
      const fragDirs = new Float32Array(fragCount * 3);
      const fragJitter = new Float32Array(fragCount);
      for (let f = 0; f < fragCount; f++) {
        const vi = Math.floor(Math.random() * posAttr.count);
        const vx = posAttr.getX(vi), vy = posAttr.getY(vi), vz = posAttr.getZ(vi);
        fragBase[f * 3] = vx; fragBase[f * 3 + 1] = vy; fragBase[f * 3 + 2] = vz;
        const len = Math.hypot(vx, vy, vz) || 1;
        fragDirs[f * 3] = vx / len; fragDirs[f * 3 + 1] = vy / len; fragDirs[f * 3 + 2] = vz / len;
        fragJitter[f] = 0.6 + Math.random() * 0.9;
      }
      const fragGeo = new THREE.BufferGeometry();
      fragGeo.setAttribute('position', new THREE.BufferAttribute(fragBase.slice(), 3));
      const fragMat = new THREE.PointsMaterial({
        color: def.color, size: 0.1, transparent: true, opacity: 0,
        depthWrite: false, blending: THREE.AdditiveBlending
      });
      const fragPoints = new THREE.Points(fragGeo, fragMat);
      shapesGroup.add(fragPoints);

      return {
        mesh, fragPoints, fragBase, fragDirs, fragJitter,
        baseY: def.pos[1], speed: 0.5 + Math.random() * 0.4, offset: i * 1.7, dir: i % 2 === 0 ? 1 : -1
      };
    });
    scene.add(shapesGroup);

    // ── Ambient particle field ──
    function makeSprite() {
      const c = document.createElement('canvas'); c.width = c.height = 64;
      const ctx = c.getContext('2d');
      const g = ctx.createRadialGradient(32, 32, 0, 32, 32, 32);
      g.addColorStop(0, 'rgba(255,250,235,1)');
      g.addColorStop(0.4, 'rgba(255,230,190,0.6)');
      g.addColorStop(1, 'rgba(255,230,190,0)');
      ctx.fillStyle = g; ctx.fillRect(0, 0, 64, 64);
      return new THREE.CanvasTexture(c);
    }
    const particleCount = isMobile ? 140 : 380;
    const posArr = new Float32Array(particleCount * 3);
    for (let i = 0; i < particleCount; i++) {
      posArr[i * 3] = (Math.random() - 0.5) * 22;
      posArr[i * 3 + 1] = (Math.random() - 0.5) * 20;
      posArr[i * 3 + 2] = (Math.random() - 0.5) * 14 - 2;
    }
    const particleGeo = new THREE.BufferGeometry();
    particleGeo.setAttribute('position', new THREE.BufferAttribute(posArr, 3));
    const particleMat = new THREE.PointsMaterial({
      size: 0.13, map: makeSprite(), transparent: true, depthWrite: false,
      blending: THREE.AdditiveBlending, opacity: 0.65
    });
    const points = new THREE.Points(particleGeo, particleMat);
    scene.add(points);

    // ── Highlight the shape matching whichever app card is centered on screen ──
    let highlightIndex = -1;
    window.addEventListener('site:ready', () => {
      const cardEls = Array.from(document.querySelectorAll('.app-card'));
      if (cardEls.length) {
        const cardObserver = new IntersectionObserver((entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) highlightIndex = cardEls.indexOf(entry.target);
          });
        }, { threshold: 0.6 });
        cardEls.forEach((el) => cardObserver.observe(el));
      }
    });

    // ── Resize ──
    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    // ── Scroll-linked animation loop ──
    let smoothP = 0;
    let smoothBreakP = 0;
    function tick(time) {
      const t = time * 0.001;
      const maxScroll = document.documentElement.scrollHeight - window.innerHeight;
      const p = maxScroll > 0 ? Math.min(1, Math.max(0, window.scrollY / maxScroll)) : 0;
      smoothP += (p - smoothP) * 0.06;

      camera.position.z = 9 - smoothP * 4;
      camera.position.y = -smoothP * 1.4;
      camera.lookAt(0, -smoothP * 0.6, 0);

      shapesGroup.rotation.y = smoothP * Math.PI * 0.7;
      shapesGroup.rotation.x = smoothP * 0.22;

      // Shatter progress: ramps 0 → 0.5 while scrolling through the (visible)
      // apps section, holds steady through the opaque #faq section, then
      // ramps 0.5 → 1 while scrolling through the (visible) contact section.
      const appsStart = appsEl.offsetTop;
      const appsEnd = appsStart + appsEl.offsetHeight;
      const appsMid = appsStart + appsEl.offsetHeight * 0.5;
      const contactStart = contactEl.offsetTop;
      // Clamp to maxScroll — the footer is shorter than the viewport, so the
      // literal bottom of the contact section is often past the page's actual
      // max scroll position. Anchoring to maxScroll guarantees the ramp can
      // always fully complete once you reach the true bottom of the page.
      const contactEnd = Math.max(contactStart + 1, Math.min(contactStart + contactEl.offsetHeight, maxScroll));
      let breakTarget;
      if (window.scrollY <= appsMid) breakTarget = 0;
      else if (window.scrollY <= appsEnd) breakTarget = 0.5 * (window.scrollY - appsMid) / (appsEnd - appsMid);
      else if (window.scrollY <= contactStart) breakTarget = 0.5;
      else if (window.scrollY <= contactEnd) breakTarget = 0.5 + 0.5 * (window.scrollY - contactStart) / (contactEnd - contactStart);
      else breakTarget = 1;
      smoothBreakP += (breakTarget - smoothBreakP) * 0.08;

      shapes.forEach((s, i) => {
        s.mesh.position.y = s.baseY + Math.sin(t * s.speed + s.offset) * 0.4;
        s.mesh.rotation.x += 0.0016 * s.dir;
        s.mesh.rotation.y += 0.0022 * s.dir;
        const targetIntensity = i === highlightIndex ? 1.5 : 0.35;
        s.mesh.material.emissiveIntensity += (targetIntensity - s.mesh.material.emissiveIntensity) * 0.05;

        // breakP drives the transition; the solid mesh dissolves quickly while
        // the fragments take over, so the "shattering" moment reads clearly
        // instead of just looking like a slow fade.
        const breakP = smoothBreakP;
        s.mesh.material.opacity = 0.92 * Math.max(0, 1 - breakP * 1.6);
        s.mesh.visible = breakP < 0.65;

        s.fragPoints.position.copy(s.mesh.position);
        s.fragPoints.rotation.copy(s.mesh.rotation);
        s.fragPoints.material.opacity = breakP > 0.02 ? Math.min(0.95, breakP * 2) : 0;
        s.fragPoints.material.size = 0.17 * (1 - breakP * 0.75);

        const fragPos = s.fragPoints.geometry.attributes.position;
        for (let f = 0; f < fragCount; f++) {
          const spread = breakP * s.fragJitter[f] * 6.5;
          const drift = Math.sin(t * 0.6 + f) * breakP * 0.25;
          fragPos.setXYZ(
            f,
            s.fragBase[f * 3] + s.fragDirs[f * 3] * spread + drift,
            s.fragBase[f * 3 + 1] + s.fragDirs[f * 3 + 1] * spread - breakP * 1.1,
            s.fragBase[f * 3 + 2] + s.fragDirs[f * 3 + 2] * spread + drift
          );
        }
        fragPos.needsUpdate = true;
      });

      blobMat.uniforms.uTime.value = t;
      heroBlob.rotation.y = t * 0.08;
      heroBlob.rotation.x = Math.sin(t * 0.15) * 0.1;
      const heroFade = 1 - Math.min(1, window.scrollY / (window.innerHeight * 0.9));
      heroBlob.visible = heroFade > 0.01;
      blobMat.uniforms.uOpacity.value = heroFade;
      heroBlob.scale.setScalar(1 + (1 - heroFade) * 0.15);

      points.rotation.y = t * 0.015 + smoothP * 0.3;
      points.position.y = smoothP * 1.2;

      renderer.render(scene, camera);
      requestAnimationFrame(tick);
    }
    requestAnimationFrame(tick);
  }
</script>

</body>
</html>
