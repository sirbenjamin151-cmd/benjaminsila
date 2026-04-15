<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Benjamin Sila — Financial Advisor</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">

<style>
/* ═══════════════════════════════════════════
   ROOT VARIABLES & RESET
═══════════════════════════════════════════ */
:root {
  --navy:       #0B1C2C;
  --navy-mid:   #122336;
  --navy-light: #1a3048;
  --gold:       #C9A14A;
  --gold-light: #dbb96a;
  --gold-dim:   #a07c32;
  --white:      #FFFFFF;
  --off-white:  #F5F2ED;
  --text-muted: #8a9aaa;
  --text-dim:   #c5cdd6;
  --serif:      'Cormorant Garamond', Georgia, serif;
  --sans:       'DM Sans', system-ui, sans-serif;
  --transition: 0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; font-size: 16px; }

body {
  background: var(--navy);
  color: var(--white);
  font-family: var(--sans);
  font-weight: 300;
  line-height: 1.7;
  overflow-x: hidden;
}

/* ═══════════════════════════════════════════
   SCROLLBAR
═══════════════════════════════════════════ */
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: var(--navy); }
::-webkit-scrollbar-thumb { background: var(--gold-dim); border-radius: 2px; }

/* ═══════════════════════════════════════════
   CURSOR DOT
═══════════════════════════════════════════ */
.cursor {
  width: 8px; height: 8px;
  background: var(--gold);
  border-radius: 50%;
  position: fixed;
  pointer-events: none;
  z-index: 9999;
  transform: translate(-50%, -50%);
  transition: transform 0.1s, width 0.3s, height 0.3s, opacity 0.3s;
}
.cursor-ring {
  width: 36px; height: 36px;
  border: 1px solid rgba(201, 161, 74, 0.5);
  border-radius: 50%;
  position: fixed;
  pointer-events: none;
  z-index: 9998;
  transform: translate(-50%, -50%);
  transition: transform 0.15s ease-out, width 0.4s, height 0.4s, opacity 0.3s;
}

/* ═══════════════════════════════════════════
   NOISE TEXTURE OVERLAY
═══════════════════════════════════════════ */
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none;
  z-index: 1;
  opacity: 0.6;
}

/* ═══════════════════════════════════════════
   NAVIGATION
═══════════════════════════════════════════ */
nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  padding: 1.5rem 5%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: background var(--transition), padding var(--transition);
}

nav.scrolled {
  background: rgba(11, 28, 44, 0.95);
  backdrop-filter: blur(20px);
  padding: 1rem 5%;
  border-bottom: 1px solid rgba(201, 161, 74, 0.15);
}

.nav-logo {
  font-family: var(--serif);
  font-size: 1.3rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  color: var(--white);
  text-decoration: none;
}

.nav-logo span { color: var(--gold); }

.nav-links {
  display: flex;
  gap: 2.5rem;
  list-style: none;
}

.nav-links a {
  font-size: 0.78rem;
  font-weight: 400;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--text-dim);
  text-decoration: none;
  transition: color var(--transition);
  position: relative;
}

.nav-links a::after {
  content: '';
  position: absolute;
  bottom: -4px; left: 0;
  width: 0; height: 1px;
  background: var(--gold);
  transition: width var(--transition);
}

.nav-links a:hover { color: var(--gold); }
.nav-links a:hover::after { width: 100%; }

.nav-cta {
  font-size: 0.75rem;
  font-weight: 400;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--gold);
  border: 1px solid rgba(201, 161, 74, 0.5);
  padding: 0.55rem 1.4rem;
  text-decoration: none;
  transition: all var(--transition);
}

.nav-cta:hover {
  background: var(--gold);
  color: var(--navy);
  border-color: var(--gold);
}

.nav-hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
  padding: 4px;
}

.nav-hamburger span {
  display: block;
  width: 24px; height: 1.5px;
  background: var(--white);
  transition: all var(--transition);
}

/* ═══════════════════════════════════════════
   HERO SECTION
═══════════════════════════════════════════ */
#hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  position: relative;
  overflow: hidden;
  padding: 10rem 5% 6rem;
}

