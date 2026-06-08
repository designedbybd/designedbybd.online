[index.html](https://github.com/user-attachments/files/28712613/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Mohamed Barakat — Creative Designer</title>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400;600&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --primary: #23132d;
      --accent: #c9a96e;
      --accent2: #7c4fa0;
      --light: #f5f0eb;
      --muted: #a89db5;
      --white: #ffffff;
      --card-bg: #2e1d3d;
    }

    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

    html { scroll-behavior: smooth; }

    body {
      background: var(--primary);
      color: var(--light);
      font-family: 'DM Sans', sans-serif;
      font-weight: 300;
      overflow-x: hidden;
    }

    /* ── NOISE OVERLAY ── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 9999;
      opacity: 0.4;
    }

    /* ── NAV ── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.5rem 4rem;
      background: rgba(35,19,45,0.85);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid rgba(201,169,110,0.1);
    }

    .nav-logo {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.4rem;
      font-weight: 600;
      color: var(--accent);
      letter-spacing: 0.05em;
      text-decoration: none;
    }

    .nav-links {
      display: flex;
      gap: 2.5rem;
      list-style: none;
    }

    .nav-links a {
      color: var(--muted);
      text-decoration: none;
      font-size: 0.8rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      transition: color 0.3s;
    }

    .nav-links a:hover { color: var(--accent); }

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
      width: 500px; height: 500px;
      background: rgba(124,79,160,0.25);
      top: -100px; right: -100px;
      animation: float1 8s ease-in-out infinite;
    }

    .hero-bg-circle.c2 {
      width: 300px; height: 300px;
      background: rgba(201,169,110,0.12);
      bottom: 50px; left: 10%;
      animation: float2 10s ease-in-out infinite;
    }

    @keyframes float1 {
      0%,100% { transform: translate(0,0); }
      50% { transform: translate(-30px, 40px); }
    }

    @keyframes float2 {
      0%,100% { transform: translate(0,0); }
      50% { transform: translate(20px,-30px); }
    }

    .hero-content {
      max-width: 700px;
      animation: fadeUp 1s ease both;
    }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(40px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    .hero-tag {
      display: inline-block;
      font-size: 0.75rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--accent);
      border: 1px solid rgba(201,169,110,0.4);
      padding: 0.35rem 1rem;
      border-radius: 2rem;
      margin-bottom: 2rem;
      animation: fadeUp 1s 0.1s ease both;
    }

    .hero-name {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(3.5rem, 8vw, 7rem);
      font-weight: 300;
      line-height: 1;
      color: var(--white);
      animation: fadeUp 1s 0.2s ease both;
    }

    .hero-name span { color: var(--accent); }

    .hero-title {
      margin-top: 1.5rem;
      font-size: clamp(0.9rem, 1.5vw, 1.05rem);
      color: var(--muted);
      line-height: 1.7;
      max-width: 500px;
      animation: fadeUp 1s 0.3s ease both;
    }

    .hero-cta {
      margin-top: 2.5rem;
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
      animation: fadeUp 1s 0.4s ease both;
    }

    .btn-primary {
      background: var(--accent);
      color: var(--primary);
      padding: 0.85rem 2rem;
      border-radius: 0.25rem;
      text-decoration: none;
      font-size: 0.85rem;
      font-weight: 500;
      letter-spacing: 0.05em;
      transition: all 0.3s;
    }

    .btn-primary:hover {
      background: #d4b57e;
      transform: translateY(-2px);
      box-shadow: 0 8px 24px rgba(201,169,110,0.3);
    }

    .btn-outline {
      border: 1px solid rgba(201,169,110,0.4);
      color: var(--accent);
      padding: 0.85rem 2rem;
      border-radius: 0.25rem;
      text-decoration: none;
      font-size: 0.85rem;
      letter-spacing: 0.05em;
      transition: all 0.3s;
    }

    .btn-outline:hover {
      border-color: var(--accent);
      background: rgba(201,169,110,0.08);
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
      font-size: 0.7rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      animation: fadeUp 1s 0.6s ease both;
    }

    .scroll-line {
      width: 1px;
      height: 40px;
      background: linear-gradient(to bottom, var(--accent), transparent);
      animation: scrollDown 2s ease-in-out infinite;
    }

    @keyframes scrollDown {
      0%,100% { transform: scaleY(1); opacity: 1; }
      50% { transform: scaleY(0.5); opacity: 0.3; }
    }

    /* ── SECTIONS ── */
    section {
      padding: 7rem 4rem;
    }

    .section-label {
      font-size: 0.72rem;
      letter-spacing: 0.25em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 1rem;
    }

    .section-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(2.2rem, 4vw, 3.5rem);
      font-weight: 300;
      color: var(--white);
      line-height: 1.1;
      margin-bottom: 1.5rem;
    }

    .section-divider {
      width: 60px;
      height: 1px;
      background: var(--accent);
      margin-bottom: 3rem;
    }

    /* ── ABOUT ── */
    #about {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 5rem;
      align-items: center;
    }

    .about-text p {
      color: var(--muted);
      line-height: 1.9;
      margin-bottom: 1.2rem;
      font-size: 0.95rem;
    }

    .about-stats {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 2rem;
    }

    .stat-item {
      padding: 1.8rem;
      border: 1px solid rgba(201,169,110,0.15);
      border-radius: 0.5rem;
      background: rgba(255,255,255,0.02);
      transition: border-color 0.3s, transform 0.3s;
    }

    .stat-item:hover {
      border-color: rgba(201,169,110,0.4);
      transform: translateY(-4px);
    }

    .stat-number {
      font-family: 'Cormorant Garamond', serif;
      font-size: 3rem;
      font-weight: 300;
      color: var(--accent);
      line-height: 1;
    }

    .stat-label {
      font-size: 0.78rem;
      color: var(--muted);
      letter-spacing: 0.05em;
      margin-top: 0.5rem;
    }

    /* ── SERVICES ── */
    #services { background: rgba(255,255,255,0.015); }

    .services-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1.5rem;
      margin-top: 1rem;
    }

    .service-card {
      padding: 2.5rem;
      border: 1px solid rgba(201,169,110,0.12);
      border-radius: 0.5rem;
      background: rgba(46,29,61,0.5);
      transition: all 0.4s;
      position: relative;
      overflow: hidden;
    }

    .service-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 3px;
      height: 0;
      background: var(--accent);
      transition: height 0.4s;
    }

    .service-card:hover::before { height: 100%; }

    .service-card:hover {
      border-color: rgba(201,169,110,0.3);
      transform: translateY(-6px);
      box-shadow: 0 20px 50px rgba(0,0,0,0.3);
    }

    .service-icon {
      font-size: 2rem;
      margin-bottom: 1.2rem;
    }

    .service-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.4rem;
      color: var(--white);
      margin-bottom: 0.8rem;
    }

    .service-desc {
      font-size: 0.85rem;
      color: var(--muted);
      line-height: 1.8;
    }

    /* ── PORTFOLIO ── */
    .portfolio-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1.5rem;
      margin-top: 1rem;
    }

    .portfolio-item {
      aspect-ratio: 4/3;
      border-radius: 0.5rem;
      background: var(--card-bg);
      border: 1px solid rgba(201,169,110,0.1);
      overflow: hidden;
      position: relative;
      cursor: pointer;
      transition: transform 0.4s;
    }

    .portfolio-item:hover { transform: scale(1.02); }

    .portfolio-item:hover .portfolio-overlay { opacity: 1; }

    .portfolio-placeholder {
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      gap: 0.8rem;
    }

    .portfolio-placeholder .p-icon {
      font-size: 2.5rem;
      opacity: 0.3;
    }

    .portfolio-placeholder .p-label {
      font-size: 0.75rem;
      color: var(--muted);
      letter-spacing: 0.1em;
      text-transform: uppercase;
    }

    .portfolio-overlay {
      position: absolute;
      inset: 0;
      background: rgba(35,19,45,0.92);
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      gap: 0.5rem;
      opacity: 0;
      transition: opacity 0.3s;
    }

    .portfolio-overlay h4 {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.3rem;
      color: var(--white);
    }

    .portfolio-overlay p {
      font-size: 0.75rem;
      color: var(--accent);
      letter-spacing: 0.1em;
      text-transform: uppercase;
    }

    .portfolio-cta {
      margin-top: 3rem;
      text-align: center;
    }

    /* ── CONTACT ── */
    #contact {
      background: rgba(255,255,255,0.015);
    }

    .contact-inner {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 5rem;
      align-items: start;
    }

    .contact-info p {
      color: var(--muted);
      line-height: 1.9;
      font-size: 0.95rem;
      margin-bottom: 2.5rem;
    }

    .contact-links {
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    .contact-link {
      display: flex;
      align-items: center;
      gap: 1rem;
      text-decoration: none;
      color: var(--muted);
      font-size: 0.88rem;
      transition: color 0.3s;
      padding: 0.8rem 1rem;
      border: 1px solid rgba(201,169,110,0.1);
      border-radius: 0.35rem;
      background: rgba(255,255,255,0.02);
    }

    .contact-link:hover {
      color: var(--accent);
      border-color: rgba(201,169,110,0.3);
    }

    .contact-link-icon {
      width: 36px; height: 36px;
      background: rgba(201,169,110,0.1);
      border-radius: 50%;
      display: flex; align-items: center; justify-content: center;
      font-size: 1rem;
      flex-shrink: 0;
    }

    .contact-form {
      display: flex;
      flex-direction: column;
      gap: 1.2rem;
    }

    .form-group {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }

    .form-group label {
      font-size: 0.75rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--muted);
    }

    .form-group input,
    .form-group textarea {
      background: rgba(255,255,255,0.04);
      border: 1px solid rgba(201,169,110,0.15);
      border-radius: 0.35rem;
      padding: 0.9rem 1.1rem;
      color: var(--white);
      font-family: 'DM Sans', sans-serif;
      font-size: 0.88rem;
      transition: border-color 0.3s;
      outline: none;
      resize: none;
    }

    .form-group input:focus,
    .form-group textarea:focus {
      border-color: rgba(201,169,110,0.5);
    }

    .form-group textarea { min-height: 130px; }

    /* ── FOOTER ── */
    footer {
      padding: 2.5rem 4rem;
      border-top: 1px solid rgba(201,169,110,0.1);
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    footer p {
      font-size: 0.78rem;
      color: var(--muted);
    }

    .footer-socials {
      display: flex;
      gap: 1.5rem;
    }

    .footer-socials a {
      font-size: 0.78rem;
      color: var(--muted);
      text-decoration: none;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      transition: color 0.3s;
    }

    .footer-socials a:hover { color: var(--accent); }

    /* ── SCROLL REVEAL ── */
    .reveal {
      opacity: 0;
      transform: translateY(30px);
      transition: opacity 0.8s ease, transform 0.8s ease;
    }

    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* ── RESPONSIVE ── */
    @media (max-width: 900px) {
      nav { padding: 1.2rem 2rem; }
      #hero, section { padding-left: 2rem; padding-right: 2rem; }
      #about { grid-template-columns: 1fr; gap: 3rem; }
      .services-grid { grid-template-columns: 1fr 1fr; }
      .portfolio-grid { grid-template-columns: 1fr 1fr; }
      .contact-inner { grid-template-columns: 1fr; gap: 3rem; }
      footer { flex-direction: column; gap: 1rem; text-align: center; }
    }

    @media (max-width: 600px) {
      .nav-links { display: none; }
      .services-grid { grid-template-columns: 1fr; }
      .portfolio-grid { grid-template-columns: 1fr; }
      .about-stats { grid-template-columns: 1fr 1fr; }
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
  </nav>

  <!-- HERO -->
  <section id="hero">
    <div class="hero-bg-circle c1"></div>
    <div class="hero-bg-circle c2"></div>
    <div class="hero-content">
      <span class="hero-tag">Available for Projects</span>
      <h1 class="hero-name">Mohamed<br><span>Barakat</span></h1>
      <p class="hero-title">Creative Graphic Designer & Social Media Specialist with expertise in web design, e-commerce, data entry, and SEO strategies.</p>
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

  <!-- ABOUT -->
  <section id="about">
    <div class="about-text reveal">
      <p class="section-label">About Me</p>
      <h2 class="section-title">Crafting Visual<br>Experiences</h2>
      <div class="section-divider"></div>
      <p>I'm a Creative Graphic Designer and Social Media Specialist based in Cairo, Egypt, with 7+ years of experience bridging design and e-commerce. Currently leading the Online & E-Commerce Division at Eliraqi Company.</p>
      <p>My work spans brand identity, social media design, video production, product listings, SEO, and full e-commerce operations — delivering results that connect brands with their audience.</p>
      <div style="margin-top:2rem; display:flex; gap:1rem; flex-wrap:wrap;">
        <a href="https://www.behance.net/mbarakat960b56" target="_blank" class="btn-primary">Behance Portfolio</a>
        <a href="https://www.linkedin.com/in/mohammedbarakat1/" target="_blank" class="btn-outline">LinkedIn</a>
      </div>
    </div>
    <div class="about-stats reveal">
      <div class="stat-item">
        <div class="stat-number">7+</div>
        <div class="stat-label">Years of Experience</div>
      </div>
      <div class="stat-item">
        <div class="stat-number">50+</div>
        <div class="stat-label">Projects Delivered</div>
      </div>
      <div class="stat-item">
        <div class="stat-number">3</div>
        <div class="stat-label">Core Specialties</div>
      </div>
      <div class="stat-item">
        <div class="stat-number">∞</div>
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
        <div class="service-icon">🎨</div>
        <h3 class="service-title">Graphic Design</h3>
        <p class="service-desc">Brand identity, logo design, social media visuals, print materials, and creative campaigns that leave a lasting impression.</p>
      </div>
      <div class="service-card reveal">
        <div class="service-icon">📱</div>
        <h3 class="service-title">Social Media</h3>
        <p class="service-desc">Strategic content creation, visual storytelling, and platform management to grow your brand's online presence.</p>
      </div>
      <div class="service-card reveal">
        <div class="service-icon">🛒</div>
        <h3 class="service-title">E-Commerce</h3>
        <p class="service-desc">Product listings, store optimization, SEO strategies, and full e-commerce operations to boost your online sales.</p>
      </div>
      <div class="service-card reveal">
        <div class="service-icon">🌐</div>
        <h3 class="service-title">Web Design</h3>
        <p class="service-desc">Clean, modern, and conversion-focused web designs tailored for businesses and e-commerce platforms.</p>
      </div>
      <div class="service-card reveal">
        <div class="service-icon">🎬</div>
        <h3 class="service-title">Video Production</h3>
        <p class="service-desc">Motion graphics, promotional videos, reels, and animated content that captures attention and drives engagement.</p>
      </div>
      <div class="service-card reveal">
        <div class="service-icon">🔍</div>
        <h3 class="service-title">SEO & Data Entry</h3>
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
    <div class="portfolio-grid">
      <div class="portfolio-item reveal">
        <div class="portfolio-placeholder">
          <span class="p-icon">🏠</span>
          <span class="p-label">Home Appliances Branding</span>
        </div>
        <div class="portfolio-overlay">
          <h4>Eliraqi Brand</h4>
          <p>Social Media Design</p>
        </div>
      </div>
      <div class="portfolio-item reveal">
        <div class="portfolio-placeholder">
          <span class="p-icon">👁️</span>
          <span class="p-label">Mariam Lenses</span>
        </div>
        <div class="portfolio-overlay">
          <h4>Mariam Lenses</h4>
          <p>Brand Identity</p>
        </div>
      </div>
      <div class="portfolio-item reveal">
        <div class="portfolio-placeholder">
          <span class="p-icon">🏡</span>
          <span class="p-label">BEYOT Real Estate</span>
        </div>
        <div class="portfolio-overlay">
          <h4>BEYOT Real Estate</h4>
          <p>Company Profile Design</p>
        </div>
      </div>
      <div class="portfolio-item reveal">
        <div class="portfolio-placeholder">
          <span class="p-icon">👶</span>
          <span class="p-label">Haven Baby Care</span>
        </div>
        <div class="portfolio-overlay">
          <h4>Haven Baby Care</h4>
          <p>Social Media & Branding</p>
        </div>
      </div>
      <div class="portfolio-item reveal">
        <div class="portfolio-placeholder">
          <span class="p-icon">🛋️</span>
          <span class="p-label">Diva Furnishings</span>
        </div>
        <div class="portfolio-overlay">
          <h4>Diva Furnishings</h4>
          <p>Logo & Brand Identity</p>
        </div>
      </div>
      <div class="portfolio-item reveal">
        <div class="portfolio-placeholder">
          <span class="p-icon">☕</span>
          <span class="p-label">Coffee Shop Branding</span>
        </div>
        <div class="portfolio-overlay">
          <h4>Coffee Shop Branding</h4>
          <p>Full Brand Kit</p>
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
      <p class="section-label">Let's Talk</p>
      <h2 class="section-title">Get In Touch</h2>
      <div class="section-divider"></div>
    </div>
    <div class="contact-inner">
      <div class="contact-info reveal">
        <p>Available for freelance projects, full-time opportunities, and creative collaborations. Based in Cairo — open to relocation especially to Saudi Arabia.</p>
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
          <label>Your Name</label>
          <input type="text" placeholder="John Doe" />
        </div>
        <div class="form-group">
          <label>Email Address</label>
          <input type="email" placeholder="john@example.com" />
        </div>
        <div class="form-group">
          <label>Subject</label>
          <input type="text" placeholder="Project Inquiry" />
        </div>
        <div class="form-group">
          <label>Message</label>
          <textarea placeholder="Tell me about your project..."></textarea>
        </div>
        <a href="mailto:mbarakat960@gmail.com" class="btn-primary" style="text-align:center;">Send Message</a>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <p>© 2026 Mohamed Barakat. All rights reserved.</p>
    <div class="footer-socials">
      <a href="https://www.behance.net/mbarakat960b56" target="_blank">Behance</a>
      <a href="https://www.instagram.com/designedby.bd" target="_blank">Instagram</a>
      <a href="https://www.linkedin.com/in/mohammedbarakat1/" target="_blank">LinkedIn</a>
    </div>
  </footer>

  <script>
    // Scroll Reveal
    const reveals = document.querySelectorAll('.reveal');
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry, i) => {
        if (entry.isIntersecting) {
          setTimeout(() => entry.target.classList.add('visible'), i * 80);
        }
      });
    }, { threshold: 0.1 });
    reveals.forEach(el => observer.observe(el));
  </script>

</body>
</html>
