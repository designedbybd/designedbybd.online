
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Mohamed Barakat &mdash; Creative Designer</title>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --primary: #23132d;
      --accent: #c9a96e;
      --accent2: #7c4fa0;
      --light: #f5f0eb;
      --muted: #a89db5;
      --white: #ffffff;
      --card-bg: #2e1d3d;
      --glass: rgba(46,29,61,0.6);
    }

    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
    html { scroll-behavior: smooth; }

    body {
      background: var(--primary);
      color: var(--light);
      font-family: 'DM Sans', sans-serif;
      font-weight: 300;
      overflow-x: hidden;
      cursor: none;
    }

    /* ── CUSTOM CURSOR ── */
    #cursor {
      position: fixed;
      width: 10px; height: 10px;
      background: var(--accent);
      border-radius: 50%;
      pointer-events: none;
      z-index: 99999;
      transition: transform 0.1s;
      mix-blend-mode: difference;
    }
    #cursor-ring {
      position: fixed;
      width: 36px; height: 36px;
      border: 1px solid rgba(201,169,110,0.5);
      border-radius: 50%;
      pointer-events: none;
      z-index: 99998;
      transition: transform 0.18s ease, width 0.3s, height 0.3s, border-color 0.3s;
    }
    body.hovering #cursor-ring {
      width: 56px; height: 56px;
      border-color: var(--accent);
    }

    /* ── NOISE OVERLAY ── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 9999;
      opacity: 0.35;
    }

    /* ── PROGRESS BAR ── */
    #progress {
      position: fixed;
      top: 0; left: 0;
      height: 2px;
      background: linear-gradient(to right, var(--accent2), var(--accent));
      z-index: 10001;
      width: 0%;
      transition: width 0.1s;
    }

    /* ── NAV ── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 1000;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.4rem 4rem;
      background: rgba(35,19,45,0.8);
      backdrop-filter: blur(20px);
      border-bottom: 1px solid rgba(201,169,110,0.08);
      transition: padding 0.4s, background 0.4s;
    }
    nav.scrolled {
      padding: 1rem 4rem;
      background: rgba(35,19,45,0.95);
    }
    .nav-logo {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.4rem;
      font-weight: 600;
      color: var(--accent);
      letter-spacing: 0.05em;
      text-decoration: none;
      transition: opacity 0.3s;
    }
    .nav-links { display: flex; gap: 2.5rem; list-style: none; }
    .nav-links a {
      color: var(--muted);
      text-decoration: none;
      font-size: 0.75rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      transition: color 0.3s;
      position: relative;
      padding-bottom: 2px;
    }
    .nav-links a::after {
      content: '';
      position: absolute;
      bottom: 0; left: 0;
      width: 0; height: 1px;
      background: var(--accent);
      transition: width 0.3s;
    }
    .nav-links a:hover { color: var(--accent); }
    .nav-links a:hover::after { width: 100%; }
    .nav-links a.active { color: var(--accent); }
    .nav-links a.active::after { width: 100%; }

    /* ── MOBILE NAV TOGGLE ── */
    .nav-toggle {
      display: none;
      flex-direction: column;
      gap: 5px;
      cursor: pointer;
      padding: 4px;
    }
    .nav-toggle span {
      display: block;
      width: 24px; height: 1px;
      background: var(--accent);
      transition: transform 0.3s, opacity 0.3s;
    }
    .nav-toggle.open span:nth-child(1) { transform: translateY(6px) rotate(45deg); }
    .nav-toggle.open span:nth-child(2) { opacity: 0; }
    .nav-toggle.open span:nth-child(3) { transform: translateY(-6px) rotate(-45deg); }

    .mobile-menu {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(35,19,45,0.98);
      backdrop-filter: blur(20px);
      z-index: 999;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 2.5rem;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.4s;
    }
    .mobile-menu.open {
      opacity: 1;
      pointer-events: all;
    }
    .mobile-menu a {
      font-family: 'Cormorant Garamond', serif;
      font-size: 3rem;
      font-weight: 300;
      color: var(--white);
      text-decoration: none;
      letter-spacing: 0.05em;
      transition: color 0.3s;
    }
    .mobile-menu a:hover { color: var(--accent); }

    /* ── HERO ── */
    #hero {
      min-height: 100vh;
      display: flex;
      align-items: center;
      padding: 0 4rem;
      position: relative;
      overflow: hidden;
    }
    .hero-bg-circle {
      position: absolute;
      border-radius: 50%;
      filter: blur(80px);
      pointer-events: none;
    }
    .hero-bg-circle.c1 {
      width: 600px; height: 600px;
      background: rgba(124,79,160,0.2);
      top: -150px; right: -100px;
      animation: float1 9s ease-in-out infinite;
    }
    .hero-bg-circle.c2 {
      width: 350px; height: 350px;
      background: rgba(201,169,110,0.1);
      bottom: 50px; left: 5%;
      animation: float2 11s ease-in-out infinite;
    }
    .hero-bg-circle.c3 {
      width: 200px; height: 200px;
      background: rgba(201,169,110,0.06);
      top: 40%; left: 40%;
      animation: float1 14s ease-in-out infinite reverse;
    }
    @keyframes float1 {
      0%,100% { transform: translate(0,0); }
      50% { transform: translate(-30px, 40px); }
    }
    @keyframes float2 {
      0%,100% { transform: translate(0,0); }
      50% { transform: translate(20px,-30px); }
    }

    .hero-content { max-width: 720px; position: relative; z-index: 1; }
    .hero-tag {
      display: inline-flex;
      align-items: center;
      gap: 0.5rem;
      font-size: 0.72rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--accent);
      border: 1px solid rgba(201,169,110,0.35);
      padding: 0.35rem 1rem;
      border-radius: 2rem;
      margin-bottom: 2rem;
      opacity: 0;
      animation: fadeUp 0.9s 0.1s ease forwards;
    }
    .hero-tag::before {
      content: '';
      width: 6px; height: 6px;
      background: var(--accent);
      border-radius: 50%;
      animation: pulse 2s infinite;
    }
    @keyframes pulse {
      0%,100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.4; transform: scale(0.7); }
    }

    .hero-name {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(3.8rem, 8.5vw, 7.5rem);
      font-weight: 300;
      line-height: 0.95;
      color: var(--white);
      opacity: 0;
      animation: fadeUp 0.9s 0.2s ease forwards;
      letter-spacing: -0.02em;
    }
    .hero-name span { color: var(--accent); display: block; }
    .hero-name .outline {
      -webkit-text-stroke: 1px rgba(255,255,255,0.3);
      color: transparent;
    }

    .hero-title {
      margin-top: 1.8rem;
      font-size: clamp(0.88rem, 1.4vw, 1rem);
      color: var(--muted);
      line-height: 1.75;
      max-width: 460px;
      opacity: 0;
      animation: fadeUp 0.9s 0.3s ease forwards;
    }

    .hero-cta {
      margin-top: 2.5rem;
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
      opacity: 0;
      animation: fadeUp 0.9s 0.4s ease forwards;
    }

    .hero-scroll {
      position: absolute;
      bottom: 2.5rem;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0.5rem;
      color: var(--muted);
      font-size: 0.68rem;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      opacity: 0;
      animation: fadeUp 1s 0.7s ease forwards;
    }
    .scroll-line {
      width: 1px; height: 44px;
      background: linear-gradient(to bottom, var(--accent), transparent);
      animation: scrollDown 2.2s ease-in-out infinite;
    }
    @keyframes scrollDown {
      0%,100% { transform: scaleY(1); opacity: 1; }
      50% { transform: scaleY(0.4); opacity: 0.2; }
    }
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(35px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* ── BUTTONS ── */
    .btn-primary {
      background: var(--accent);
      color: var(--primary);
      padding: 0.85rem 2rem;
      border-radius: 0.25rem;
      text-decoration: none;
      font-size: 0.82rem;
      font-weight: 500;
      letter-spacing: 0.06em;
      transition: all 0.3s;
      position: relative;
      overflow: hidden;
      display: inline-block;
    }
    .btn-primary::after {
      content: '';
      position: absolute;
      inset: 0;
      background: rgba(255,255,255,0.15);
      transform: translateX(-100%);
      transition: transform 0.4s ease;
    }
    .btn-primary:hover::after { transform: translateX(0); }
    .btn-primary:hover {
      transform: translateY(-2px);
      box-shadow: 0 10px 30px rgba(201,169,110,0.35);
    }

    .btn-outline {
      border: 1px solid rgba(201,169,110,0.4);
      color: var(--accent);
      padding: 0.85rem 2rem;
      border-radius: 0.25rem;
      text-decoration: none;
      font-size: 0.82rem;
      letter-spacing: 0.06em;
      transition: all 0.3s;
      display: inline-block;
    }
    .btn-outline:hover {
      border-color: var(--accent);
      background: rgba(201,169,110,0.08);
      transform: translateY(-2px);
    }

    /* ── SECTIONS ── */
    section { padding: 7rem 4rem; }
    .section-label {
      font-size: 0.7rem;
      letter-spacing: 0.28em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 0.9rem;
    }
    .section-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(2.4rem, 4.5vw, 3.8rem);
      font-weight: 300;
      color: var(--white);
      line-height: 1.05;
      margin-bottom: 1.5rem;
      letter-spacing: -0.01em;
    }
    .section-divider {
      width: 50px; height: 1px;
      background: var(--accent);
      margin-bottom: 3rem;
    }

    /* ── ABOUT ── */
    #about {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 6rem;
      align-items: center;
    }
    .about-text p {
      color: var(--muted);
      line-height: 1.9;
      margin-bottom: 1.2rem;
      font-size: 0.93rem;
    }
    .about-stats {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1.5rem;
    }
    .stat-item {
      padding: 2rem;
      border: 1px solid rgba(201,169,110,0.12);
      border-radius: 0.5rem;
      background: rgba(255,255,255,0.02);
      transition: border-color 0.4s, transform 0.4s, background 0.4s;
      position: relative;
      overflow: hidden;
    }
    .stat-item::before {
      content: '';
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at 0% 100%, rgba(201,169,110,0.06) 0%, transparent 60%);
      opacity: 0;
      transition: opacity 0.4s;
    }
    .stat-item:hover { border-color: rgba(201,169,110,0.35); transform: translateY(-5px); }
    .stat-item:hover::before { opacity: 1; }
    .stat-number {
      font-family: 'Cormorant Garamond', serif;
      font-size: 3.2rem;
      font-weight: 300;
      color: var(--accent);
      line-height: 1;
      font-variant-numeric: tabular-nums;
    }
    .stat-label { font-size: 0.76rem; color: var(--muted); letter-spacing: 0.05em; margin-top: 0.5rem; }

    /* ── SKILLS TAGS ── */
    .skills-tags {
      display: flex;
      flex-wrap: wrap;
      gap: 0.6rem;
      margin-top: 1.8rem;
    }
    .skill-tag {
      font-size: 0.72rem;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      color: var(--muted);
      border: 1px solid rgba(168,157,181,0.2);
      padding: 0.3rem 0.8rem;
      border-radius: 2rem;
      transition: all 0.3s;
    }
    .skill-tag:hover {
      color: var(--accent);
      border-color: rgba(201,169,110,0.4);
      background: rgba(201,169,110,0.05);
    }

    /* ── SERVICES ── */
    #services { background: rgba(255,255,255,0.012); }
    .services-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1.5rem;
      margin-top: 1rem;
    }
    .service-card {
      padding: 2.5rem;
      border: 1px solid rgba(201,169,110,0.1);
      border-radius: 0.5rem;
      background: rgba(46,29,61,0.4);
      transition: all 0.4s cubic-bezier(0.4,0,0.2,1);
      position: relative;
      overflow: hidden;
    }
    .service-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 3px; height: 0;
      background: linear-gradient(to bottom, var(--accent2), var(--accent));
      transition: height 0.4s cubic-bezier(0.4,0,0.2,1);
    }
    .service-card::after {
      content: '';
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at 30% 50%, rgba(124,79,160,0.08) 0%, transparent 70%);
      opacity: 0;
      transition: opacity 0.4s;
    }
    .service-card:hover::before { height: 100%; }
    .service-card:hover::after { opacity: 1; }
    .service-card:hover {
      border-color: rgba(201,169,110,0.25);
      transform: translateY(-8px);
      box-shadow: 0 24px 60px rgba(0,0,0,0.35);
    }
    .service-icon {
      font-size: 1.8rem;
      margin-bottom: 1.4rem;
      display: block;
      position: relative;
      z-index: 1;
    }
    .service-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.45rem;
      color: var(--white);
      margin-bottom: 0.8rem;
      position: relative;
      z-index: 1;
    }
    .service-desc {
      font-size: 0.84rem;
      color: var(--muted);
      line-height: 1.8;
      position: relative;
      z-index: 1;
    }

    /* ── COUNTER ANIM ── */
    .count-up { display: inline-block; }

    /* ── PORTFOLIO ── */
    #portfolio { position: relative; }
    .portfolio-filter {
      display: flex;
      gap: 0.8rem;
      flex-wrap: wrap;
      margin-bottom: 2rem;
    }
    .filter-btn {
      font-size: 0.72rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--muted);
      border: 1px solid rgba(168,157,181,0.2);
      background: transparent;
      padding: 0.4rem 1rem;
      border-radius: 2rem;
      cursor: none;
      transition: all 0.3s;
      font-family: 'DM Sans', sans-serif;
    }
    .filter-btn.active, .filter-btn:hover {
      color: var(--accent);
      border-color: rgba(201,169,110,0.5);
      background: rgba(201,169,110,0.07);
    }

    .portfolio-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1.5rem;
    }
    .portfolio-item {
      aspect-ratio: 4/3;
      border-radius: 0.6rem;
      background: var(--card-bg);
      border: 1px solid rgba(201,169,110,0.08);
      overflow: hidden;
      position: relative;
      cursor: none;
      transition: transform 0.5s cubic-bezier(0.4,0,0.2,1), opacity 0.4s;
    }
    .portfolio-item.hide { opacity: 0; transform: scale(0.9); pointer-events: none; }
    .portfolio-item:hover { transform: scale(1.03); }
    .portfolio-item:hover .portfolio-overlay { opacity: 1; }
    .portfolio-item:hover .p-icon { transform: scale(1.15); }

    .portfolio-placeholder {
      width: 100%; height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      gap: 0.8rem;
    }
    .portfolio-placeholder .p-icon {
      font-size: 2.8rem;
      opacity: 0.25;
      transition: transform 0.4s;
    }
    .portfolio-placeholder .p-label {
      font-size: 0.72rem;
      color: var(--muted);
      letter-spacing: 0.1em;
      text-transform: uppercase;
      opacity: 0.6;
    }
    .portfolio-overlay {
      position: absolute;
      inset: 0;
      background: linear-gradient(135deg, rgba(35,19,45,0.95) 0%, rgba(124,79,160,0.85) 100%);
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      gap: 0.5rem;
      opacity: 0;
      transition: opacity 0.35s;
    }
    .portfolio-overlay h4 {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.4rem;
      color: var(--white);
    }
    .portfolio-overlay p {
      font-size: 0.72rem;
      color: var(--accent);
      letter-spacing: 0.12em;
      text-transform: uppercase;
    }
    .portfolio-overlay .view-link {
      margin-top: 0.8rem;
      font-size: 0.72rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: rgba(255,255,255,0.6);
      border: 1px solid rgba(255,255,255,0.2);
      padding: 0.35rem 1rem;
      border-radius: 2rem;
      text-decoration: none;
      transition: all 0.3s;
    }
    .portfolio-overlay .view-link:hover {
      color: var(--white);
      border-color: rgba(255,255,255,0.5);
    }

    .portfolio-cta { margin-top: 3rem; text-align: center; }

    /* ── TESTIMONIAL / MARQUEE ── */
    .marquee-wrap {
      overflow: hidden;
      padding: 2rem 0;
      background: rgba(255,255,255,0.015);
      border-top: 1px solid rgba(201,169,110,0.08);
      border-bottom: 1px solid rgba(201,169,110,0.08);
      margin: 0 -4rem;
    }
    .marquee-track {
      display: flex;
      gap: 3rem;
      animation: marquee 20s linear infinite;
      width: max-content;
    }
    .marquee-track:hover { animation-play-state: paused; }
    .marquee-item {
      display: flex;
      align-items: center;
      gap: 0.8rem;
      white-space: nowrap;
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.1rem;
      font-weight: 300;
      color: var(--muted);
      letter-spacing: 0.05em;
    }
    .marquee-dot {
      width: 5px; height: 5px;
      background: var(--accent);
      border-radius: 50%;
      flex-shrink: 0;
    }
    @keyframes marquee {
      from { transform: translateX(0); }
      to { transform: translateX(-50%); }
    }

    /* ── CONTACT ── */
    #contact { background: rgba(255,255,255,0.012); }
    .contact-inner {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 5rem;
      align-items: start;
    }
    .contact-info p {
      color: var(--muted);
      line-height: 1.9;
      font-size: 0.93rem;
      margin-bottom: 2.5rem;
    }
    .contact-links { display: flex; flex-direction: column; gap: 0.8rem; }
    .contact-link {
      display: flex;
      align-items: center;
      gap: 1rem;
      text-decoration: none;
      color: var(--muted);
      font-size: 0.86rem;
      transition: all 0.3s;
      padding: 0.9rem 1.1rem;
      border: 1px solid rgba(201,169,110,0.1);
      border-radius: 0.4rem;
      background: rgba(255,255,255,0.02);
    }
    .contact-link:hover {
      color: var(--accent);
      border-color: rgba(201,169,110,0.3);
      background: rgba(201,169,110,0.04);
      transform: translateX(4px);
    }
    .contact-link-icon {
      width: 36px; height: 36px;
      background: rgba(201,169,110,0.08);
      border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      font-size: 0.95rem;
      flex-shrink: 0;
      transition: background 0.3s;
    }
    .contact-link:hover .contact-link-icon { background: rgba(201,169,110,0.15); }

    .contact-form { display: flex; flex-direction: column; gap: 1.2rem; }
    .form-group { display: flex; flex-direction: column; gap: 0.5rem; }
    .form-group label {
      font-size: 0.72rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--muted);
    }
    .form-group input,
    .form-group textarea {
      background: rgba(255,255,255,0.04);
      border: 1px solid rgba(201,169,110,0.12);
      border-radius: 0.4rem;
      padding: 0.9rem 1.1rem;
      color: var(--white);
      font-family: 'DM Sans', sans-serif;
      font-size: 0.88rem;
      transition: border-color 0.3s, background 0.3s, box-shadow 0.3s;
      outline: none;
      resize: none;
    }
    .form-group input:focus,
    .form-group textarea:focus {
      border-color: rgba(201,169,110,0.5);
      background: rgba(201,169,110,0.04);
      box-shadow: 0 0 0 3px rgba(201,169,110,0.06);
    }
    .form-group textarea { min-height: 140px; }

    .form-submit {
      background: var(--accent);
      color: var(--primary);
      padding: 0.9rem 2rem;
      border: none;
      border-radius: 0.25rem;
      font-size: 0.82rem;
      font-weight: 500;
      letter-spacing: 0.06em;
      cursor: none;
      font-family: 'DM Sans', sans-serif;
      transition: all 0.3s;
      position: relative;
      overflow: hidden;
    }
    .form-submit::after {
      content: '';
      position: absolute;
      inset: 0;
      background: rgba(255,255,255,0.15);
      transform: translateX(-100%);
      transition: transform 0.4s ease;
    }
    .form-submit:hover::after { transform: translateX(0); }
    .form-submit:hover {
      transform: translateY(-2px);
      box-shadow: 0 10px 30px rgba(201,169,110,0.3);
    }
    .form-submit.sent { background: #4caf7d; color: white; pointer-events: none; }

    /* ── FOOTER ── */
    footer {
      padding: 2.5rem 4rem;
      border-top: 1px solid rgba(201,169,110,0.08);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    footer p { font-size: 0.76rem; color: var(--muted); }
    .footer-socials { display: flex; gap: 1.5rem; }
    .footer-socials a {
      font-size: 0.76rem;
      color: var(--muted);
      text-decoration: none;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      transition: color 0.3s;
    }
    .footer-socials a:hover { color: var(--accent); }

    /* ── BACK TO TOP ── */
    #back-top {
      position: fixed;
      bottom: 2rem; right: 2rem;
      width: 44px; height: 44px;
      background: rgba(201,169,110,0.12);
      border: 1px solid rgba(201,169,110,0.25);
      border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      cursor: none;
      opacity: 0;
      pointer-events: none;
      transition: all 0.4s;
      z-index: 100;
      color: var(--accent);
      font-size: 0.9rem;
      text-decoration: none;
    }
    #back-top.visible { opacity: 1; pointer-events: all; }
    #back-top:hover { background: rgba(201,169,110,0.22); transform: translateY(-3px); }

    /* ── REVEAL ── */
    .reveal {
      opacity: 0;
      transform: translateY(28px);
      transition: opacity 0.8s ease, transform 0.8s ease;
    }
    .reveal.visible { opacity: 1; transform: translateY(0); }

    /* ── RESPONSIVE ── */
    @media (max-width: 900px) {
      nav { padding: 1.2rem 2rem; }
      #hero, section { padding-left: 2rem; padding-right: 2rem; }
      #about { grid-template-columns: 1fr; gap: 3rem; }
      .services-grid { grid-template-columns: 1fr 1fr; }
      .portfolio-grid { grid-template-columns: 1fr 1fr; }
      .contact-inner { grid-template-columns: 1fr; gap: 3rem; }
      footer { flex-direction: column; gap: 1rem; text-align: center; }
      .marquee-wrap { margin: 0 -2rem; }
      nav.scrolled { padding: 0.9rem 2rem; }
    }
    @media (max-width: 600px) {
      .nav-links { display: none; }
      .nav-toggle { display: flex; }
      .mobile-menu { display: flex; }
      .services-grid { grid-template-columns: 1fr; }
      .portfolio-grid { grid-template-columns: 1fr; }
      .about-stats { grid-template-columns: 1fr 1fr; }
      body { cursor: auto; }
      #cursor, #cursor-ring { display: none; }
    }
  </style>
</head>
<body>

  <!-- CURSOR -->
  <div id="cursor"></div>
  <div id="cursor-ring"></div>

  <!-- PROGRESS -->
  <div id="progress"></div>

  <!-- BACK TO TOP -->
  <a href="#hero" id="back-top" aria-label="Back to top">↑</a>

  <!-- NAV -->
  <nav id="nav">
    <a href="#hero" class="nav-logo">MB.</a>
    <ul class="nav-links">
      <li><a href="#about">About</a></li>
      <li><a href="#services">Services</a></li>
      <li><a href="#portfolio">Work</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
    <div class="nav-toggle" id="navToggle" onclick="toggleMobile()">
      <span></span><span></span><span></span>
    </div>
  </nav>

  <!-- MOBILE MENU -->
  <div class="mobile-menu" id="mobileMenu">
    <a href="#about" onclick="closeMobile()">About</a>
    <a href="#services" onclick="closeMobile()">Services</a>
    <a href="#portfolio" onclick="closeMobile()">Work</a>
    <a href="#contact" onclick="closeMobile()">Contact</a>
  </div>

  <!-- HERO -->
  <section id="hero">
    <div class="hero-bg-circle c1"></div>
    <div class="hero-bg-circle c2"></div>
    <div class="hero-bg-circle c3"></div>
    <div class="hero-content">
      <span class="hero-tag">Available for Projects</span>
      <h1 class="hero-name">
        Mohamed<br>
        <span>Barakat</span>
      </h1>
      <p class="hero-title">Creative Graphic Designer &amp; Social Media Specialist with expertise in web design, e-commerce, data entry, and SEO strategies.</p>
      <div class="hero-cta">
        <a href="#portfolio" class="btn-primary">View My Work</a>
        <a href="#contact" class="btn-outline">Get In Touch</a>
      </div>
    </div>
    <div class="hero-scroll">
      <div class="scroll-line"></div>
      <span>Scroll</span>
    </div>
  </section>

  <!-- MARQUEE -->
  <div class="marquee-wrap">
    <div class="marquee-track" id="marquee">
      <div class="marquee-item"><span class="marquee-dot"></span>Graphic Design</div>
      <div class="marquee-item"><span class="marquee-dot"></span>Social Media</div>
      <div class="marquee-item"><span class="marquee-dot"></span>Brand Identity</div>
      <div class="marquee-item"><span class="marquee-dot"></span>E-Commerce</div>
      <div class="marquee-item"><span class="marquee-dot"></span>Web Design</div>
      <div class="marquee-item"><span class="marquee-dot"></span>Video Production</div>
      <div class="marquee-item"><span class="marquee-dot"></span>SEO &amp; Strategy</div>
      <div class="marquee-item"><span class="marquee-dot"></span>Motion Graphics</div>
      <!-- Duplicate -->
      <div class="marquee-item"><span class="marquee-dot"></span>Graphic Design</div>
      <div class="marquee-item"><span class="marquee-dot"></span>Social Media</div>
      <div class="marquee-item"><span class="marquee-dot"></span>Brand Identity</div>
      <div class="marquee-item"><span class="marquee-dot"></span>E-Commerce</div>
      <div class="marquee-item"><span class="marquee-dot"></span>Web Design</div>
      <div class="marquee-item"><span class="marquee-dot"></span>Video Production</div>
      <div class="marquee-item"><span class="marquee-dot"></span>SEO &amp; Strategy</div>
      <div class="marquee-item"><span class="marquee-dot"></span>Motion Graphics</div>
    </div>
  </div>

  <!-- ABOUT -->
  <section id="about">
    <div class="about-text reveal">
      <p class="section-label">About Me</p>
      <h2 class="section-title">Crafting Visual<br>Experiences</h2>
      <div class="section-divider"></div>
      <p>I&rsquo;m a Creative Graphic Designer and Social Media Specialist based in Cairo, Egypt, with 7+ years of experience bridging design and e-commerce. Currently leading the Online &amp; E-Commerce Division at Eliraqi Company.</p>
      <p>My work spans brand identity, social media design, video production, product listings, SEO, and full e-commerce operations&mdash;delivering results that connect brands with their audience.</p>
      <div class="skills-tags">
        <span class="skill-tag">Adobe Photoshop</span>
        <span class="skill-tag">Illustrator</span>
        <span class="skill-tag">Premiere Pro</span>
        <span class="skill-tag">After Effects</span>
        <span class="skill-tag">nopCommerce</span>
        <span class="skill-tag">SEO</span>
        <span class="skill-tag">Social Media</span>
        <span class="skill-tag">Canva</span>
      </div>
      <div style="margin-top:2rem; display:flex; gap:1rem; flex-wrap:wrap;">
        <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="btn-primary">Behance Portfolio</a>
        <a href="https://www.linkedin.com/in/mohammedbarakat1/" target="_blank" class="btn-outline">LinkedIn</a>
      </div>
    </div>
    <div class="about-stats reveal">
      <div class="stat-item">
        <div class="stat-number"><span class="count-up" data-target="7">0</span>+</div>
        <div class="stat-label">Years of Experience</div>
      </div>
      <div class="stat-item">
        <div class="stat-number"><span class="count-up" data-target="50">0</span>+</div>
        <div class="stat-label">Projects Delivered</div>
      </div>
      <div class="stat-item">
        <div class="stat-number"><span class="count-up" data-target="3">0</span></div>
        <div class="stat-label">Core Specialties</div>
      </div>
      <div class="stat-item">
        <div class="stat-number">&infin;</div>
        <div class="stat-label">Creative Ideas</div>
      </div>
    </div>
  </section>

  <!-- SERVICES -->
  <section id="services">
    <div class="reveal">
      <p class="section-label">What I Do</p>
      <h2 class="section-title">Services</h2>
      <div class="section-divider"></div>
    </div>
    <div class="services-grid">
      <div class="service-card reveal">
        <span class="service-icon">🎨</span>
        <h3 class="service-title">Graphic Design</h3>
        <p class="service-desc">Brand identity, logo design, social media visuals, print materials, and creative campaigns that leave a lasting impression.</p>
      </div>
      <div class="service-card reveal">
        <span class="service-icon">📱</span>
        <h3 class="service-title">Social Media</h3>
        <p class="service-desc">Strategic content creation, visual storytelling, and platform management to grow your brand&rsquo;s online presence.</p>
      </div>
      <div class="service-card reveal">
        <span class="service-icon">🛒</span>
        <h3 class="service-title">E-Commerce</h3>
        <p class="service-desc">Product listings, store optimization, SEO strategies, and full e-commerce operations to boost your online sales.</p>
      </div>
      <div class="service-card reveal">
        <span class="service-icon">🌐</span>
        <h3 class="service-title">Web Design</h3>
        <p class="service-desc">Clean, modern, and conversion-focused web designs tailored for businesses and e-commerce platforms.</p>
      </div>
      <div class="service-card reveal">
        <span class="service-icon">🎬</span>
        <h3 class="service-title">Video Production</h3>
        <p class="service-desc">Motion graphics, promotional videos, reels, and animated content that captures attention and drives engagement.</p>
      </div>
      <div class="service-card reveal">
        <span class="service-icon">🔍</span>
        <h3 class="service-title">SEO &amp; Data Entry</h3>
        <p class="service-desc">On-page SEO optimization, keyword strategies, and accurate data management to improve visibility and performance.</p>
      </div>
    </div>
  </section>

  <!-- PORTFOLIO -->
  <section id="portfolio">
    <div class="reveal">
      <p class="section-label">Selected Work</p>
      <h2 class="section-title">Portfolio</h2>
      <div class="section-divider"></div>
    </div>
    <div class="portfolio-filter reveal">
      <button class="filter-btn active" data-filter="all">All Work</button>
      <button class="filter-btn" data-filter="branding">Branding</button>
      <button class="filter-btn" data-filter="social">Social Media</button>
      <button class="filter-btn" data-filter="ecommerce">E-Commerce</button>
    </div>
    <div class="portfolio-grid">
      <div class="portfolio-item reveal" data-cat="social branding">
        <div class="portfolio-placeholder">
          <span class="p-icon">🏠</span>
          <span class="p-label">Home Appliances</span>
        </div>
        <div class="portfolio-overlay">
          <h4>Eliraqi Brand</h4>
          <p>Social Media Design</p>
          <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="view-link">View on Behance</a>
        </div>
      </div>
      <div class="portfolio-item reveal" data-cat="branding">
        <div class="portfolio-placeholder">
          <span class="p-icon">👁️</span>
          <span class="p-label">Mariam Lenses</span>
        </div>
        <div class="portfolio-overlay">
          <h4>Mariam Lenses</h4>
          <p>Brand Identity</p>
          <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="view-link">View on Behance</a>
        </div>
      </div>
      <div class="portfolio-item reveal" data-cat="branding">
        <div class="portfolio-placeholder">
          <span class="p-icon">🏡</span>
          <span class="p-label">BEYOT Real Estate</span>
        </div>
        <div class="portfolio-overlay">
          <h4>BEYOT Real Estate</h4>
          <p>Company Profile Design</p>
          <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="view-link">View on Behance</a>
        </div>
      </div>
      <div class="portfolio-item reveal" data-cat="social branding">
        <div class="portfolio-placeholder">
          <span class="p-icon">👶</span>
          <span class="p-label">Haven Baby Care</span>
        </div>
        <div class="portfolio-overlay">
          <h4>Haven Baby Care</h4>
          <p>Social Media &amp; Branding</p>
          <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="view-link">View on Behance</a>
        </div>
      </div>
      <div class="portfolio-item reveal" data-cat="branding">
        <div class="portfolio-placeholder">
          <span class="p-icon">🛋️</span>
          <span class="p-label">Diva Furnishings</span>
        </div>
        <div class="portfolio-overlay">
          <h4>Diva Furnishings</h4>
          <p>Logo &amp; Brand Identity</p>
          <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="view-link">View on Behance</a>
        </div>
      </div>
      <div class="portfolio-item reveal" data-cat="branding social">
        <div class="portfolio-placeholder">
          <span class="p-icon">☕</span>
          <span class="p-label">Coffee Shop Branding</span>
        </div>
        <div class="portfolio-overlay">
          <h4>Coffee Shop Branding</h4>
          <p>Full Brand Kit</p>
          <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="view-link">View on Behance</a>
        </div>
      </div>
    </div>
    <div class="portfolio-cta reveal">
      <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="btn-primary">View Full Portfolio on Behance</a>
    </div>
  </section>

  <!-- CONTACT -->
  <section id="contact">
    <div class="reveal">
      <p class="section-label">Let&rsquo;s Talk</p>
      <h2 class="section-title">Get In Touch</h2>
      <div class="section-divider"></div>
    </div>
    <div class="contact-inner">
      <div class="contact-info reveal">
        <p>Available for freelance projects, full-time opportunities, and creative collaborations. Based in Cairo&mdash;open to relocation especially to Saudi Arabia.</p>
        <div class="contact-links">
          <a href="mailto:mbarakat960@gmail.com" class="contact-link">
            <div class="contact-link-icon">✉️</div>
            mbarakat960@gmail.com
          </a>
          <a href="tel:00201008153733" class="contact-link">
            <div class="contact-link-icon">📞</div>
            +20 100 815 3733
          </a>
          <a href="https://www.instagram.com/designedby.bd" target="_blank" class="contact-link">
            <div class="contact-link-icon">📷</div>
            @designedby.bd
          </a>
          <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="contact-link">
            <div class="contact-link-icon">🎨</div>
            Behance Portfolio
          </a>
          <a href="https://www.linkedin.com/in/mohammedbarakat1/" target="_blank" class="contact-link">
            <div class="contact-link-icon">💼</div>
            LinkedIn Profile
          </a>
        </div>
      </div>
      <div class="contact-form reveal">
        <div class="form-group">
          <label for="f-name">Your Name</label>
          <input id="f-name" type="text" placeholder="John Doe" />
        </div>
        <div class="form-group">
          <label for="f-email">Email Address</label>
          <input id="f-email" type="email" placeholder="john@example.com" />
        </div>
        <div class="form-group">
          <label for="f-subject">Subject</label>
          <input id="f-subject" type="text" placeholder="Project Inquiry" />
        </div>
        <div class="form-group">
          <label for="f-msg">Message</label>
          <textarea id="f-msg" placeholder="Tell me about your project&hellip;"></textarea>
        </div>
        <button class="form-submit" id="sendBtn" onclick="handleSend()">Send Message</button>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <p>&copy;&nbsp;2026 Mohamed Barakat. All rights reserved.</p>
    <div class="footer-socials">
      <a href="https://www.behance.net/mbarakat960b56" target="_blank">Behance</a>
      <a href="https://www.instagram.com/designedby.bd" target="_blank">Instagram</a>
      <a href="https://www.linkedin.com/in/mohammedbarakat1/" target="_blank">LinkedIn</a>
    </div>
  </footer>

  <script>
    /* ── CURSOR ── */
    const cur = document.getElementById('cursor');
    const ring = document.getElementById('cursor-ring');
    let mx = 0, my = 0, rx = 0, ry = 0;

    document.addEventListener('mousemove', e => {
      mx = e.clientX; my = e.clientY;
      cur.style.left = mx - 5 + 'px';
      cur.style.top  = my - 5 + 'px';
    });

    function animateRing() {
      rx += (mx - rx - 18) * 0.15;
      ry += (my - ry - 18) * 0.15;
      ring.style.left = rx + 'px';
      ring.style.top  = ry + 'px';
      requestAnimationFrame(animateRing);
    }
    animateRing();

    document.querySelectorAll('a, button, .portfolio-item, .stat-item, .service-card, .filter-btn').forEach(el => {
      el.addEventListener('mouseenter', () => document.body.classList.add('hovering'));
      el.addEventListener('mouseleave', () => document.body.classList.remove('hovering'));
    });

    /* ── PROGRESS BAR ── */
    const prog = document.getElementById('progress');
    window.addEventListener('scroll', () => {
      const pct = (window.scrollY / (document.body.scrollHeight - window.innerHeight)) * 100;
      prog.style.width = pct + '%';
    });

    /* ── NAV SHRINK + ACTIVE ── */
    const nav = document.getElementById('nav');
    const sections = document.querySelectorAll('section[id]');
    const navLinks = document.querySelectorAll('.nav-links a');
    const backTop  = document.getElementById('back-top');

    window.addEventListener('scroll', () => {
      nav.classList.toggle('scrolled', window.scrollY > 50);
      backTop.classList.toggle('visible', window.scrollY > 400);

      let current = '';
      sections.forEach(s => {
        if (window.scrollY >= s.offsetTop - 200) current = s.id;
      });
      navLinks.forEach(a => {
        a.classList.toggle('active', a.getAttribute('href') === '#' + current);
      });
    });

    /* ── MOBILE MENU ── */
    function toggleMobile() {
      const t = document.getElementById('navToggle');
      const m = document.getElementById('mobileMenu');
      t.classList.toggle('open');
      m.classList.toggle('open');
    }
    function closeMobile() {
      document.getElementById('navToggle').classList.remove('open');
      document.getElementById('mobileMenu').classList.remove('open');
    }

    /* ── SCROLL REVEAL ── */
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry, i) => {
        if (entry.isIntersecting) {
          setTimeout(() => entry.target.classList.add('visible'), i * 90);
          // trigger count-up once visible
          entry.target.querySelectorAll('.count-up').forEach(el => animateCount(el));
        }
      });
    }, { threshold: 0.12 });
    document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

    /* ── COUNT UP ── */
    function animateCount(el) {
      if (el.dataset.done) return;
      el.dataset.done = true;
      const target = +el.dataset.target;
      const dur = 1200;
      const start = performance.now();
      function step(now) {
        const t = Math.min((now - start) / dur, 1);
        const ease = 1 - Math.pow(1 - t, 3);
        el.textContent = Math.round(ease * target);
        if (t < 1) requestAnimationFrame(step);
      }
      requestAnimationFrame(step);
    }

    /* ── PORTFOLIO FILTER ── */
    document.querySelectorAll('.filter-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        const filter = btn.dataset.filter;
        document.querySelectorAll('.portfolio-item').forEach(item => {
          const cats = item.dataset.cat || '';
          if (filter === 'all' || cats.includes(filter)) {
            item.classList.remove('hide');
          } else {
            item.classList.add('hide');
          }
        });
      });
    });

    /* ── FORM SEND ── */
    function handleSend() {
      const name    = document.getElementById('f-name').value.trim();
      const email   = document.getElementById('f-email').value.trim();
      const subject = document.getElementById('f-subject').value.trim();
      const msg     = document.getElementById('f-msg').value.trim();
      if (!name || !email || !msg) { alert('Please fill in the required fields.'); return; }
      const btn = document.getElementById('sendBtn');
      btn.textContent = 'Opening mail client…';
      const mailto = `mailto:mbarakat960@gmail.com?subject=${encodeURIComponent(subject || 'Portfolio Inquiry')}&body=${encodeURIComponent('Name: ' + name + '\nEmail: ' + email + '\n\n' + msg)}`;
      window.location.href = mailto;
      setTimeout(() => {
        btn.textContent = 'Message Sent ✓';
        btn.classList.add('sent');
      }, 1500);
    }
  </script>
</body>
</html>