/* Geometric background lines */
.hero-lines {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.hero-lines::before {
  content: '';
  position: absolute;
  top: -20%; right: -10%;
  width: 60vw; height: 60vw;
  border: 1px solid rgba(201, 161, 74, 0.07);
  border-radius: 50%;
  transform: rotate(15deg);
}

.hero-lines::after {
  content: '';
  position: absolute;
  top: 5%; right: -5%;
  width: 40vw; height: 40vw;
  border: 1px solid rgba(201, 161, 74, 0.05);
  border-radius: 50%;
}

.hero-grid-line {
  position: absolute;
  background: rgba(201, 161, 74, 0.06);
}

.hero-grid-line:nth-child(1) { left: 33%; top: 0; width: 1px; height: 100%; }
.hero-grid-line:nth-child(2) { left: 66%; top: 0; width: 1px; height: 100%; }
.hero-grid-line:nth-child(3) { top: 50%; left: 0; height: 1px; width: 100%; }

.hero-content {
  position: relative;
  z-index: 2;
  max-width: 780px;
}

.hero-eyebrow {
  font-size: 0.72rem;
  font-weight: 400;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: var(--gold);
  margin-bottom: 1.8rem;
  opacity: 0;
  animation: fadeUp 1s 0.3s forwards;
}

.hero-eyebrow::before {
  content: '';
  display: inline-block;
  width: 32px; height: 1px;
  background: var(--gold);
  vertical-align: middle;
  margin-right: 1rem;
}

.hero-headline {
  font-family: var(--serif);
  font-size: clamp(2.8rem, 6vw, 5.2rem);
  font-weight: 300;
  line-height: 1.12;
  letter-spacing: -0.01em;
  color: var(--white);
  margin-bottom: 2rem;
  opacity: 0;
  animation: fadeUp 1s 0.5s forwards;
}

.hero-headline em {
  font-style: italic;
  color: var(--gold);
}

.hero-sub {
  font-size: 1.05rem;
  font-weight: 300;
  color: var(--text-dim);
  max-width: 560px;
  line-height: 1.8;
  margin-bottom: 3rem;
  opacity: 0;
  animation: fadeUp 1s 0.7s forwards;
}

.hero-buttons {
  display: flex;
  gap: 1.2rem;
  flex-wrap: wrap;
  opacity: 0;
  animation: fadeUp 1s 0.9s forwards;
}

.btn-primary {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  background: var(--gold);
  color: var(--navy);
  font-family: var(--sans);
  font-size: 0.78rem;
  font-weight: 500;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  text-decoration: none;
  padding: 1rem 2.2rem;
  transition: all var(--transition);
  position: relative;
  overflow: hidden;
}

.btn-primary::before {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--gold-light);
  transform: scaleX(0);
  transform-origin: left;
  transition: transform var(--transition);
}

.btn-primary:hover::before { transform: scaleX(1); }
.btn-primary span { position: relative; z-index: 1; }

.btn-primary:hover {
  box-shadow: 0 12px 40px rgba(201, 161, 74, 0.35);
  transform: translateY(-2px);
}

.btn-secondary {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  background: transparent;
  color: var(--white);
  font-family: var(--sans);
  font-size: 0.78rem;
  font-weight: 400;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  text-decoration: none;
  padding: 1rem 2.2rem;
  border: 1px solid rgba(255,255,255,0.2);
  transition: all var(--transition);
}

.btn-secondary:hover {
  border-color: var(--gold);
  color: var(--gold);
  transform: translateY(-2px);
}

/* WhatsApp icon */
.wa-icon { font-size: 1rem; }

.hero-scroll-hint {
  position: absolute;
  bottom: 2.5rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  color: var(--text-muted);
  font-size: 0.65rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  opacity: 0;
  animation: fadeIn 1s 1.4s forwards;
}

.scroll-line {
  width: 1px;
  height: 48px;
  background: linear-gradient(to bottom, var(--gold), transparent);
  animation: scrollPulse 2s ease-in-out infinite;
}

/* Hero right: decorative stat card */
.hero-stat-panel {
  position: absolute;
  right: 8%;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  opacity: 0;
  animation: fadeLeft 1s 1.1s forwards;
  z-index: 2;
}

.hero-stat {
  border-left: 2px solid var(--gold);
  padding: 0.6rem 1.4rem;
  background: rgba(201, 161, 74, 0.04);
}

.hero-stat-num {
  font-family: var(--serif);
  font-size: 2.2rem;
  font-weight: 300;
  color: var(--gold);
  line-height: 1;
}

.hero-stat-label {
  font-size: 0.7rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--text-muted);
  margin-top: 0.2rem;
}

/* ═══════════════════════════════════════════
   SECTION COMMONS
═══════════════════════════════════════════ */
section { padding: 8rem 5%; position: relative; z-index: 2; }

.section-tag {
  font-size: 0.7rem;
  font-weight: 400;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: var(--gold);
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.section-tag::before {
  content: '';
  display: block;
  width: 24px; height: 1px;
  background: var(--gold);
}

.section-title {
  font-family: var(--serif);
  font-size: clamp(2rem, 4vw, 3.4rem);
  font-weight: 300;
  line-height: 1.15;
  color: var(--white);
  margin-bottom: 1.5rem;
}

.section-title em {
  font-style: italic;
  color: var(--gold);
}

/* reveal on scroll */
.reveal {
  opacity: 0;
  transform: translateY(32px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}

.reveal-delay-1 { transition-delay: 0.1s; }
.reveal-delay-2 { transition-delay: 0.2s; }
.reveal-delay-3 { transition-delay: 0.3s; }
.reveal-delay-4 { transition-delay: 0.4s; }

/* ═══════════════════════════════════════════
   ABOUT SECTION
═══════════════════════════════════════════ */
#about {
  background: linear-gradient(135deg, var(--navy-mid) 0%, var(--navy) 100%);
}

.about-inner {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 6rem;
  align-items: start;
  max-width: 1200px;
  margin: 0 auto;
}

.about-left { position: sticky; top: 8rem; }

.about-portrait {
  width: 100%;
  max-width: 320px;
  aspect-ratio: 3/4;
  background: var(--navy-light);
  position: relative;
  overflow: hidden;
  margin-bottom: 2rem;
}

.about-portrait img {
  position: absolute;
  top: 50%;
  left: 50%;
  width: auto;
  height: auto;
  max-width: 100%;
  max-height: 100%;
  transform: translate(-50%, -50%);
  display: block;
  object-fit: cover;
}

.about-portrait-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, var(--navy-light), var(--navy-mid));
  font-family: var(--serif);
  font-size: 5rem;
  font-weight: 300;
  color: rgba(201, 161, 74, 0.3);
  letter-spacing: 0.1em;
}

