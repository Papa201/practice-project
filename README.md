<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Butiki Planet — Coffee & Food</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Bebas+Neue&family=Montserrat:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --gold: #C9A84C;
    --gold-light: #F0D080;
    --amber: #D4823A;
    --cream: #F5EDD8;
    --dark: #0A0806;
    --dark2: #120F0A;
    --dark3: #1C1710;
    --text-muted: #8A7A60;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Montserrat', sans-serif;
    background: var(--dark);
    color: var(--cream);
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 12px; height: 12px;
    background: var(--gold);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s ease, width 0.2s ease, height 0.2s ease, background 0.2s ease;
    mix-blend-mode: difference;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid var(--gold);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.15s ease, width 0.3s ease, height 0.3s ease, opacity 0.3s ease;
    opacity: 0.5;
  }
  body:hover .cursor { opacity: 1; }

  /* Nav */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex; justify-content: space-between; align-items: center;
    padding: 1.5rem 5vw;
    background: linear-gradient(to bottom, rgba(10,8,6,0.95) 0%, transparent 100%);
    transition: background 0.4s;
  }
  nav.scrolled { background: rgba(10,8,6,0.98); border-bottom: 1px solid rgba(201,168,76,0.15); }

  .nav-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.6rem;
    letter-spacing: 0.12em;
    color: var(--gold);
    text-decoration: none;
  }
  .nav-logo span { color: var(--cream); }

  .nav-links { display: flex; gap: 2.5rem; list-style: none; }
  .nav-links a {
    font-size: 0.68rem; letter-spacing: 0.18em; text-transform: uppercase;
    color: var(--text-muted); text-decoration: none;
    transition: color 0.3s;
    font-weight: 400;
  }
  .nav-links a:hover { color: var(--gold); }

  .nav-cta {
    font-size: 0.68rem; letter-spacing: 0.15em; text-transform: uppercase;
    color: var(--dark); background: var(--gold);
    padding: 0.6rem 1.6rem; text-decoration: none;
    font-weight: 500;
    transition: background 0.3s, transform 0.2s;
  }
  .nav-cta:hover { background: var(--gold-light); transform: translateY(-1px); }

  /* Hero */
  #hero {
    min-height: 100vh;
    display: flex; align-items: center; justify-content: center;
    position: relative; overflow: hidden;
    background: var(--dark);
  }

  .hero-bg {
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse 80% 60% at 70% 40%, rgba(201,168,76,0.08) 0%, transparent 60%),
      radial-gradient(ellipse 50% 50% at 20% 70%, rgba(212,130,58,0.06) 0%, transparent 50%),
      radial-gradient(ellipse 30% 30% at 80% 80%, rgba(201,168,76,0.04) 0%, transparent 50%);
  }

  /* Star field */
  .stars {
    position: absolute; inset: 0; overflow: hidden;
  }
  .star {
    position: absolute; background: white; border-radius: 50%;
    animation: twinkle var(--d) ease-in-out infinite alternate;
    opacity: var(--o);
  }
  @keyframes twinkle { from { opacity: var(--o); } to { opacity: calc(var(--o) * 0.2); } }

  /* Planet rings */
  .planet-container {
    position: absolute; right: -5vw; top: 50%; transform: translateY(-50%);
    width: 55vw; height: 55vw; max-width: 700px; max-height: 700px;
    pointer-events: none;
  }
  .planet {
    width: 100%; height: 100%;
    border-radius: 50%;
    background: radial-gradient(circle at 35% 35%,
      #3D2E18 0%, #1C160C 40%, #0A0806 70%, #050403 100%);
    box-shadow:
      inset -20px -20px 60px rgba(0,0,0,0.8),
      inset 10px 10px 40px rgba(201,168,76,0.08),
      0 0 80px rgba(201,168,76,0.06),
      0 0 200px rgba(201,168,76,0.03);
    position: relative;
    animation: planetFloat 8s ease-in-out infinite, planetRotate 30s linear infinite;
  }
  @keyframes planetRotate {
    from { transform: rotateY(0deg); }
    to { transform: rotateY(360deg); }
  }
  @keyframes planetFloat {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-20px); }
  }

  .planet::before {
    content: '';
    position: absolute; inset: 5%;
    border-radius: 50%;
    background: radial-gradient(circle at 30% 25%,
      rgba(201,168,76,0.15) 0%, transparent 50%);
  }

  /* Ring */
  .planet-ring {
    position: absolute;
    top: 50%; left: 50%;
    width: 145%; height: 18%;
    transform: translate(-50%, -50%) rotateX(78deg);
    border-radius: 50%;
    border: 14px solid rgba(201,168,76,0.12);
    box-shadow:
      0 0 20px rgba(201,168,76,0.06),
      inset 0 0 20px rgba(201,168,76,0.04);
    animation: ringFloat 8s ease-in-out infinite;
  }
  @keyframes ringFloat {
    0%, 100% { transform: translate(-50%, -50%) rotateX(78deg) translateY(0); }
    50% { transform: translate(-50%, -50%) rotateX(78deg) translateY(-20px); }
  }

  .hero-content {
    position: relative; z-index: 2;
    text-align: left; padding: 0 5vw;
    max-width: 600px;
    animation: heroReveal 1.2s ease forwards;
    opacity: 0; transform: translateY(30px);
  }
  @keyframes heroReveal {
    to { opacity: 1; transform: translateY(0); }
  }

  .hero-overline {
    font-size: 0.65rem; letter-spacing: 0.3em; text-transform: uppercase;
    color: var(--gold); margin-bottom: 1.5rem;
    font-weight: 400;
    display: flex; align-items: center; gap: 1rem;
  }
  .hero-overline::before {
    content: ''; width: 40px; height: 1px; background: var(--gold); opacity: 0.6;
  }

  .hero-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(3.5rem, 8vw, 7rem);
    font-weight: 300;
    line-height: 1;
    letter-spacing: -0.02em;
    color: var(--cream);
    margin-bottom: 0.2rem;
  }
  .hero-title em {
    font-style: italic; color: var(--gold);
    display: block;
  }
  .hero-title strong {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.1em; letter-spacing: 0.05em;
    font-weight: 400; color: var(--cream);
    display: block;
  }

  .hero-subtitle {
    margin-top: 2rem;
    font-size: 0.8rem; line-height: 1.9; letter-spacing: 0.05em;
    color: var(--text-muted); max-width: 380px; font-weight: 300;
  }

  .hero-actions {
    margin-top: 3rem; display: flex; gap: 1.5rem; align-items: center;
  }
  .btn-primary {
    display: inline-block;
    background: var(--gold); color: var(--dark);
    padding: 1rem 2.5rem;
    font-size: 0.7rem; letter-spacing: 0.2em; text-transform: uppercase;
    text-decoration: none; font-weight: 500;
    transition: all 0.3s;
    position: relative; overflow: hidden;
  }
  .btn-primary::after {
    content: ''; position: absolute; inset: 0;
    background: var(--gold-light); transform: translateX(-100%);
    transition: transform 0.3s ease;
  }
  .btn-primary:hover::after { transform: translateX(0); }
  .btn-primary span { position: relative; z-index: 1; }

  .btn-ghost {
    font-size: 0.7rem; letter-spacing: 0.18em; text-transform: uppercase;
    color: var(--text-muted); text-decoration: none; font-weight: 400;
    border-bottom: 1px solid rgba(138,122,96,0.3);
    padding-bottom: 2px;
    transition: color 0.3s, border-color 0.3s;
  }
  .btn-ghost:hover { color: var(--gold); border-color: var(--gold); }

  .hero-scroll {
    position: absolute; bottom: 3rem; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 0.8rem;
    color: var(--text-muted); font-size: 0.6rem; letter-spacing: 0.2em; text-transform: uppercase;
  }
  .scroll-line {
    width: 1px; height: 50px; background: var(--gold);
    animation: scrollDown 1.8s ease-in-out infinite;
    opacity: 0.7;
  }
  @keyframes scrollDown {
    0% { transform: scaleY(0); transform-origin: top; }
    50% { transform: scaleY(1); transform-origin: top; }
    50.01% { transform-origin: bottom; }
    100% { transform: scaleY(0); transform-origin: bottom; }
  }

  /* Marquee strip */
  .marquee-strip {
    background: var(--gold);
    padding: 0.9rem 0; overflow: hidden;
    display: flex;
  }
  .marquee-track {
    display: flex; gap: 3rem; white-space: nowrap;
    animation: marquee 40s linear infinite;
  }
  .marquee-track:hover {
    animation-play-state: paused;
  }
  .marquee-item {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 0.9rem; letter-spacing: 0.15em;
    color: var(--dark); flex-shrink: 0;
  }
  .marquee-dot { color: rgba(10,8,6,0.4); }
  @keyframes marquee { from { transform: translateX(0); } to { transform: translateX(-50%); } }

  /* About */
  #about {
    padding: 10rem 5vw;
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 5rem; align-items: center;
    background: var(--dark2);
    position: relative;
  }
  #about::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 1px;
    background: linear-gradient(to right, transparent, rgba(201,168,76,0.3), transparent);
  }

  .about-visual {
    position: relative;
  }
  .about-img-frame {
    aspect-ratio: 3/4;
    background:
      radial-gradient(circle at 40% 30%, rgba(201,168,76,0.15) 0%, transparent 60%),
      linear-gradient(135deg, #1C160C 0%, #0A0806 100%);
    border: 1px solid rgba(201,168,76,0.12);
    position: relative; overflow: hidden;
    display: flex; align-items: center; justify-content: center;
  }
  .about-img-frame::after {
    content: '';
    position: absolute; inset: 0;
    background: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='60' height='60'%3E%3Ccircle cx='1' cy='1' r='0.5' fill='rgba(201,168,76,0.08)'/%3E%3C/svg%3E");
  }
  .coffee-icon {
    font-size: 8rem; opacity: 0.3;
    filter: sepia(1) saturate(2) hue-rotate(-10deg);
  }
  .about-badge {
    position: absolute; bottom: -1.5rem; right: -1.5rem;
    width: 120px; height: 120px;
    background: var(--gold);
    border-radius: 50%;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    color: var(--dark);
  }
  .about-badge-num {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 2.2rem; line-height: 1;
  }
  .about-badge-text {
    font-size: 0.55rem; letter-spacing: 0.12em;
    text-transform: uppercase; font-weight: 500;
    text-align: center; line-height: 1.4;
  }

  .about-text {
    flex: 1;
  }
  .section-label {
    font-size: 0.65rem; letter-spacing: 0.3em; text-transform: uppercase;
    color: var(--gold); margin-bottom: 1.5rem; font-weight: 400;
    display: flex; align-items: center; gap: 1rem;
  }
  .section-label::before { content: '01'; color: rgba(201,168,76,0.3); font-family: 'Bebas Neue', sans-serif; font-size: 0.9rem; }

  .section-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(2.5rem, 4vw, 4rem);
    font-weight: 300; line-height: 1.1;
    color: var(--cream); margin-bottom: 2rem;
  }
  .section-title em { font-style: italic; color: var(--gold); }

  .about-body {
    font-size: 0.82rem; line-height: 2;
    color: var(--text-muted); font-weight: 300;
    margin-bottom: 2.5rem;
  }

  .about-stats {
    display: grid; grid-template-columns: repeat(3, 1fr);
    gap: 2rem; margin-top: 3rem;
    padding-top: 3rem;
    border-top: 1px solid rgba(201,168,76,0.1);
  }
  .stat-num {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2.5rem; font-weight: 300;
    color: var(--gold); line-height: 1;
  }
  .stat-label {
    font-size: 0.62rem; letter-spacing: 0.15em;
    text-transform: uppercase; color: var(--text-muted);
    margin-top: 0.3rem;
  }

  /* Menu */
  #menu {
    padding: 10rem 5vw;
    background: var(--dark);
    position: relative;
  }
  .menu-header {
    text-align: center; margin-bottom: 6rem;
  }
  .menu-header .section-label::before { content: '02'; }
  .menu-header .section-label { justify-content: center; }

  .menu-tabs {
    display: flex; justify-content: center; gap: 0;
    margin-bottom: 4rem;
    border: 1px solid rgba(201,168,76,0.15);
    width: fit-content; margin-left: auto; margin-right: auto;
  }
  .tab-btn {
    padding: 0.8rem 2rem;
    font-size: 0.65rem; letter-spacing: 0.18em; text-transform: uppercase;
    background: none; border: none; color: var(--text-muted);
    cursor: none; font-family: 'Montserrat', sans-serif; font-weight: 400;
    transition: all 0.3s;
    border-right: 1px solid rgba(201,168,76,0.15);
    position: relative;
  }
  .tab-btn:last-child { border-right: none; }
  .tab-btn.active, .tab-btn:hover {
    color: var(--dark); background: var(--gold);
  }

  .menu-grid {
    display: grid; grid-template-columns: repeat(3, 1fr);
    gap: 2px;
  }
  .menu-item {
    background: var(--dark3);
    padding: 2.5rem;
    position: relative; overflow: hidden;
    transition: background 0.3s;
    cursor: none;
  }
  .menu-item::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 2px;
    background: var(--gold);
    transform: scaleX(0); transform-origin: left;
    transition: transform 0.4s ease;
  }
  .menu-item:hover { background: #1C160C; }
  .menu-item:hover::before { transform: scaleX(1); }

  .menu-cat {
    font-size: 0.55rem; letter-spacing: 0.25em; text-transform: uppercase;
    color: var(--gold); margin-bottom: 0.8rem; opacity: 0.7;
  }
  .menu-name {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.5rem; font-weight: 400;
    color: var(--cream); margin-bottom: 0.8rem;
    line-height: 1.2;
  }
  .menu-desc {
    font-size: 0.72rem; line-height: 1.8;
    color: var(--text-muted); font-weight: 300;
    margin-bottom: 1.5rem;
  }
  .menu-price {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.3rem; color: var(--gold);
    font-weight: 300;
  }
  .menu-num {
    position: absolute; top: 1.5rem; right: 1.5rem;
    font-family: 'Bebas Neue', sans-serif;
    font-size: 3rem; color: rgba(201,168,76,0.05);
    line-height: 1;
  }

  /* Experience section */
  #experience {
    padding: 10rem 5vw;
    background: var(--dark2);
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 5rem; align-items: center;
    position: relative;
  }
  #experience::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 1px;
    background: linear-gradient(to right, transparent, rgba(201,168,76,0.3), transparent);
  }

  .exp-text .section-label::before { content: '03'; }

  .exp-features { margin-top: 3rem; display: flex; flex-direction: column; gap: 2rem; }
  .exp-feature {
    display: flex; gap: 1.5rem; align-items: flex-start;
    padding-bottom: 2rem;
    border-bottom: 1px solid rgba(201,168,76,0.08);
  }
  .exp-feature:last-child { border-bottom: none; padding-bottom: 0; }
  .feature-icon {
    width: 40px; height: 40px; flex-shrink: 0;
    border: 1px solid rgba(201,168,76,0.25);
    display: flex; align-items: center; justify-content: center;
    font-size: 1.1rem;
    color: var(--gold);
  }
  .feature-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.1rem; color: var(--cream); margin-bottom: 0.4rem;
  }
  .feature-desc {
    font-size: 0.72rem; line-height: 1.8;
    color: var(--text-muted); font-weight: 300;
  }

  .exp-visual {
    display: grid; grid-template-columns: 1fr 1fr; gap: 1rem;
  }
  .exp-card {
    aspect-ratio: 1;
    background: var(--dark3);
    border: 1px solid rgba(201,168,76,0.08);
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    gap: 0.8rem;
    transition: border-color 0.3s, background 0.3s;
    position: relative; overflow: hidden;
  }
  .exp-card:hover {
    border-color: rgba(201,168,76,0.3);
    background: #1C160C;
  }
  .exp-card:nth-child(2) { margin-top: 1.5rem; }
  .exp-card:nth-child(3) { margin-top: -1.5rem; }
  .exp-card-emoji { font-size: 2rem; }
  .exp-card-label {
    font-size: 0.65rem; letter-spacing: 0.15em; text-transform: uppercase;
    color: var(--text-muted);
  }

  /* Testimonials */
  #testimonials {
    padding: 10rem 5vw;
    background: var(--dark);
    text-align: center;
  }
  .testimonials-header .section-label::before { content: '04'; }
  .testimonials-header .section-label { justify-content: center; }

  .testimonials-grid {
    display: grid; grid-template-columns: repeat(3, 1fr);
    gap: 2px; margin-top: 5rem;
  }
  .testimonial {
    background: var(--dark3);
    padding: 3rem 2.5rem;
    text-align: left; position: relative;
  }
  .quote-mark {
    font-family: 'Cormorant Garamond', serif;
    font-size: 5rem; color: var(--gold); opacity: 0.15;
    line-height: 0.5; margin-bottom: 1.5rem;
  }
  .testimonial-text {
    font-family: 'Cormorant Garamond', serif;
    font-style: italic; font-size: 1.1rem;
    line-height: 1.8; color: var(--cream); font-weight: 300;
    margin-bottom: 2rem;
  }
  .testimonial-author {
    font-size: 0.65rem; letter-spacing: 0.15em;
    text-transform: uppercase; color: var(--gold);
  }
  .stars-rating { color: var(--gold); font-size: 0.7rem; margin-bottom: 1rem; letter-spacing: 0.2em; }

  /* Reservation CTA */
  #reserve {
    padding: 10rem 5vw;
    background: var(--dark2);
    text-align: center;
    position: relative; overflow: hidden;
  }
  #reserve::before {
    content: '';
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse 60% 60% at 50% 50%, rgba(201,168,76,0.06) 0%, transparent 70%);
  }
  .reserve-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(3rem, 6vw, 6rem);
    font-weight: 300; line-height: 1; color: var(--cream);
    margin-bottom: 2rem;
  }
  .reserve-title em { color: var(--gold); font-style: italic; }
  .reserve-sub {
    font-size: 0.78rem; line-height: 2; color: var(--text-muted);
    max-width: 450px; margin: 0 auto 3rem; font-weight: 300;
  }

  .reserve-form {
    display: flex; gap: 0; max-width: 500px;
    margin: 0 auto; border: 1px solid rgba(201,168,76,0.25);
  }
  .reserve-input {
    flex: 1; background: none; border: none; outline: none;
    padding: 1rem 1.5rem;
    font-family: 'Montserrat', sans-serif;
    font-size: 0.75rem; letter-spacing: 0.05em;
    color: var(--cream); font-weight: 300;
  }
  .reserve-input::placeholder { color: rgba(138,122,96,0.6); }
  .reserve-input:focus { border-left: 2px solid var(--gold) !important; }
  .reserve-btn {
    background: var(--gold); border: none; outline: none;
    padding: 1rem 2rem;
    font-family: 'Montserrat', sans-serif;
    font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--dark); font-weight: 500;
    cursor: none; transition: all 0.3s ease;
  }
  .reserve-btn:hover { background: var(--gold-light); transform: translateY(-2px); }
  .reserve-btn.sent { background: #6FA85F; color: var(--cream); }

  /* Hours strip */
  .hours-strip {
    display: flex; justify-content: center; gap: 4rem;
    margin-top: 4rem; padding-top: 4rem;
    border-top: 1px solid rgba(201,168,76,0.1);
  }
  .hour-item { text-align: center; }
  .hour-day { font-size: 0.6rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--text-muted); margin-bottom: 0.4rem; }
  .hour-time { font-family: 'Cormorant Garamond', serif; font-size: 1.1rem; color: var(--gold); }

  /* Footer */
  footer {
    background: var(--dark);
    border-top: 1px solid rgba(201,168,76,0.1);
    padding: 4rem 5vw;
    display: grid; grid-template-columns: 2fr 1fr 1fr 1fr;
    gap: 3rem;
  }
  .footer-brand {}
  .footer-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.8rem; color: var(--gold);
    letter-spacing: 0.1em; margin-bottom: 1rem;
  }
  .footer-logo span { color: var(--cream); }
  .footer-tagline {
    font-size: 0.72rem; line-height: 1.9; color: var(--text-muted);
    font-weight: 300; max-width: 220px;
  }
  .footer-col-title {
    font-size: 0.6rem; letter-spacing: 0.25em; text-transform: uppercase;
    color: var(--gold); margin-bottom: 1.5rem; font-weight: 500;
  }
  .footer-links { list-style: none; display: flex; flex-direction: column; gap: 0.8rem; }
  .footer-links a {
    font-size: 0.72rem; color: var(--text-muted);
    text-decoration: none; font-weight: 300;
    transition: color 0.3s;
  }
  .footer-links a:hover { color: var(--cream); }
  .footer-bottom {
    grid-column: 1/-1;
    padding-top: 3rem; margin-top: 1rem;
    border-top: 1px solid rgba(201,168,76,0.08);
    display: flex; justify-content: space-between; align-items: center;
  }
  .footer-copy {
    font-size: 0.65rem; color: var(--text-muted); letter-spacing: 0.05em;
  }
  .social-links { display: flex; gap: 1.5rem; }
  .social-link {
    font-size: 0.65rem; letter-spacing: 0.15em; text-transform: uppercase;
    color: var(--text-muted); text-decoration: none;
    transition: color 0.3s;
  }
  .social-link:hover { color: var(--gold); }

  /* Scroll reveal */
  .reveal { opacity: 0; transform: translateY(40px); transition: opacity 0.8s ease, transform 0.8s ease; }
  .reveal.visible { opacity: 1; transform: translateY(0); }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }

  @media (max-width: 768px) {
    #about, #experience { grid-template-columns: 1fr; }
    .menu-grid, .testimonials-grid { grid-template-columns: 1fr; }
    footer { grid-template-columns: 1fr 1fr; }
    .about-badge { display: none; }
    nav .nav-links, nav .nav-cta { display: none; }
    .hero-content { text-align: center; }
    .hero-overline { justify-content: center; }
    .hero-overline::before { display: none; }
    .hero-actions { justify-content: center; }
    .hours-strip { flex-direction: column; gap: 1.5rem; }
    .exp-visual { display: none; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- Nav -->
<nav id="navbar">
  <a href="#hero" class="nav-logo">Butiki <span>Planet</span></a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#menu">Menu</a></li>
    <li><a href="#experience">Experience</a></li>
    <li><a href="#reserve">Reserve</a></li>
  </ul>
  <a href="#reserve" class="nav-cta">Book a Table</a>
</nav>

<!-- Hero -->
<section id="hero">
  <div class="hero-bg"></div>
  <div class="stars" id="stars"></div>

  <div class="planet-container">
    <div class="planet">
      <div class="planet-ring"></div>
    </div>
  </div>

  <div class="hero-content">
    <div class="hero-overline">Mombasa's Finest</div>
    <h1 class="hero-title">
      Where Coffee<br>
      <em>Meets the</em>
      <strong>Universe</strong>
    </h1>
    <p class="hero-subtitle">
      An otherworldly culinary experience where every sip and bite takes you beyond the ordinary. Specialty brews, inspired cuisine, and an atmosphere unlike anything on this planet.
    </p>
    <div class="hero-actions">
      <a href="#menu" class="btn-primary"><span>Explore Menu</span></a>
      <a href="#reserve" class="btn-ghost">Reserve a Table</a>
    </div>
  </div>

  <div class="hero-scroll">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- Marquee -->
<div class="marquee-strip">
  <div class="marquee-track" id="marqueeTrack">
    <span class="marquee-item">Single Origin Espresso <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Cold Brew <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Specialty Lattes <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Artisan Food <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Mombasa's Finest <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Open Daily <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Single Origin Espresso <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Cold Brew <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Specialty Lattes <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Artisan Food <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Mombasa's Finest <span class="marquee-dot">✦</span></span>
    <span class="marquee-item">Open Daily <span class="marquee-dot">✦</span></span>
  </div>
</div>

<!-- About -->
<section id="about">
  <div class="about-visual reveal">
    <div class="about-img-frame">
      <div class="coffee-icon">☕</div>
    </div>
    <div class="about-badge">
      <div class="about-badge-num">7+</div>
      <div class="about-badge-text">Years of<br>Excellence</div>
    </div>
  </div>
  <div class="about-text">
    <div class="section-label reveal">Our Story</div>
    <h2 class="section-title reveal reveal-delay-1">Born from a <em>Passion</em><br>for the Perfect Cup</h2>
    <p class="about-body reveal reveal-delay-2">
      Butiki Planet began as a dream — to create a space where coffee culture, great food, and warm community could orbit together in perfect harmony. We source our beans from the finest farms across East Africa, roasting each batch to reveal its unique constellation of flavors.
      <br><br>
      Every dish on our menu is crafted with the same devotion — local ingredients, global technique, and a sprinkle of the unexpected.
    </p>
    <div class="about-stats reveal reveal-delay-3">
      <div>
        <div class="stat-num">40+</div>
        <div class="stat-label">Menu Items</div>
      </div>
      <div>
        <div class="stat-num">12</div>
        <div class="stat-label">Bean Origins</div>
      </div>
      <div>
        <div class="stat-num">5★</div>
        <div class="stat-label">Rated</div>
      </div>
    </div>
  </div>
</section>

<!-- Menu -->
<section id="menu">
  <div class="menu-header">
    <div class="section-label reveal">What We Serve</div>
    <h2 class="section-title reveal reveal-delay-1">Crafted with <em>Intention</em></h2>
  </div>

  <div class="menu-tabs reveal">
    <button class="tab-btn active" onclick="filterMenu('all', this)">All</button>
    <button class="tab-btn" onclick="filterMenu('coffee', this)">Coffee</button>
    <button class="tab-btn" onclick="filterMenu('food', this)">Food</button>
    <button class="tab-btn" onclick="filterMenu('cold', this)">Cold Drinks</button>
  </div>

  <div class="menu-grid" id="menuGrid">
    <div class="menu-item reveal" data-cat="coffee">
      <div class="menu-num">01</div>
      <div class="menu-cat">Espresso</div>
      <div class="menu-name">Planet Signature Latte</div>
      <div class="menu-desc">Our house blend with velvety steamed milk, a whisper of cardamom, and salted caramel swirl.</div>
      <div class="menu-price">KSh 380</div>
    </div>
    <div class="menu-item reveal reveal-delay-1" data-cat="coffee">
      <div class="menu-num">02</div>
      <div class="menu-cat">Pour Over</div>
      <div class="menu-name">Ethiopian Yirgacheffe</div>
      <div class="menu-desc">Bright and floral. Notes of jasmine, bergamot, and dark berry. Brewed to order over 4 minutes.</div>
      <div class="menu-price">KSh 450</div>
    </div>
    <div class="menu-item reveal reveal-delay-2" data-cat="cold">
      <div class="menu-num">03</div>
      <div class="menu-cat">Cold Brew</div>
      <div class="menu-name">Midnight Cold Brew</div>
      <div class="menu-desc">24-hour steeped, double-strength cold brew served over crystal ice. Smooth, dark, unapologetic.</div>
      <div class="menu-price">KSh 420</div>
    </div>
    <div class="menu-item reveal" data-cat="food">
      <div class="menu-num">04</div>
      <div class="menu-cat">All-Day Breakfast</div>
      <div class="menu-name">Avocado on Dark Rye</div>
      <div class="menu-desc">House-whipped avocado, sumac, pickled red onion, and a slow-poached egg on thick Kenyan rye.</div>
      <div class="menu-price">KSh 650</div>
    </div>
    <div class="menu-item reveal reveal-delay-1" data-cat="food">
      <div class="menu-num">05</div>
      <div class="menu-cat">Mains</div>
      <div class="menu-name">Coastal Pilau Bowl</div>
      <div class="menu-desc">Slow-spiced pilau rice, grilled coastal tilapia, coconut-lime drizzle, and crispy shallots.</div>
      <div class="menu-price">KSh 920</div>
    </div>
    <div class="menu-item reveal reveal-delay-2" data-cat="cold">
      <div class="menu-num">06</div>
      <div class="menu-cat">Fruit & Tea</div>
      <div class="menu-name">Hibiscus Solar Storm</div>
      <div class="menu-desc">Iced hibiscus tea with ginger, honey, and sparkling water. A sunset in a glass.</div>
      <div class="menu-price">KSh 320</div>
    </div>
  </div>
</section>

<!-- Experience -->
<section id="experience">
  <div class="exp-text">
    <div class="section-label reveal">Why Butiki</div>
    <h2 class="section-title reveal reveal-delay-1">A World <em>Beyond</em><br>the Ordinary</h2>
    <div class="exp-features reveal reveal-delay-2">
      <div class="exp-feature">
        <div class="feature-icon">✦</div>
        <div>
          <div class="feature-title">Single-Origin Sourcing</div>
          <div class="feature-desc">Every bean traced directly to its farm. We visit, we taste, we choose with intention and respect for the grower.</div>
        </div>
      </div>
      <div class="exp-feature">
        <div class="feature-icon">⬡</div>
        <div>
          <div class="feature-title">Expert Baristas</div>
          <div class="feature-desc">Our baristas are trained to championship standard. Your cup is a craft, not a routine.</div>
        </div>
      </div>
      <div class="exp-feature">
        <div class="feature-icon">◈</div>
        <div>
          <div class="feature-title">The Atmosphere</div>
          <div class="feature-desc">Designed for lingering — warm lighting, curated sound, and a space that feels like it belongs to you.</div>
        </div>
      </div>
    </div>
  </div>
  <div class="exp-visual reveal">
    <div class="exp-card">
      <div class="exp-card-emoji">☕</div>
      <div class="exp-card-label">Espresso Bar</div>
    </div>
    <div class="exp-card">
      <div class="exp-card-emoji">🌿</div>
      <div class="exp-card-label">Garden Seating</div>
    </div>
    <div class="exp-card">
      <div class="exp-card-emoji">🎵</div>
      <div class="exp-card-label">Live Music</div>
    </div>
    <div class="exp-card">
      <div class="exp-card-emoji">🛖</div>
      <div class="exp-card-label">Private Events</div>
    </div>
  </div>
</section>

<!-- Testimonials -->
<section id="testimonials">
  <div class="testimonials-header">
    <div class="section-label reveal">Word on the Street</div>
    <h2 class="section-title reveal reveal-delay-1">Guests <em>Rave</em> About Us</h2>
  </div>
  <div class="testimonials-grid">
    <div class="testimonial reveal">
      <div class="quote-mark">"</div>
      <div class="stars-rating">★★★★★</div>
      <div class="testimonial-text">The Planet Signature Latte completely changed how I think about coffee in Mombasa. The space feels like stepping into another world.</div>
      <div class="testimonial-author">— Amina K., Regular</div>
    </div>
    <div class="testimonial reveal reveal-delay-1">
      <div class="quote-mark">"</div>
      <div class="stars-rating">★★★★★</div>
      <div class="testimonial-text">I've never had a cold brew quite like the Midnight. It's serious coffee. And the Coastal Pilau Bowl? Absolute perfection every single time.</div>
      <div class="testimonial-author">— Brian O., Food Critic</div>
    </div>
    <div class="testimonial reveal reveal-delay-2">
      <div class="quote-mark">"</div>
      <div class="stars-rating">★★★★★</div>
      <div class="testimonial-text">Butiki Planet is where I come for every important meeting, date, and solo work session. Unmatched vibes, unmatched coffee.</div>
      <div class="testimonial-author">— Safia M., Entrepreneur</div>
    </div>
  </div>
</section>

<!-- Reserve -->
<section id="reserve">
  <div class="section-label reveal" style="justify-content:center;">Reserve</div>
  <h2 class="reserve-title reveal reveal-delay-1">
    Secure Your<br><em>Orbit</em>
  </h2>
  <p class="reserve-sub reveal reveal-delay-2">
    Reserve a table and let us take care of the rest. Groups, dates, business — we craft every visit to your needs.
  </p>
  <div class="reserve-form reveal reveal-delay-3">
    <input type="tel" class="reserve-input" placeholder="Your phone number">
    <button class="reserve-btn">Reserve Now</button>
  </div>

  <div class="hours-strip reveal">
    <div class="hour-item">
      <div class="hour-day">Mon — Fri</div>
      <div class="hour-time">7:00 AM — 10:00 PM</div>
    </div>
    <div class="hour-item">
      <div class="hour-day">Saturday</div>
      <div class="hour-time">8:00 AM — 11:00 PM</div>
    </div>
    <div class="hour-item">
      <div class="hour-day">Sunday</div>
      <div class="hour-time">9:00 AM — 9:00 PM</div>
    </div>
  </div>
</section>

<!-- Footer -->
<footer>
  <div class="footer-brand">
    <div class="footer-logo">Butiki <span>Planet</span></div>
    <p class="footer-tagline">Coffee & Food for the curious soul. Find us in the heart of Mombasa.</p>
  </div>
  <div>
    <div class="footer-col-title">Navigate</div>
    <ul class="footer-links">
      <li><a href="#about">Our Story</a></li>
      <li><a href="#menu">Menu</a></li>
      <li><a href="#experience">Experience</a></li>
      <li><a href="#reserve">Reserve</a></li>
    </ul>
  </div>
  <div>
    <div class="footer-col-title">Contact</div>
    <ul class="footer-links">
      <li><a href="#">+254 700 000 000</a></li>
      <li><a href="#">hello@butikiplanet.co.ke</a></li>
      <li><a href="#">Mombasa, Kenya</a></li>
    </ul>
  </div>
  <div>
    <div class="footer-col-title">Hours</div>
    <ul class="footer-links">
      <li><a href="#">Mon–Fri: 7am–10pm</a></li>
      <li><a href="#">Sat: 8am–11pm</a></li>
      <li><a href="#">Sun: 9am–9pm</a></li>
    </ul>
  </div>
  <div class="footer-bottom">
    <div class="footer-copy">© 2025 Butiki Planet Coffee & Food. All rights reserved.</div>
    <div class="social-links">
      <a href="#" class="social-link">Instagram</a>
      <a href="#" class="social-link">Facebook</a>
      <a href="#" class="social-link">Twitter</a>
    </div>
  </div>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
  });

  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px'; ring.style.top = ry + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  document.querySelectorAll('a, button, .menu-item, .exp-card').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.width = '20px'; cursor.style.height = '20px';
      ring.style.width = '60px'; ring.style.height = '60px';
      ring.style.opacity = '0.3';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.width = '12px'; cursor.style.height = '12px';
      ring.style.width = '36px'; ring.style.height = '36px';
      ring.style.opacity = '0.5';
    });
  });

  // Generate stars
  const starsContainer = document.getElementById('stars');
  for (let i = 0; i < 150; i++) {
    const s = document.createElement('div');
    s.className = 'star';
    const size = Math.random() * 2 + 0.5;
    const opacity = Math.random() * 0.6 + 0.15;
    s.style.cssText = `
      width:${size}px; height:${size}px;
      left:${Math.random()*100}%;
      top:${Math.random()*100}%;
      --o:${opacity};
      --d:${Math.random()*4+2}s;
      animation-delay:${Math.random()*4}s;
    `;
    starsContainer.appendChild(s);
  }

  // Navbar scroll
  const navbar = document.getElementById('navbar');
  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 80);
  });

  // Scroll reveal
  const revealEls = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); } });
  }, { threshold: 0.1 });
  revealEls.forEach(el => observer.observe(el));

  // Menu filter
  function filterMenu(cat, btn) {
    document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    document.querySelectorAll('.menu-item').forEach(item => {
      if (cat === 'all' || item.dataset.cat === cat) {
        item.style.display = '';
      } else {
        item.style.display = 'none';
      }
    });
  }

  // Reserve button feedback
  document.querySelector('.reserve-btn').addEventListener('click', function() {
    const input = document.querySelector('.reserve-input');
    const phoneRegex = /^[+]?[(]?[0-9]{3}[)]?[-\s.]?[0-9]{3}[-\s.]?[0-9]{4,6}$/;
    const phoneValue = input.value.trim();
    
    if (!phoneValue) {
      input.style.borderLeft = '2px solid #C9A84C';
      input.focus();
      setTimeout(() => input.style.borderLeft = '', 2000);
      return;
    }
    
    if (!phoneRegex.test(phoneValue)) {
      input.style.borderLeft = '2px solid #D4823A';
      setTimeout(() => input.style.borderLeft = '', 2000);
      return;
    }
    
    this.classList.add('sent');
    const originalText = this.textContent;
    this.textContent = 'Request Sent ✦';
    
    setTimeout(() => {
      this.classList.remove('sent');
      this.textContent = originalText;
      input.value = '';
    }, 3000);
  });
</script>
</body>
</html>
