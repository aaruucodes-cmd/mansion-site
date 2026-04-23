<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Maison Élite | Luxury Furniture & Living Spaces</title>
<meta name="description" content="Maison Élite — Premium luxury furniture showroom crafting bespoke living spaces. Custom furniture design, interior consultation, and premium installation services.">
<meta name="keywords" content="luxury furniture, premium furniture, custom furniture design, interior consultation, bespoke furniture">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=Jost:wght@200;300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --gold: #C9A84C;
    --gold-light: #E8CC8A;
    --gold-dark: #8B6914;
    --black: #0A0A0A;
    --dark: #111111;
    --dark-2: #1A1A1A;
    --dark-3: #252525;
    --dark-4: #2E2E2E;
    --white: #FAFAF8;
    --white-dim: rgba(250,250,248,0.85);
    --white-faint: rgba(250,250,248,0.06);
    --glass: rgba(255,255,255,0.04);
    --glass-border: rgba(201,168,76,0.2);
    --text-muted: rgba(250,250,248,0.45);
    --text-secondary: rgba(250,250,248,0.7);
    --section-pad: clamp(80px, 10vw, 140px);
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; font-size: 16px; }

  body {
    background: var(--black);
    color: var(--white);
    font-family: 'Jost', sans-serif;
    font-weight: 300;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom Cursor */
  .cursor {
    position: fixed;
    width: 8px; height: 8px;
    background: var(--gold);
    border-radius: 50%;
    pointer-events: none;
    z-index: 99999;
    transform: translate(-50%, -50%);
    transition: width 0.3s, height 0.3s, background 0.3s;
    mix-blend-mode: difference;
  }
  .cursor-follower {
    position: fixed;
    width: 36px; height: 36px;
    border: 1px solid rgba(201,168,76,0.5);
    border-radius: 50%;
    pointer-events: none;
    z-index: 99998;
    transform: translate(-50%, -50%);
    transition: transform 0.12s ease-out, width 0.3s, height 0.3s;
  }
  body:hover .cursor-follower { }

  /* Loader */
  #loader {
    position: fixed; inset: 0;
    background: var(--black);
    z-index: 99990;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 32px;
    transition: opacity 0.8s ease, visibility 0.8s ease;
  }
  #loader.hidden { opacity: 0; visibility: hidden; }
  .loader-brand {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(28px, 4vw, 44px);
    font-weight: 300;
    letter-spacing: 0.25em;
    color: var(--white);
  }
  .loader-brand span { color: var(--gold); }
  .loader-bar-wrap {
    width: 200px; height: 1px;
    background: rgba(255,255,255,0.1);
    position: relative; overflow: hidden;
  }
  .loader-bar {
    position: absolute; left: -100%; top: 0;
    width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, var(--gold), transparent);
    animation: loaderSlide 1.6s ease-in-out forwards;
  }
  @keyframes loaderSlide { to { left: 100%; } }
  .loader-pct {
    font-size: 11px; letter-spacing: 0.3em;
    color: var(--text-muted); font-weight: 400;
  }

  /* Navbar */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 1000;
    padding: 0 clamp(24px, 5vw, 80px);
    height: 80px;
    display: flex; align-items: center; justify-content: space-between;
    transition: background 0.4s ease, backdrop-filter 0.4s ease, border-bottom 0.4s;
  }
  nav.scrolled {
    background: rgba(10,10,10,0.85);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--glass-border);
  }
  .nav-logo {
    font-family: 'Cormorant Garamond', serif;
    font-size: 22px; font-weight: 400;
    letter-spacing: 0.15em; color: var(--white);
    text-decoration: none;
  }
  .nav-logo span { color: var(--gold); }
  .nav-links {
    display: flex; gap: 40px; list-style: none;
  }
  .nav-links a {
    font-size: 11px; letter-spacing: 0.2em;
    text-transform: uppercase; color: var(--text-secondary);
    text-decoration: none; font-weight: 400;
    transition: color 0.3s;
    position: relative;
  }
  .nav-links a::after {
    content: ''; position: absolute;
    bottom: -4px; left: 0; right: 100%;
    height: 1px; background: var(--gold);
    transition: right 0.3s ease;
  }
  .nav-links a:hover { color: var(--white); }
  .nav-links a:hover::after { right: 0; }
  .nav-cta {
    font-size: 11px; letter-spacing: 0.2em;
    text-transform: uppercase; font-weight: 400;
    padding: 10px 24px;
    border: 1px solid var(--gold);
    color: var(--gold);
    text-decoration: none;
    transition: background 0.3s, color 0.3s;
  }
  .nav-cta:hover { background: var(--gold); color: var(--black); }
  .nav-hamburger { display: none; flex-direction: column; gap: 5px; cursor: pointer; }
  .nav-hamburger span { width: 24px; height: 1px; background: var(--white); display: block; transition: all 0.3s; }

  /* Hero */
  #hero {
    position: relative;
    height: 100vh; min-height: 700px;
    display: flex; align-items: center; justify-content: center;
    overflow: hidden;
  }
  .hero-bg {
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse 80% 60% at 70% 50%, rgba(201,168,76,0.07) 0%, transparent 60%),
      radial-gradient(ellipse 50% 80% at 20% 80%, rgba(201,168,76,0.04) 0%, transparent 50%),
      linear-gradient(180deg, #0a0a0a 0%, #111111 50%, #0a0a0a 100%);
  }
  .hero-grid-overlay {
    position: absolute; inset: 0;
    background-image:
      linear-gradient(rgba(201,168,76,0.05) 1px, transparent 1px),
      linear-gradient(90deg, rgba(201,168,76,0.05) 1px, transparent 1px);
    background-size: 80px 80px;
    mask-image: radial-gradient(ellipse 80% 80% at center, black 30%, transparent 80%);
  }
  .hero-3d-shape {
    position: absolute; right: 5%; top: 50%;
    transform: translateY(-50%);
    width: clamp(320px, 45vw, 680px);
    height: clamp(320px, 45vw, 680px);
    opacity: 0.9;
  }
  .hero-content {
    position: relative; z-index: 2;
    text-align: center;
    max-width: 900px;
    padding: 0 clamp(24px, 5vw, 60px);
    opacity: 0; transform: translateY(40px);
    animation: heroReveal 1.2s ease 1.8s forwards;
  }
  @keyframes heroReveal { to { opacity: 1; transform: translateY(0); } }
  .hero-eyebrow {
    display: inline-flex; align-items: center; gap: 16px;
    font-size: 10px; letter-spacing: 0.4em;
    text-transform: uppercase; color: var(--gold);
    font-weight: 400; margin-bottom: 32px;
  }
  .hero-eyebrow::before, .hero-eyebrow::after {
    content: ''; width: 40px; height: 1px; background: var(--gold); opacity: 0.5;
  }
  .hero-headline {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(44px, 7vw, 92px);
    font-weight: 300; line-height: 1.05;
    letter-spacing: -0.01em;
    margin-bottom: 28px;
  }
  .hero-headline em { font-style: italic; color: var(--gold); }
  .hero-sub {
    font-size: clamp(13px, 1.5vw, 16px);
    color: var(--text-secondary);
    letter-spacing: 0.05em; line-height: 1.8;
    max-width: 500px; margin: 0 auto 48px;
    font-weight: 300;
  }
  .hero-btns { display: flex; gap: 16px; justify-content: center; flex-wrap: wrap; }
  .btn-primary {
    padding: 16px 40px;
    background: var(--gold);
    color: var(--black);
    font-size: 11px; letter-spacing: 0.25em;
    text-transform: uppercase; font-weight: 500;
    text-decoration: none; border: none; cursor: pointer;
    transition: background 0.3s, transform 0.2s;
  }
  .btn-primary:hover { background: var(--gold-light); transform: translateY(-2px); }
  .btn-ghost {
    padding: 15px 40px;
    border: 1px solid rgba(201,168,76,0.4);
    color: var(--white);
    font-size: 11px; letter-spacing: 0.25em;
    text-transform: uppercase; font-weight: 400;
    text-decoration: none; cursor: pointer;
    background: transparent;
    transition: border-color 0.3s, color 0.3s, transform 0.2s;
  }
  .btn-ghost:hover { border-color: var(--gold); color: var(--gold); transform: translateY(-2px); }
  .hero-scroll {
    position: absolute; bottom: 40px; left: 50%;
    transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    font-size: 9px; letter-spacing: 0.4em;
    text-transform: uppercase; color: var(--text-muted);
    animation: heroReveal 1s ease 2.5s both;
  }
  .hero-scroll-line {
    width: 1px; height: 50px;
    background: linear-gradient(to bottom, var(--gold), transparent);
    animation: scrollPulse 2s ease-in-out infinite;
  }
  @keyframes scrollPulse { 0%,100%{opacity:0.4;transform:scaleY(1)} 50%{opacity:1;transform:scaleY(0.6)} }
  .hero-stats {
    position: absolute; bottom: 50px; right: clamp(24px, 5vw, 80px);
    display: flex; gap: 48px;
    animation: heroReveal 1s ease 2.2s both;
  }
  .hero-stat-item { text-align: center; }
  .hero-stat-num {
    font-family: 'Cormorant Garamond', serif;
    font-size: 32px; font-weight: 400; color: var(--white);
    line-height: 1;
  }
  .hero-stat-num span { color: var(--gold); font-size: 20px; }
  .hero-stat-label {
    font-size: 9px; letter-spacing: 0.3em;
    text-transform: uppercase; color: var(--text-muted);
    margin-top: 4px;
  }

  /* Section Shared */
  section { padding: var(--section-pad) clamp(24px, 5vw, 80px); }
  .section-eyebrow {
    display: inline-flex; align-items: center; gap: 12px;
    font-size: 10px; letter-spacing: 0.4em;
    text-transform: uppercase; color: var(--gold);
    font-weight: 400; margin-bottom: 20px;
  }
  .section-eyebrow::before {
    content: ''; width: 30px; height: 1px; background: var(--gold);
  }
  .section-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(36px, 5vw, 62px);
    font-weight: 300; line-height: 1.1;
    margin-bottom: 24px;
  }
  .section-title em { font-style: italic; color: var(--gold); }
  .reveal {
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }
  .reveal-delay-4 { transition-delay: 0.4s; }
  .reveal-delay-5 { transition-delay: 0.5s; }

  /* About */
  #about {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: clamp(40px, 6vw, 100px);
    align-items: center;
    background: var(--dark);
  }
  .about-visual {
    position: relative;
    aspect-ratio: 4/5;
  }
  .about-img-main {
    width: 100%; height: 100%;
    background: var(--dark-2);
    position: relative; overflow: hidden;
  }
  .about-img-inner {
    width: 100%; height: 100%;
    background:
      linear-gradient(135deg, #1a1a1a 0%, #252525 50%, #1e1e1e 100%);
    display: flex; align-items: center; justify-content: center;
  }
  .about-3d-sofa { width: 80%; max-width: 380px; }
  .about-badge {
    position: absolute; bottom: -24px; right: -24px;
    width: 130px; height: 130px;
    background: var(--gold);
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
  }
  .about-badge-num {
    font-family: 'Cormorant Garamond', serif;
    font-size: 44px; font-weight: 400; color: var(--black);
    line-height: 1;
  }
  .about-badge-label {
    font-size: 9px; letter-spacing: 0.25em;
    text-transform: uppercase; color: var(--black);
    opacity: 0.7; font-weight: 500;
  }
  .about-tag {
    position: absolute; top: 24px; left: -16px;
    background: rgba(10,10,10,0.95);
    border: 1px solid var(--glass-border);
    backdrop-filter: blur(20px);
    padding: 14px 20px;
    font-size: 11px; color: var(--gold);
    letter-spacing: 0.15em; text-transform: uppercase;
  }
  .about-content p {
    color: var(--text-secondary);
    line-height: 1.9; font-size: 15px;
    margin-bottom: 20px; font-weight: 300;
  }
  .about-features {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 20px; margin: 40px 0;
  }
  .about-feature {
    padding: 20px;
    border: 1px solid var(--glass-border);
    background: var(--glass);
    position: relative; overflow: hidden;
    transition: border-color 0.3s, background 0.3s;
  }
  .about-feature::before {
    content: ''; position: absolute;
    top: 0; left: 0; right: 100%; height: 2px;
    background: var(--gold);
    transition: right 0.4s ease;
  }
  .about-feature:hover { border-color: rgba(201,168,76,0.4); background: rgba(201,168,76,0.03); }
  .about-feature:hover::before { right: 0; }
  .about-feature-icon {
    width: 36px; height: 36px;
    margin-bottom: 12px; color: var(--gold);
  }
  .about-feature h4 {
    font-size: 12px; letter-spacing: 0.2em;
    text-transform: uppercase; font-weight: 500;
    margin-bottom: 6px;
  }
  .about-feature p {
    font-size: 12px; color: var(--text-muted);
    line-height: 1.6; margin: 0;
  }

  /* Collections */
  #collections { background: var(--black); }
  .collections-header {
    display: flex; align-items: flex-end;
    justify-content: space-between;
    margin-bottom: clamp(40px, 6vw, 72px);
    flex-wrap: wrap; gap: 20px;
  }
  .collections-desc {
    max-width: 360px;
    color: var(--text-secondary); font-size: 15px;
    line-height: 1.8; font-weight: 300;
  }
  .collections-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: auto auto;
    gap: 2px;
  }
  .collection-card {
    position: relative; overflow: hidden;
    aspect-ratio: 4/5; background: var(--dark-2);
    cursor: pointer;
    transition: transform 0.4s ease;
  }
  .collection-card:first-child {
    grid-column: span 2; aspect-ratio: unset; min-height: 560px;
  }
  .collection-card:nth-child(5) { grid-column: span 2; }
  .collection-card-bg {
    position: absolute; inset: 0;
    transition: transform 0.6s ease;
  }
  .collection-card:hover .collection-card-bg { transform: scale(1.04); }
  .card-inner {
    width: 100%; height: 100%;
    display: flex; align-items: center; justify-content: center;
    position: relative;
  }
  .cc-1 { background: linear-gradient(135deg, #181818, #242424); }
  .cc-2 { background: linear-gradient(135deg, #1c1c1c, #282828); }
  .cc-3 { background: linear-gradient(135deg, #151515, #202020); }
  .cc-4 { background: linear-gradient(135deg, #1e1e1e, #2a2a2a); }
  .cc-5 { background: linear-gradient(135deg, #191919, #252525); }
  .collection-card-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0.2) 50%, transparent 100%);
    transition: background 0.4s;
  }
  .collection-card:hover .collection-card-overlay {
    background: linear-gradient(to top, rgba(0,0,0,0.95) 0%, rgba(0,0,0,0.4) 60%, transparent 100%);
  }
  .collection-card-info {
    position: absolute; bottom: 0; left: 0; right: 0;
    padding: 32px;
    transform: translateY(20px);
    transition: transform 0.4s ease;
  }
  .collection-card:hover .collection-card-info { transform: translateY(0); }
  .collection-tag {
    font-size: 9px; letter-spacing: 0.35em;
    text-transform: uppercase; color: var(--gold);
    font-weight: 400; margin-bottom: 8px; display: block;
  }
  .collection-name {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(24px, 3vw, 36px); font-weight: 300;
    line-height: 1.1; margin-bottom: 12px;
  }
  .collection-desc {
    font-size: 13px; color: var(--text-secondary);
    line-height: 1.7; max-width: 400px;
    opacity: 0; transform: translateY(10px);
    transition: opacity 0.4s 0.1s, transform 0.4s 0.1s;
  }
  .collection-card:hover .collection-desc { opacity: 1; transform: translateY(0); }
  .collection-link {
    display: inline-flex; align-items: center; gap: 10px;
    font-size: 10px; letter-spacing: 0.25em;
    text-transform: uppercase; color: var(--gold);
    font-weight: 400; margin-top: 16px;
    opacity: 0; transform: translateY(10px);
    transition: opacity 0.4s 0.15s, transform 0.4s 0.15s;
  }
  .collection-card:hover .collection-link { opacity: 1; transform: translateY(0); }
  .collection-link::after { content: '→'; transition: margin 0.3s; }
  .collection-link:hover::after { margin-left: 6px; }

  /* Services */
  #services {
    background: var(--dark);
    position: relative; overflow: hidden;
  }
  .services-bg-accent {
    position: absolute; top: -50%; right: -20%;
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(201,168,76,0.04) 0%, transparent 70%);
    pointer-events: none;
  }
  .services-layout {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: clamp(40px, 6vw, 100px);
    align-items: start;
  }
  .services-intro p {
    color: var(--text-secondary); font-size: 15px;
    line-height: 1.9; font-weight: 300; margin-top: 24px;
  }
  .services-grid {
    display: flex; flex-direction: column; gap: 2px;
  }
  .service-item {
    display: flex; align-items: flex-start; gap: 24px;
    padding: 28px 32px;
    border: 1px solid transparent;
    background: var(--glass);
    transition: border-color 0.3s, background 0.3s;
    cursor: pointer;
  }
  .service-item:hover {
    border-color: var(--glass-border);
    background: rgba(201,168,76,0.03);
  }
  .service-num {
    font-family: 'Cormorant Garamond', serif;
    font-size: 13px; color: var(--gold);
    opacity: 0.6; min-width: 28px; font-weight: 400;
    padding-top: 3px;
  }
  .service-content h3 {
    font-size: 14px; letter-spacing: 0.1em;
    text-transform: uppercase; font-weight: 400;
    margin-bottom: 8px; color: var(--white);
  }
  .service-content p {
    font-size: 13px; color: var(--text-muted);
    line-height: 1.7; font-weight: 300;
  }
  .service-icon {
    width: 40px; height: 40px; color: var(--gold);
    opacity: 0.7; flex-shrink: 0; transition: opacity 0.3s;
  }
  .service-item:hover .service-icon { opacity: 1; }

  /* Testimonials */
  #testimonials { background: var(--black); }
  .testimonials-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 24px; margin-top: clamp(40px, 5vw, 64px);
  }
  .testimonial-card {
    padding: 36px;
    background: var(--dark-2);
    border: 1px solid rgba(255,255,255,0.06);
    position: relative; overflow: hidden;
    transition: border-color 0.3s, transform 0.3s;
  }
  .testimonial-card::before {
    content: '\201C';
    position: absolute; top: 20px; right: 28px;
    font-family: 'Cormorant Garamond', serif;
    font-size: 100px; font-weight: 300;
    color: var(--gold); opacity: 0.12; line-height: 1;
  }
  .testimonial-card:hover {
    border-color: var(--glass-border);
    transform: translateY(-4px);
  }
  .testimonial-stars {
    display: flex; gap: 4px; margin-bottom: 20px;
  }
  .star { color: var(--gold); font-size: 14px; }
  .testimonial-text {
    font-family: 'Cormorant Garamond', serif;
    font-size: 18px; font-weight: 300;
    line-height: 1.7; color: var(--white-dim);
    font-style: italic; margin-bottom: 28px;
  }
  .testimonial-author { display: flex; align-items: center; gap: 14px; }
  .testimonial-avatar {
    width: 44px; height: 44px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-family: 'Cormorant Garamond', serif;
    font-size: 16px; font-weight: 400;
    background: var(--dark-4); border: 1px solid var(--glass-border);
    color: var(--gold);
  }
  .testimonial-name {
    font-size: 13px; font-weight: 400; letter-spacing: 0.05em;
  }
  .testimonial-role {
    font-size: 11px; color: var(--text-muted);
    letter-spacing: 0.1em; margin-top: 2px;
  }

  /* Gallery */
  #gallery { background: var(--dark); }
  .gallery-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(2, 280px);
    gap: 4px; margin-top: clamp(40px, 5vw, 64px);
  }
  .gallery-item {
    position: relative; overflow: hidden;
    background: var(--dark-2); cursor: pointer;
  }
  .gallery-item:first-child { grid-row: span 2; grid-column: span 2; }
  .gallery-item:nth-child(4) { grid-row: span 2; }
  .gallery-inner {
    width: 100%; height: 100%;
    transition: transform 0.6s ease;
    display: flex; align-items: center; justify-content: center;
  }
  .gallery-item:hover .gallery-inner { transform: scale(1.06); }
  .gallery-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(0,0,0,0.6), rgba(0,0,0,0.2));
    opacity: 0;
    transition: opacity 0.3s;
    display: flex; align-items: center; justify-content: center;
  }
  .gallery-item:hover .gallery-overlay { opacity: 1; }
  .gallery-overlay-icon {
    width: 48px; height: 48px;
    border: 1px solid rgba(201,168,76,0.7);
    display: flex; align-items: center; justify-content: center;
    color: var(--gold); font-size: 20px;
    transform: scale(0.7); transition: transform 0.3s;
  }
  .gallery-item:hover .gallery-overlay-icon { transform: scale(1); }
  .g1 { background: linear-gradient(135deg, #1d1612, #2a221a); }
  .g2 { background: linear-gradient(135deg, #121215, #1e1e22); }
  .g3 { background: linear-gradient(135deg, #141a14, #1e261e); }
  .g4 { background: linear-gradient(135deg, #1a1612, #28221a); }
  .g5 { background: linear-gradient(135deg, #141414, #222222); }
  .g6 { background: linear-gradient(135deg, #161612, #22221a); }

  /* Contact */
  #contact { background: var(--black); }
  .contact-layout {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: clamp(40px, 6vw, 100px);
  }
  .contact-info p {
    color: var(--text-secondary); font-size: 15px;
    line-height: 1.9; font-weight: 300; margin: 24px 0 40px;
  }
  .contact-details { display: flex; flex-direction: column; gap: 20px; }
  .contact-detail {
    display: flex; align-items: center; gap: 16px;
    padding: 18px 20px;
    border: 1px solid rgba(255,255,255,0.06);
    background: var(--white-faint);
    transition: border-color 0.3s;
  }
  .contact-detail:hover { border-color: var(--glass-border); }
  .contact-detail-icon { color: var(--gold); width: 20px; height: 20px; flex-shrink: 0; }
  .contact-detail-text { font-size: 13px; color: var(--text-secondary); line-height: 1.5; }
  .contact-detail-label {
    font-size: 9px; letter-spacing: 0.3em;
    text-transform: uppercase; color: var(--gold);
    font-weight: 400; display: block; margin-bottom: 2px;
  }
  .map-container {
    margin-top: 24px; height: 180px; overflow: hidden;
    border: 1px solid var(--glass-border); position: relative;
  }
  .map-container iframe {
    width: 100%; height: 100%; border: none; filter: invert(0.9) hue-rotate(180deg) brightness(0.85) contrast(1.1);
  }
  .contact-form { display: flex; flex-direction: column; gap: 16px; }
  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .form-group { display: flex; flex-direction: column; gap: 8px; }
  .form-group label {
    font-size: 10px; letter-spacing: 0.3em;
    text-transform: uppercase; color: var(--text-muted); font-weight: 400;
  }
  .form-group input, .form-group select, .form-group textarea {
    background: var(--dark-2);
    border: 1px solid rgba(255,255,255,0.08);
    color: var(--white); font-family: 'Jost', sans-serif;
    font-size: 14px; font-weight: 300;
    padding: 14px 18px;
    outline: none; transition: border-color 0.3s;
    appearance: none; -webkit-appearance: none;
    resize: none;
  }
  .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
    border-color: var(--gold);
  }
  .form-group input::placeholder, .form-group textarea::placeholder { color: rgba(250,250,248,0.2); }
  .form-group select { color: var(--text-secondary); }
  .form-group select option { background: var(--dark-2); }

  /* Footer */
  footer {
    background: var(--dark);
    border-top: 1px solid var(--glass-border);
    padding: 60px clamp(24px, 5vw, 80px) 32px;
  }
  .footer-grid {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr;
    gap: 60px; margin-bottom: 60px;
  }
  .footer-brand-desc {
    font-size: 13px; color: var(--text-muted);
    line-height: 1.8; margin: 16px 0 24px; max-width: 280px;
  }
  .footer-social { display: flex; gap: 12px; }
  .footer-social a {
    width: 36px; height: 36px;
    border: 1px solid rgba(255,255,255,0.1);
    display: flex; align-items: center; justify-content: center;
    color: var(--text-muted); text-decoration: none; font-size: 12px;
    transition: border-color 0.3s, color 0.3s;
  }
  .footer-social a:hover { border-color: var(--gold); color: var(--gold); }
  .footer-col h4 {
    font-size: 10px; letter-spacing: 0.3em;
    text-transform: uppercase; color: var(--gold);
    font-weight: 400; margin-bottom: 20px;
  }
  .footer-col ul { list-style: none; display: flex; flex-direction: column; gap: 10px; }
  .footer-col ul li a {
    font-size: 13px; color: var(--text-muted);
    text-decoration: none; font-weight: 300;
    transition: color 0.3s;
  }
  .footer-col ul li a:hover { color: var(--white); }
  .footer-bottom {
    border-top: 1px solid rgba(255,255,255,0.06);
    padding-top: 28px;
    display: flex; align-items: center; justify-content: space-between;
    flex-wrap: wrap; gap: 12px;
  }
  .footer-bottom p { font-size: 12px; color: var(--text-muted); }
  .footer-bottom a { color: var(--gold); text-decoration: none; }

  /* WhatsApp Float */
  .whatsapp-float {
    position: fixed; bottom: 32px; right: 32px;
    width: 56px; height: 56px;
    background: #25D366;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    z-index: 990; text-decoration: none;
    box-shadow: 0 4px 24px rgba(37,211,102,0.3);
    transition: transform 0.3s, box-shadow 0.3s;
    animation: waFloat 3s ease-in-out infinite;
  }
  .whatsapp-float:hover {
    transform: scale(1.1);
    box-shadow: 0 8px 32px rgba(37,211,102,0.45);
  }
  @keyframes waFloat { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-6px)} }
  .whatsapp-float svg { width: 28px; height: 28px; fill: white; }
  .wa-tooltip {
    position: absolute; right: 68px; top: 50%;
    transform: translateY(-50%);
    background: var(--dark-2); color: var(--white);
    font-size: 12px; letter-spacing: 0.05em;
    white-space: nowrap; padding: 8px 16px;
    opacity: 0; transition: opacity 0.3s;
    border: 1px solid var(--glass-border);
    pointer-events: none;
  }
  .whatsapp-float:hover .wa-tooltip { opacity: 1; }

  /* Divider */
  .gold-divider {
    width: 60px; height: 1px; background: var(--gold); opacity: 0.6;
    margin: 24px 0;
  }

  /* Marquee strip */
  .marquee-strip {
    background: var(--gold);
    overflow: hidden; white-space: nowrap;
    padding: 14px 0;
  }
  .marquee-track {
    display: inline-flex; gap: 0;
    animation: marquee 25s linear infinite;
  }
  .marquee-item {
    display: inline-flex; align-items: center; gap: 32px;
    padding: 0 32px;
    font-size: 11px; letter-spacing: 0.25em;
    text-transform: uppercase; font-weight: 500;
    color: var(--black);
  }
  .marquee-dot { width: 4px; height: 4px; background: rgba(0,0,0,0.4); border-radius: 50%; }
  @keyframes marquee { to { transform: translateX(-50%); } }

  /* Mobile Menu */
  .mobile-menu {
    position: fixed; inset: 0; z-index: 999;
    background: rgba(10,10,10,0.98);
    backdrop-filter: blur(20px);
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    gap: 32px;
    transform: translateX(100%);
    transition: transform 0.4s ease;
  }
  .mobile-menu.open { transform: translateX(0); }
  .mobile-menu a {
    font-family: 'Cormorant Garamond', serif;
    font-size: 32px; font-weight: 300;
    color: var(--white); text-decoration: none;
    letter-spacing: 0.05em; text-align: center;
    transition: color 0.3s;
  }
  .mobile-menu a:hover { color: var(--gold); }
  .mobile-close {
    position: absolute; top: 28px; right: 28px;
    background: none; border: none; cursor: pointer;
    color: var(--white); font-size: 28px; line-height: 1;
  }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--black); }
  ::-webkit-scrollbar-thumb { background: var(--gold-dark); }
  ::-webkit-scrollbar-thumb:hover { background: var(--gold); }

  /* Responsive */
  @media (max-width: 1024px) {
    .collections-grid { grid-template-columns: repeat(2, 1fr); }
    .collection-card:first-child { grid-column: span 2; min-height: 420px; }
    .collection-card:nth-child(5) { grid-column: span 1; }
    .footer-grid { grid-template-columns: 1fr 1fr; }
  }
  @media (max-width: 768px) {
    body { cursor: auto; }
    .cursor, .cursor-follower { display: none; }
    nav { padding: 0 20px; }
    .nav-links, .nav-cta { display: none; }
    .nav-hamburger { display: flex; }
    #about { grid-template-columns: 1fr; }
    .about-visual { aspect-ratio: 4/3; max-height: 320px; }
    .about-badge { width: 90px; height: 90px; bottom: -16px; right: -8px; }
    .about-badge-num { font-size: 30px; }
    .services-layout { grid-template-columns: 1fr; }
    .testimonials-grid { grid-template-columns: 1fr; }
    .gallery-grid { grid-template-columns: 1fr 1fr; grid-template-rows: auto; }
    .gallery-item:first-child { grid-row: span 1; grid-column: span 2; min-height: 220px; }
    .gallery-item:nth-child(4) { grid-row: span 1; }
    .contact-layout { grid-template-columns: 1fr; }
    .form-row { grid-template-columns: 1fr; }
    .footer-grid { grid-template-columns: 1fr 1fr; gap: 32px; }
    .hero-stats { display: none; }
    .collections-grid { grid-template-columns: 1fr; }
    .collection-card:first-child, .collection-card:nth-child(5) { grid-column: span 1; }
    .about-features { grid-template-columns: 1fr; }
  }
  @media (max-width: 480px) {
    .footer-grid { grid-template-columns: 1fr; }
    .whatsapp-float { bottom: 20px; right: 20px; }
  }
</style>
</head>
<body>

<!-- Custom Cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-follower" id="cursorFollower"></div>

<!-- Loader -->
<div id="loader">
  <div class="loader-brand">MAISON <span>ÉLITE</span></div>
  <div class="loader-bar-wrap"><div class="loader-bar"></div></div>
  <div class="loader-pct" id="loaderPct">Loading…</div>
</div>

<!-- Mobile Menu -->
<div class="mobile-menu" id="mobileMenu">
  <button class="mobile-close" id="mobileClose">×</button>
  <a href="#hero" onclick="closeMobile()">Home</a>
  <a href="#about" onclick="closeMobile()">About</a>
  <a href="#collections" onclick="closeMobile()">Collections</a>
  <a href="#services" onclick="closeMobile()">Services</a>
  <a href="#gallery" onclick="closeMobile()">Gallery</a>
  <a href="#contact" onclick="closeMobile()">Contact</a>
</div>

<!-- Navbar -->
<nav id="navbar">
  <a href="#hero" class="nav-logo">MAISON <span>ÉLITE</span></a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#collections">Collections</a></li>
    <li><a href="#services">Services</a></li>
    <li><a href="#gallery">Gallery</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <a href="#contact" class="nav-cta">Book Consultation</a>
  <div class="nav-hamburger" id="hamburger" onclick="openMobile()">
    <span></span><span></span><span></span>
  </div>
</nav>

<!-- Hero -->
<section id="hero">
  <div class="hero-bg"></div>
  <div class="hero-grid-overlay"></div>

  <!-- 3D SVG Furniture Visual -->
  <div class="hero-3d-shape">
    <svg viewBox="0 0 600 600" xmlns="http://www.w3.org/2000/svg" style="width:100%;height:100%;opacity:0;animation:heroReveal 1.5s ease 1.5s forwards">
      <defs>
        <radialGradient id="roomGlow" cx="50%" cy="60%" r="50%">
          <stop offset="0%" stop-color="#C9A84C" stop-opacity="0.12"/>
          <stop offset="100%" stop-color="#C9A84C" stop-opacity="0"/>
        </radialGradient>
        <linearGradient id="floorGrad" x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%" stop-color="#1C1A14"/>
          <stop offset="100%" stop-color="#12100C"/>
        </linearGradient>
        <linearGradient id="wallGrad" x1="0%" y1="0%" x2="0%" y2="100%">
          <stop offset="0%" stop-color="#1A1A1A"/>
          <stop offset="100%" stop-color="#141414"/>
        </linearGradient>
        <linearGradient id="sofaBody" x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%" stop-color="#2E2620"/>
          <stop offset="100%" stop-color="#1E1A16"/>
        </linearGradient>
        <linearGradient id="sofaTop" x1="0%" y1="0%" x2="0%" y2="100%">
          <stop offset="0%" stop-color="#3A3028"/>
          <stop offset="100%" stop-color="#2A2218"/>
        </linearGradient>
        <linearGradient id="goldMetal" x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%" stop-color="#E8CC8A"/>
          <stop offset="50%" stop-color="#C9A84C"/>
          <stop offset="100%" stop-color="#8B6914"/>
        </linearGradient>
        <linearGradient id="tableTop" x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%" stop-color="#1E1A14"/>
          <stop offset="100%" stop-color="#2C2418"/>
        </linearGradient>
        <filter id="glow">
          <feGaussianBlur in="SourceGraphic" stdDeviation="3" result="blur"/>
          <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
        </filter>
        <linearGradient id="lampGlow" x1="50%" y1="0%" x2="50%" y2="100%">
          <stop offset="0%" stop-color="#C9A84C" stop-opacity="0.9"/>
          <stop offset="100%" stop-color="#C9A84C" stop-opacity="0.1"/>
        </linearGradient>
      </defs>

      <!-- Room glow -->
      <ellipse cx="300" cy="400" rx="280" ry="200" fill="url(#roomGlow)"/>

      <!-- Floor perspective -->
      <polygon points="60,420 540,420 480,580 120,580" fill="url(#floorGrad)"/>
      <!-- Floor lines -->
      <line x1="60" y1="420" x2="120" y2="580" stroke="#C9A84C" stroke-width="0.5" stroke-opacity="0.12"/>
      <line x1="180" y1="420" x2="210" y2="580" stroke="#C9A84C" stroke-width="0.5" stroke-opacity="0.12"/>
      <line x1="300" y1="420" x2="300" y2="580" stroke="#C9A84C" stroke-width="0.5" stroke-opacity="0.12"/>
      <line x1="420" y1="420" x2="390" y2="580" stroke="#C9A84C" stroke-width="0.5" stroke-opacity="0.12"/>
      <line x1="540" y1="420" x2="480" y2="580" stroke="#C9A84C" stroke-width="0.5" stroke-opacity="0.12"/>

      <!-- Back wall -->
      <rect x="60" y="120" width="480" height="300" fill="url(#wallGrad)"/>
      <!-- Wall panel lines -->
      <line x1="60" y1="200" x2="540" y2="200" stroke="#C9A84C" stroke-width="0.4" stroke-opacity="0.1"/>
      <line x1="200" y1="120" x2="200" y2="420" stroke="#C9A84C" stroke-width="0.4" stroke-opacity="0.1"/>
      <line x1="400" y1="120" x2="400" y2="420" stroke="#C9A84C" stroke-width="0.4" stroke-opacity="0.1"/>

      <!-- Artwork on wall -->
      <rect x="230" y="145" width="140" height="100" fill="#191919" stroke="#C9A84C" stroke-width="0.8" stroke-opacity="0.4"/>
      <rect x="242" y="155" width="116" height="80" fill="#141414"/>
      <line x1="242" y1="155" x2="358" y2="235" stroke="#C9A84C" stroke-width="0.5" stroke-opacity="0.25"/>
      <line x1="358" y1="155" x2="242" y2="235" stroke="#C9A84C" stroke-width="0.5" stroke-opacity="0.25"/>
      <circle cx="300" cy="195" r="25" fill="none" stroke="#C9A84C" stroke-width="0.8" stroke-opacity="0.3"/>

      <!-- Floor lamp -->
      <line x1="480" y1="420" x2="480" y2="240" stroke="#C9A84C" stroke-width="2" stroke-opacity="0.6"/>
      <polygon points="460,240 500,240 490,260 470,260" fill="url(#goldMetal)"/>
      <!-- Lamp light cone -->
      <polygon points="470,260 490,260 510,380 450,380" fill="url(#lampGlow)" opacity="0.3"/>
      <!-- Lamp base -->
      <ellipse cx="480" cy="420" rx="18" ry="6" fill="url(#goldMetal)" opacity="0.8"/>

      <!-- Sofa - main body -->
      <rect x="110" y="340" width="320" height="80" rx="4" fill="url(#sofaBody)"/>
      <!-- Sofa back -->
      <rect x="110" y="275" width="320" height="70" rx="4" fill="url(#sofaBody)"/>
      <!-- Sofa top rail -->
      <rect x="106" y="268" width="328" height="14" rx="3" fill="url(#sofaTop)"/>
      <!-- Sofa seat top -->
      <rect x="106" y="332" width="328" height="14" rx="2" fill="url(#sofaTop)"/>
      <!-- Sofa cushion divider -->
      <line x1="270" y1="275" x2="270" y2="345" stroke="#1A1512" stroke-width="2"/>
      <!-- Armrests -->
      <rect x="90" y="275" width="28" height="145" rx="4" fill="url(#sofaBody)"/>
      <rect x="422" y="275" width="28" height="145" rx="4" fill="url(#sofaBody)"/>
      <!-- Sofa legs (gold) -->
      <rect x="120" y="415" width="10" height="18" rx="2" fill="url(#goldMetal)"/>
      <rect x="200" y="415" width="10" height="18" rx="2" fill="url(#goldMetal)"/>
      <rect x="330" y="415" width="10" height="18" rx="2" fill="url(#goldMetal)"/>
      <rect x="410" y="415" width="10" height="18" rx="2" fill="url(#goldMetal)"/>
      <!-- Scatter pillows -->
      <rect x="118" y="286" width="100" height="52" rx="6" fill="#3A2E26" transform="rotate(-3,168,312)"/>
      <rect x="122" y="290" width="92" height="44" rx="5" fill="#2E2420" transform="rotate(-3,168,312)"/>
      <rect x="310" y="286" width="100" height="52" rx="6" fill="#26302A" transform="rotate(3,360,312)"/>
      <rect x="314" y="290" width="92" height="44" rx="5" fill="#1E2822" transform="rotate(3,360,312)"/>

      <!-- Coffee table -->
      <rect x="180" y="400" width="190" height="18" rx="2" fill="url(#tableTop)"/>
      <line x1="180" y1="400" x2="190" y2="418" stroke="#C9A84C" stroke-width="0.4" stroke-opacity="0.3"/>
      <line x1="370" y1="400" x2="360" y2="418" stroke="#C9A84C" stroke-width="0.4" stroke-opacity="0.3"/>
      <!-- Table edge highlight -->
      <rect x="180" y="400" width="190" height="3" rx="1" fill="#C9A84C" opacity="0.2"/>
      <!-- Table decoration -->
      <ellipse cx="275" cy="403" rx="30" ry="5" fill="#C9A84C" opacity="0.06"/>
      <!-- Vase on table -->
      <ellipse cx="275" cy="400" rx="12" ry="4" fill="#1A1814"/>
      <path d="M263,400 Q261,385 267,378 Q275,374 283,378 Q289,385 287,400" fill="#1A1814"/>
      <path d="M263,400 Q261,385 267,378 Q275,374 283,378" fill="none" stroke="#C9A84C" stroke-width="0.8" stroke-opacity="0.5"/>

      <!-- Gold accent lines decoration -->
      <line x1="60" y1="119" x2="540" y2="119" stroke="#C9A84C" stroke-width="1" stroke-opacity="0.25"/>
      <line x1="60" y1="420" x2="540" y2="420" stroke="#C9A84C" stroke-width="1" stroke-opacity="0.2"/>

      <!-- Subtle particles -->
      <circle cx="150" cy="200" r="1.5" fill="#C9A84C" opacity="0.3">
        <animate attributeName="opacity" values="0.3;0.8;0.3" dur="3s" repeatCount="indefinite"/>
      </circle>
      <circle cx="450" cy="180" r="1" fill="#C9A84C" opacity="0.4">
        <animate attributeName="opacity" values="0.4;0.9;0.4" dur="2s" repeatCount="indefinite"/>
      </circle>
      <circle cx="380" cy="310" r="1.5" fill="#C9A84C" opacity="0.2">
        <animate attributeName="opacity" values="0.2;0.6;0.2" dur="4s" repeatCount="indefinite"/>
      </circle>
    </svg>
  </div>

  <div class="hero-content">
    <div class="hero-eyebrow">Luxury Living Redefined</div>
    <h1 class="hero-headline">
      Crafting <em>Luxury</em><br>Living Spaces
    </h1>
    <p class="hero-sub">
      Where master craftsmanship meets timeless elegance. Every piece tells a story of uncompromising quality and bespoke artistry.
    </p>
    <div class="hero-btns">
      <a href="#collections" class="btn-primary">Explore Collection</a>
      <a href="#contact" class="btn-ghost">Book Consultation</a>
    </div>
  </div>

  <div class="hero-stats">
    <div class="hero-stat-item">
      <div class="hero-stat-num">15<span>+</span></div>
      <div class="hero-stat-label">Years Crafting</div>
    </div>
    <div class="hero-stat-item">
      <div class="hero-stat-num">2400<span>+</span></div>
      <div class="hero-stat-label">Happy Clients</div>
    </div>
    <div class="hero-stat-item">
      <div class="hero-stat-num">50<span>+</span></div>
      <div class="hero-stat-label">Bespoke Designs</div>
    </div>
  </div>

  <div class="hero-scroll">
    <div class="hero-scroll-line"></div>
    Scroll
  </div>
</section>

<!-- Marquee -->
<div class="marquee-strip">
  <div class="marquee-track">
    <span class="marquee-item">Bespoke Furniture <span class="marquee-dot"></span></span>
    <span class="marquee-item">Premium Craftsmanship <span class="marquee-dot"></span></span>
    <span class="marquee-item">Interior Consultation <span class="marquee-dot"></span></span>
    <span class="marquee-item">Custom Design <span class="marquee-dot"></span></span>
    <span class="marquee-item">Luxury Living <span class="marquee-dot"></span></span>
    <span class="marquee-item">Expert Installation <span class="marquee-dot"></span></span>
    <span class="marquee-item">Bespoke Furniture <span class="marquee-dot"></span></span>
    <span class="marquee-item">Premium Craftsmanship <span class="marquee-dot"></span></span>
    <span class="marquee-item">Interior Consultation <span class="marquee-dot"></span></span>
    <span class="marquee-item">Custom Design <span class="marquee-dot"></span></span>
    <span class="marquee-item">Luxury Living <span class="marquee-dot"></span></span>
    <span class="marquee-item">Expert Installation <span class="marquee-dot"></span></span>
  </div>
</div>

<!-- About -->
<section id="about">
  <div class="about-visual reveal">
    <div class="about-img-main">
      <div class="about-img-inner">
        <!-- Premium chair SVG -->
        <svg class="about-3d-sofa" viewBox="0 0 400 500" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <linearGradient id="chairBody" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="#2A2218"/>
              <stop offset="100%" stop-color="#1A150E"/>
            </linearGradient>
            <linearGradient id="chairBack" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="#332A1E"/>
              <stop offset="100%" stop-color="#1E170F"/>
            </linearGradient>
            <linearGradient id="chairGold" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="#E8CC8A"/>
              <stop offset="100%" stop-color="#8B6914"/>
            </linearGradient>
            <radialGradient id="chairGlow" cx="50%" cy="80%" r="40%">
              <stop offset="0%" stop-color="#C9A84C" stop-opacity="0.15"/>
              <stop offset="100%" stop-color="#C9A84C" stop-opacity="0"/>
            </radialGradient>
          </defs>
          <ellipse cx="200" cy="440" rx="160" ry="20" fill="url(#chairGlow)"/>
          <!-- Chair back -->
          <rect x="80" y="120" width="240" height="220" rx="12" fill="url(#chairBack)"/>
          <rect x="90" y="130" width="220" height="200" rx="8" fill="url(#chairBody)"/>
          <!-- Tufting pattern -->
          <circle cx="150" cy="200" r="4" fill="#C9A84C" opacity="0.3"/>
          <circle cx="200" cy="180" r="4" fill="#C9A84C" opacity="0.3"/>
          <circle cx="250" cy="200" r="4" fill="#C9A84C" opacity="0.3"/>
          <circle cx="175" cy="240" r="4" fill="#C9A84C" opacity="0.3"/>
          <circle cx="225" cy="240" r="4" fill="#C9A84C" opacity="0.3"/>
          <line x1="150" y1="200" x2="200" y2="180" stroke="#C9A84C" stroke-width="0.6" stroke-opacity="0.2"/>
          <line x1="200" y1="180" x2="250" y2="200" stroke="#C9A84C" stroke-width="0.6" stroke-opacity="0.2"/>
          <line x1="150" y1="200" x2="175" y2="240" stroke="#C9A84C" stroke-width="0.6" stroke-opacity="0.2"/>
          <line x1="250" y1="200" x2="225" y2="240" stroke="#C9A84C" stroke-width="0.6" stroke-opacity="0.2"/>
          <!-- Seat -->
          <rect x="60" y="320" width="280" height="60" rx="8" fill="url(#chairBack)"/>
          <rect x="70" y="325" width="260" height="50" rx="6" fill="url(#chairBody)"/>
          <!-- Seat front lip -->
          <rect x="60" y="372" width="280" height="12" rx="4" fill="#2E2418"/>
          <!-- Arms -->
          <rect x="50" y="200" width="36" height="150" rx="8" fill="url(#chairBack)"/>
          <rect x="314" y="200" width="36" height="150" rx="8" fill="url(#chairBack)"/>
          <!-- Arm caps -->
          <rect x="46" y="196" width="44" height="14" rx="4" fill="#3A2E20"/>
          <rect x="310" y="196" width="44" height="14" rx="4" fill="#3A2E20"/>
          <!-- Legs -->
          <path d="M90,384 Q85,420 80,440" stroke="url(#chairGold)" stroke-width="8" fill="none" stroke-linecap="round"/>
          <path d="M310,384 Q315,420 320,440" stroke="url(#chairGold)" stroke-width="8" fill="none" stroke-linecap="round"/>
          <path d="M100,384 Q95,430 90,450" stroke="url(#chairGold)" stroke-width="8" fill="none" stroke-linecap="round"/>
          <path d="M300,384 Q305,430 310,450" stroke="url(#chairGold)" stroke-width="8" fill="none" stroke-linecap="round"/>
          <!-- Leg feet -->
          <ellipse cx="80" cy="441" rx="8" ry="4" fill="#C9A84C" opacity="0.8"/>
          <ellipse cx="321" cy="441" rx="8" ry="4" fill="#C9A84C" opacity="0.8"/>
        </svg>
      </div>
    </div>
    <div class="about-badge">
      <div class="about-badge-num">15</div>
      <div class="about-badge-label">Years of<br>Excellence</div>
    </div>
    <div class="about-tag">Est. 2009 · Bhopal</div>
  </div>

  <div class="about-content">
    <div class="reveal">
      <div class="section-eyebrow">Our Story</div>
      <h2 class="section-title">Where Art Meets<br><em>Functionality</em></h2>
      <div class="gold-divider"></div>
    </div>
    <div class="reveal reveal-delay-1">
      <p>Maison Élite was born from a singular passion — to bring the world's finest furniture craftsmanship to discerning homes and businesses. For over 15 years, we have been the trusted name for those who refuse to compromise on quality.</p>
      <p>Every piece in our collection is a testament to the perfect union of traditional artisan techniques and contemporary design sensibility, sourced from the finest materials across the globe.</p>
    </div>
    <div class="about-features reveal reveal-delay-2">
      <div class="about-feature">
        <svg class="about-feature-icon" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M20 4L24 16H36L26 24L30 36L20 28L10 36L14 24L4 16H16L20 4Z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/>
        </svg>
        <h4>Premium Materials</h4>
        <p>Only the finest teak, walnut, and exotic veneers from sustainable sources.</p>
      </div>
      <div class="about-feature">
        <svg class="about-feature-icon" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="20" cy="20" r="14" stroke="currentColor" stroke-width="1.5"/>
          <path d="M13 20L17 24L27 14" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
        <h4>Lifetime Warranty</h4>
        <p>Every piece backed by our comprehensive lifetime craftsmanship guarantee.</p>
      </div>
      <div class="about-feature">
        <svg class="about-feature-icon" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect x="6" y="14" width="28" height="20" rx="2" stroke="currentColor" stroke-width="1.5"/>
          <path d="M14 14V10a6 6 0 0112 0v4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          <circle cx="20" cy="24" r="2" fill="currentColor"/>
        </svg>
        <h4>Bespoke Design</h4>
        <p>Every client receives a fully personalised design consultation experience.</p>
      </div>
      <div class="about-feature">
        <svg class="about-feature-icon" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M8 28C8 22 14 18 20 18C26 18 32 22 32 28" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          <circle cx="20" cy="12" r="5" stroke="currentColor" stroke-width="1.5"/>
          <path d="M20 18v10" stroke="currentColor" stroke-width="1" stroke-opacity="0.5"/>
        </svg>
        <h4>Expert Team</h4>
        <p>A dedicated team of master craftsmen and interior design specialists.</p>
      </div>
    </div>
    <div class="reveal reveal-delay-3">
      <a href="#contact" class="btn-primary">Discover Our Story</a>
    </div>
  </div>
</section>

<!-- Collections -->
<section id="collections">
  <div class="collections-header">
    <div>
      <div class="section-eyebrow reveal">Our Collections</div>
      <h2 class="section-title reveal reveal-delay-1">Curated for the<br><em>Discerning</em> Eye</h2>
    </div>
    <p class="collections-desc reveal reveal-delay-2">
      Five distinct collections, each a masterclass in design, comfort, and enduring craftsmanship. Explore the full range and find your signature piece.
    </p>
  </div>

  <div class="collections-grid">
    <!-- Sofa - large feature card -->
    <div class="collection-card reveal">
      <div class="collection-card-bg">
        <div class="card-inner cc-1">
          <svg viewBox="0 0 560 320" xmlns="http://www.w3.org/2000/svg" style="width:75%;max-width:440px;opacity:0.85">
            <defs>
              <linearGradient id="s1body" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#2E2620"/><stop offset="100%" stop-color="#1A1510"/>
              </linearGradient>
              <linearGradient id="s1gold" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#E8CC8A"/><stop offset="100%" stop-color="#8B6914"/>
              </linearGradient>
            </defs>
            <rect x="20" y="160" width="520" height="100" rx="8" fill="url(#s1body)"/>
            <rect x="20" y="95" width="520" height="72" rx="6" fill="#261E16"/>
            <rect x="16" y="88" width="528" height="14" rx="3" fill="#3A2C20"/>
            <rect x="16" y="152" width="528" height="14" rx="3" fill="#302418"/>
            <rect x="0" y="95" width="26" height="165" rx="6" fill="#261E16"/>
            <rect x="534" y="95" width="26" height="165" rx="6" fill="#261E16"/>
            <line x1="280" y1="95" x2="280" y2="165" stroke="#1A1310" stroke-width="2.5"/>
            <rect x="40" y="254" width="14" height="24" rx="3" fill="url(#s1gold)"/>
            <rect x="130" y="254" width="14" height="24" rx="3" fill="url(#s1gold)"/>
            <rect x="416" y="254" width="14" height="24" rx="3" fill="url(#s1gold)"/>
            <rect x="506" y="254" width="14" height="24" rx="3" fill="url(#s1gold)"/>
            <rect x="72" y="104" width="155" height="56" rx="8" fill="#2A2018" transform="rotate(-2,149,132)"/>
            <rect x="334" y="104" width="155" height="56" rx="8" fill="#2A2018" transform="rotate(2,411,132)"/>
          </svg>
        </div>
      </div>
      <div class="collection-card-overlay"></div>
      <div class="collection-card-info">
        <span class="collection-tag">Collection 01</span>
        <h3 class="collection-name">Living Room Sofas</h3>
        <p class="collection-desc">From classic Chesterfields to contemporary sectionals — each sofa is a statement of refined living, upholstered in the finest leathers and fabrics.</p>
        <a href="#contact" class="collection-link">Explore Collection</a>
      </div>
    </div>

    <!-- Dining -->
    <div class="collection-card reveal reveal-delay-1">
      <div class="collection-card-bg">
        <div class="card-inner cc-2">
          <svg viewBox="0 0 280 320" xmlns="http://www.w3.org/2000/svg" style="width:80%;opacity:0.85">
            <defs>
              <linearGradient id="tableW" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#1C1814"/><stop offset="100%" stop-color="#12100C"/>
              </linearGradient>
              <linearGradient id="cg2" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#E8CC8A"/><stop offset="100%" stop-color="#8B6914"/>
              </linearGradient>
            </defs>
            <!-- Table top -->
            <ellipse cx="140" cy="160" rx="120" ry="40" fill="url(#tableW)"/>
            <ellipse cx="140" cy="154" rx="118" ry="38" fill="#1E1A14"/>
            <ellipse cx="140" cy="154" rx="118" ry="38" fill="none" stroke="#C9A84C" stroke-width="0.8" stroke-opacity="0.3"/>
            <line x1="22" y1="154" x2="258" y2="154" stroke="#C9A84C" stroke-width="0.4" stroke-opacity="0.15"/>
            <!-- Leg -->
            <rect x="126" y="190" width="28" height="80" fill="#1A1610"/>
            <ellipse cx="140" cy="270" rx="36" ry="12" fill="#221C14"/>
            <path d="M104,270 Q90,278 78,275" stroke="url(#cg2)" stroke-width="6" fill="none" stroke-linecap="round"/>
            <path d="M176,270 Q190,278 202,275" stroke="url(#cg2)" stroke-width="6" fill="none" stroke-linecap="round"/>
            <!-- Chairs hint -->
            <rect x="10" y="110" width="30" height="70" rx="4" fill="#2A2218" opacity="0.6"/>
            <rect x="240" y="110" width="30" height="70" rx="4" fill="#2A2218" opacity="0.6"/>
          </svg>
        </div>
      </div>
      <div class="collection-card-overlay"></div>
      <div class="collection-card-info">
        <span class="collection-tag">Collection 02</span>
        <h3 class="collection-name">Dining Sets</h3>
        <p class="collection-desc">Gather in elegance. Dining tables and chairs crafted for memorable occasions.</p>
        <a href="#contact" class="collection-link">Explore</a>
      </div>
    </div>

    <!-- Bedroom -->
    <div class="collection-card reveal reveal-delay-2">
      <div class="collection-card-bg">
        <div class="card-inner cc-3">
          <svg viewBox="0 0 280 320" xmlns="http://www.w3.org/2000/svg" style="width:80%;opacity:0.85">
            <defs>
              <linearGradient id="bedFrame" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#221C14"/><stop offset="100%" stop-color="#16120C"/>
              </linearGradient>
              <linearGradient id="cg3" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#E8CC8A"/><stop offset="100%" stop-color="#8B6914"/>
              </linearGradient>
            </defs>
            <!-- Headboard -->
            <rect x="20" y="80" width="240" height="120" rx="8" fill="url(#bedFrame)"/>
            <rect x="28" y="88" width="224" height="104" rx="6" fill="#1A1610"/>
            <!-- Headboard pattern -->
            <rect x="40" y="98" width="80" height="84" rx="4" fill="#221C14"/>
            <rect x="160" y="98" width="80" height="84" rx="4" fill="#221C14"/>
            <!-- Mattress -->
            <rect x="16" y="196" width="248" height="80" rx="4" fill="#2A2420"/>
            <rect x="16" y="196" width="248" height="12" rx="4" fill="#3A3028"/>
            <!-- Pillows -->
            <rect x="32" y="204" width="88" height="52" rx="8" fill="#F5F0E8" opacity="0.08"/>
            <rect x="160" y="204" width="88" height="52" rx="8" fill="#F5F0E8" opacity="0.08"/>
            <!-- Blanket -->
            <rect x="16" y="236" width="248" height="40" rx="4" fill="#1A1812"/>
            <line x1="16" y1="242" x2="264" y2="242" stroke="#C9A84C" stroke-width="0.6" stroke-opacity="0.2"/>
            <!-- Legs -->
            <rect x="24" y="272" width="12" height="24" rx="2" fill="url(#cg3)"/>
            <rect x="244" y="272" width="12" height="24" rx="2" fill="url(#cg3)"/>
          </svg>
        </div>
      </div>
      <div class="collection-card-overlay"></div>
      <div class="collection-card-info">
        <span class="collection-tag">Collection 03</span>
        <h3 class="collection-name">Bedroom Furniture</h3>
        <p class="collection-desc">Rest in luxury. Beds and wardrobes designed for the finest bedrooms.</p>
        <a href="#contact" class="collection-link">Explore</a>
      </div>
    </div>

    <!-- Office - span 2 -->
    <div class="collection-card reveal reveal-delay-3">
      <div class="collection-card-bg">
        <div class="card-inner cc-4">
          <svg viewBox="0 0 400 300" xmlns="http://www.w3.org/2000/svg" style="width:85%;opacity:0.85">
            <defs>
              <linearGradient id="deskG" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#1E1A12"/><stop offset="100%" stop-color="#141008"/>
              </linearGradient>
              <linearGradient id="cg4" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#E8CC8A"/><stop offset="100%" stop-color="#8B6914"/>
              </linearGradient>
            </defs>
            <!-- Desk top -->
            <rect x="20" y="140" width="360" height="20" rx="4" fill="url(#deskG)"/>
            <rect x="20" y="140" width="360" height="5" rx="2" fill="#2E2618" opacity="0.8"/>
            <!-- Desk modesty panel -->
            <rect x="30" y="158" width="340" height="60" rx="2" fill="#1A1610"/>
            <!-- Drawer unit -->
            <rect x="280" y="158" width="90" height="60" rx="2" fill="#221C14"/>
            <rect x="285" y="165" width="80" height="24" rx="2" fill="#1A1610"/>
            <rect x="285" y="193" width="80" height="20" rx="2" fill="#1A1610"/>
            <ellipse cx="325" cy="177" rx="6" ry="3" fill="url(#cg4)"/>
            <ellipse cx="325" cy="203" rx="6" ry="3" fill="url(#cg4)"/>
            <!-- Legs -->
            <rect x="30" y="158" width="16" height="60" rx="2" fill="#221C14"/>
            <rect x="22" y="215" width="32" height="12" rx="2" fill="url(#cg4)"/>
            <rect x="346" y="215" width="32" height="12" rx="2" fill="url(#cg4)"/>
            <!-- Chair hint -->
            <rect x="150" y="90" width="100" height="55" rx="4" fill="#2A2218" opacity="0.5"/>
            <rect x="150" y="140" width="100" height="20" rx="3" fill="#221C14" opacity="0.7"/>
            <line x1="160" y1="160" x2="155" y2="200" stroke="#C9A84C" stroke-width="3" stroke-opacity="0.5"/>
            <line x1="240" y1="160" x2="245" y2="200" stroke="#C9A84C" stroke-width="3" stroke-opacity="0.5"/>
          </svg>
        </div>
      </div>
      <div class="collection-card-overlay"></div>
      <div class="collection-card-info">
        <span class="collection-tag">Collection 04</span>
        <h3 class="collection-name">Office Furniture</h3>
        <p class="collection-desc">Command presence in every meeting. Executive desks and ergonomic chairs that speak to authority and refined taste.</p>
        <a href="#contact" class="collection-link">Explore Collection</a>
      </div>
    </div>

    <!-- Modular -->
    <div class="collection-card reveal reveal-delay-4">
      <div class="collection-card-bg">
        <div class="card-inner cc-5">
          <svg viewBox="0 0 280 320" xmlns="http://www.w3.org/2000/svg" style="width:75%;opacity:0.85">
            <defs>
              <linearGradient id="modG" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#1E1A14"/><stop offset="100%" stop-color="#141008"/>
              </linearGradient>
              <linearGradient id="cg5" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#E8CC8A"/><stop offset="100%" stop-color="#8B6914"/>
              </linearGradient>
            </defs>
            <!-- Modular unit -->
            <rect x="20" y="60" width="240" height="220" rx="4" fill="url(#modG)"/>
            <!-- Shelves -->
            <rect x="20" y="100" width="240" height="3" fill="#2A2218"/>
            <rect x="20" y="160" width="240" height="3" fill="#2A2218"/>
            <rect x="20" y="220" width="240" height="3" fill="#2A2218"/>
            <!-- Vertical dividers -->
            <rect x="100" y="60" width="3" height="220" fill="#2A2218"/>
            <rect x="180" y="60" width="3" height="160" fill="#2A2218"/>
            <!-- Doors bottom section -->
            <rect x="22" y="223" width="75" height="55" rx="2" fill="#221C14"/>
            <rect x="102" y="223" width="75" height="55" rx="2" fill="#221C14"/>
            <rect x="183" y="223" width="75" height="55" rx="2" fill="#221C14"/>
            <!-- Handles -->
            <rect x="55" y="250" rx="2" width="12" height="3" fill="url(#cg5)"/>
            <rect x="135" y="250" rx="2" width="12" height="3" fill="url(#cg5)"/>
            <rect x="215" y="250" rx="2" width="12" height="3" fill="url(#cg5)"/>
            <!-- Top decor items -->
            <rect x="30" y="70" width="60" height="24" rx="2" fill="#2E2620" opacity="0.6"/>
            <rect x="110" y="70" width="40" height="24" rx="2" fill="#2E2620" opacity="0.6"/>
            <!-- Legs -->
            <rect x="24" y="278" width="8" height="16" rx="2" fill="url(#cg5)"/>
            <rect x="248" y="278" width="8" height="16" rx="2" fill="url(#cg5)"/>
          </svg>
        </div>
      </div>
      <div class="collection-card-overlay"></div>
      <div class="collection-card-info">
        <span class="collection-tag">Collection 05</span>
        <h3 class="collection-name">Modular Furniture</h3>
        <p class="collection-desc">Intelligent spaces demand intelligent furniture. Modular systems that adapt to every lifestyle and layout.</p>
        <a href="#contact" class="collection-link">Explore Collection</a>
      </div>
    </div>
  </div>
</section>

<!-- Services -->
<section id="services">
  <div class="services-bg-accent"></div>
  <div class="services-layout">
    <div class="services-intro">
      <div class="section-eyebrow reveal">What We Offer</div>
      <h2 class="section-title reveal reveal-delay-1">A Complete<br><em>Luxury</em><br>Experience</h2>
      <div class="gold-divider reveal reveal-delay-2"></div>
      <p class="reveal reveal-delay-2">
        From the first design sketch to the final placement of your furniture, our end-to-end service is crafted to deliver a seamless, entirely personal experience. We handle every detail so you can simply enjoy the result.
      </p>
      <div style="margin-top:40px" class="reveal reveal-delay-3">
        <a href="#contact" class="btn-primary">Start Your Project</a>
      </div>
    </div>

    <div class="services-grid reveal reveal-delay-1">
      <div class="service-item">
        <svg class="service-icon" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M8 32L20 8L32 32" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
          <path d="M11 26h18" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
        </svg>
        <div>
          <span class="service-num">01</span>
          <div class="service-content">
            <h3>Custom Furniture Design</h3>
            <p>Your vision, brought to life by our master craftsmen. Every dimension, material, and finish tailored exclusively for you.</p>
          </div>
        </div>
      </div>
      <div class="service-item">
        <svg class="service-icon" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect x="6" y="6" width="28" height="28" rx="3" stroke="currentColor" stroke-width="1.5"/>
          <path d="M6 14h28" stroke="currentColor" stroke-width="1.5"/>
          <path d="M14 6v8" stroke="currentColor" stroke-width="1.5"/>
          <path d="M26 6v8" stroke="currentColor" stroke-width="1.5"/>
          <circle cx="20" cy="25" r="4" stroke="currentColor" stroke-width="1.2"/>
        </svg>
        <div>
          <span class="service-num">02</span>
          <div class="service-content">
            <h3>Interior Consultation</h3>
            <p>One-on-one sessions with our expert interior designers to conceptualise and curate your ideal living environment.</p>
          </div>
        </div>
      </div>
      <div class="service-item">
        <svg class="service-icon" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M8 28L14 14L22 22L28 16L34 28H8Z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/>
        </svg>
        <div>
          <span class="service-num">03</span>
          <div class="service-content">
            <h3>White Glove Delivery</h3>
            <p>Premium white-glove delivery service ensuring your furniture arrives pristine, on time, and to your exact specifications.</p>
          </div>
        </div>
      </div>
      <div class="service-item">
        <svg class="service-icon" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="20" cy="20" r="13" stroke="currentColor" stroke-width="1.5"/>
          <path d="M20 12v8l6 3" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
        </svg>
        <div>
          <span class="service-num">04</span>
          <div class="service-content">
            <h3>Professional Installation</h3>
            <p>Expert installation by certified technicians who treat your home with the utmost care and precision.</p>
          </div>
        </div>
      </div>
      <div class="service-item">
        <svg class="service-icon" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
          <rect x="6" y="20" width="28" height="14" rx="2" stroke="currentColor" stroke-width="1.5"/>
          <path d="M10 20V14a10 10 0 0120 0v6" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
        </svg>
        <div>
          <span class="service-num">05</span>
          <div class="service-content">
            <h3>Bulk Commercial Projects</h3>
            <p>Dedicated project management for hotels, corporate offices, and large-scale residential developments with exclusive volume pricing.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Testimonials -->
<section id="testimonials">
  <div class="section-eyebrow reveal">Client Stories</div>
  <h2 class="section-title reveal reveal-delay-1">What Our Clients<br><em>Say</em></h2>

  <div class="testimonials-grid">
    <div class="testimonial-card reveal reveal-delay-1">
      <div class="testimonial-stars">
        <span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span>
      </div>
      <p class="testimonial-text">"Maison Élite transformed our home into something we could not have imagined. The attention to detail in every single piece is extraordinary — this is craftsmanship at its absolute finest."</p>
      <div class="testimonial-author">
        <div class="testimonial-avatar">AR</div>
        <div>
          <div class="testimonial-name">Arjun Rathore</div>
          <div class="testimonial-role">Director, Rathore Estates · Bhopal</div>
        </div>
      </div>
    </div>
    <div class="testimonial-card reveal reveal-delay-2">
      <div class="testimonial-stars">
        <span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span>
      </div>
      <p class="testimonial-text">"We furnished our entire boutique hotel through Maison Élite. The team's professionalism, craftsmanship, and commitment to delivering perfection is simply unmatched in the industry."</p>
      <div class="testimonial-author">
        <div class="testimonial-avatar">PS</div>
        <div>
          <div class="testimonial-name">Priya Sharma</div>
          <div class="testimonial-role">Founder, The Velvet Stay · Indore</div>
        </div>
      </div>
    </div>
    <div class="testimonial-card reveal reveal-delay-3">
      <div class="testimonial-stars">
        <span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span><span class="star">★</span>
      </div>
      <p class="testimonial-text">"From the first consultation to the final installation, the experience was impeccably handled. Our custom dining set is a conversation piece at every dinner party. Absolutely worth every rupee."</p>
      <div class="testimonial-author">
        <div class="testimonial-avatar">VK</div>
        <div>
          <div class="testimonial-name">Vikram Kapoor</div>
          <div class="testimonial-role">CEO, Kapoor Industries · Bhopal</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Gallery -->
<section id="gallery">
  <div class="section-eyebrow reveal">Our Work</div>
  <h2 class="section-title reveal reveal-delay-1">Spaces We've<br><em>Transformed</em></h2>

  <div class="gallery-grid">
    <div class="gallery-item reveal">
      <div class="gallery-inner">
        <div class="g1" style="width:100%;height:100%;display:flex;align-items:center;justify-content:center">
          <svg viewBox="0 0 560 560" xmlns="http://www.w3.org/2000/svg" style="width:70%;opacity:0.7">
            <defs>
              <linearGradient id="gl1" x1="0" y1="0" x2="1" y2="1">
                <stop offset="0%" stop-color="#2A2218"/><stop offset="100%" stop-color="#161008"/>
              </linearGradient>
            </defs>
            <!-- Full room scene -->
            <rect x="0" y="0" width="560" height="560" fill="#1A1510" opacity="0.5"/>
            <rect x="0" y="320" width="560" height="240" fill="#221A10" opacity="0.4"/>
            <rect x="120" y="160" width="320" height="200" rx="6" fill="url(#gl1)"/>
            <rect x="120" y="150" width="320" height="16" rx="3" fill="#3A2C1E"/>
            <line x1="280" y1="160" x2="280" y2="360" stroke="#C9A84C" stroke-width="2" stroke-opacity="0.1"/>
            <rect x="60" y="160" width="26" height="200" rx="4" fill="#221A12"/>
            <rect x="474" y="160" width="26" height="200" rx="4" fill="#221A12"/>
            <rect x="130" y="340" width="80" height="80" rx="3" fill="#1E180E" opacity="0.7"/>
            <rect x="350" y="340" width="80" height="80" rx="3" fill="#1E180E" opacity="0.7"/>
            <text x="280" y="480" text-anchor="middle" fill="#C9A84C" font-size="11" letter-spacing="4" opacity="0.6" font-family="Jost, sans-serif" font-weight="300">LIVING ROOM SUITE</text>
          </svg>
        </div>
      </div>
      <div class="gallery-overlay">
        <div class="gallery-overlay-icon">+</div>
      </div>
    </div>

    <div class="gallery-item reveal reveal-delay-1">
      <div class="gallery-inner">
        <div class="g2" style="width:100%;height:100%;display:flex;align-items:center;justify-content:center">
          <svg viewBox="0 0 280 280" xmlns="http://www.w3.org/2000/svg" style="width:75%;opacity:0.75">
            <ellipse cx="140" cy="160" rx="110" ry="36" fill="#1C1814" opacity="0.8"/>
            <ellipse cx="140" cy="148" rx="108" ry="34" fill="#1A1610"/>
            <rect x="122" y="180" width="36" height="70" fill="#181410"/>
            <ellipse cx="140" cy="250" rx="50" ry="16" fill="#201A12"/>
            <path d="M90,250 Q70,262 55,258" stroke="#C9A84C" stroke-width="6" fill="none" stroke-linecap="round" opacity="0.7"/>
            <path d="M190,250 Q210,262 225,258" stroke="#C9A84C" stroke-width="6" fill="none" stroke-linecap="round" opacity="0.7"/>
            <text x="140" y="290" text-anchor="middle" fill="#C9A84C" font-size="9" letter-spacing="3" opacity="0.5" font-family="Jost, sans-serif">DINING TABLE</text>
          </svg>
        </div>
      </div>
      <div class="gallery-overlay">
        <div class="gallery-overlay-icon">+</div>
      </div>
    </div>

    <div class="gallery-item reveal reveal-delay-2">
      <div class="gallery-inner">
        <div class="g3" style="width:100%;height:100%;display:flex;align-items:center;justify-content:center">
          <svg viewBox="0 0 280 280" xmlns="http://www.w3.org/2000/svg" style="width:75%;opacity:0.75">
            <rect x="20" y="60" width="240" height="120" rx="8" fill="#1E1A12"/>
            <rect x="28" y="68" width="224" height="104" rx="6" fill="#181410"/>
            <rect x="40" y="80" width="80" height="80" rx="4" fill="#221C14"/>
            <rect x="160" y="80" width="80" height="80" rx="4" fill="#221C14"/>
            <rect x="16" y="176" width="248" height="70" rx="4" fill="#201A14"/>
            <rect x="30" y="182" width="96" height="54" rx="6" fill="#F5F0E8" opacity="0.05"/>
            <rect x="154" y="182" width="96" height="54" rx="6" fill="#F5F0E8" opacity="0.05"/>
            <rect x="24" y="244" width="10" height="20" rx="2" fill="#C9A84C" opacity="0.7"/>
            <rect x="246" y="244" width="10" height="20" rx="2" fill="#C9A84C" opacity="0.7"/>
            <text x="140" y="278" text-anchor="middle" fill="#C9A84C" font-size="9" letter-spacing="3" opacity="0.5" font-family="Jost, sans-serif">MASTER BEDROOM</text>
          </svg>
        </div>
      </div>
      <div class="gallery-overlay">
        <div class="gallery-overlay-icon">+</div>
      </div>
    </div>

    <div class="gallery-item reveal reveal-delay-3">
      <div class="gallery-inner">
        <div class="g4" style="width:100%;height:100%;display:flex;align-items:center;justify-content:center">
          <svg viewBox="0 0 280 560" xmlns="http://www.w3.org/2000/svg" style="width:55%;opacity:0.75">
            <rect x="20" y="40" width="240" height="360" rx="4" fill="#1E1A12"/>
            <rect x="20" y="80" width="240" height="3" fill="#2A2218"/>
            <rect x="20" y="160" width="240" height="3" fill="#2A2218"/>
            <rect x="20" y="240" width="240" height="3" fill="#2A2218"/>
            <rect x="20" y="320" width="240" height="3" fill="#2A2218"/>
            <rect x="100" y="40" width="3" height="360" fill="#2A2218"/>
            <rect x="180" y="40" width="3" height="280" fill="#2A2218"/>
            <rect x="22" y="323" width="75" height="75" rx="2" fill="#221C14"/>
            <rect x="103" y="323" width="75" height="75" rx="2" fill="#221C14"/>
            <rect x="183" y="323" width="75" height="75" rx="2" fill="#221C14"/>
            <rect x="50" y="355" rx="2" width="18" height="4" fill="#C9A84C" opacity="0.6"/>
            <rect x="132" y="355" rx="2" width="18" height="4" fill="#C9A84C" opacity="0.6"/>
            <rect x="212" y="355" rx="2" width="18" height="4" fill="#C9A84C" opacity="0.6"/>
            <text x="140" y="430" text-anchor="middle" fill="#C9A84C" font-size="9" letter-spacing="3" opacity="0.5" font-family="Jost, sans-serif">MODULAR UNIT</text>
          </svg>
        </div>
      </div>
      <div class="gallery-overlay">
        <div class="gallery-overlay-icon">+</div>
      </div>
    </div>

    <div class="gallery-item reveal reveal-delay-4">
      <div class="gallery-inner">
        <div class="g5" style="width:100%;height:100%;display:flex;align-items:center;justify-content:center">
          <svg viewBox="0 0 280 280" xmlns="http://www.w3.org/2000/svg" style="width:75%;opacity:0.75">
            <rect x="20" y="80" width="240" height="20" rx="3" fill="#1E1A12"/>
            <rect x="30" y="98" width="80" height="100" rx="2" fill="#181410"/>
            <rect x="170" y="98" width="80" height="100" rx="2" fill="#181410"/>
            <rect x="120" y="98" width="40" height="100" rx="2" fill="#181410"/>
            <rect x="20" y="196" width="240" height="14" rx="3" fill="#221C14"/>
            <rect x="36" y="208" width="14" height="40" rx="3" fill="#C9A84C" opacity="0.6"/>
            <rect x="230" y="208" width="14" height="40" rx="3" fill="#C9A84C" opacity="0.6"/>
            <rect x="80" y="100" width="12" height="3" rx="1" fill="#C9A84C" opacity="0.5"/>
            <rect x="182" y="100" width="12" height="3" rx="1" fill="#C9A84C" opacity="0.5"/>
            <text x="140" y="264" text-anchor="middle" fill="#C9A84C" font-size="9" letter-spacing="3" opacity="0.5" font-family="Jost, sans-serif">EXECUTIVE DESK</text>
          </svg>
        </div>
      </div>
      <div class="gallery-overlay">
        <div class="gallery-overlay-icon">+</div>
      </div>
    </div>

    <div class="gallery-item reveal reveal-delay-5">
      <div class="gallery-inner">
        <div class="g6" style="width:100%;height:100%;display:flex;align-items:center;justify-content:center">
          <svg viewBox="0 0 280 280" xmlns="http://www.w3.org/2000/svg" style="width:75%;opacity:0.75">
            <rect x="40" y="60" width="200" height="140" rx="6" fill="#1E1A12"/>
            <rect x="48" y="68" width="184" height="124" rx="4" fill="#181410"/>
            <circle cx="80" cy="100" r="16" fill="#C9A84C" opacity="0.08"/>
            <circle cx="80" cy="100" r="10" fill="#C9A84C" opacity="0.1"/>
            <circle cx="80" cy="100" r="5" fill="#C9A84C" opacity="0.3"/>
            <rect x="60" y="160" width="160" height="50" rx="4" fill="#221C14" opacity="0.7"/>
            <rect x="50" y="198" width="180" height="12" rx="3" fill="#1A1610"/>
            <rect x="70" y="208" width="14" height="30" rx="2" fill="#C9A84C" opacity="0.6"/>
            <rect x="196" y="208" width="14" height="30" rx="2" fill="#C9A84C" opacity="0.6"/>
            <text x="140" y="254" text-anchor="middle" fill="#C9A84C" font-size="9" letter-spacing="3" opacity="0.5" font-family="Jost, sans-serif">LOUNGE CHAIR</text>
          </svg>
        </div>
      </div>
      <div class="gallery-overlay">
        <div class="gallery-overlay-icon">+</div>
      </div>
    </div>
  </div>
</section>

<!-- Contact -->
<section id="contact">
  <div class="contact-layout">
    <div class="contact-info reveal">
      <div class="section-eyebrow">Get In Touch</div>
      <h2 class="section-title">Begin Your<br><em>Journey</em></h2>
      <p>Whether you're furnishing a single room or an entire estate, our consultants are ready to guide you every step of the way. Experience luxury, personally.</p>

      <div class="contact-details">
        <div class="contact-detail">
          <svg class="contact-detail-icon" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M10 11a3 3 0 100-6 3 3 0 000 6z" stroke="currentColor" stroke-width="1.2"/>
            <path d="M10 2C6.69 2 4 4.69 4 8c0 5.25 6 10 6 10s6-4.75 6-10c0-3.31-2.69-6-6-6z" stroke="currentColor" stroke-width="1.2"/>
          </svg>
          <div class="contact-detail-text">
            <span class="contact-detail-label">Showroom</span>
            Plot No. 42, MP Nagar Zone II,<br>Bhopal, Madhya Pradesh 462011
          </div>
        </div>
        <div class="contact-detail">
          <svg class="contact-detail-icon" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M3 5a2 2 0 012-2h1.5a1 1 0 01.97.757l.74 2.97a1 1 0 01-.48 1.11l-1.3.77a10 10 0 004.96 4.96l.77-1.3a1 1 0 011.11-.48l2.97.74A1 1 0 0117 13.5V15a2 2 0 01-2 2C7.16 17 3 12.84 3 7V5z" stroke="currentColor" stroke-width="1.2"/>
          </svg>
          <div class="contact-detail-text">
            <span class="contact-detail-label">Phone</span>
            +91 98765 43210
          </div>
        </div>
        <div class="contact-detail">
          <svg class="contact-detail-icon" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <rect x="2" y="4" width="16" height="12" rx="2" stroke="currentColor" stroke-width="1.2"/>
            <path d="M2 7l8 5 8-5" stroke="currentColor" stroke-width="1.2"/>
          </svg>
          <div class="contact-detail-text">
            <span class="contact-detail-label">Email</span>
            hello@maisonelite.in
          </div>
        </div>
        <div class="contact-detail">
          <svg class="contact-detail-icon" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
            <circle cx="10" cy="10" r="7" stroke="currentColor" stroke-width="1.2"/>
            <path d="M10 6v4l3 2" stroke="currentColor" stroke-width="1.2" stroke-linecap="round"/>
          </svg>
          <div class="contact-detail-text">
            <span class="contact-detail-label">Showroom Hours</span>
            Mon – Sat: 10:00 AM – 8:00 PM
          </div>
        </div>
      </div>

      <div class="map-container reveal reveal-delay-2">
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3666.5!2d77.4154!3d23.2332!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x0%3A0x0!2zMjPCsDEzJzU5LjUiTiA3N8KwMjQnNTUuNCJF!5e0!3m2!1sen!2sin!4v1680000000000!5m2!1sen!2sin"
          allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"
          title="Maison Élite Showroom Location">
        </iframe>
      </div>
    </div>

    <div class="reveal reveal-delay-1">
      <div class="section-eyebrow" style="margin-bottom:28px">Send Enquiry</div>
      <form class="contact-form" onsubmit="handleSubmit(event)">
        <div class="form-row">
          <div class="form-group">
            <label for="fname">First Name</label>
            <input type="text" id="fname" placeholder="Arjun" required>
          </div>
          <div class="form-group">
            <label for="lname">Last Name</label>
            <input type="text" id="lname" placeholder="Sharma" required>
          </div>
        </div>
        <div class="form-group">
          <label for="email">Email Address</label>
          <input type="email" id="email" placeholder="arjun@example.com" required>
        </div>
        <div class="form-group">
          <label for="phone">Phone Number</label>
          <input type="tel" id="phone" placeholder="+91 98765 43210">
        </div>
        <div class="form-group">
          <label for="service">Service Interest</label>
          <select id="service">
            <option value="" disabled selected>Select a service</option>
            <option>Custom Furniture Design</option>
            <option>Interior Consultation</option>
            <option>Bedroom Furniture</option>
            <option>Living Room / Sofa</option>
            <option>Dining Sets</option>
            <option>Office Furniture</option>
            <option>Modular Furniture</option>
            <option>Bulk / Commercial Project</option>
          </select>
        </div>
        <div class="form-group">
          <label for="budget">Budget Range</label>
          <select id="budget">
            <option value="" disabled selected>Select budget range</option>
            <option>₹1L – ₹3L</option>
            <option>₹3L – ₹7L</option>
            <option>₹7L – ₹15L</option>
            <option>₹15L – ₹30L</option>
            <option>₹30L+</option>
          </select>
        </div>
        <div class="form-group">
          <label for="message">Your Message</label>
          <textarea id="message" rows="4" placeholder="Tell us about your project, space, and vision…"></textarea>
        </div>
        <button type="submit" class="btn-primary" style="width:100%;border:none;cursor:pointer;font-family:'Jost',sans-serif;font-size:11px;letter-spacing:0.25em" id="submitBtn">
          Send Enquiry
        </button>
        <div id="formSuccess" style="display:none;text-align:center;padding:16px;border:1px solid rgba(201,168,76,0.3);color:var(--gold);font-size:12px;letter-spacing:0.15em">
          ✓ &nbsp; Message received. We'll contact you within 24 hours.
        </div>
      </form>
    </div>
  </div>
</section>

<!-- Footer -->
<footer>
  <div class="footer-grid">
    <div>
      <div class="nav-logo" style="font-family:'Cormorant Garamond',serif;font-size:22px;font-weight:400;letter-spacing:0.15em;color:var(--white)">
        MAISON <span style="color:var(--gold)">ÉLITE</span>
      </div>
      <p class="footer-brand-desc">
        Bhopal's most trusted name in luxury furniture. Crafting bespoke living spaces with uncompromising quality since 2009.
      </p>
      <div class="footer-social">
        <a href="#" aria-label="Instagram">In</a>
        <a href="#" aria-label="Facebook">Fb</a>
        <a href="#" aria-label="Pinterest">Pt</a>
        <a href="#" aria-label="YouTube">Yt</a>
      </div>
    </div>
    <div class="footer-col">
      <h4>Collections</h4>
      <ul>
        <li><a href="#collections">Living Room Sofas</a></li>
        <li><a href="#collections">Dining Sets</a></li>
        <li><a href="#collections">Bedroom Furniture</a></li>
        <li><a href="#collections">Office Furniture</a></li>
        <li><a href="#collections">Modular Furniture</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h4>Services</h4>
      <ul>
        <li><a href="#services">Custom Design</a></li>
        <li><a href="#services">Interior Consultation</a></li>
        <li><a href="#services">Home Delivery</a></li>
        <li><a href="#services">Installation</a></li>
        <li><a href="#services">Commercial Projects</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h4>Company</h4>
      <ul>
        <li><a href="#about">About Us</a></li>
        <li><a href="#gallery">Gallery</a></li>
        <li><a href="#testimonials">Testimonials</a></li>
        <li><a href="#contact">Contact Us</a></li>
        <li><a href="#contact">Book Consultation</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <p>© 2025 Maison Élite. All rights reserved. Crafted with excellence in Bhopal.</p>
    <p><a href="#">Privacy Policy</a> · <a href="#">Terms of Service</a></p>
  </div>
</footer>

<!-- Floating WhatsApp -->
<a href="https://wa.me/919876543210?text=Hello%20Maison%20Élite!%20I'm%20interested%20in%20your%20luxury%20furniture%20collection."
   class="whatsapp-float" target="_blank" rel="noopener" aria-label="Chat on WhatsApp">
  <div class="wa-tooltip">Chat with us</div>
  <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
    <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
  </svg>
</a>

<script>
// Custom Cursor
const cursor = document.getElementById('cursor');
const follower = document.getElementById('cursorFollower');
let mouseX = 0, mouseY = 0, follX = 0, follY = 0;

document.addEventListener('mousemove', e => {
  mouseX = e.clientX; mouseY = e.clientY;
  cursor.style.left = mouseX + 'px';
  cursor.style.top = mouseY + 'px';
});

function animateFollower() {
  follX += (mouseX - follX) * 0.12;
  follY += (mouseY - follY) * 0.12;
  follower.style.left = follX + 'px';
  follower.style.top = follY + 'px';
  requestAnimationFrame(animateFollower);
}
animateFollower();

document.querySelectorAll('a, button, .collection-card, .gallery-item, .service-item, .about-feature').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.width = '14px'; cursor.style.height = '14px';
    follower.style.width = '56px'; follower.style.height = '56px';
  });
  el.addEventListener('mouseleave', () => {
    cursor.style.width = '8px'; cursor.style.height = '8px';
    follower.style.width = '36px'; follower.style.height = '36px';
  });
});

// Loader
let pct = 0;
const loaderPct = document.getElementById('loaderPct');
const loaderInterval = setInterval(() => {
  pct = Math.min(pct + Math.random() * 18, 100);
  loaderPct.textContent = Math.floor(pct) + '%';
  if (pct >= 100) {
    clearInterval(loaderInterval);
    loaderPct.textContent = '100%';
    setTimeout(() => {
      document.getElementById('loader').classList.add('hidden');
    }, 500);
  }
}, 80);

// Navbar scroll
const navbar = document.getElementById('navbar');
window.addEventListener('scroll', () => {
  navbar.classList.toggle('scrolled', window.scrollY > 60);
});

// Reveal on scroll
const revealEls = document.querySelectorAll('.reveal');
const revealObserver = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
    }
  });
}, { threshold: 0.12 });
revealEls.forEach(el => revealObserver.observe(el));