.about-portrait::after {
  content: '';
  position: absolute;
  inset: 0;
  border: 1px solid rgba(201, 161, 74, 0.2);
  pointer-events: none;
}

.about-portrait-corner {
  position: absolute;
  width: 24px; height: 24px;
  border-color: var(--gold);
  border-style: solid;
}

.about-portrait-corner:nth-child(2) { top: -1px; left: -1px; border-width: 2px 0 0 2px; }
.about-portrait-corner:nth-child(3) { top: -1px; right: -1px; border-width: 2px 2px 0 0; }
.about-portrait-corner:nth-child(4) { bottom: -1px; left: -1px; border-width: 0 0 2px 2px; }
.about-portrait-corner:nth-child(5) { bottom: -1px; right: -1px; border-width: 0 2px 2px 0; }

.about-credentials {
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}

.credential-item {
  font-size: 0.72rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--text-muted);
  padding: 0.5rem 0;
  border-bottom: 1px solid rgba(255,255,255,0.06);
  display: flex;
  align-items: center;
  gap: 0.6rem;
}

.credential-item::before {
  content: '';
  width: 4px; height: 4px;
  background: var(--gold);
  border-radius: 50%;
  flex-shrink: 0;
}

.about-body p {
  font-size: 1.05rem;
  color: var(--text-dim);
  line-height: 1.9;
  margin-bottom: 1.4rem;
}

.about-body p:first-of-type {
  font-family: var(--serif);
  font-size: 1.4rem;
  font-weight: 300;
  color: var(--white);
  line-height: 1.6;
}

.about-divider {
  width: 48px;
  height: 1px;
  background: var(--gold);
  margin: 2.5rem 0;
}

/* ═══════════════════════════════════════════
   SERVICES SECTION
═══════════════════════════════════════════ */
#services { background: var(--navy); }

.services-header {
  max-width: 600px;
  margin: 0 auto 5rem;
  text-align: center;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5px;
  max-width: 1200px;
  margin: 0 auto;
  background: rgba(201, 161, 74, 0.12);
}

.service-card {
  background: var(--navy);
  padding: 3rem 2.5rem;
  position: relative;
  overflow: hidden;
  cursor: default;
  transition: background var(--transition);
}

.service-card::before {
  content: '';
  position: absolute;
  bottom: 0; left: 0;
  width: 100%; height: 2px;
  background: var(--gold);
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.service-card:hover { background: var(--navy-light); }
.service-card:hover::before { transform: scaleX(1); }

.service-num {
  font-family: var(--serif);
  font-size: 3.5rem;
  font-weight: 300;
  color: rgba(201, 161, 74, 0.12);
  line-height: 1;
  margin-bottom: 1.5rem;
  transition: color var(--transition);
}

.service-card:hover .service-num { color: rgba(201, 161, 74, 0.25); }

.service-icon {
  width: 44px; height: 44px;
  border: 1px solid rgba(201, 161, 74, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1.5rem;
  font-size: 1.1rem;
  color: var(--gold);
  transition: all var(--transition);
}

.service-card:hover .service-icon {
  background: var(--gold);
  color: var(--navy);
  border-color: var(--gold);
}

.service-title {
  font-family: var(--serif);
  font-size: 1.5rem;
  font-weight: 400;
  color: var(--white);
  line-height: 1.3;
  margin-bottom: 1rem;
}

.service-desc {
  font-size: 0.9rem;
  color: var(--text-muted);
  line-height: 1.8;
}

.service-arrow {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.72rem;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--gold);
  margin-top: 1.8rem;
  opacity: 0;
  transform: translateX(-8px);
  transition: all var(--transition);
}

.service-card:hover .service-arrow {
  opacity: 1;
  transform: translateX(0);
}

/* ═══════════════════════════════════════════
   WHY ME SECTION
═══════════════════════════════════════════ */
#why {
  background: var(--off-white);
  color: var(--navy);
}

#why .section-tag { color: var(--gold-dim); }
#why .section-tag::before { background: var(--gold-dim); }
#why .section-title { color: var(--navy); }

.why-inner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 6rem;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
}

.why-pillars {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2px;
  background: rgba(11, 28, 44, 0.1);
}

.pillar {
  background: var(--off-white);
  padding: 2.5rem 2rem;
  transition: background var(--transition);
}

.pillar:hover { background: white; }

.pillar-icon {
  font-size: 1.5rem;
  margin-bottom: 1.2rem;
  display: block;
}

.pillar-title {
  font-family: var(--serif);
  font-size: 1.2rem;
  font-weight: 500;
  color: var(--navy);
  margin-bottom: 0.6rem;
}

.pillar-desc {
  font-size: 0.88rem;
  color: #5a6a7a;
  line-height: 1.7;
}

.why-statement {
  padding-left: 2rem;
  border-left: 2px solid var(--gold);
}

.why-quote {
  font-family: var(--serif);
  font-size: clamp(1.4rem, 2.5vw, 2rem);
  font-weight: 300;
  color: var(--navy);
  line-height: 1.5;
  font-style: italic;
  margin-bottom: 2rem;
}

.why-quote strong {
  font-style: normal;
  font-weight: 600;
  color: var(--gold-dim);
}

.why-signature {
  font-family: var(--serif);
  font-size: 1.1rem;
  font-style: italic;
  color: var(--navy);
  opacity: 0.6;
}

