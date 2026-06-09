
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <link rel="preconnect" href="https://fonts.googleapis.com"/>
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=Outfit:wght@300;400;500;600&display=swap" rel="stylesheet"/>
  <style>
    /* ─── RESET & BASE ─────────────────────────────── */
    *, *::before, *::after { margin:0; padding:0; box-sizing:border-box; }
    html { scroll-behavior:smooth; font-size:16px; }

    :root {
      --bg:       #23132d;
      --bg2:      #2c1a38;
      --card:     #311e3f;
      --accent:   #c9a96e;
      --accent2:  #9b6fc4;
      --light:    #f0eaf8;
      --muted:    #a090b8;
      --white:    #ffffff;
      --border:   rgba(201,169,110,0.15);
      --nav-h:    70px;
    }

    body {
      background: var(--bg);
      color: var(--light);
      font-family: 'Outfit', sans-serif;
      font-weight: 300;
      overflow-x: hidden;
      line-height: 1.6;
    }

    img { display:block; max-width:100%; }
    a   { text-decoration:none; }

    /* noise grain */
    body::after {
      content:'';
      position:fixed; inset:0;
      background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.75' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='300' height='300' filter='url(%23n)' opacity='.03'/%3E%3C/svg%3E");
      pointer-events:none; z-index:9000;
    }

    /* ─── UTILITIES ─────────────────────────────────── */
    .section-label {
      font-size:.72rem; letter-spacing:.25em; text-transform:uppercase;
      color:var(--accent); margin-bottom:.75rem; font-weight:500;
    }
    .section-title {
      font-family:'Playfair Display', serif;
      font-size:clamp(2rem, 4vw, 3.2rem);
      font-weight:700; color:var(--white); line-height:1.15;
      margin-bottom:1.2rem;
    }
    .section-divider {
      width:50px; height:2px;
      background:linear-gradient(90deg,var(--accent),transparent);
      margin-bottom:2.5rem;
    }
    .reveal { opacity:0; transform:translateY(28px); transition:opacity .75s ease, transform .75s ease; }
    .reveal.visible { opacity:1; transform:translateY(0); }

    .btn-gold {
      display:inline-block;
      background:var(--accent); color:var(--bg);
      padding:.8rem 1.9rem; border-radius:.3rem;
      font-size:.85rem; font-weight:600; letter-spacing:.04em;
      transition:all .3s;
    }
    .btn-gold:hover { background:#d9ba82; transform:translateY(-2px); box-shadow:0 8px 24px rgba(201,169,110,.3); }

    .btn-ghost {
      display:inline-block;
      border:1px solid var(--border); color:var(--accent);
      padding:.8rem 1.9rem; border-radius:.3rem;
      font-size:.85rem; letter-spacing:.04em;
      transition:all .3s;
    }
    .btn-ghost:hover { border-color:var(--accent); background:rgba(201,169,110,.07); }

    /* ─── NAV ────────────────────────────────────────── */
    nav {
      position:fixed; top:0; left:0; right:0; z-index:500;
      height:var(--nav-h);
      display:flex; align-items:center; justify-content:space-between;
      padding:0 clamp(1.2rem, 5vw, 4rem);
      background:rgba(35,19,45,.88);
      backdrop-filter:blur(14px);
      border-bottom:1px solid var(--border);
    }
    .nav-logo {
      font-family:'Playfair Display', serif;
      font-size:1.55rem; font-weight:700;
      color:var(--accent); letter-spacing:.04em;
    }
    .nav-links { display:flex; gap:2rem; list-style:none; }
    .nav-links a {
      font-size:.78rem; letter-spacing:.16em; text-transform:uppercase;
      color:var(--muted); transition:color .25s; font-weight:400;
    }
    .nav-links a:hover { color:var(--accent); }

    /* hamburger */
    .hamburger {
      display:none; flex-direction:column; gap:5px; cursor:pointer;
      background:none; border:none; padding:4px;
    }
    .hamburger span { display:block; width:24px; height:2px; background:var(--muted); border-radius:2px; transition:all .3s; }
    .hamburger.open span:nth-child(1) { transform:translateY(7px) rotate(45deg); }
    .hamburger.open span:nth-child(2) { opacity:0; }
    .hamburger.open span:nth-child(3) { transform:translateY(-7px) rotate(-45deg); }

    .mobile-menu {
      display:none; position:fixed; top:var(--nav-h); left:0; right:0;
      background:rgba(35,19,45,.97); backdrop-filter:blur(16px);
      padding:1.5rem clamp(1.2rem,5vw,4rem) 2rem;
      border-bottom:1px solid var(--border); z-index:490;
      flex-direction:column; gap:.2rem;
    }
    .mobile-menu.open { display:flex; }
    .mobile-menu a {
      padding:.85rem 0; font-size:.9rem; letter-spacing:.1em;
      text-transform:uppercase; color:var(--muted);
      border-bottom:1px solid var(--border); transition:color .25s;
    }
    .mobile-menu a:last-child { border-bottom:none; }
    .mobile-menu a:hover { color:var(--accent); }

    /* ─── HERO ───────────────────────────────────────── */
    #hero {
      min-height:100vh;
      padding-top:var(--nav-h);
      display:flex; align-items:center;
      padding-left:clamp(1.2rem,5vw,4rem);
      padding-right:clamp(1.2rem,5vw,4rem);
      position:relative; overflow:hidden;
    }
    .hero-orb {
      position:absolute; border-radius:50%; pointer-events:none;
      filter:blur(90px);
    }
    .hero-orb.o1 {
      width:clamp(280px,50vw,550px); height:clamp(280px,50vw,550px);
      background:rgba(155,111,196,.2);
      top:-80px; right:-80px;
      animation:orb1 9s ease-in-out infinite;
    }
    .hero-orb.o2 {
      width:clamp(180px,30vw,320px); height:clamp(180px,30vw,320px);
      background:rgba(201,169,110,.1);
      bottom:60px; left:5%;
      animation:orb2 11s ease-in-out infinite;
    }
    @keyframes orb1 { 0%,100%{transform:translate(0,0)} 50%{transform:translate(-25px,35px)} }
    @keyframes orb2 { 0%,100%{transform:translate(0,0)} 50%{transform:translate(18px,-25px)} }

    .hero-content { position:relative; z-index:1; max-width:780px; }

    .hero-badge {
      display:inline-flex; align-items:center; gap:.5rem;
      border:1px solid rgba(201,169,110,.35);
      background:rgba(201,169,110,.06);
      padding:.38rem 1.1rem; border-radius:2rem; margin-bottom:2rem;
      font-size:.72rem; letter-spacing:.18em; text-transform:uppercase;
      color:var(--accent); font-weight:500;
      animation:fadeUp .9s .05s both;
    }
    .hero-badge::before { content:'●'; font-size:.45rem; color:#5dca82; }

    .hero-name {
      font-family:'Playfair Display', serif;
      font-size:clamp(3.8rem, 11vw, 9rem);
      font-weight:900; line-height:.95;
      color:var(--white); letter-spacing:-.02em;
      animation:fadeUp .9s .15s both;
    }
    .hero-name .gold { color:var(--accent); }

    .hero-role {
      margin-top:1.4rem;
      font-size:clamp(.95rem,1.8vw,1.15rem);
      color:var(--muted); line-height:1.75; max-width:520px;
      animation:fadeUp .9s .25s both;
    }
    .hero-role strong { color:var(--light); font-weight:500; }

    .hero-cta {
      margin-top:2.5rem; display:flex; gap:1rem; flex-wrap:wrap;
      animation:fadeUp .9s .35s both;
    }

    .hero-scroll {
      position:absolute; bottom:2rem; left:50%; transform:translateX(-50%);
      display:flex; flex-direction:column; align-items:center; gap:.5rem;
      color:var(--muted); font-size:.65rem; letter-spacing:.2em; text-transform:uppercase;
      animation:fadeUp .9s .55s both; z-index:1;
    }
    .scroll-bar {
      width:1px; height:36px;
      background:linear-gradient(var(--accent),transparent);
      animation:pulse 2s ease-in-out infinite;
    }
    @keyframes pulse { 0%,100%{opacity:1;transform:scaleY(1)} 50%{opacity:.3;transform:scaleY(.5)} }
    @keyframes fadeUp { from{opacity:0;transform:translateY(36px)} to{opacity:1;transform:translateY(0)} }

    /* ─── SLIDER ─────────────────────────────────────── */
    #slider-section {
      padding: clamp(3rem,6vw,5rem) clamp(1.2rem,5vw,4rem);
      background: var(--bg2);
    }
    .slider-header { margin-bottom:2rem; }

    .slider-wrap { position:relative; overflow:hidden; border-radius:.6rem; }

    .slides-track {
      display:flex;
      transition:transform .6s cubic-bezier(.4,0,.2,1);
    }

    .slide {
      min-width:100%; position:relative;
      aspect-ratio:16/7;
      background:var(--card);
      overflow:hidden; flex-shrink:0;
    }
    @media(max-width:600px){ .slide{ aspect-ratio:4/3; } }

    .slide-inner {
      width:100%; height:100%;
      display:flex; align-items:center; justify-content:center;
      position:relative; overflow:hidden;
    }

    /* placeholder gradients until real images are added */
    .slide:nth-child(1) .slide-inner { background:linear-gradient(135deg,#1a0d26 0%,#3d1f5a 50%,#c9a96e22 100%); }
    .slide:nth-child(2) .slide-inner { background:linear-gradient(135deg,#0d1a26 0%,#1f3d5a 50%,#6ec9c922 100%); }
    .slide:nth-child(3) .slide-inner { background:linear-gradient(135deg,#1a1a0d 0%,#3d3d1f 50%,#c9c96e22 100%); }
    .slide:nth-child(4) .slide-inner { background:linear-gradient(135deg,#1a0d0d 0%,#5a1f1f 50%,#c96e6e22 100%); }
    .slide:nth-child(5) .slide-inner { background:linear-gradient(135deg,#0d1a0d 0%,#1f5a1f 50%,#6ec96e22 100%); }

    /* actual image inside slide */
    .slide img {
      position:absolute; inset:0;
      width:100%; height:100%; object-fit:cover;
      opacity:0; transition:opacity .4s;
    }
    .slide img.loaded { opacity:1; }

    .slide-label {
      position:absolute; bottom:0; left:0; right:0;
      padding:2rem 2rem 1.4rem;
      background:linear-gradient(transparent,rgba(35,19,45,.92));
      z-index:2;
    }
    .slide-label h3 {
      font-family:'Playfair Display',serif;
      font-size:clamp(1.1rem,3vw,1.6rem);
      color:var(--white); margin-bottom:.3rem;
    }
    .slide-label p { font-size:.78rem; color:var(--accent); letter-spacing:.1em; text-transform:uppercase; }

    /* placeholder icon */
    .slide-placeholder {
      display:flex; flex-direction:column; align-items:center;
      gap:.8rem; color:var(--muted); z-index:1;
    }
    .slide-placeholder .pl-icon { font-size:3rem; opacity:.25; }
    .slide-placeholder .pl-txt { font-size:.75rem; letter-spacing:.12em; text-transform:uppercase; opacity:.4; }

    /* nav arrows */
    .slider-arrow {
      position:absolute; top:50%; transform:translateY(-50%);
      z-index:10; background:rgba(35,19,45,.75); border:1px solid var(--border);
      color:var(--accent); width:42px; height:42px; border-radius:50%;
      display:flex; align-items:center; justify-content:center;
      cursor:pointer; font-size:1.1rem; transition:all .25s;
      backdrop-filter:blur(6px);
    }
    .slider-arrow:hover { background:var(--accent); color:var(--bg); border-color:var(--accent); }
    .slider-arrow.prev { left:1rem; }
    .slider-arrow.next { right:1rem; }

    /* dots */
    .slider-dots {
      display:flex; justify-content:center; gap:.6rem; margin-top:1.2rem;
    }
    .dot {
      width:8px; height:8px; border-radius:50%;
      background:rgba(201,169,110,.25); cursor:pointer; transition:all .3s;
      border:none;
    }
    .dot.active { background:var(--accent); transform:scale(1.3); }

    /* ─── ABOUT ──────────────────────────────────────── */
    #about {
      padding:clamp(4rem,8vw,7rem) clamp(1.2rem,5vw,4rem);
      display:grid; grid-template-columns:1fr 1fr; gap:clamp(2.5rem,5vw,5rem);
      align-items:center;
    }
    @media(max-width:800px){ #about{ grid-template-columns:1fr; } }

    .about-text p { color:var(--muted); line-height:1.9; margin-bottom:1.1rem; font-size:.93rem; }
    .about-btns { margin-top:2rem; display:flex; gap:1rem; flex-wrap:wrap; }

    .stats-grid { display:grid; grid-template-columns:1fr 1fr; gap:1.2rem; }
    .stat-card {
      padding:1.8rem 1.5rem; border:1px solid var(--border);
      border-radius:.5rem; background:rgba(255,255,255,.02);
      transition:border-color .3s, transform .3s;
    }
    .stat-card:hover { border-color:rgba(201,169,110,.4); transform:translateY(-4px); }
    .stat-num {
      font-family:'Playfair Display',serif;
      font-size:2.8rem; font-weight:700; color:var(--accent); line-height:1;
    }
    .stat-lbl { font-size:.78rem; color:var(--muted); margin-top:.4rem; }

    /* ─── SERVICES ───────────────────────────────────── */
    #services {
      padding:clamp(4rem,8vw,7rem) clamp(1.2rem,5vw,4rem);
      background:var(--bg2);
    }
    .services-grid {
      display:grid;
      grid-template-columns:repeat(auto-fit, minmax(min(280px,100%), 1fr));
      gap:1.3rem;
    }
    .service-card {
      padding:2.2rem; border:1px solid var(--border);
      border-radius:.5rem; background:rgba(49,30,63,.5);
      position:relative; overflow:hidden; transition:all .35s;
    }
    .service-card::after {
      content:''; position:absolute; bottom:0; left:0;
      width:0; height:2px; background:var(--accent); transition:width .35s;
    }
    .service-card:hover { transform:translateY(-5px); border-color:rgba(201,169,110,.28); box-shadow:0 16px 40px rgba(0,0,0,.25); }
    .service-card:hover::after { width:100%; }
    .svc-icon { font-size:1.8rem; margin-bottom:1rem; }
    .svc-title { font-family:'Playfair Display',serif; font-size:1.25rem; color:var(--white); margin-bottom:.7rem; }
    .svc-desc { font-size:.84rem; color:var(--muted); line-height:1.8; }

    /* ─── PORTFOLIO ──────────────────────────────────── */
    #portfolio { padding:clamp(4rem,8vw,7rem) clamp(1.2rem,5vw,4rem); }
    .portfolio-grid {
      display:grid;
      grid-template-columns:repeat(auto-fit, minmax(min(280px,100%), 1fr));
      gap:1.3rem;
    }
    .p-card {
      aspect-ratio:4/3; border-radius:.5rem;
      background:var(--card); border:1px solid var(--border);
      overflow:hidden; position:relative; cursor:pointer;
      transition:transform .35s;
    }
    .p-card:hover { transform:scale(1.02); }
    .p-card:hover .p-overlay { opacity:1; }
    .p-card img {
      width:100%; height:100%; object-fit:cover;
      opacity:0; transition:opacity .4s; position:absolute; inset:0;
    }
    .p-card img.loaded { opacity:1; }
    .p-ph {
      width:100%; height:100%;
      display:flex; flex-direction:column; align-items:center; justify-content:center;
      gap:.7rem; position:absolute; inset:0;
    }
    .p-ph .p-ico { font-size:2.2rem; opacity:.25; }
    .p-ph .p-lbl { font-size:.7rem; color:var(--muted); letter-spacing:.1em; text-transform:uppercase; opacity:.5; }
    .p-overlay {
      position:absolute; inset:0;
      background:rgba(35,19,45,.92);
      display:flex; flex-direction:column; align-items:center; justify-content:center;
      gap:.4rem; opacity:0; transition:opacity .3s; padding:1rem; text-align:center;
    }
    .p-overlay h4 { font-family:'Playfair Display',serif; font-size:1.2rem; color:var(--white); }
    .p-overlay p  { font-size:.72rem; color:var(--accent); letter-spacing:.1em; text-transform:uppercase; }

    .portfolio-footer { margin-top:2.5rem; text-align:center; }

    /* ─── CONTACT ────────────────────────────────────── */
    #contact {
      padding:clamp(4rem,8vw,7rem) clamp(1.2rem,5vw,4rem);
      background:var(--bg2);
    }
    .contact-grid {
      display:grid; grid-template-columns:1fr 1fr;
      gap:clamp(2.5rem,5vw,5rem); align-items:start;
    }
    @media(max-width:800px){ .contact-grid{ grid-template-columns:1fr; } }

    .contact-desc { font-size:.93rem; color:var(--muted); line-height:1.9; margin-bottom:2rem; }
    .c-links { display:flex; flex-direction:column; gap:.8rem; }
    .c-link {
      display:flex; align-items:center; gap:.9rem;
      padding:.85rem 1.1rem; border:1px solid var(--border);
      border-radius:.35rem; background:rgba(255,255,255,.02);
      color:var(--muted); font-size:.86rem; transition:all .28s;
    }
    .c-link:hover { color:var(--accent); border-color:rgba(201,169,110,.35); background:rgba(201,169,110,.04); }
    .c-icon {
      width:34px; height:34px; background:rgba(201,169,110,.1);
      border-radius:50%; display:flex; align-items:center; justify-content:center;
      font-size:.95rem; flex-shrink:0;
    }

    /* form */
    .contact-form { display:flex; flex-direction:column; gap:1.1rem; }
    .f-group { display:flex; flex-direction:column; gap:.45rem; }
    .f-group label { font-size:.7rem; letter-spacing:.12em; text-transform:uppercase; color:var(--muted); }
    .f-group input,
    .f-group textarea {
      background:rgba(255,255,255,.04); border:1px solid var(--border);
      border-radius:.35rem; padding:.85rem 1rem;
      color:var(--white); font-family:'Outfit',sans-serif;
      font-size:.88rem; outline:none; resize:none;
      transition:border-color .25s;
    }
    .f-group input:focus,
    .f-group textarea:focus { border-color:rgba(201,169,110,.5); }
    .f-group textarea { min-height:120px; }
    .form-submit {
      background:var(--accent); color:var(--bg);
      padding:.85rem; border-radius:.35rem;
      border:none; cursor:pointer; font-family:'Outfit',sans-serif;
      font-size:.88rem; font-weight:600; letter-spacing:.05em;
      transition:all .3s;
    }
    .form-submit:hover { background:#d9ba82; transform:translateY(-2px); }

    /* ─── FOOTER ─────────────────────────────────────── */
    footer {
      padding:2rem clamp(1.2rem,5vw,4rem);
      border-top:1px solid var(--border);
      display:flex; justify-content:space-between; align-items:center;
      flex-wrap:wrap; gap:1rem;
    }
    footer p { font-size:.76rem; color:var(--muted); }
    .f-socials { display:flex; gap:1.5rem; flex-wrap:wrap; }
    .f-socials a {
      font-size:.76rem; color:var(--muted); letter-spacing:.1em;
      text-transform:uppercase; transition:color .25s;
    }
    .f-socials a:hover { color:var(--accent); }

    /* ─── RESPONSIVE OVERRIDES ───────────────────────── */
    @media(max-width:768px) {
      .nav-links { display:none; }
      .hamburger { display:flex; }
    }
    @media(max-width:480px) {
      .hero-name { letter-spacing:-.03em; }
      .hero-cta  { flex-direction:column; }
      .hero-cta .btn-gold,
      .hero-cta .btn-ghost { text-align:center; }
      .about-btns { flex-direction:column; }
      .stats-grid { grid-template-columns:1fr 1fr; }
      footer { flex-direction:column; text-align:center; }
    }
  </style>
</head>
<body>

<!-- NAV -->
<nav>
  <a href="#hero" class="nav-logo">MB.</a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#services">Services</a></li>
    <li><a href="#portfolio">Work</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <button class="hamburger" id="ham" aria-label="Menu">
    <span></span><span></span><span></span>
  </button>
</nav>
<div class="mobile-menu" id="mob">
  <a href="#about"    onclick="closeMob()">About</a>
  <a href="#services" onclick="closeMob()">Services</a>
  <a href="#portfolio"onclick="closeMob()">Work</a>
  <a href="#contact"  onclick="closeMob()">Contact</a>
</div>

<!-- HERO -->
<section id="hero">
  <div class="hero-orb o1"></div>
  <div class="hero-orb o2"></div>
  <div class="hero-content">
    <div class="hero-badge">Available for Projects</div>
    <h1 class="hero-name">Mohamed<br><span class="gold">Barakat</span></h1>
    <p class="hero-role">
      <strong>Creative Graphic Designer & Social Media Specialist</strong><br>
      Expertise in web design, e-commerce, branding, and SEO strategies — crafting visuals that connect and convert.
    </p>
    <div class="hero-cta">
      <a href="#slider-section" class="btn-gold">View My Work</a>
      <a href="#contact" class="btn-ghost">Get In Touch</a>
    </div>
  </div>
  <div class="hero-scroll">
    <div class="scroll-bar"></div>
    <span>Scroll</span>
  </div>
</section>

<!-- SLIDER -->
<section id="slider-section">
  <div class="slider-header reveal">
    <p class="section-label">Featured Projects</p>
    <h2 class="section-title">Best Work</h2>
    <div class="section-divider"></div>
  </div>

  <div class="slider-wrap reveal">
    <div class="slides-track" id="track">

      <!-- Slide 1 -->
      <div class="slide">
        <div class="slide-inner">
          <!-- Replace src below with your real image URL -->
          <!-- <img src="YOUR_IMAGE_URL" alt="Eliraqi Brand" onload="this.classList.add('loaded')"/> -->
          <div class="slide-placeholder">
            <span class="pl-icon">🏠</span>
            <span class="pl-txt">Add your image here</span>
          </div>
        </div>
        <div class="slide-label">
          <h3>Eliraqi Brand</h3>
          <p>Social Media Design · E-Commerce</p>
        </div>
      </div>

      <!-- Slide 2 -->
      <div class="slide">
        <div class="slide-inner">
          <!-- <img src="YOUR_IMAGE_URL" alt="BEYOT Real Estate" onload="this.classList.add('loaded')"/> -->
          <div class="slide-placeholder">
            <span class="pl-icon">🏡</span>
            <span class="pl-txt">Add your image here</span>
          </div>
        </div>
        <div class="slide-label">
          <h3>BEYOT Real Estate</h3>
          <p>Company Profile · Brand Identity</p>
        </div>
      </div>

      <!-- Slide 3 -->
      <div class="slide">
        <div class="slide-inner">
          <!-- <img src="YOUR_IMAGE_URL" alt="Haven Baby Care" onload="this.classList.add('loaded')"/> -->
          <div class="slide-placeholder">
            <span class="pl-icon">👶</span>
            <span class="pl-txt">Add your image here</span>
          </div>
        </div>
        <div class="slide-label">
          <h3>Haven Baby Care</h3>
          <p>Branding · Social Media · Events</p>
        </div>
      </div>

      <!-- Slide 4 -->
      <div class="slide">
        <div class="slide-inner">
          <!-- <img src="YOUR_IMAGE_URL" alt="Coffee Shop Branding" onload="this.classList.add('loaded')"/> -->
          <div class="slide-placeholder">
            <span class="pl-icon">☕</span>
            <span class="pl-txt">Add your image here</span>
          </div>
        </div>
        <div class="slide-label">
          <h3>Coffee Shop Branding</h3>
          <p>Full Brand Kit · Print Design</p>
        </div>
      </div>

      <!-- Slide 5 -->
      <div class="slide">
        <div class="slide-inner">
          <!-- <img src="YOUR_IMAGE_URL" alt="designedby.bd" onload="this.classList.add('loaded')"/> -->
          <div class="slide-placeholder">
            <span class="pl-icon">✏️</span>
            <span class="pl-txt">Add your image here</span>
          </div>
        </div>
        <div class="slide-label">
          <h3>@designedby.bd</h3>
          <p>Freelance Design · Logo · Identity</p>
        </div>
      </div>

    </div><!-- /track -->

    <button class="slider-arrow prev" id="prev" aria-label="Previous">&#8592;</button>
    <button class="slider-arrow next" id="next" aria-label="Next">&#8594;</button>
  </div>

  <div class="slider-dots" id="dots"></div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="about-text reveal">
    <p class="section-label">About Me</p>
    <h2 class="section-title">Crafting Visual<br>Experiences</h2>
    <div class="section-divider"></div>
    <p>I'm a Creative Graphic Designer and Social Media Specialist based in Cairo, Egypt, with 7+ years of experience bridging design and e-commerce.</p>
    <p>Currently leading the Online & E-Commerce Division at Eliraqi Company — managing social media design, video production, product listings, SEO, and full e-commerce operations.</p>
    <p>Open to relocation and new senior opportunities — especially in Saudi Arabia's home appliances and electronics sector.</p>
    <div class="about-btns">
      <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="btn-gold">Behance Portfolio</a>
      <a href="https://www.linkedin.com/in/mohammedbarakat1/" target="_blank" class="btn-ghost">LinkedIn</a>
    </div>
  </div>
  <div class="stats-grid reveal">
    <div class="stat-card">
      <div class="stat-num">7+</div>
      <div class="stat-lbl">Years Experience</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">50+</div>
      <div class="stat-lbl">Projects Delivered</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">6</div>
      <div class="stat-lbl">Core Services</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">∞</div>
      <div class="stat-lbl">Creative Ideas</div>
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
      <div class="svc-icon">🎨</div>
      <h3 class="svc-title">Graphic Design</h3>
      <p class="svc-desc">Brand identity, logo design, social media visuals, print materials, and creative campaigns that leave a lasting impression.</p>
    </div>
    <div class="service-card reveal">
      <div class="svc-icon">📱</div>
      <h3 class="svc-title">Social Media</h3>
      <p class="svc-desc">Strategic content creation, visual storytelling, and platform management to grow your brand's online presence.</p>
    </div>
    <div class="service-card reveal">
      <div class="svc-icon">🛒</div>
      <h3 class="svc-title">E-Commerce</h3>
      <p class="svc-desc">Product listings, store optimization, SEO strategies, and full e-commerce operations to boost your online sales.</p>
    </div>
    <div class="service-card reveal">
      <div class="svc-icon">🌐</div>
      <h3 class="svc-title">Web Design</h3>
      <p class="svc-desc">Clean, modern, conversion-focused web designs tailored for businesses and e-commerce platforms.</p>
    </div>
    <div class="service-card reveal">
      <div class="svc-icon">🎬</div>
      <h3 class="svc-title">Video Production</h3>
      <p class="svc-desc">Motion graphics, promotional videos, reels, and animated content that captures attention and drives engagement.</p>
    </div>
    <div class="service-card reveal">
      <div class="svc-icon">🔍</div>
      <h3 class="svc-title">SEO & Data Entry</h3>
      <p class="svc-desc">On-page SEO optimization, keyword strategies, and accurate data management to improve visibility and performance.</p>
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
  <div class="portfolio-grid">
    <div class="p-card reveal">
      <div class="p-ph"><span class="p-ico">🏠</span><span class="p-lbl">Home Appliances</span></div>
      <div class="p-overlay"><h4>Eliraqi Brand</h4><p>Social Media Design</p></div>
    </div>
    <div class="p-card reveal">
      <div class="p-ph"><span class="p-ico">👁️</span><span class="p-lbl">Mariam Lenses</span></div>
      <div class="p-overlay"><h4>Mariam Lenses</h4><p>Brand Identity</p></div>
    </div>
    <div class="p-card reveal">
      <div class="p-ph"><span class="p-ico">🏡</span><span class="p-lbl">Real Estate</span></div>
      <div class="p-overlay"><h4>BEYOT Real Estate</h4><p>Company Profile Design</p></div>
    </div>
    <div class="p-card reveal">
      <div class="p-ph"><span class="p-ico">👶</span><span class="p-lbl">Baby Care</span></div>
      <div class="p-overlay"><h4>Haven Baby Care</h4><p>Social Media & Branding</p></div>
    </div>
    <div class="p-card reveal">
      <div class="p-ph"><span class="p-ico">🛋️</span><span class="p-lbl">Furnishings</span></div>
      <div class="p-overlay"><h4>Diva Furnishings</h4><p>Logo & Brand Identity</p></div>
    </div>
    <div class="p-card reveal">
      <div class="p-ph"><span class="p-ico">☕</span><span class="p-lbl">Coffee Shop</span></div>
      <div class="p-overlay"><h4>Coffee Shop Branding</h4><p>Full Brand Kit</p></div>
    </div>
  </div>
  <div class="portfolio-footer reveal">
    <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="btn-gold">View Full Portfolio on Behance</a>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="reveal">
    <p class="section-label">Let's Talk</p>
    <h2 class="section-title">Get In Touch</h2>
    <div class="section-divider"></div>
  </div>
  <div class="contact-grid">
    <div class="reveal">
      <p class="contact-desc">Available for freelance projects, full-time roles, and creative collaborations. Based in Cairo — open to relocation, especially to Saudi Arabia.</p>
      <div class="c-links">
        <a href="mailto:mbarakat960@gmail.com" class="c-link">
          <div class="c-icon">✉️</div>mbarakat960@gmail.com
        </a>
        <a href="tel:00201008153733" class="c-link">
          <div class="c-icon">📞</div>+20 100 815 3733
        </a>
        <a href="https://www.instagram.com/designedby.bd" target="_blank" class="c-link">
          <div class="c-icon">📷</div>@designedby.bd
        </a>
        <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="c-link">
          <div class="c-icon">🎨</div>Behance Portfolio
        </a>
        <a href="https://www.linkedin.com/in/mohammedbarakat1/" target="_blank" class="c-link">
          <div class="c-icon">💼</div>LinkedIn Profile
        </a>
      </div>
    </div>
    <div class="contact-form reveal">
      <div class="f-group">
        <label>Your Name</label>
        <input type="text" placeholder="John Doe"/>
      </div>
      <div class="f-group">
        <label>Email Address</label>
        <input type="email" placeholder="john@example.com"/>
      </div>
      <div class="f-group">
        <label>Subject</label>
        <input type="text" placeholder="Project Inquiry"/>
      </div>
      <div class="f-group">
        <label>Message</label>
        <textarea placeholder="Tell me about your project..."></textarea>
      </div>
      <button class="form-submit" onclick="window.location.href='mailto:mbarakat960@gmail.com'">Send Message</button>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <p>© 2026 Mohamed Barakat. All rights reserved.</p>
  <div class="f-socials">
    <a href="https://www.behance.net/mbarakat960b56" target="_blank">Behance</a>
    <a href="https://www.instagram.com/designedby.bd" target="_blank">Instagram</a>
    <a href="https://www.linkedin.com/in/mohammedbarakat1/" target="_blank">LinkedIn</a>
  </div>
</footer>

<script>
  /* ── Mobile Menu ── */
  const ham = document.getElementById('ham');
  const mob = document.getElementById('mob');
  ham.addEventListener('click', () => {
    ham.classList.toggle('open');
    mob.classList.toggle('open');
  });
  function closeMob() {
    ham.classList.remove('open');
    mob.classList.remove('open');
  }

  /* ── Slider ── */
  const track  = document.getElementById('track');
  const slides = track.querySelectorAll('.slide');
  const dotsEl = document.getElementById('dots');
  let cur = 0, total = slides.length, timer;

  // build dots
  slides.forEach((_,i) => {
    const d = document.createElement('button');
    d.className = 'dot' + (i===0?' active':'');
    d.setAttribute('aria-label','Slide '+(i+1));
    d.addEventListener('click', () => goTo(i));
    dotsEl.appendChild(d);
  });

  function goTo(n) {
    cur = (n + total) % total;
    track.style.transform = `translateX(-${cur * 100}%)`;
    dotsEl.querySelectorAll('.dot').forEach((d,i) => d.classList.toggle('active', i===cur));
    resetTimer();
  }

  function resetTimer() {
    clearInterval(timer);
    timer = setInterval(() => goTo(cur + 1), 4500);
  }

  document.getElementById('prev').addEventListener('click', () => goTo(cur - 1));
  document.getElementById('next').addEventListener('click', () => goTo(cur + 1));

  // touch/swipe
  let tx = 0;
  track.addEventListener('touchstart', e => { tx = e.touches[0].clientX; }, {passive:true});
  track.addEventListener('touchend',   e => {
    const diff = tx - e.changedTouches[0].clientX;
    if (Math.abs(diff) > 40) goTo(diff > 0 ? cur+1 : cur-1);
  });

  resetTimer();

  /* ── Scroll Reveal ── */
  const io = new IntersectionObserver(entries => {
    entries.forEach((e, idx) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), idx * 70);
        io.unobserve(e.target);
      }
    });
  }, { threshold: 0.1 });
  document.querySelectorAll('.reveal').forEach(el => io.observe(el));
</script>
</body>
</html>