// Mobile menu
function openMobile() { document.getElementById('mobileMenu').classList.add('open'); }
function closeMobile() { document.getElementById('mobileMenu').classList.remove('open'); }
document.getElementById('mobileClose').addEventListener('click', closeMobile);

// Form submit
function handleSubmit(e) {
  e.preventDefault();
  const btn = document.getElementById('submitBtn');
  btn.textContent = 'Sending…';
  btn.style.opacity = '0.6';
  setTimeout(() => {
    btn.style.display = 'none';
    document.getElementById('formSuccess').style.display = 'block';
    e.target.reset();
  }, 1200);
}

// Smooth scroll
document.querySelectorAll('a[href^="#"]').forEach(a => {
  a.addEventListener('click', e => {
    const target = document.querySelector(a.getAttribute('href'));
    if (target) {
      e.preventDefault();
      target.scrollIntoView({ behavior: 'smooth', block: 'start' });
    }
  });
});

// Parallax hero
window.addEventListener('scroll', () => {
  const hero = document.getElementById('hero');
  const scroll = window.scrollY;
  const shape = hero.querySelector('.hero-3d-shape');
  if (shape && scroll < window.innerHeight) {
    shape.style.transform = `translateY(calc(-50% + ${scroll * 0.18}px))`;
  }
});
</script>
</body>
</html>