/* ═══════════════════════════════════════════
   EXPERIENCE SECTION
═══════════════════════════════════════════ */
#experience { background: var(--navy-mid); }

.exp-inner {
  max-width: 900px;
  margin: 0 auto;
}

.exp-header { margin-bottom: 4rem; }

.timeline {
  position: relative;
  padding-left: 2rem;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 0; top: 0; bottom: 0;
  width: 1px;
  background: linear-gradient(to bottom, var(--gold), transparent);
}

.timeline-item {
  position: relative;
  padding: 0 0 3.5rem 2.5rem;
}

.timeline-item::before {
  content: '';
  position: absolute;
  left: -4px; top: 6px;
  width: 9px; height: 9px;
  border: 1px solid var(--gold);
  background: var(--navy-mid);
  border-radius: 50%;
  transition: background var(--transition);
}

.timeline-item:hover::before { background: var(--gold); }

.timeline-tag {
  font-size: 0.68rem;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--gold);
  margin-bottom: 0.5rem;
}

.timeline-title {
  font-family: var(--serif);
  font-size: 1.5rem;
  font-weight: 400;
  color: var(--white);
  margin-bottom: 0.8rem;
  line-height: 1.3;
}

.timeline-body {
  font-size: 0.92rem;
  color: var(--text-muted);
  line-height: 1.8;
  max-width: 600px;
}

/* ═══════════════════════════════════════════
   TESTIMONIALS SECTION
═══════════════════════════════════════════ */
#testimonials { background: var(--navy); }

.test-header {
  max-width: 500px;
  margin-bottom: 4rem;
}

.test-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 1.5rem;
  max-width: 1200px;
}

.test-card {
  border: 1px solid rgba(201, 161, 74, 0.15);
  padding: 2.8rem;
  position: relative;
  transition: border-color var(--transition), transform var(--transition);
  background: rgba(201, 161, 74, 0.02);
}

.test-card:hover {
  border-color: rgba(201, 161, 74, 0.4);
  transform: translateY(-4px);
}

.test-quote-mark {
  font-family: var(--serif);
  font-size: 5rem;
  line-height: 1;
  color: var(--gold);
  opacity: 0.2;
  position: absolute;
  top: 1.5rem; left: 2rem;
  user-select: none;
}

.test-body {
  font-family: var(--serif);
  font-size: 1.08rem;
  font-style: italic;
  color: var(--text-dim);
  line-height: 1.8;
  margin-bottom: 2rem;
  position: relative;
  z-index: 1;
}

.test-author {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.test-avatar {
  width: 44px; height: 44px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--gold-dim), var(--navy-light));
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--serif);
  font-size: 1rem;
  color: var(--white);
  flex-shrink: 0;
}

.test-name {
  font-weight: 500;
  font-size: 0.92rem;
  color: var(--white);
}

.test-role {
  font-size: 0.78rem;
  color: var(--text-muted);
  letter-spacing: 0.06em;
}

.test-stars {
  color: var(--gold);
  font-size: 0.7rem;
  letter-spacing: 0.2em;
  margin-top: 0.2rem;
}

/* ═══════════════════════════════════════════
   CONTACT SECTION
═══════════════════════════════════════════ */
#contact {
  background: var(--off-white);
  color: var(--navy);
}

#contact .section-tag { color: var(--gold-dim); }
#contact .section-tag::before { background: var(--gold-dim); }
#contact .section-title { color: var(--navy); }

.contact-inner {
  display: grid;
  grid-template-columns: 1fr 1.3fr;
  gap: 6rem;
  max-width: 1100px;
  margin: 0 auto;
  align-items: start;
}

.contact-info p {
  font-size: 1rem;
  color: #4a5a6a;
  line-height: 1.8;
  margin-bottom: 2.5rem;
}

.contact-detail {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  margin-bottom: 1.4rem;
}

.contact-detail-icon {
  width: 36px; height: 36px;
  border: 1px solid rgba(11,28,44,0.15);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.9rem;
  color: var(--gold-dim);
  flex-shrink: 0;
  transition: all var(--transition);
}

.contact-detail:hover .contact-detail-icon {
  background: var(--gold-dim);
  color: var(--white);
  border-color: var(--gold-dim);
}

.contact-detail-text label {
  display: block;
  font-size: 0.68rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: #8a9aaa;
  margin-bottom: 0.15rem;
}

.contact-detail-text span {
  font-size: 0.95rem;
  color: var(--navy);
}

/* Form */
.contact-form { display: flex; flex-direction: column; gap: 1.2rem; }

.form-group { display: flex; flex-direction: column; gap: 0.5rem; }

.form-group label {
  font-size: 0.7rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: #6a7a8a;
}

.form-group input,
.form-group textarea {
  background: white;
  border: 1px solid rgba(11,28,44,0.15);
  padding: 0.9rem 1.2rem;
  font-family: var(--sans);
  font-size: 0.95rem;
  color: var(--navy);
  outline: none;
  transition: border-color var(--transition);
  resize: none;
  width: 100%;
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: var(--gold-dim);
}

.form-group textarea { height: 130px; }

.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 1.2rem; }

.btn-submit {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  background: var(--navy);
  color: var(--white);
  font-family: var(--sans);
  font-size: 0.78rem;
  font-weight: 400;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  border: none;
  padding: 1.1rem 2.5rem;
  cursor: pointer;
  transition: all var(--transition);
  align-self: flex-start;
  position: relative;
  overflow: hidden;
}

.btn-submit::before {
  content: '';
  position: absolute;
  inset: 0;
  background: var(--gold-dim);
  transform: scaleX(0);
  transform-origin: left;
  transition: transform var(--transition);
}

.btn-submit:hover::before { transform: scaleX(1); }
.btn-submit span { position: relative; z-index: 1; }
.btn-submit:hover { transform: translateY(-2px); box-shadow: 0 10px 30px rgba(11,28,44,0.25); }

/* ═══════════════════════════════════════════
   FOOTER
═══════════════════════════════════════════ */
footer {
  background: var(--navy);
  border-top: 1px solid rgba(201, 161, 74, 0.12);
  padding: 2.5rem 5%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
  z-index: 2;
}

.footer-logo {
  font-family: var(--serif);
  font-size: 1.1rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  color: var(--white);
}

.footer-logo span { color: var(--gold); }

.footer-copy {
  font-size: 0.75rem;
  color: var(--text-muted);
  letter-spacing: 0.08em;
}

.footer-links {
  display: flex;
  gap: 2rem;
}

.footer-links a {
  font-size: 0.72rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--text-muted);
  text-decoration: none;
  transition: color var(--transition);
}

.footer-links a:hover { color: var(--gold); }

/* ═══════════════════════════════════════════
   ANIMATIONS
═══════════════════════════════════════════ */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}

@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}

@keyframes fadeLeft {
  from { opacity: 0; transform: translate(24px, -50%); }
  to   { opacity: 1; transform: translate(0, -50%); }
}

@keyframes scrollPulse {
  0%, 100% { opacity: 1; }
  50%       { opacity: 0.3; }
}

/* ═══════════════════════════════════════════
   MOBILE NAV OVERLAY
═══════════════════════════════════════════ */
.mobile-nav {
  position: fixed;
  inset: 0;
  background: var(--navy);
  z-index: 99;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 2.5rem;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.4s ease;
}

.mobile-nav.open {
  opacity: 1;
  pointer-events: all;
}

.mobile-nav a {
  font-family: var(--serif);
  font-size: 2.2rem;
  font-weight: 300;
  color: var(--white);
  text-decoration: none;
  letter-spacing: 0.04em;
  transition: color var(--transition);
}

.mobile-nav a:hover { color: var(--gold); }

.nav-close {
  position: absolute;
  top: 2rem; right: 5%;
  font-size: 1.5rem;
  color: var(--white);
  cursor: pointer;
  background: none;
  border: none;
  color: var(--text-dim);
  transition: color var(--transition);
}

.nav-close:hover { color: var(--gold); }

/* ═══════════════════════════════════════════
   RESPONSIVE
═══════════════════════════════════════════ */
@media (max-width: 1024px) {
  .hero-stat-panel { display: none; }
  .about-inner { grid-template-columns: 1fr; gap: 3rem; }
  .about-left { position: static; }
  .about-portrait { max-width: 320px; }
  .why-inner { grid-template-columns: 1fr; gap: 3rem; }
  .contact-inner { grid-template-columns: 1fr; gap: 3rem; }
}

@media (max-width: 768px) {
  .nav-links, .nav-cta { display: none; }
  .nav-hamburger { display: flex; }
  section { padding: 5rem 6%; }
  .why-pillars { grid-template-columns: 1fr; }
  .form-row { grid-template-columns: 1fr; }
  footer { flex-direction: column; gap: 1rem; text-align: center; }
  .footer-links { gap: 1.2rem; }
  .cursor, .cursor-ring { display: none; }
}

@media (max-width: 480px) {
  .hero-buttons { flex-direction: column; }
  .btn-primary, .btn-secondary { justify-content: center; }
}
</style>
</head>

<body>

<!-- Custom cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- Mobile nav overlay -->
<div class="mobile-nav" id="mobileNav">
  <button class="nav-close" onclick="toggleMobileNav()">✕</button>
  <a href="#about"        onclick="toggleMobileNav()">About</a>
  <a href="#services"     onclick="toggleMobileNav()">Services</a>
  <a href="#experience"   onclick="toggleMobileNav()">Experience</a>
  <a href="#testimonials" onclick="toggleMobileNav()">Testimonials</a>
  <a href="#contact"      onclick="toggleMobileNav()">Contact</a>
</div>

<!-- ═══════════════════════════════ NAVIGATION ═══ -->
<nav id="mainNav">
  <a href="#hero" class="nav-logo">Benjamin<span>.</span>Sila</a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#services">Services</a></li>
    <li><a href="#experience">Experience</a></li>
    <li><a href="#testimonials">Testimonials</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <a href="#contact" class="nav-cta">Private Consultation</a>
  <div class="nav-hamburger" onclick="toggleMobileNav()">
    <span></span><span></span><span></span>
  </div>
</nav>

<!-- ═══════════════════════════════ HERO ═══════════ -->
<section id="hero">
  <div class="hero-lines">
    <div class="hero-grid-line"></div>
    <div class="hero-grid-line"></div>
    <div class="hero-grid-line"></div>
  </div>

  <div class="hero-content">
    <p class="hero-eyebrow">Financial Advisor · Nairobi, Kenya</p>

    <h1 class="hero-headline">
      Strategic Wealth.<br>
      Structured <em>Protection.</em><br>
      Lasting Legacy.
    </h1>

    <p class="hero-sub">
      I advise individuals and families on preserving, growing, and transferring wealth through tailored financial decisions and solutions grounded in data forecasting and precision.
    </p>

    <div class="hero-buttons">
      <a href="#contact" class="btn-primary">
        <span>Schedule a Private Consultation</span>
        <span>→</span>
      </a>
      <a href="https://wa.me/254768275003" target="_blank" class="btn-secondary">
        <span class="wa-icon">✆</span>
        <span>Chat on WhatsApp</span>
      </a>
    </div>
  </div>

  <!-- Floating stat cards -->
  <div class="hero-stat-panel">
    <div class="hero-stat">
      <div class="hero-stat-num">5+</div>
      <div class="hero-stat-label">Years of Practice</div>
    </div>
    <div class="hero-stat">
      <div class="hero-stat-num">200+</div>
      <div class="hero-stat-label">Clients Advised</div>
    </div>
    <div class="hero-stat">
      <div class="hero-stat-num">100%</div>
      <div class="hero-stat-label">Data-Driven Approach</div>
    </div>
  </div>

  <div class="hero-scroll-hint">
    <div class="scroll-line"></div>
    <span>Scroll</span>
  </div>
</section>

<!-- ═══════════════════════════════ ABOUT ══════════ -->
<section id="about">
  <div class="about-inner">

    <div class="about-left reveal">
      <div class="about-portrait">
        <img src="1772628565973 (1).jpg" alt="Portrait of Benjamin Sila">
        <div class="about-portrait-corner"></div>
        <div class="about-portrait-corner"></div>
        <div class="about-portrait-corner"></div>
        <div class="about-portrait-corner"></div>
      </div>
      <div class="about-credentials">
        <div class="credential-item">Actuarial Science</div>
        <div class="credential-item">Advanced Data Analytics</div>
        <div class="credential-item">SPSS · STATA · R · Excel</div>
        <div class="credential-item">Nairobi, Kenya</div>
      </div>
    </div>

    <div class="about-body">
      <p class="section-tag reveal">Who I Am</p>
      <h2 class="section-title reveal reveal-delay-1">
        A Precision Approach<br>to <em>Wealth Advisory</em>
      </h2>

      <div class="about-divider reveal reveal-delay-2"></div>

      <p class="reveal reveal-delay-2">
        I'm a Financial Advisor specializing in delivering sophisticated, data-driven financial solutions for individuals and families seeking both long-term wealth security and short-term financial goals.
      </p>
      <p class="reveal reveal-delay-3">
        With a strong foundation and experience in financial planning and advanced data analytics, I bring a refined, analytical approach to financial planning — leveraging tools to assess risk, interpret market trends, and design precision-tailored strategies.
      </p>
      <p class="reveal reveal-delay-3">
        My advisory approach is built on clarity, discretion, and performance. I work closely with clients to structure intelligent insurance, savings, and investment solutions that not only protect wealth but also protect the financial position of their loved ones — while positioning it for sustainable growth.
      </p>
      <p class="reveal reveal-delay-4">
        I am committed to providing a premium, personalized experience — where every financial decision is informed, intentional, and aligned with long-term success.
      </p>
    </div>

  </div>
</section>

<!-- ═══════════════════════════════ SERVICES ════════ -->
<section id="services">
  <div class="services-header reveal">
    <p class="section-tag">What I Offer</p>
    <h2 class="section-title">Premium <em>Advisory</em><br>Services</h2>
  </div>

  <div class="services-grid">

    <div class="service-card reveal">
      <div class="service-num">01</div>
      <div class="service-icon">◈</div>
      <h3 class="service-title">Wealth Structuring &amp; Financial Planning</h3>
      <p class="service-desc">Comprehensive, bespoke financial plans designed to consolidate, grow, and protect your assets across every life stage — from accumulation to distribution.</p>
      <div class="service-arrow">Explore ↗</div>
    </div>

    <div class="service-card reveal reveal-delay-1">
      <div class="service-num">02</div>
      <div class="service-icon">⬡</div>
      <h3 class="service-title">Insurance &amp; Risk Advisory</h3>
      <p class="service-desc">Actuarially-grounded risk assessment and insurance structuring to protect against unexpected events — calibrated precisely to your lifestyle and risk profile.</p>
      <div class="service-arrow">Explore ↗</div>
    </div>

    <div class="service-card reveal reveal-delay-2">
      <div class="service-num">03</div>
      <div class="service-icon">△</div>
      <h3 class="service-title">Investment Strategy</h3>
      <p class="service-desc">Data-driven portfolio construction and market analysis tailored to your return objectives, time horizon, and risk tolerance — with precision and discipline.</p>
      <div class="service-arrow">Explore ↗</div>
    </div>

    <div class="service-card reveal reveal-delay-3">
      <div class="service-num">04</div>
      <div class="service-icon">◇</div>
      <h3 class="service-title">Legacy &amp; Future Planning</h3>
      <p class="service-desc">Structured wealth transfer, estate planning, and intergenerational strategies designed to ensure your legacy endures — and grows — beyond your lifetime.</p>
      <div class="service-arrow">Explore ↗</div>
    </div>

  </div>
</section>

<!-- ═══════════════════════════════ WHY ME ══════════ -->
<section id="why">
  <div class="why-inner">

    <div>
      <p class="section-tag reveal">Why Work With Me</p>
      <h2 class="section-title reveal reveal-delay-1">The Principles<br>Behind My <em>Practice</em></h2>
      <div class="why-pillars reveal reveal-delay-2">

        <div class="pillar">
          <span class="pillar-icon">◉</span>
          <div class="pillar-title">Data-Driven Advisory</div>
          <p class="pillar-desc">Every recommendation is backed by rigorous quantitative analysis, not intuition or generic templates.</p>
        </div>

        <div class="pillar">
          <span class="pillar-icon">◎</span>
          <div class="pillar-title">Personalized Strategies</div>
          <p class="pillar-desc">No two clients are alike. Your financial plan is built exclusively around your circumstances and goals.</p>
        </div>

        <div class="pillar">
          <span class="pillar-icon">◈</span>
          <div class="pillar-title">Discreet &amp; Professional</div>
          <p class="pillar-desc">Absolute confidentiality and the highest professional standards guide every client engagement.</p>
        </div>

        <div class="pillar">
          <span class="pillar-icon">△</span>
          <div class="pillar-title">Long-Term Partnership</div>
          <p class="pillar-desc">I invest in your financial journey for the long run — adapting strategies as your life evolves.</p>
        </div>

      </div>
    </div>

    <div class="why-statement reveal reveal-delay-2">
      <blockquote class="why-quote">
        "Wealth is not built by chance. It is <strong>structured with intention</strong>, protected with precision, and transferred with purpose."
      </blockquote>
      <p class="why-signature">— Benjamin Sila</p>
    </div>

  </div>
</section>

<!-- ═══════════════════════════════ EXPERIENCE ══════ -->
<section id="experience">
  <div class="exp-inner">
    <div class="exp-header">
      <p class="section-tag reveal">Professional Background</p>
      <h2 class="section-title reveal reveal-delay-1">Experience &amp;<br><em>Expertise</em></h2>
    </div>

    <div class="timeline">

      <div class="timeline-item reveal">
        <div class="timeline-tag">Core Practice</div>
        <h3 class="timeline-title">Financial Advisory & Wealth Management</h3>
        <p class="timeline-body">Extensive experience guiding high-net-worth individuals and families through complex financial decisions — from insurance architecture to multi-asset investment strategies, retirement planning, and structured savings.</p>
      </div>

      <div class="timeline-item reveal reveal-delay-1">
        <div class="timeline-tag">Technical Expertise</div>
        <h3 class="timeline-title">Advanced Data Analytics</h3>
        <p class="timeline-body">Proficient in SPSS, STATA, R, and advanced Excel modelling — applied to risk quantification, actuarial assessment, market trend analysis, and financial forecasting with statistical rigour.</p>
      </div>

      <div class="timeline-item reveal reveal-delay-2">
        <div class="timeline-tag">Leadership</div>
        <h3 class="timeline-title">Business Management & Team Leadership</h3>
        <p class="timeline-body">Demonstrated experience leading advisory teams and managing client portfolios at scale — combining strategic oversight with hands-on client relationship management across diverse industries.</p>
      </div>

      <div class="timeline-item reveal reveal-delay-3">
        <div class="timeline-tag">Sector Exposure</div>
        <h3 class="timeline-title">Public & International Sector Engagement</h3>
        <p class="timeline-body">Exposure to public sector financial frameworks and international financial markets, bringing a broader macroeconomic perspective to individual and institutional advisory engagements.</p>
      </div>

    </div>
  </div>
</section>

<!-- ═══════════════════════════════ TESTIMONIALS ════ -->
<section id="testimonials">
  <div class="test-header">
    <p class="section-tag reveal">Client Voices</p>
    <h2 class="section-title reveal reveal-delay-1">What Clients<br><em>Say</em></h2>
  </div>

  <div class="test-grid">

    <div class="test-card reveal">
      <div class="test-quote-mark">"</div>
      <p class="test-body">Benjamin transformed the way I think about my finances. His analytical approach gave me a clarity I had never had before — my portfolio is now structured to grow through any market condition.</p>
      <div class="test-author">
        <div class="test-avatar">DM</div>
        <div>
          <div class="test-name">David M.</div>
          <div class="test-role">Business Owner, Nairobi</div>
          <div class="test-stars">★ ★ ★ ★ ★</div>
        </div>
      </div>
    </div>

    <div class="test-card reveal reveal-delay-1">
      <div class="test-quote-mark">"</div>
      <p class="test-body">The level of discretion, professionalism, and genuine care Benjamin brings to every session is exceptional. He doesn't just manage wealth — he builds a relationship that lasts decades.</p>
      <div class="test-author">
        <div class="test-avatar">AN</div>
        <div>
          <div class="test-name">Amina N.</div>
          <div class="test-role">Senior Executive, Mombasa</div>
          <div class="test-stars">★ ★ ★ ★ ★</div>
        </div>
      </div>
    </div>

    <div class="test-card reveal reveal-delay-2">
      <div class="test-quote-mark">"</div>
      <p class="test-body">I came to Benjamin without a clear plan for my family's future. Within months, we had a comprehensive legacy strategy in place. His precision and dedication are truly unmatched in Kenya.</p>
      <div class="test-author">
        <div class="test-avatar">JK</div>
        <div>
          <div class="test-name">James K.</div>
          <div class="test-role">Medical Professional, Kisumu</div>
          <div class="test-stars">★ ★ ★ ★ ★</div>
        </div>
      </div>
    </div>

  </div>
</section>

<!-- ═══════════════════════════════ CONTACT ═════════ -->
<section id="contact">
  <div class="contact-inner">

    <div>
      <p class="section-tag reveal">Get in Touch</p>
      <h2 class="section-title reveal reveal-delay-1">Begin Your<br><em>Private</em> Consultation</h2>
      <p class="reveal reveal-delay-2">Every great financial outcome begins with a single, well-considered conversation. Reach out to schedule a confidential consultation.</p>

      <div class="reveal reveal-delay-3">
        <div class="contact-detail">
          <div class="contact-detail-icon">◉</div>
          <div class="contact-detail-text">
            <label>Location</label>
            <span>Nairobi, Kenya</span>
          </div>
        </div>
        <div class="contact-detail">
          <div class="contact-detail-icon">✆</div>
          <div class="contact-detail-text">
            <label>Phone / WhatsApp</label>
            <span>+254 768 275 003</span>
          </div>
        </div>
        <div class="contact-detail">
          <div class="contact-detail-icon">✉</div>
          <div class="contact-detail-text">
            <label>Email</label>
            <span>sirbenjamin151@gmail.com</span>
          </div>
        </div>
      </div>
    </div>

    <form class="contact-form reveal reveal-delay-2" onsubmit="handleSubmit(event)">
      <div class="form-row">
        <div class="form-group">
          <label>Full Name</label>
          <input type="text" placeholder="Your name" required>
        </div>
        <div class="form-group">
          <label>Email Address</label>
          <input type="email" placeholder="your@email.com" required>
        </div>
      </div>
      <div class="form-group">
        <label>Phone (optional)</label>
        <input type="tel" placeholder="+254 000 000 000">
      </div>
      <div class="form-group">
        <label>Message</label>
        <textarea placeholder="Tell me about your financial goals or questions…" required></textarea>
      </div>
      <button type="submit" class="btn-submit">
        <span>Send Message →</span>
      </button>
      <div id="formSuccess" style="display:none; font-size:0.85rem; color:#3a7a4a; padding:0.8rem 0; letter-spacing:0.06em;">
        ✓ Message sent. I'll be in touch within 24 hours.
      </div>
    </form>

  </div>
</section>

<!-- ═══════════════════════════════ FOOTER ══════════ -->
<footer>
  <div class="footer-logo">Benjamin <span>Sila</span></div>
  <p class="footer-copy">© 2025 Benjamin Sila. All rights reserved.</p>
  <div class="footer-links">
    <a href="#about">About</a>
    <a href="#services">Services</a>
    <a href="#contact">Contact</a>
  </div>
</footer>

<!-- ═══════════════════════════════ JAVASCRIPT ══════ -->
<script>
/* ── Custom cursor ── */
const cursor     = document.getElementById('cursor');
const cursorRing = document.getElementById('cursorRing');
let mouseX = 0, mouseY = 0, ringX = 0, ringY = 0;

document.addEventListener('mousemove', e => {
  mouseX = e.clientX; mouseY = e.clientY;
  cursor.style.left = mouseX + 'px';
  cursor.style.top  = mouseY + 'px';
});

function animateRing() {
  ringX += (mouseX - ringX) * 0.12;
  ringY += (mouseY - ringY) * 0.12;
  cursorRing.style.left = ringX + 'px';
  cursorRing.style.top  = ringY + 'px';
  requestAnimationFrame(animateRing);
}
animateRing();

/* Expand cursor on hover */
document.querySelectorAll('a, button, .service-card, .test-card, .pillar').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.width     = '16px';
    cursor.style.height    = '16px';
    cursorRing.style.width = '56px';
    cursorRing.style.height= '56px';
  });
  el.addEventListener('mouseleave', () => {
    cursor.style.width     = '8px';
    cursor.style.height    = '8px';
    cursorRing.style.width = '36px';
    cursorRing.style.height= '36px';
  });
});

/* ── Sticky nav ── */
const nav = document.getElementById('mainNav');
window.addEventListener('scroll', () => {
  nav.classList.toggle('scrolled', window.scrollY > 60);
});

/* ── Mobile nav ── */
function toggleMobileNav() {
  document.getElementById('mobileNav').classList.toggle('open');
}

/* ── Scroll reveal ── */
const revealEls = document.querySelectorAll('.reveal');
const observer  = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      observer.unobserve(e.target);
    }
  });
}, { threshold: 0.12, rootMargin: '0px 0px -40px 0px' });

revealEls.forEach(el => observer.observe(el));

/* ── Form submit ── */
function handleSubmit(e) {
  e.preventDefault();
  const btn     = e.target.querySelector('.btn-submit');
  const success = document.getElementById('formSuccess');
  btn.disabled  = true;
  btn.querySelector('span').textContent = 'Sending…';
  setTimeout(() => {
    btn.style.display = 'none';
    success.style.display = 'block';
    e.target.reset();
  }, 1200);
}

/* ── Smooth anchor offset (for fixed nav) ── */
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function(e) {
    const target = document.querySelector(this.getAttribute('href'));
    if (target) {
      e.preventDefault();
      const offset = 80;
      const top    = target.getBoundingClientRect().top + window.scrollY - offset;
      window.scrollTo({ top, behavior: 'smooth' });
    }
  });
});
</script>

</body>
</html>
