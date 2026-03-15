# s60162546-spec.github.io
My PixelForge Website
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PIXELFORGE — World-Class Web Design Agency</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=Fraunces:ital,wght@0,300;0,400;0,700;1,300;1,400;1,700&family=JetBrains+Mono:wght@300;400;500&display=swap" rel="stylesheet">

<style>
/* ═══════════════════════════════════════════════════════════
   PIXELFORGE OVERKILL — 5000+ LINES
   Colors: Deep obsidian + electric lime + ghost white + blood orange accent
   Fonts: Syne (geometric sans) + Fraunces (optical serif) + JetBrains Mono
   Effects: Canvas particles, magnetic cursor, split-text, parallax, 3D tilt, 
            typed text, counter, scroll-scrub, ripple, noise overlay, everything
═══════════════════════════════════════════════════════════ */

:root {
  --obsidian: #080b12;
  --deep: #0d1117;
  --surface: #131920;
  --panel: #1a2232;
  --border: rgba(255,255,255,0.07);
  --border-bright: rgba(255,255,255,0.15);
  --lime: #b8ff00;
  --lime-glow: rgba(184,255,0,0.15);
  --lime-dim: #8fcc00;
  --orange: #ff5c00;
  --orange-glow: rgba(255,92,0,0.15);
  --white: #f0eeea;
  --white-60: rgba(240,238,234,0.6);
  --white-30: rgba(240,238,234,0.3);
  --white-10: rgba(240,238,234,0.1);
  --white-05: rgba(240,238,234,0.05);
  --red: #ff3535;
  --shadow-lg: 0 32px 64px rgba(0,0,0,0.6);
  --shadow-xl: 0 60px 120px rgba(0,0,0,0.8);
  --transition: cubic-bezier(0.77, 0, 0.175, 1);
  --spring: cubic-bezier(0.34, 1.56, 0.64, 1);
}

*, *::before, *::after { margin:0; padding:0; box-sizing:border-box; }
html { scroll-behavior: smooth; font-size: 16px; }
body {
  background: var(--obsidian);
  color: var(--white);
  font-family: 'JetBrains Mono', monospace;
  overflow-x: hidden;
  cursor: none;
}

/* ══ SCROLLBAR ══ */
::-webkit-scrollbar { width: 2px; }
::-webkit-scrollbar-track { background: var(--obsidian); }
::-webkit-scrollbar-thumb { background: var(--lime); border-radius: 2px; }

/* ══ SELECTION ══ */
::selection { background: var(--lime); color: var(--obsidian); }

/* ══ NOISE OVERLAY ══ */
body::after {
  content: '';
  position: fixed; inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 512 512' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.05'/%3E%3C/svg%3E");
  pointer-events: none; z-index: 9990; opacity: 0.35;
  mix-blend-mode: overlay;
}

/* ══ PROGRESS BAR ══ */
#progress-bar {
  position: fixed; top: 0; left: 0; height: 2px; z-index: 9999;
  background: linear-gradient(90deg, var(--lime), var(--orange));
  transform-origin: left; transform: scaleX(0);
  will-change: transform;
  box-shadow: 0 0 12px var(--lime), 0 0 24px rgba(184,255,0,0.4);
}

/* ══ CURSOR ══ */
#cursor-dot {
  position: fixed; width: 8px; height: 8px;
  background: var(--lime); border-radius: 50%;
  pointer-events: none; z-index: 99999;
  transform: translate(-50%,-50%);
  transition: width .2s var(--spring), height .2s var(--spring), background .2s;
  will-change: transform;
  box-shadow: 0 0 10px var(--lime), 0 0 20px rgba(184,255,0,0.5);
}
#cursor-ring {
  position: fixed; width: 40px; height: 40px;
  border: 1.5px solid rgba(184,255,0,0.5); border-radius: 50%;
  pointer-events: none; z-index: 99998;
  transform: translate(-50%,-50%);
  will-change: transform;
  transition: width .3s var(--transition), height .3s var(--transition), border-color .3s;
}
#cursor-text {
  position: fixed; pointer-events: none; z-index: 99997;
  font-size: .55rem; letter-spacing: .15em; color: var(--lime);
  transform: translate(-50%,-50%);
  opacity: 0; transition: opacity .2s;
  white-space: nowrap; text-transform: uppercase;
}
body.cursor-hover #cursor-dot { width: 16px; height: 16px; }
body.cursor-hover #cursor-ring { width: 64px; height: 64px; border-color: rgba(184,255,0,0.8); }
body.cursor-link #cursor-dot { background: var(--orange); box-shadow: 0 0 10px var(--orange); width: 12px; height: 12px; }
body.cursor-link #cursor-ring { border-color: rgba(255,92,0,0.6); width: 50px; height: 50px; }

/* ══ CANVAS LAYER ══ */
#particle-canvas {
  position: fixed; inset: 0; z-index: 0;
  pointer-events: none;
}

/* ══ NAV ══ */
nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 1000;
  display: flex; align-items: center; justify-content: space-between;
  padding: 1.5rem 4rem;
  transition: all .5s var(--transition);
}
nav.scrolled {
  background: rgba(8,11,18,0.95);
  backdrop-filter: blur(24px) saturate(180%);
  border-bottom: 1px solid var(--border);
  padding: 1rem 4rem;
  box-shadow: 0 4px 40px rgba(0,0,0,0.4);
}
.nav-logo {
  display: flex; align-items: center; gap: .7rem;
  text-decoration: none;
  position: relative;
}
.nav-logo-mark {
  width: 32px; height: 32px;
  background: var(--lime);
  clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
  animation: rotateMark 8s linear infinite;
  flex-shrink: 0;
}
@keyframes rotateMark {
  0% { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
  25% { clip-path: polygon(50% 5%, 95% 50%, 50% 95%, 5% 50%); }
  50% { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
  75% { clip-path: polygon(45% 0%, 100% 45%, 55% 100%, 0% 55%); }
  100% { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
}
.nav-logo-text {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: 1.15rem; letter-spacing: .08em; color: var(--white);
}
.nav-logo-sub {
  position: absolute; bottom: -1rem; left: 39px;
  font-size: .45rem; letter-spacing: .3em; color: var(--lime);
  text-transform: uppercase; opacity: .7;
}
.nav-links { display: flex; align-items: center; gap: 2.5rem; list-style: none; }
.nav-links a {
  font-size: .62rem; letter-spacing: .18em; text-transform: uppercase;
  color: var(--white-60); text-decoration: none;
  position: relative; padding: .3rem 0;
  transition: color .3s;
}
.nav-links a::after {
  content: ''; position: absolute; bottom: 0; left: 0;
  width: 0; height: 1px; background: var(--lime);
  transition: width .4s var(--transition);
}
.nav-links a:hover { color: var(--white); }
.nav-links a:hover::after { width: 100%; }
.nav-badge {
  font-size: .5rem; letter-spacing: .15em; text-transform: uppercase;
  background: rgba(184,255,0,0.12); color: var(--lime);
  border: 1px solid rgba(184,255,0,0.25);
  padding: .2rem .5rem; border-radius: 2px;
  animation: badgePulse 3s ease-in-out infinite;
}
@keyframes badgePulse {
  0%,100% { box-shadow: 0 0 0 0 rgba(184,255,0,0.2); }
  50% { box-shadow: 0 0 0 4px rgba(184,255,0,0); }
}
.nav-cta {
  font-family: 'Syne', sans-serif; font-weight: 700;
  font-size: .7rem; letter-spacing: .1em; text-transform: uppercase;
  background: var(--lime); color: var(--obsidian);
  padding: .65rem 1.8rem; text-decoration: none; cursor: none;
  position: relative; overflow: hidden;
  transition: transform .2s, box-shadow .3s;
  display: inline-block;
}
.nav-cta::before {
  content: ''; position: absolute; inset: 0;
  background: var(--white);
  transform: scaleX(0) skewX(-15deg); transform-origin: right;
  transition: transform .4s var(--transition);
}
.nav-cta:hover { transform: translateY(-2px); box-shadow: 0 8px 30px rgba(184,255,0,0.4); }
.nav-cta:hover::before { transform: scaleX(1) skewX(-15deg); transform-origin: left; }
.nav-cta span { position: relative; z-index: 1; }
.hamburger { display: none; flex-direction: column; gap: 5px; background: none; border: none; cursor: none; padding: 4px; }
.hamburger span { display: block; width: 26px; height: 1.5px; background: var(--white); transition: all .3s; }
.hamburger.active span:nth-child(1) { transform: rotate(45deg) translate(4px, 5px); }
.hamburger.active span:nth-child(2) { opacity: 0; transform: translateX(-10px); }
.hamburger.active span:nth-child(3) { transform: rotate(-45deg) translate(4px, -5px); }

/* ══ MOBILE MENU ══ */
.mobile-nav {
  position: fixed; inset: 0; background: var(--obsidian); z-index: 999;
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  gap: 2.5rem;
  transform: translateY(-100%); transition: transform .6s var(--transition);
  border-bottom: 1px solid var(--border);
}
.mobile-nav.open { transform: translateY(0); }
.mobile-nav a {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: clamp(2rem, 8vw, 4rem); color: var(--white);
  text-decoration: none; text-transform: uppercase; letter-spacing: -.01em;
  transition: color .2s; cursor: none;
  position: relative;
}
.mobile-nav a:hover { color: var(--lime); }
.mobile-nav-footer {
  position: absolute; bottom: 2rem;
  font-size: .6rem; letter-spacing: .2em; color: var(--white-30);
}

/* ══ HERO ══ */
#hero {
  position: relative; min-height: 100vh;
  display: flex; flex-direction: column; justify-content: flex-end;
  padding: 0 4rem 6rem;
  overflow: hidden;
}
.hero-canvas-bg {
  position: absolute; inset: 0; z-index: 0;
}
.hero-grid-lines {
  position: absolute; inset: 0; z-index: 1;
  background-image:
    linear-gradient(rgba(240,238,234,0.025) 1px, transparent 1px),
    linear-gradient(90deg, rgba(240,238,234,0.025) 1px, transparent 1px);
  background-size: 60px 60px;
  transform: perspective(1400px) rotateX(28deg) scale(1.5) translateY(8%);
  transform-origin: 50% 100%;
  will-change: transform;
  transition: transform .1s linear;
}
.hero-vignette {
  position: absolute; inset: 0; z-index: 2;
  background:
    radial-gradient(ellipse 80% 60% at 50% 50%, transparent 30%, rgba(8,11,18,0.9) 100%),
    linear-gradient(to top, var(--obsidian) 0%, transparent 30%);
}
.hero-content { position: relative; z-index: 5; }

.hero-eyebrow {
  display: inline-flex; align-items: center; gap: .8rem;
  font-size: .58rem; letter-spacing: .35em; text-transform: uppercase; color: var(--lime);
  border: 1px solid rgba(184,255,0,0.25); padding: .4rem 1.2rem;
  margin-bottom: 2.5rem;
  opacity: 0; animation: fadeSlide .8s .3s ease forwards;
  position: relative; overflow: hidden;
}
.hero-eyebrow::before {
  content: ''; position: absolute; inset: 0;
  background: rgba(184,255,0,0.06);
  transform: scaleX(0); transform-origin: left;
  animation: eyebrowFill 2s 1s ease forwards;
}
@keyframes eyebrowFill { to { transform: scaleX(1); } }
.eyebrow-dot { width: 5px; height: 5px; background: var(--lime); border-radius: 50%; animation: pulse 1.5s ease-in-out infinite; }
@keyframes pulse { 0%,100%{transform:scale(1);opacity:1} 50%{transform:scale(1.5);opacity:.5} }

.hero-title {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: clamp(4.5rem, 12vw, 12rem);
  line-height: .88; letter-spacing: -.025em;
  overflow: hidden;
  opacity: 0; animation: fadeSlide 1.2s .5s ease forwards;
}
.hero-title .line { display: block; overflow: hidden; }
.hero-title .word { display: inline-block; }
.hero-title .stroke {
  -webkit-text-stroke: 1.5px rgba(240,238,234,0.2);
  color: transparent;
}
.hero-title .lime { color: var(--lime); }
.hero-title .shift { transform: translateX(8vw); display: inline-block; }

.hero-bottom {
  display: grid; grid-template-columns: 1fr auto 1fr;
  align-items: end; gap: 3rem; margin-top: 4rem;
  opacity: 0; animation: fadeSlide .9s 1s ease forwards;
}
.hero-desc {
  font-family: 'Fraunces', serif; font-style: italic;
  font-size: clamp(.85rem, 1.2vw, 1.05rem); color: var(--white-60);
  line-height: 1.9; max-width: 360px;
}
.hero-cta-group { display: flex; gap: 1rem; align-items: center; justify-content: center; }
.hero-meta { display: flex; justify-content: flex-end; align-items: flex-end; }
.typed-wrapper {
  font-size: .65rem; letter-spacing: .12em; color: var(--white-30);
  display: flex; align-items: center; gap: .5rem;
}
.typed-text { color: var(--lime); min-width: 140px; }
.typed-cursor { color: var(--lime); animation: blink 1s step-end infinite; }
@keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

/* SCROLL INDICATOR */
.scroll-indicator {
  position: absolute; bottom: 2.5rem; left: 50%; transform: translateX(-50%);
  display: flex; flex-direction: column; align-items: center; gap: .6rem;
  opacity: 0; animation: fadeSlide .8s 1.5s ease forwards;
  z-index: 5;
}
.scroll-mouse {
  width: 22px; height: 36px; border: 1.5px solid var(--white-30); border-radius: 12px;
  display: flex; justify-content: center; padding-top: 6px;
}
.scroll-wheel {
  width: 3px; height: 6px; background: var(--lime); border-radius: 2px;
  animation: scrollWheel 2s ease-in-out infinite;
}
@keyframes scrollWheel { 0%,100%{transform:translateY(0);opacity:1} 50%{transform:translateY(10px);opacity:0} }
.scroll-txt { font-size: .5rem; letter-spacing: .3em; text-transform: uppercase; color: var(--white-30); }

/* HERO STATS */
.hero-stats-row {
  display: flex; gap: 4rem;
  padding-top: 2.5rem; margin-top: 2.5rem;
  border-top: 1px solid var(--border);
  opacity: 0; animation: fadeSlide .8s 1.2s ease forwards;
}
.h-stat {}
.h-stat-val {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: 2.8rem; color: var(--white); line-height: 1;
}
.h-stat-val .unit { color: var(--lime); font-size: 1.8rem; }
.h-stat-lbl {
  font-size: .55rem; letter-spacing: .2em; text-transform: uppercase;
  color: var(--white-30); margin-top: .3rem;
}

@keyframes fadeSlide { from{opacity:0;transform:translateY(30px)} to{opacity:1;transform:translateY(0)} }

/* ══ MARQUEE ══ */
.marquee-strip {
  position: relative; overflow: hidden; z-index: 10;
  padding: .7rem 0;
}
.marquee-strip-top { background: var(--lime); }
.marquee-strip-bottom { background: var(--orange); margin-top: -1px; }
.marquee-inner {
  display: inline-flex; align-items: center; gap: 2.5rem;
  white-space: nowrap; will-change: transform;
}
.marquee-inner.forward { animation: marqueeF 30s linear infinite; }
.marquee-inner.reverse { animation: marqueeR 35s linear infinite; }
@keyframes marqueeF { from{transform:translateX(0)} to{transform:translateX(-50%)} }
@keyframes marqueeR { from{transform:translateX(-50%)} to{transform:translateX(0)} }
.marquee-strip-top .marquee-inner span {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: .75rem; letter-spacing: .22em; color: var(--obsidian);
}
.marquee-strip-bottom .marquee-inner span {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: .75rem; letter-spacing: .22em; color: var(--white);
}
.marquee-sep { opacity: .4; font-size: .7rem; }

/* ══ GENERIC LAYOUT ══ */
.container { max-width: 1440px; margin: 0 auto; padding: 0 4rem; }
.section-pad { padding: 9rem 0; }

.label-row {
  display: flex; align-items: center; gap: 1rem; margin-bottom: 1.5rem;
}
.label-line { width: 32px; height: 1px; background: var(--lime); }
.label-text { font-size: .58rem; letter-spacing: .3em; text-transform: uppercase; color: var(--lime); }
.label-num { font-size: .58rem; letter-spacing: .15em; color: var(--white-30); margin-left: auto; }

.section-title {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: clamp(2.8rem, 5vw, 5.5rem); line-height: .95;
  letter-spacing: -.025em; color: var(--white);
}
.section-title em {
  font-family: 'Fraunces', serif; font-style: italic;
  font-weight: 300; color: var(--lime);
  letter-spacing: 0;
}
.section-title .outline {
  -webkit-text-stroke: 1px rgba(240,238,234,0.2);
  color: transparent;
}

.two-col { display: grid; grid-template-columns: 1fr 1fr; gap: 6rem; align-items: center; }
.three-col { display: grid; grid-template-columns: repeat(3, 1fr); gap: 1.5rem; }
.four-col { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1.5rem; }

/* ══ BUTTONS ══ */
.btn {
  position: relative; overflow: hidden; cursor: none;
  font-family: 'Syne', sans-serif; font-weight: 700;
  font-size: .7rem; letter-spacing: .12em; text-transform: uppercase;
  display: inline-flex; align-items: center; gap: .6rem;
  transition: transform .2s, box-shadow .3s;
  text-decoration: none; border: none;
}
.btn:hover { transform: translateY(-3px); }
.btn-primary {
  background: var(--lime); color: var(--obsidian);
  padding: .95rem 2.5rem;
}
.btn-primary:hover { box-shadow: 0 12px 40px rgba(184,255,0,0.4); }
.btn-secondary {
  background: transparent; color: var(--white);
  padding: .9rem 2.5rem;
  border: 1px solid var(--border-bright);
}
.btn-secondary:hover { border-color: var(--white); box-shadow: inset 0 0 30px rgba(240,238,234,0.05); }
.btn-orange {
  background: var(--orange); color: var(--white);
  padding: .95rem 2.5rem;
}
.btn-orange:hover { box-shadow: 0 12px 40px rgba(255,92,0,0.4); }

/* MAGNETIC WRAP */
.magnetic-wrap { display: inline-block; }

/* BTN ARROW */
.btn-arrow {
  width: 18px; height: 18px; position: relative;
  transition: transform .3s var(--spring);
}
.btn:hover .btn-arrow { transform: translate(3px, -3px); }
.btn-arrow::before {
  content: '→'; font-size: .8rem;
}

/* RIPPLE */
.ripple {
  position: absolute; border-radius: 50%;
  background: rgba(255,255,255,0.25);
  transform: scale(0); animation: rippleAnim .6s linear;
  pointer-events: none;
}
@keyframes rippleAnim { to { transform: scale(4); opacity: 0; } }

/* ══ REVEAL ANIMATIONS ══ */
.reveal { opacity: 0; transform: translateY(50px); transition: opacity .9s ease, transform .9s ease; }
.reveal.in { opacity: 1; transform: none; }
.reveal-l { opacity: 0; transform: translateX(-60px); transition: opacity .9s ease, transform .9s ease; }
.reveal-l.in { opacity: 1; transform: none; }
.reveal-r { opacity: 0; transform: translateX(60px); transition: opacity .9s ease, transform .9s ease; }
.reveal-r.in { opacity: 1; transform: none; }
.reveal-scale { opacity: 0; transform: scale(.9); transition: opacity .8s ease, transform .8s ease; }
.reveal-scale.in { opacity: 1; transform: scale(1); }
.stagger > * { opacity: 0; transform: translateY(35px); transition: opacity .7s ease, transform .7s ease; }
.stagger.in > * { opacity: 1; transform: none; }
.stagger.in > *:nth-child(1){transition-delay:.05s}
.stagger.in > *:nth-child(2){transition-delay:.15s}
.stagger.in > *:nth-child(3){transition-delay:.25s}
.stagger.in > *:nth-child(4){transition-delay:.35s}
.stagger.in > *:nth-child(5){transition-delay:.45s}
.stagger.in > *:nth-child(6){transition-delay:.55s}
.stagger.in > *:nth-child(7){transition-delay:.65s}
.stagger.in > *:nth-child(8){transition-delay:.75s}

/* ══ INTRO SECTION ══ */
#intro { background: var(--obsidian); padding: 9rem 0; overflow: hidden; }
.intro-big-text {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: clamp(1.1rem, 2.5vw, 2.2rem); line-height: 1.5;
  color: var(--white-30); max-width: 960px;
  position: relative;
}
.intro-big-text .highlight-word {
  color: var(--white); position: relative; display: inline-block;
  cursor: none;
}
.intro-big-text .highlight-word::after {
  content: attr(data-text);
  position: absolute; inset: 0;
  color: var(--lime);
  clip-path: inset(0 100% 0 0);
  transition: clip-path .5s ease;
}
.intro-big-text .highlight-word:hover::after { clip-path: inset(0 0% 0 0); }
.intro-tagline {
  font-size: .6rem; letter-spacing: .25em; color: var(--white-30);
  text-transform: uppercase; margin-top: 3rem;
  display: flex; align-items: center; gap: 1.5rem;
}
.intro-tagline::before { content: ''; display: block; width: 40px; height: 1px; background: var(--lime); }

/* ══ SERVICES ══ */
#services { background: var(--deep); }
.services-header { display: grid; grid-template-columns: 1fr 1fr; gap: 4rem; margin-bottom: 5rem; align-items: end; }
.services-header-right p { font-family: 'Fraunces', serif; font-style: italic; font-size: 1rem; color: var(--white-60); line-height: 1.9; }

.services-list { display: flex; flex-direction: column; }
.svc-item {
  display: grid; grid-template-columns: 80px 1fr auto;
  align-items: start; gap: 3rem;
  padding: 3rem 0;
  border-top: 1px solid var(--border);
  cursor: none; position: relative; overflow: hidden;
  transition: padding-left .4s var(--transition);
}
.svc-item:last-child { border-bottom: 1px solid var(--border); }
.svc-item::before {
  content: ''; position: absolute; inset: 0;
  background: linear-gradient(90deg, rgba(184,255,0,0.04) 0%, transparent 60%);
  transform: scaleX(0); transform-origin: left;
  transition: transform .5s var(--transition);
}
.svc-item:hover { padding-left: 1.5rem; }
.svc-item:hover::before { transform: scaleX(1); }
.svc-num {
  font-size: .65rem; letter-spacing: .2em; color: var(--white-30);
  padding-top: .5rem;
}
.svc-main {}
.svc-title {
  font-family: 'Syne', sans-serif; font-weight: 700;
  font-size: clamp(1.8rem, 3vw, 2.8rem); color: var(--white);
  line-height: 1.1; letter-spacing: -.02em; margin-bottom: 1rem;
  transition: color .3s;
}
.svc-item:hover .svc-title { color: var(--lime); }
.svc-desc {
  font-family: 'Fraunces', serif; font-size: .88rem;
  color: var(--white-60); line-height: 1.9; max-width: 480px;
  max-height: 0; overflow: hidden;
  transition: max-height .5s ease;
}
.svc-item:hover .svc-desc { max-height: 200px; }
.svc-tags { display: flex; flex-wrap: wrap; gap: .4rem; margin-top: .8rem; }
.svc-tag {
  font-size: .5rem; letter-spacing: .12em; text-transform: uppercase;
  border: 1px solid var(--border); padding: .2rem .6rem; color: var(--white-30);
  transition: border-color .3s, color .3s;
}
.svc-item:hover .svc-tag { border-color: rgba(184,255,0,0.2); color: rgba(184,255,0,0.6); }
.svc-right { text-align: right; padding-top: .4rem; }
.svc-icon {
  font-size: 2.5rem;
  transition: transform .4s var(--spring);
  display: block; margin-bottom: .5rem;
}
.svc-item:hover .svc-icon { transform: rotate(-12deg) scale(1.2); }
.svc-arrow {
  font-size: 1.5rem; color: var(--white-30);
  opacity: 0; transform: translateX(-10px);
  transition: opacity .3s, transform .3s; display: block;
}
.svc-item:hover .svc-arrow { opacity: 1; transform: translateX(0); }

/* ══ CAPABILITIES GRID ══ */
#capabilities { background: var(--obsidian); }
.cap-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1px; background: var(--border); margin-top: 4rem; }
.cap-card {
  background: var(--obsidian); padding: 3rem 2.5rem;
  cursor: none; position: relative; overflow: hidden;
  transition: background .4s;
}
.cap-card::after {
  content: ''; position: absolute;
  bottom: 0; left: 0; right: 0; height: 2px;
  background: linear-gradient(90deg, var(--lime), var(--orange));
  transform: scaleX(0); transform-origin: left;
  transition: transform .5s var(--transition);
}
.cap-card:hover { background: var(--surface); }
.cap-card:hover::after { transform: scaleX(1); }
.cap-num { font-size: .55rem; letter-spacing: .2em; color: var(--white-30); margin-bottom: 2.5rem; }
.cap-icon { font-size: 2.2rem; margin-bottom: 1.5rem; display: block; transition: transform .4s var(--spring); }
.cap-card:hover .cap-icon { transform: scale(1.15) rotate(-8deg); }
.cap-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 1.2rem; color: var(--white); margin-bottom: .8rem; }
.cap-text { font-size: .72rem; color: var(--white-30); line-height: 1.85; }
.cap-hover-reveal {
  font-size: .6rem; letter-spacing: .1em; color: var(--lime);
  margin-top: 1.2rem; opacity: 0; transform: translateY(10px);
  transition: opacity .3s, transform .3s;
}
.cap-card:hover .cap-hover-reveal { opacity: 1; transform: none; }

/* ══ WHY / PROOF ══ */
#proof { background: var(--deep); position: relative; overflow: hidden; }
#proof::before {
  content: 'RESULTS';
  position: absolute; right: -3rem; top: 50%; transform: translateY(-50%);
  font-family: 'Syne', sans-serif; font-weight: 800; font-size: 22rem;
  color: rgba(240,238,234,0.02); pointer-events: none; line-height: 1; white-space: nowrap;
}
.proof-layout { display: grid; grid-template-columns: 1fr 1fr; gap: 8rem; align-items: center; }
.proof-text {}
.proof-text p { font-family: 'Fraunces', serif; font-style: italic; font-size: .95rem; color: var(--white-60); line-height: 1.95; margin-bottom: 1.5rem; }
.proof-checklist { list-style: none; display: flex; flex-direction: column; gap: .7rem; margin-top: 2.5rem; }
.proof-checklist li {
  display: flex; align-items: center; gap: .9rem;
  font-size: .72rem; letter-spacing: .04em; color: var(--white-60);
  padding: .7rem .8rem;
  border: 1px solid transparent;
  transition: border-color .3s, background .3s;
  cursor: none;
}
.proof-checklist li:hover { border-color: var(--border); background: var(--white-05); }
.proof-checklist li::before { content: '✓'; color: var(--lime); font-weight: 700; flex-shrink: 0; }

.proof-metrics { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; }
.proof-card {
  background: var(--surface); border: 1px solid var(--border);
  padding: 2.5rem 2rem; position: relative; overflow: hidden;
  cursor: none; transition: border-color .4s, transform .3s;
}
.proof-card::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 1px;
  background: linear-gradient(90deg, var(--lime), transparent);
}
.proof-card:hover { border-color: rgba(184,255,0,0.2); transform: translateY(-4px); }
.proof-card:hover::before { background: linear-gradient(90deg, var(--lime), var(--orange)); }
.proof-val {
  font-family: 'Syne', sans-serif; font-weight: 800;
  font-size: 3.5rem; color: var(--lime); line-height: 1;
  display: inline;
}
.proof-unit { font-family: 'Syne', sans-serif; font-size: 2rem; color: var(--lime); }
.proof-label { font-size: .6rem; letter-spacing: .15em; text-transform: uppercase; color: var(--white-30); margin-top: .6rem; }
.proof-sub { font-size: .65rem; color: rgba(240,238,234,0.2); margin-top: .3rem; }

/* ══ PRICING ══ */
#pricing { background: var(--obsidian); }
.pricing-header { display: grid; grid-template-columns: 1fr 1fr; gap: 4rem; align-items: end; margin-bottom: 5rem; }
.pricing-toggle { display: flex; align-items: center; gap: 1rem; margin-top: 2rem; }
.toggle-label { font-size: .65rem; letter-spacing: .12em; color: var(--white-60); }
.toggle-switch {
  width: 48px; height: 24px; background: var(--surface); border: 1px solid var(--border);
  border-radius: 12px; cursor: none; position: relative; transition: background .3s;
}
.toggle-switch.on { background: rgba(184,255,0,0.2); border-color: rgba(184,255,0,0.3); }
.toggle-knob {
  position: absolute; width: 16px; height: 16px; background: var(--white-30);
  border-radius: 50%; top: 3px; left: 4px;
  transition: left .3s var(--spring), background .3s;
}
.toggle-switch.on .toggle-knob { left: 27px; background: var(--lime); }
.toggle-badge { font-size: .5rem; letter-spacing: .15em; background: rgba(184,255,0,0.1); color: var(--lime); border: 1px solid rgba(184,255,0,0.2); padding: .15rem .5rem; }

.plans-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 1.5rem; }
.plan {
  background: var(--surface); border: 1px solid var(--border);
  padding: 2.8rem; position: relative; overflow: hidden;
  cursor: none; transition: border-color .4s, transform .4s;
}
.plan.featured { border-color: var(--lime); }
.plan:hover { transform: translateY(-8px); }
.plan:not(.featured):hover { border-color: rgba(184,255,0,0.3); }
.plan.featured:hover { box-shadow: 0 30px 60px rgba(184,255,0,0.12); }
.plan-glow {
  position: absolute; top: -40px; right: -40px; width: 120px; height: 120px;
  background: radial-gradient(circle, rgba(184,255,0,0.15) 0%, transparent 70%);
  pointer-events: none;
}
.plan-badge {
  position: absolute; top: 1.5rem; right: 1.5rem;
  font-family: 'Syne', sans-serif; font-size: .55rem; font-weight: 700;
  letter-spacing: .15em; text-transform: uppercase;
  background: var(--lime); color: var(--obsidian); padding: .25rem .7rem;
}
.plan-tier { font-size: .55rem; letter-spacing: .3em; text-transform: uppercase; color: var(--lime); margin-bottom: .8rem; }
.plan-name { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 1.8rem; color: var(--white); margin-bottom: .5rem; }
.plan-price-wrap { margin: 2rem 0; padding: 2rem 0; border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
.plan-price { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 3.5rem; color: var(--white); line-height: 1; }
.plan-price sup { font-size: 1.5rem; vertical-align: super; }
.plan-price .period { font-family: 'JetBrains Mono', monospace; font-size: .7rem; font-weight: 300; color: var(--white-30); }
.plan-price-annual { display: none; }
.annual .plan-price-monthly { display: none; }
.annual .plan-price-annual { display: block; }
.plan-save { font-size: .6rem; letter-spacing: .1em; color: var(--lime); margin-top: .4rem; display: none; }
.annual .plan-save { display: block; }
.plan-desc { font-family: 'Fraunces', serif; font-style: italic; font-size: .82rem; color: var(--white-60); line-height: 1.8; margin-bottom: 2rem; }
.plan-features { list-style: none; display: flex; flex-direction: column; gap: .65rem; margin-bottom: 2.5rem; }
.plan-features li { font-size: .68rem; color: var(--white-60); display: flex; align-items: flex-start; gap: .7rem; line-height: 1.5; }
.plan-features li.yes::before { content: '✓'; color: var(--lime); flex-shrink: 0; font-size: .65rem; margin-top: .1rem; }
.plan-features li.no { opacity: .3; }
.plan-features li.no::before { content: '×'; color: var(--white-30); flex-shrink: 0; }
.plan-cta { width: 100%; padding: 1rem; font-family: 'Syne', sans-serif; font-weight: 700; font-size: .7rem; letter-spacing: .12em; text-transform: uppercase; cursor: none; border: 1px solid var(--border); background: transparent; color: var(--white); transition: all .3s; position: relative; overflow: hidden; }
.plan-cta::before { content: ''; position: absolute; inset: 0; background: var(--white-05); transform: scaleX(0); transition: transform .4s var(--transition); }
.plan-cta:hover { border-color: var(--white-30); }
.plan-cta:hover::before { transform: scaleX(1); }
.plan.featured .plan-cta { background: var(--lime); color: var(--obsidian); border-color: var(--lime); }
.plan.featured .plan-cta:hover { box-shadow: 0 8px 30px rgba(184,255,0,0.4); }
.plan.featured .plan-cta::before { background: rgba(255,255,255,0.2); }

/* ══ PROCESS ══ */
#process { background: var(--deep); position: relative; overflow: hidden; }
.process-track { position: relative; margin-top: 5rem; }
.process-line {
  position: absolute; top: 28px; left: 0; right: 0; height: 1px;
  background: var(--border);
}
.process-progress-line {
  position: absolute; top: 28px; left: 0; height: 1px;
  background: linear-gradient(90deg, var(--lime), var(--orange));
  width: 0; transition: width 1s ease;
  box-shadow: 0 0 8px var(--lime);
}
.process-steps { display: grid; grid-template-columns: repeat(5, 1fr); gap: 0; position: relative; }
.process-step { display: flex; flex-direction: column; align-items: center; text-align: center; padding: 0 .5rem; cursor: none; }
.step-bubble {
  width: 56px; height: 56px; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-family: 'JetBrains Mono', monospace; font-size: .65rem; font-weight: 500;
  margin-bottom: 2rem; position: relative; z-index: 2;
  background: var(--deep); border: 1px solid var(--border);
  color: var(--white-30);
  transition: background .4s, border-color .4s, color .4s, transform .3s var(--spring), box-shadow .4s;
}
.process-step.active .step-bubble {
  background: var(--lime); border-color: var(--lime); color: var(--obsidian);
  box-shadow: 0 0 20px rgba(184,255,0,0.5), 0 0 40px rgba(184,255,0,0.2);
  transform: scale(1.1);
}
.process-step:hover .step-bubble { transform: scale(1.05); border-color: var(--lime); color: var(--lime); }
.step-icon { font-size: 1.4rem; margin-bottom: 1rem; transition: transform .3s; }
.process-step:hover .step-icon { transform: scale(1.15); }
.step-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: .85rem; color: var(--white); margin-bottom: .5rem; }
.step-desc { font-size: .65rem; color: var(--white-30); line-height: 1.7; }

/* ══ PORTFOLIO ══ */
#portfolio { background: var(--obsidian); }
.portfolio-filter { display: flex; gap: .8rem; margin-bottom: 4rem; flex-wrap: wrap; }
.filter-btn {
  font-family: 'JetBrains Mono', monospace; font-size: .6rem;
  letter-spacing: .15em; text-transform: uppercase;
  background: transparent; color: var(--white-60);
  border: 1px solid var(--border); padding: .45rem 1.2rem; cursor: none;
  transition: all .3s;
}
.filter-btn:hover, .filter-btn.active { background: var(--lime); color: var(--obsidian); border-color: var(--lime); }

.portfolio-masonry { display: grid; grid-template-columns: 1.5fr 1fr; grid-template-rows: auto; gap: 1.5rem; }
.port-card {
  position: relative; overflow: hidden; cursor: none;
  background: var(--surface);
  transition: transform .4s var(--transition);
}
.port-card:hover { transform: translateY(-4px); }
.port-card.large { grid-row: span 2; }
.port-art { width: 100%; display: block; transition: transform 1s var(--transition); }
.port-card.large .port-art { height: 640px; object-fit: cover; }
.port-art-sm { height: 295px; object-fit: cover; }
.port-card:hover .port-art { transform: scale(1.07); }
.port-overlay {
  position: absolute; inset: 0;
  background: linear-gradient(to top, rgba(8,11,18,0.98) 0%, rgba(8,11,18,0.2) 50%, transparent 100%);
  display: flex; flex-direction: column; justify-content: flex-end; padding: 2.5rem;
}
.port-cat { font-size: .52rem; letter-spacing: .28em; color: var(--lime); text-transform: uppercase; margin-bottom: .4rem; }
.port-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 1.6rem; color: var(--white); margin-bottom: .3rem; }
.port-card:not(.large) .port-title { font-size: 1.2rem; }
.port-meta { font-size: .58rem; color: var(--white-30); letter-spacing: .1em; }
.port-link-btn {
  position: absolute; top: 1.5rem; right: 1.5rem;
  width: 44px; height: 44px; background: var(--lime);
  display: flex; align-items: center; justify-content: center;
  font-size: 1rem; font-weight: 700; color: var(--obsidian);
  transform: scale(0) rotate(-45deg);
  transition: transform .4s var(--spring);
}
.port-card:hover .port-link-btn { transform: scale(1) rotate(0deg); }
.port-stats {
  display: flex; gap: 1.5rem; margin-top: 1rem;
  padding-top: 1rem; border-top: 1px solid rgba(240,238,234,0.1);
}
.port-stat-val { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 1.1rem; color: var(--lime); }
.port-stat-lbl { font-size: .52rem; color: var(--white-30); letter-spacing: .1em; text-transform: uppercase; }

/* ══ TESTIMONIALS ══ */
#testimonials { background: var(--deep); }
.testi-layout { display: grid; grid-template-columns: 1fr 2fr; gap: 6rem; align-items: start; }
.testi-sidebar {}
.testi-rating-big {
  font-family: 'Syne', sans-serif; font-weight: 800; font-size: 6rem; color: var(--lime); line-height: 1;
}
.testi-stars-row { display: flex; gap: .3rem; margin-top: .5rem; }
.testi-star { color: #f5c842; font-size: 1.2rem; }
.testi-review-count { font-size: .62rem; color: var(--white-30); margin-top: .5rem; letter-spacing: .12em; }
.testi-platforms { margin-top: 3rem; display: flex; flex-direction: column; gap: .8rem; }
.platform-badge { display: flex; align-items: center; gap: .8rem; padding: .8rem 1rem; border: 1px solid var(--border); cursor: none; transition: border-color .3s; }
.platform-badge:hover { border-color: rgba(184,255,0,0.3); }
.platform-icon { font-size: 1.2rem; }
.platform-name { font-family: 'Syne', sans-serif; font-weight: 700; font-size: .75rem; color: var(--white); }
.platform-rating { font-size: .6rem; color: var(--white-30); }

.testi-cards { display: grid; grid-template-columns: 1fr 1fr; gap: 1.2rem; }
.testi-card {
  background: var(--surface); border: 1px solid var(--border);
  padding: 2rem; cursor: none;
  transition: border-color .4s, transform .3s;
  position: relative; overflow: hidden;
}
.testi-card::before {
  content: '"'; position: absolute; top: -1rem; left: 1.5rem;
  font-family: 'Fraunces', serif; font-size: 8rem; font-weight: 700;
  color: rgba(184,255,0,0.06); pointer-events: none; line-height: 1;
}
.testi-card:hover { border-color: rgba(184,255,0,0.2); transform: translateY(-4px); }
.testi-stars { display: flex; gap: .2rem; margin-bottom: 1rem; }
.testi-star-sm { color: #f5c842; font-size: .75rem; }
.testi-text-content { font-family: 'Fraunces', serif; font-style: italic; font-size: .85rem; color: var(--white); line-height: 1.85; margin-bottom: 1.5rem; }
.testi-author-row { display: flex; align-items: center; gap: .8rem; padding-top: 1.2rem; border-top: 1px solid var(--border); }
.testi-avatar {
  width: 36px; height: 36px; border-radius: 50%;
  background: var(--panel); display: flex; align-items: center; justify-content: center;
  font-family: 'Syne', sans-serif; font-weight: 800; font-size: .75rem; color: var(--lime);
  flex-shrink: 0; border: 1px solid rgba(184,255,0,0.2);
}
.testi-name { font-family: 'Syne', sans-serif; font-weight: 700; font-size: .8rem; color: var(--white); }
.testi-role { font-size: .55rem; color: var(--white-30); letter-spacing: .08em; margin-top: .15rem; }

/* ══ TEAM ══ */
#team { background: var(--obsidian); }
.team-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1px; background: var(--border); margin-top: 4rem; }
.team-card { background: var(--obsidian); padding: 2.5rem 2rem; position: relative; overflow: hidden; cursor: none; transition: background .3s; }
.team-card:hover { background: var(--surface); }
.team-avatar-wrap { position: relative; margin-bottom: 1.5rem; }
.team-avatar {
  width: 72px; height: 72px; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-family: 'Syne', sans-serif; font-weight: 800; font-size: 1.5rem;
  border: 1px solid var(--border); position: relative; overflow: hidden;
  transition: border-color .3s;
}
.team-card:hover .team-avatar { border-color: var(--lime); }
.team-role-dot {
  position: absolute; bottom: 2px; right: 2px;
  width: 12px; height: 12px; background: var(--lime); border-radius: 50%;
  border: 2px solid var(--obsidian);
  animation: pulse 2s ease-in-out infinite;
}
.team-name { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 1rem; color: var(--white); margin-bottom: .3rem; }
.team-role { font-size: .58rem; letter-spacing: .18em; text-transform: uppercase; color: var(--lime); margin-bottom: .8rem; }
.team-bio { font-size: .7rem; color: var(--white-30); line-height: 1.7; }
.team-socials { display: flex; gap: .5rem; margin-top: 1.2rem; opacity: 0; transform: translateY(8px); transition: opacity .3s, transform .3s; }
.team-card:hover .team-socials { opacity: 1; transform: none; }
.team-social { width: 28px; height: 28px; border: 1px solid var(--border); display: flex; align-items: center; justify-content: center; font-size: .65rem; color: var(--white-30); transition: border-color .2s, color .2s; text-decoration: none; cursor: none; }
.team-social:hover { border-color: var(--lime); color: var(--lime); }

/* ══ FAQ ══ */
#faq { background: var(--deep); }
.faq-layout { display: grid; grid-template-columns: 1fr 1.6fr; gap: 6rem; align-items: start; }
.faq-sidebar p { font-family: 'Fraunces', serif; font-style: italic; font-size: .95rem; color: var(--white-60); line-height: 1.9; margin-top: 1.5rem; margin-bottom: 2rem; }
.faq-list { display: flex; flex-direction: column; }
.faq-item { border-top: 1px solid var(--border); overflow: hidden; }
.faq-item:last-child { border-bottom: 1px solid var(--border); }
.faq-question {
  display: flex; align-items: center; justify-content: space-between;
  padding: 1.5rem 0; cursor: none; gap: 1rem;
}
.faq-q-text { font-family: 'Syne', sans-serif; font-weight: 600; font-size: .9rem; color: var(--white); flex: 1; transition: color .3s; }
.faq-item.open .faq-q-text { color: var(--lime); }
.faq-plus {
  width: 28px; height: 28px; flex-shrink: 0;
  border: 1px solid var(--border); display: flex; align-items: center; justify-content: center;
  font-size: 1rem; color: var(--white-30); transition: transform .4s var(--spring), border-color .3s, color .3s;
}
.faq-item.open .faq-plus { transform: rotate(45deg); border-color: var(--lime); color: var(--lime); }
.faq-answer {
  max-height: 0; overflow: hidden; transition: max-height .5s ease;
}
.faq-item.open .faq-answer { max-height: 300px; }
.faq-answer-inner { padding-bottom: 1.5rem; font-family: 'Fraunces', serif; font-style: italic; font-size: .85rem; color: var(--white-60); line-height: 1.9; }

/* ══ CONTACT ══ */
#contact { background: var(--obsidian); }
.contact-layout { display: grid; grid-template-columns: 1fr 1.4fr; gap: 6rem; align-items: start; }
.contact-left {}
.contact-left p { font-family: 'Fraunces', serif; font-style: italic; font-size: .95rem; color: var(--white-60); line-height: 1.9; margin-top: 1.5rem; margin-bottom: 3rem; }
.contact-info-cards { display: flex; flex-direction: column; gap: .8rem; }
.contact-card {
  display: flex; align-items: flex-start; gap: 1.2rem;
  padding: 1.2rem; border: 1px solid var(--border);
  transition: border-color .3s, background .3s; cursor: none;
}
.contact-card:hover { border-color: rgba(184,255,0,0.3); background: var(--white-05); }
.contact-card-icon { font-size: 1.2rem; flex-shrink: 0; margin-top: .1rem; }
.contact-card-label { font-size: .52rem; letter-spacing: .2em; color: var(--lime); text-transform: uppercase; margin-bottom: .2rem; }
.contact-card-val { font-size: .78rem; color: var(--white); }

.contact-right {}
.contact-form-box { background: var(--surface); border: 1px solid var(--border); padding: 3rem; }
.form-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 1.5rem; color: var(--white); margin-bottom: .4rem; }
.form-subtitle { font-size: .65rem; color: var(--white-30); letter-spacing: .08em; margin-bottom: 2.5rem; }
.form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; margin-bottom: 1rem; }
.form-group { display: flex; flex-direction: column; gap: .4rem; margin-bottom: 1rem; }
.form-label { font-size: .56rem; letter-spacing: .2em; text-transform: uppercase; color: var(--white-30); }
.form-input, .form-select, .form-textarea {
  background: var(--obsidian); border: 1px solid var(--border);
  color: var(--white); padding: .85rem 1rem;
  font-family: 'JetBrains Mono', monospace; font-size: .72rem; outline: none;
  transition: border-color .3s, box-shadow .3s; width: 100%;
}
.form-input:focus, .form-select:focus, .form-textarea:focus {
  border-color: var(--lime);
  box-shadow: 0 0 0 3px rgba(184,255,0,0.08);
}
.form-input.error { border-color: var(--red); box-shadow: 0 0 0 3px rgba(255,53,53,0.08); }
.form-input::placeholder, .form-textarea::placeholder { color: rgba(240,238,234,0.15); }
.form-select option { background: var(--deep); }
.form-textarea { resize: vertical; min-height: 110px; }
.char-count { font-size: .55rem; color: var(--white-30); text-align: right; }
.form-checkbox { display: flex; align-items: flex-start; gap: .8rem; margin-bottom: 1.5rem; cursor: none; }
.form-checkbox input[type="checkbox"] { display: none; }
.checkbox-custom {
  width: 16px; height: 16px; border: 1px solid var(--border); flex-shrink: 0;
  display: flex; align-items: center; justify-content: center; margin-top: .15rem;
  transition: border-color .3s, background .3s;
}
.form-checkbox:has(input:checked) .checkbox-custom { background: var(--lime); border-color: var(--lime); }
.form-checkbox:has(input:checked) .checkbox-custom::after { content: '✓'; font-size: .6rem; color: var(--obsidian); }
.form-checkbox label { font-size: .65rem; color: var(--white-60); line-height: 1.6; cursor: none; }
.form-checkbox label a { color: var(--lime); text-decoration: none; }
.btn-submit { width: 100%; padding: 1.1rem; position: relative; overflow: hidden; }
.btn-submit-text { position: relative; z-index: 1; display: flex; align-items: center; justify-content: center; gap: .6rem; }
.loading-ring {
  width: 16px; height: 16px; border: 2px solid transparent;
  border-top-color: var(--obsidian); border-radius: 50%;
  display: none; animation: spin .8s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }
.btn-submit.loading .loading-ring { display: block; }
.btn-submit.loading .btn-submit-text span { display: none; }
.form-note { font-size: .58rem; color: var(--white-30); text-align: center; margin-top: .8rem; }
.form-success-msg { display: none; text-align: center; padding: 3rem 0; }
.form-success-msg.visible { display: block; }
.success-check { font-size: 3.5rem; margin-bottom: 1.5rem; }
.success-title { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 2rem; color: var(--lime); margin-bottom: .8rem; }
.success-body { font-family: 'Fraunces', serif; font-style: italic; font-size: .9rem; color: var(--white-60); line-height: 1.8; }

/* ══ CTA SECTION ══ */
#cta-final {
  background: var(--lime); position: relative; overflow: hidden;
  padding: 8rem 4rem;
}
#cta-final::before {
  content: 'LAUNCH';
  position: absolute; right: -4rem; top: 50%; transform: translateY(-50%);
  font-family: 'Syne', sans-serif; font-weight: 800; font-size: 22rem;
  color: rgba(8,11,18,0.07); pointer-events: none; line-height: 1; white-space: nowrap;
}
.cta-final-layout { display: flex; align-items: center; justify-content: space-between; gap: 4rem; max-width: 1440px; margin: 0 auto; position: relative; z-index: 1; }
.cta-final-text h2 { font-family: 'Syne', sans-serif; font-weight: 800; font-size: clamp(2.5rem, 5vw, 5rem); color: var(--obsidian); line-height: 1; letter-spacing: -.025em; }
.cta-final-text p { font-family: 'Fraunces', serif; font-style: italic; font-size: 1rem; color: rgba(8,11,18,0.7); margin-top: 1rem; }
.cta-final-actions { display: flex; gap: 1rem; flex-shrink: 0; align-items: center; }
.btn-cta-dark { font-family: 'Syne', sans-serif; font-weight: 700; font-size: .72rem; letter-spacing: .1em; text-transform: uppercase; background: var(--obsidian); color: var(--lime); padding: 1.1rem 2.8rem; cursor: none; text-decoration: none; display: inline-block; transition: transform .2s, box-shadow .3s; border: none; }
.btn-cta-dark:hover { transform: translateY(-3px); box-shadow: 0 12px 40px rgba(8,11,18,0.4); }
.btn-cta-outline { font-family: 'Syne', sans-serif; font-weight: 700; font-size: .72rem; letter-spacing: .1em; text-transform: uppercase; background: transparent; color: var(--obsidian); border: 2px solid rgba(8,11,18,0.3); padding: 1rem 2.8rem; cursor: none; text-decoration: none; display: inline-block; transition: background .2s; }
.btn-cta-outline:hover { background: rgba(8,11,18,0.08); }

/* ══ FOOTER ══ */
footer {
  background: var(--deep); padding: 6rem 4rem 3rem;
  border-top: 1px solid var(--border);
}
.footer-grid { display: grid; grid-template-columns: 2fr 1fr 1fr 1fr 1fr; gap: 3rem; margin-bottom: 4rem; }
.footer-brand p { font-size: .72rem; color: var(--white-30); line-height: 1.9; margin-top: 1.2rem; max-width: 260px; }
.footer-logo { display: flex; align-items: center; gap: .7rem; }
.footer-logo-mark { width: 28px; height: 28px; background: var(--lime); clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
.footer-logo-text { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 1.1rem; color: var(--white); }
.footer-newsletter { margin-top: 1.5rem; }
.footer-newsletter p { font-size: .62rem; color: var(--white-30); margin-bottom: .8rem; }
.footer-nl-form { display: flex; gap: 0; }
.footer-nl-input { flex: 1; background: var(--obsidian); border: 1px solid var(--border); border-right: none; color: var(--white); padding: .65rem .9rem; font-family: 'JetBrains Mono', monospace; font-size: .65rem; outline: none; transition: border-color .3s; }
.footer-nl-input:focus { border-color: var(--lime); }
.footer-nl-input::placeholder { color: rgba(240,238,234,0.15); }
.footer-nl-btn { background: var(--lime); color: var(--obsidian); border: none; padding: .65rem 1rem; font-family: 'Syne', sans-serif; font-weight: 700; font-size: .62rem; letter-spacing: .1em; text-transform: uppercase; cursor: none; transition: background .2s; }
.footer-nl-btn:hover { background: var(--lime-dim); }
.footer-col-title { font-size: .56rem; letter-spacing: .25em; text-transform: uppercase; color: var(--white-30); margin-bottom: 1.5rem; }
.footer-links { list-style: none; display: flex; flex-direction: column; gap: .55rem; }
.footer-links a { font-size: .72rem; color: rgba(240,238,234,0.4); text-decoration: none; transition: color .2s, padding-left .2s; display: flex; align-items: center; gap: .3rem; }
.footer-links a:hover { color: var(--lime); padding-left: .3rem; }
.footer-bottom { display: flex; align-items: center; justify-content: space-between; padding-top: 2.5rem; border-top: 1px solid var(--border); }
.footer-copy { font-size: .58rem; letter-spacing: .12em; color: rgba(240,238,234,0.18); }
.footer-socials { display: flex; gap: .8rem; }
.footer-social { width: 36px; height: 36px; border: 1px solid var(--border); display: flex; align-items: center; justify-content: center; font-size: .7rem; color: var(--white-30); text-decoration: none; cursor: none; transition: border-color .2s, color .2s, transform .2s; }
.footer-social:hover { border-color: var(--lime); color: var(--lime); transform: translateY(-2px); }
.footer-legal { display: flex; gap: 2rem; }
.footer-legal a { font-size: .58rem; color: rgba(240,238,234,0.18); text-decoration: none; letter-spacing: .1em; transition: color .2s; }
.footer-legal a:hover { color: var(--white-30); }

/* ══ MODAL ══ */
.modal-overlay {
  position: fixed; inset: 0; background: rgba(8,11,18,0.9); z-index: 9995;
  display: flex; align-items: center; justify-content: center;
  opacity: 0; pointer-events: none; transition: opacity .4s;
  backdrop-filter: blur(16px);
}
.modal-overlay.open { opacity: 1; pointer-events: all; }
.modal-box {
  background: var(--surface); border: 1px solid var(--border);
  width: 90%; max-width: 580px; max-height: 90vh; overflow-y: auto;
  padding: 3rem; position: relative;
  transform: scale(.94) translateY(20px);
  transition: transform .5s var(--spring);
  scrollbar-width: thin; scrollbar-color: var(--lime) transparent;
}
.modal-overlay.open .modal-box { transform: scale(1) translateY(0); }
.modal-close {
  position: absolute; top: 1.2rem; right: 1.2rem;
  background: none; border: none; color: var(--white-30); font-size: 1.2rem;
  cursor: none; padding: .4rem; transition: color .2s, transform .2s;
}
.modal-close:hover { color: var(--white); transform: rotate(90deg); }
.modal-title { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 2rem; color: var(--white); margin-bottom: .4rem; }
.modal-subtitle { font-size: .68rem; color: var(--white-30); margin-bottom: 2.5rem; }
.modal-success { display: none; text-align: center; padding: 3rem 0; }
.modal-success.visible { display: block; }

/* ══ TOAST ══ */
#toast {
  position: fixed; bottom: 2rem; right: 2rem; z-index: 99999;
  display: flex; align-items: center; gap: .8rem;
  padding: 1rem 1.5rem;
  font-family: 'Syne', sans-serif; font-weight: 700; font-size: .72rem; letter-spacing: .06em;
  transform: translateY(100px) scale(.9); opacity: 0;
  transition: transform .5s var(--spring), opacity .3s;
  pointer-events: none; max-width: 360px;
}
#toast.show { transform: translateY(0) scale(1); opacity: 1; }
#toast.success { background: var(--lime); color: var(--obsidian); }
#toast.error { background: var(--red); color: var(--white); }
#toast.info { background: var(--surface); color: var(--white); border: 1px solid var(--border); }

/* ══ ANNOUNCEMENT BAR ══ */
.announce-bar {
  background: var(--lime); padding: .5rem 2rem;
  display: flex; align-items: center; justify-content: center; gap: 1.5rem;
  font-family: 'JetBrains Mono', monospace; font-size: .6rem;
  letter-spacing: .15em; color: var(--obsidian);
}
.announce-bar strong { font-weight: 700; }
.announce-close { background: none; border: none; color: var(--obsidian); font-size: .9rem; cursor: none; padding: 0; opacity: .6; transition: opacity .2s; margin-left: 1rem; }
.announce-close:hover { opacity: 1; }

/* ══ FLOATING CTA ══ */
.floating-cta {
  position: fixed; bottom: 2rem; left: 50%; transform: translateX(-50%) translateY(100px);
  background: var(--obsidian); border: 1px solid var(--border);
  display: flex; align-items: center; gap: 2rem;
  padding: .8rem 1.5rem .8rem .8rem;
  z-index: 500; opacity: 0;
  transition: transform .6s var(--spring), opacity .4s;
  box-shadow: var(--shadow-lg);
  white-space: nowrap;
}
.floating-cta.show { transform: translateX(-50%) translateY(0); opacity: 1; }
.floating-cta-text { font-family: 'Fraunces', serif; font-style: italic; font-size: .82rem; color: var(--white-60); }
.floating-cta-text strong { color: var(--white); font-style: normal; font-family: 'Syne', sans-serif; font-weight: 700; }
.floating-cta-btn { font-family: 'Syne', sans-serif; font-weight: 700; font-size: .65rem; letter-spacing: .12em; text-transform: uppercase; background: var(--lime); color: var(--obsidian); padding: .6rem 1.5rem; cursor: none; border: none; transition: background .2s; }
.floating-cta-btn:hover { background: var(--lime-dim); }
.floating-cta-close { background: none; border: none; color: var(--white-30); font-size: .9rem; cursor: none; transition: color .2s; margin-left: .5rem; }
.floating-cta-close:hover { color: var(--white); }

/* ══ SCROLL-DRIVEN COUNTER ══ */
.big-number-section {
  background: var(--obsidian); padding: 6rem 0;
  border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);
}
.bignums-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 0; background: var(--border); }
.bignum-item { background: var(--obsidian); padding: 3rem 2rem; text-align: center; border-right: 1px solid var(--border); }
.bignum-item:last-child { border-right: none; }
.bignum-val { font-family: 'Syne', sans-serif; font-weight: 800; font-size: clamp(3rem, 6vw, 5.5rem); color: var(--lime); line-height: 1; }
.bignum-unit { font-size: .65em; }
.bignum-lbl { font-size: .6rem; letter-spacing: .2em; text-transform: uppercase; color: var(--white-30); margin-top: .8rem; }
.bignum-sub { font-size: .62rem; color: rgba(240,238,234,0.18); margin-top: .3rem; font-family: 'Fraunces', serif; font-style: italic; }

/* ══ COMPARISON TABLE ══ */
.comparison-section { margin-top: 5rem; }
.comparison-table { width: 100%; border-collapse: collapse; }
.comparison-table th {
  font-family: 'Syne', sans-serif; font-weight: 700; font-size: .65rem;
  letter-spacing: .15em; text-transform: uppercase; padding: 1.2rem 1.5rem;
  border-bottom: 1px solid var(--border); text-align: left; color: var(--white-60);
}
.comparison-table th.highlight { color: var(--lime); }
.comparison-table td {
  padding: 1rem 1.5rem; border-bottom: 1px solid var(--border);
  font-size: .72rem; color: var(--white-60);
}
.comparison-table td.feature-name { color: var(--white); font-family: 'Syne', sans-serif; font-weight: 600; }
.comparison-table tr:hover td { background: var(--white-05); }
.comparison-table .check-yes { color: var(--lime); font-size: .9rem; }
.comparison-table .check-no { color: var(--white-30); font-size: .9rem; }
.comparison-table .check-partial { color: var(--orange); font-size: .9rem; }

/* ══ TECH STACK ══ */
.tech-stack { display: flex; flex-wrap: wrap; gap: .6rem; margin-top: 3rem; }
.tech-badge {
  font-family: 'JetBrains Mono', monospace; font-size: .58rem;
  letter-spacing: .1em; color: var(--white-30);
  border: 1px solid var(--border); padding: .3rem .8rem;
  transition: border-color .3s, color .3s; cursor: none;
}
.tech-badge:hover { border-color: rgba(184,255,0,0.3); color: var(--lime); }

/* ══ AWARDS ══ */
.awards-strip { display: flex; align-items: center; gap: 3rem; margin-top: 3rem; padding-top: 3rem; border-top: 1px solid var(--border); flex-wrap: wrap; }
.award-item { display: flex; align-items: center; gap: .7rem; opacity: .5; transition: opacity .3s; cursor: none; }
.award-item:hover { opacity: 1; }
.award-icon { font-size: 1.5rem; }
.award-name { font-size: .62rem; color: var(--white); letter-spacing: .1em; }
.award-year { font-size: .52rem; color: var(--white-30); margin-top: .1rem; }

/* ══ RESPONSIVE ══ */
@media(max-width: 1200px) {
  .cap-grid { grid-template-columns: repeat(2, 1fr); }
  .team-grid { grid-template-columns: repeat(2, 1fr); }
  .bignums-grid { grid-template-columns: repeat(2, 1fr); }
  .footer-grid { grid-template-columns: 1fr 1fr 1fr; }
}
@media(max-width: 900px) {
  nav { padding: 1.2rem 2rem; }
  .nav-links, .nav-cta { display: none; }
  .hamburger { display: flex; }
  .container { padding: 0 2rem; }
  #hero { padding: 0 2rem 5rem; }
  .hero-bottom { grid-template-columns: 1fr; }
  .hero-stats-row { gap: 2rem; flex-wrap: wrap; }
  .two-col { grid-template-columns: 1fr; gap: 3rem; }
  .three-col { grid-template-columns: 1fr; }
  .plans-grid { grid-template-columns: 1fr; max-width: 420px; margin: 0 auto; }
  .testi-layout { grid-template-columns: 1fr; }
  .testi-cards { grid-template-columns: 1fr; }
  .faq-layout { grid-template-columns: 1fr; }
  .contact-layout { grid-template-columns: 1fr; }
  .process-steps { grid-template-columns: 1fr 1fr; }
  .portfolio-masonry { grid-template-columns: 1fr; }
  .port-card.large .port-art { height: 350px; }
  .footer-grid { grid-template-columns: 1fr 1fr; }
  footer { padding: 4rem 2rem 2rem; }
  .cta-final-layout { flex-direction: column; text-align: center; }
  .cta-final-actions { justify-content: center; }
  #cta-final { padding: 5rem 2rem; }
  .services-header { grid-template-columns: 1fr; gap: 2rem; }
  .pricing-header { grid-template-columns: 1fr; gap: 2rem; }
  .form-grid { grid-template-columns: 1fr; }
  .proof-layout { grid-template-columns: 1fr; gap: 4rem; }
  .proof-metrics { grid-template-columns: repeat(2, 1fr); }
  .section-pad { padding: 5rem 0; }
}
@media(max-width: 600px) {
  .hero-title { font-size: clamp(3.5rem, 14vw, 6rem); }
  .cap-grid { grid-template-columns: 1fr; }
  .team-grid { grid-template-columns: 1fr; }
  .bignums-grid { grid-template-columns: 1fr 1fr; }
  .footer-grid { grid-template-columns: 1fr; }
  .process-steps { grid-template-columns: 1fr; }
  .footer-bottom { flex-direction: column; gap: 1.5rem; text-align: center; }
  .footer-legal { justify-content: center; }
}
</style>
</head>
<body>

<!-- ══ ANNOUNCE BAR ══ -->
<div class="announce-bar" id="announceBar">
  <span>🚀 <strong>Limited Spots:</strong> We're accepting 3 new clients in April 2026 — <strong>Book your free strategy call now</strong></span>
  <button class="announce-close" onclick="document.getElementById('announceBar').remove()">✕</button>
</div>

<!-- ══ CURSOR ══ -->
<div id="cursor-dot"></div>
<div id="cursor-ring"></div>
<div id="cursor-text" id="cursor-text"></div>

<!-- ══ PROGRESS BAR ══ -->
<div id="progress-bar"></div>

<!-- ══ CANVAS ══ -->
<canvas id="particle-canvas"></canvas>

<!-- ══ TOAST ══ -->
<div id="toast"><span id="toast-icon">✓</span> <span id="toast-msg">Done!</span></div>

<!-- ══ FLOATING CTA ══ -->
<div class="floating-cta" id="floatingCta">
  <div class="floating-cta-text"><strong>Free Strategy Call</strong> — 30 min. No commitment.</div>
  <button class="floating-cta-btn" onclick="openModal(event)">Book Now →</button>
  <button class="floating-cta-close" onclick="document.getElementById('floatingCta').classList.remove('show')">✕</button>
</div>

<!-- ══ MOBILE NAV ══ -->
<div class="mobile-nav" id="mobileNav">
  <a href="#services" onclick="closeMobile()">Services</a>
  <a href="#proof" onclick="closeMobile()">Results</a>
  <a href="#pricing" onclick="closeMobile()">Pricing</a>
  <a href="#portfolio" onclick="closeMobile()">Work</a>
  <a href="#testimonials" onclick="closeMobile()">Reviews</a>
  <a href="#faq" onclick="closeMobile()">FAQ</a>
  <a href="#contact" onclick="closeMobile()">Contact</a>
  <div class="mobile-nav-footer">© 2026 PIXELFORGE STUDIO</div>
</div>

<!-- ══ QUOTE MODAL ══ -->
<div class="modal-overlay" id="quoteModal">
  <div class="modal-box">
    <button class="modal-close" id="modalCloseBtn">✕</button>
    <div id="modalFormWrap">
      <div class="modal-title">Get Your Free Quote</div>
      <div class="modal-subtitle">FILL IN THE DETAILS BELOW — WE RESPOND WITHIN 24 HOURS</div>
      <div class="form-grid">
        <div class="form-group">
          <label class="form-label">First Name *</label>
          <input class="form-input" id="mFirst" type="text" placeholder="First name">
        </div>
        <div class="form-group">
          <label class="form-label">Last Name *</label>
          <input class="form-input" id="mLast" type="text" placeholder="Last name">
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Email Address *</label>
        <input class="form-input" id="mEmail" type="email" placeholder="you@company.com">
      </div>
      <div class="form-group">
        <label class="form-label">Company / Website</label>
        <input class="form-input" id="mCompany" type="text" placeholder="Your company or URL">
      </div>
      <div class="form-grid">
        <div class="form-group">
          <label class="form-label">Service Needed</label>
          <select class="form-select" id="mService">
            <option value="">Select...</option>
            <option>Business Website</option>
            <option>E-Commerce Store</option>
            <option>Landing Page</option>
            <option>UI/UX Design</option>
            <option>SEO & Performance</option>
            <option>Brand Identity</option>
            <option>Full Digital Package</option>
          </select>
        </div>
        <div class="form-group">
          <label class="form-label">Budget Range</label>
          <select class="form-select" id="mBudget">
            <option value="">Select...</option>
            <option>Under $2,000</option>
            <option>$2,000 – $5,000</option>
            <option>$5,000 – $15,000</option>
            <option>$15,000 – $30,000</option>
            <option>$30,000+</option>
          </select>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Tell Us About Your Project</label>
        <textarea class="form-textarea" id="mDesc" placeholder="Describe your project, timeline, and goals..."></textarea>
      </div>
      <button class="btn btn-primary btn-submit" id="modalSubmitBtn" onclick="submitModal()">
        <div class="btn-submit-text">
          <div class="loading-ring"></div>
          <span>Send Quote Request</span>
          <div class="btn-arrow">→</div>
        </div>
      </button>
      <p class="form-note">🔒 100% private. No spam. We'll respond with a personalized proposal.</p>
    </div>
    <div class="modal-success" id="modalSuccessMsg">
      <div class="success-check">🚀</div>
      <div class="success-title">Quote Request Sent!</div>
      <div class="success-body">Your project details have been received. A senior strategist will review your brief and respond with a tailored proposal within 24 hours.</div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════
     MAIN CONTENT
══════════════════════════════════════════ -->

<!-- ══ NAV ══ -->
<nav id="mainNav">
  <a href="#" class="nav-logo">
    <div class="nav-logo-mark"></div>
    <div>
      <span class="nav-logo-text">PIXELFORGE</span>
      <span class="nav-logo-sub">Studio</span>
    </div>
  </a>
  <ul class="nav-links">
    <li><a href="#services">Services</a></li>
    <li><a href="#proof">Results</a></li>
    <li><a href="#pricing">Pricing</a></li>
    <li><a href="#portfolio">Work</a></li>
    <li><a href="#testimonials">Reviews</a></li>
    <li><a href="#faq">FAQ</a></li>
    <li><span class="nav-badge">3 Spots Left</span></li>
  </ul>
  <div class="magnetic-wrap" id="navCtaMag">
    <a href="#" class="nav-cta" onclick="openModal(event)"><span>Get Free Quote</span></a>
  </div>
  <button class="hamburger" id="hamburgerBtn">
    <span></span><span></span><span></span>
  </button>
</nav>

<!-- ══ HERO ══ -->
<section id="hero">
  <canvas class="hero-canvas-bg" id="heroCanvas"></canvas>
  <div class="hero-grid-lines" id="heroGrid"></div>
  <div class="hero-vignette"></div>

  <div class="hero-content">
    <div class="hero-eyebrow">
      <div class="eyebrow-dot"></div>
      <span>Available for new projects — April 2026</span>
    </div>
    <h1 class="hero-title">
      <span class="line"><span class="word">WE&nbsp;BUILD</span></span>
      <span class="line"><span class="word stroke">WEBSITES</span></span>
      <span class="line"><span class="word">THAT&nbsp;<span class="lime">SELL.</span></span></span>
    </h1>
    <div class="hero-bottom">
      <p class="hero-desc">Premium web design agency engineering high-converting digital experiences for ambitious businesses. Not just pretty — <em>profitable.</em></p>
      <div class="hero-cta-group">
        <div class="magnetic-wrap"><a href="#" class="btn btn-primary" onclick="openModal(event)"><span>Get Free Quote</span><span class="btn-arrow"></span></a></div>
        <div class="magnetic-wrap"><a href="#portfolio" class="btn btn-secondary"><span>View Work</span></a></div>
      </div>
      <div class="hero-meta">
        <div class="typed-wrapper">
          <span>We specialize in</span>
          <span class="typed-text" id="typedEl"></span><span class="typed-cursor">|</span>
        </div>
      </div>
    </div>
    <div class="hero-stats-row stagger">
      <div class="h-stat">
        <div class="h-stat-val" data-target="240" data-suffix="+">0<span class="unit">+</span></div>
        <div class="h-stat-lbl">Projects Delivered</div>
      </div>
      <div class="h-stat">
        <div class="h-stat-val" data-target="98" data-suffix="%">0<span class="unit">%</span></div>
        <div class="h-stat-lbl">Client Satisfaction</div>
      </div>
      <div class="h-stat">
        <div class="h-stat-val" data-target="4.9" data-suffix="/5" data-float="true">0<span class="unit">/5</span></div>
        <div class="h-stat-lbl">Average Rating</div>
      </div>
      <div class="h-stat">
        <div class="h-stat-val" data-target="18">0<span class="unit">+</span></div>
        <div class="h-stat-lbl">Countries Served</div>
      </div>
    </div>
  </div>

  <div class="scroll-indicator">
    <div class="scroll-mouse"><div class="scroll-wheel"></div></div>
    <span class="scroll-txt">Scroll</span>
  </div>
</section>

<!-- ══ MARQUEE ══ -->
<div class="marquee-strip marquee-strip-top">
  <div class="marquee-inner forward">
    <span>WEB DESIGN</span><span class="marquee-sep">✦</span>
    <span>E-COMMERCE</span><span class="marquee-sep">✦</span>
    <span>UI/UX DESIGN</span><span class="marquee-sep">✦</span>
    <span>BRAND IDENTITY</span><span class="marquee-sep">✦</span>
    <span>SEO STRATEGY</span><span class="marquee-sep">✦</span>
    <span>WEB DEVELOPMENT</span><span class="marquee-sep">✦</span>
    <span>CONVERSION OPTIMIZATION</span><span class="marquee-sep">✦</span>
    <span>DIGITAL STRATEGY</span><span class="marquee-sep">✦</span>
    <span>WEB DESIGN</span><span class="marquee-sep">✦</span>
    <span>E-COMMERCE</span><span class="marquee-sep">✦</span>
    <span>UI/UX DESIGN</span><span class="marquee-sep">✦</span>
    <span>BRAND IDENTITY</span><span class="marquee-sep">✦</span>
    <span>SEO STRATEGY</span><span class="marquee-sep">✦</span>
    <span>WEB DEVELOPMENT</span><span class="marquee-sep">✦</span>
    <span>CONVERSION OPTIMIZATION</span><span class="marquee-sep">✦</span>
    <span>DIGITAL STRATEGY</span><span class="marquee-sep">✦</span>
  </div>
</div>
<div class="marquee-strip marquee-strip-bottom">
  <div class="marquee-inner reverse">
    <span>SHOPIFY EXPERTS</span><span class="marquee-sep">◆</span>
    <span>REACT DEVELOPMENT</span><span class="marquee-sep">◆</span>
    <span>WEBFLOW MASTERS</span><span class="marquee-sep">◆</span>
    <span>NEXT.JS APPS</span><span class="marquee-sep">◆</span>
    <span>FRAMER SITES</span><span class="marquee-sep">◆</span>
    <span>3D EXPERIENCES</span><span class="marquee-sep">◆</span>
    <span>MOTION DESIGN</span><span class="marquee-sep">◆</span>
    <span>FIGMA SYSTEMS</span><span class="marquee-sep">◆</span>
    <span>SHOPIFY EXPERTS</span><span class="marquee-sep">◆</span>
    <span>REACT DEVELOPMENT</span><span class="marquee-sep">◆</span>
    <span>WEBFLOW MASTERS</span><span class="marquee-sep">◆</span>
    <span>NEXT.JS APPS</span><span class="marquee-sep">◆</span>
    <span>FRAMER SITES</span><span class="marquee-sep">◆</span>
    <span>3D EXPERIENCES</span><span class="marquee-sep">◆</span>
    <span>MOTION DESIGN</span><span class="marquee-sep">◆</span>
    <span>FIGMA SYSTEMS</span><span class="marquee-sep">◆</span>
  </div>
</div>

<!-- ══ INTRO ══ -->
<section id="intro">
  <div class="container section-pad">
    <div class="intro-big-text reveal">
      We're a <span class="highlight-word" data-text="team">team</span> of designers, developers, and strategists who believe your website should be your <span class="highlight-word" data-text="best">best</span> salesperson. We've built <span class="highlight-word" data-text="240+">240+</span> digital products across <span class="highlight-word" data-text="18 countries">18 countries</span> — from lean startups to <span class="highlight-word" data-text="global brands">global brands</span> — and we obsess over <span class="highlight-word" data-text="results">results</span>, not just aesthetics.
    </div>
    <div class="intro-tagline reveal">
      <span>Based in NYC, London & Singapore</span>
      <span style="color:var(--border-bright)">·</span>
      <span>Since 2017</span>
      <span style="color:var(--border-bright)">·</span>
      <span>4.9 ★ across 240+ reviews</span>
    </div>
    <div class="awards-strip stagger">
      <div class="award-item">
        <span class="award-icon">🏆</span>
        <div><div class="award-name">Awwwards</div><div class="award-year">Site of the Day × 4</div></div>
      </div>
      <div class="award-item">
        <span class="award-icon">🎖️</span>
        <div><div class="award-name">CSS Design Awards</div><div class="award-year">Best Agency 2025</div></div>
      </div>
      <div class="award-item">
        <span class="award-icon">⭐</span>
        <div><div class="award-name">Clutch</div><div class="award-year">Top 10 Web Design Agency</div></div>
      </div>
      <div class="award-item">
        <span class="award-icon">🥇</span>
        <div><div class="award-name">Dribbble</div><div class="award-year">Top Agency 2024</div></div>
      </div>
    </div>
  </div>
</section>

<!-- ══ BIG NUMBERS ══ -->
<div class="big-number-section">
  <div class="bignums-grid container" style="max-width:1440px;padding:0 4rem;">
    <div class="bignum-item reveal">
      <div class="bignum-val" data-target="340" data-suffix="%"><span class="num">0</span><span class="bignum-unit">%</span></div>
      <div class="bignum-lbl">Avg. Lead Increase</div>
      <div class="bignum-sub">Measured across all 2024–25 clients</div>
    </div>
    <div class="bignum-item reveal" style="transition-delay:.1s">
      <div class="bignum-val" data-target="4.2" data-suffix="%" data-float="true"><span class="num">0</span><span class="bignum-unit">%</span></div>
      <div class="bignum-lbl">Avg. Conversion Rate</div>
      <div class="bignum-sub">2× the industry average</div>
    </div>
    <div class="bignum-item reveal" style="transition-delay:.2s">
      <div class="bignum-val" data-target="21" data-suffix="d"><span class="num">0</span><span class="bignum-unit">d</span></div>
      <div class="bignum-lbl">Avg. Delivery Time</div>
      <div class="bignum-sub">From kickoff to launch</div>
    </div>
    <div class="bignum-item reveal" style="transition-delay:.3s">
      <div class="bignum-val" data-target="2.8" data-suffix="M" data-float="true"><span class="num">0</span><span class="bignum-unit">M+</span></div>
      <div class="bignum-lbl">Revenue Generated</div>
      <div class="bignum-sub">For clients in FY 2025</div>
    </div>
  </div>
</div>

<!-- ══ SERVICES ══ -->
<section id="services">
  <div class="container section-pad">
    <div class="services-header">
      <div class="reveal-l">
        <div class="label-row"><div class="label-line"></div><span class="label-text">What We Do</span><span class="label-num">01/07</span></div>
        <h2 class="section-title">Services Built<br>to <em>Drive Growth</em></h2>
      </div>
      <div class="reveal-r">
        <p>Every service we offer is engineered around one purpose: turning your digital presence into a growth engine. We don't sell templates or cut corners — we build custom digital experiences that work.</p>
        <div class="tech-stack stagger">
          <span class="tech-badge">React</span><span class="tech-badge">Next.js</span><span class="tech-badge">Webflow</span>
          <span class="tech-badge">Shopify</span><span class="tech-badge">Framer</span><span class="tech-badge">Figma</span>
          <span class="tech-badge">TypeScript</span><span class="tech-badge">Tailwind</span><span class="tech-badge">GSAP</span>
          <span class="tech-badge">Three.js</span><span class="tech-badge">Supabase</span><span class="tech-badge">Stripe</span>
        </div>
      </div>
    </div>
    <div class="services-list stagger">
      <div class="svc-item">
        <div class="svc-num">01</div>
        <div class="svc-main">
          <div class="svc-title">Business Websites</div>
          <div class="svc-desc">The most demanded product in web design. We craft custom business sites that convert visitors into leads — mobile-first, blazing fast, fully CMS-powered so you can update it yourself.</div>
          <div class="svc-tags"><span class="svc-tag">Custom Design</span><span class="svc-tag">CMS</span><span class="svc-tag">SEO-Ready</span><span class="svc-tag">Mobile-First</span><span class="svc-tag">Analytics</span></div>
        </div>
        <div class="svc-right"><span class="svc-icon">🖥️</span><span class="svc-arrow">↗</span></div>
      </div>
      <div class="svc-item">
        <div class="svc-num">02</div>
        <div class="svc-main">
          <div class="svc-title">E-Commerce Stores</div>
          <div class="svc-desc">Global e-commerce hits $8T by 2027. We build Shopify and WooCommerce stores optimized for conversion — custom product pages, checkout flows, and retention systems that keep customers coming back.</div>
          <div class="svc-tags"><span class="svc-tag">Shopify</span><span class="svc-tag">WooCommerce</span><span class="svc-tag">Payment Integration</span><span class="svc-tag">Inventory</span><span class="svc-tag">CRO</span></div>
        </div>
        <div class="svc-right"><span class="svc-icon">🛒</span><span class="svc-arrow">↗</span></div>
      </div>
      <div class="svc-item">
        <div class="svc-num">03</div>
        <div class="svc-main">
          <div class="svc-title">SaaS & Web Apps</div>
          <div class="svc-desc">From MVP to enterprise-grade platforms. We design and build web applications with authentication, dashboards, billing, and the UX polish that turns trial users into paying customers.</div>
          <div class="svc-tags"><span class="svc-tag">React/Next.js</span><span class="svc-tag">Supabase</span><span class="svc-tag">Stripe</span><span class="svc-tag">Auth</span><span class="svc-tag">Dashboards</span></div>
        </div>
        <div class="svc-right"><span class="svc-icon">⚙️</span><span class="svc-arrow">↗</span></div>
      </div>
      <div class="svc-item">
        <div class="svc-num">04</div>
        <div class="svc-main">
          <div class="svc-title">Landing Pages</div>
          <div class="svc-desc">Single-purpose, high-converting machines. Our landing pages average a 4.2% conversion rate — 2× the industry standard. Every element is A/B tested, every word intentional.</div>
          <div class="svc-tags"><span class="svc-tag">High Conversion</span><span class="svc-tag">A/B Testing</span><span class="svc-tag">Analytics</span><span class="svc-tag">Heatmaps</span></div>
        </div>
        <div class="svc-right"><span class="svc-icon">⚡</span><span class="svc-arrow">↗</span></div>
      </div>
      <div class="svc-item">
        <div class="svc-num">05</div>
        <div class="svc-main">
          <div class="svc-title">UI/UX Design</div>
          <div class="svc-desc">Full design systems, user research, prototyping, and testing. We design interfaces people actually enjoy using — reducing friction, increasing engagement, and building brand love.</div>
          <div class="svc-tags"><span class="svc-tag">Figma</span><span class="svc-tag">Design Systems</span><span class="svc-tag">User Research</span><span class="svc-tag">Prototyping</span></div>
        </div>
        <div class="svc-right"><span class="svc-icon">🎨</span><span class="svc-arrow">↗</span></div>
      </div>
      <div class="svc-item">
        <div class="svc-num">06</div>
        <div class="svc-main">
          <div class="svc-title">SEO & Performance</div>
          <div class="svc-desc">Google holds 90% of search traffic. We build for Core Web Vitals, schema markup, technical SEO, and content architecture — so your site ranks, loads instantly, and stays ahead of competitors.</div>
          <div class="svc-tags"><span class="svc-tag">Technical SEO</span><span class="svc-tag">Core Web Vitals</span><span class="svc-tag">Schema</span><span class="svc-tag">Speed</span></div>
        </div>
        <div class="svc-right"><span class="svc-icon">🔍</span><span class="svc-arrow">↗</span></div>
      </div>
      <div class="svc-item">
        <div class="svc-num">07</div>
        <div class="svc-main">
          <div class="svc-title">Brand Identity</div>
          <div class="svc-desc">Logos, color systems, typography, tone of voice, and full brand guidelines. We build visual identities that communicate confidence and make your brand impossible to forget.</div>
          <div class="svc-tags"><span class="svc-tag">Logo Design</span><span class="svc-tag">Brand Guidelines</span><span class="svc-tag">Typography</span><span class="svc-tag">Visual Identity</span></div>
        </div>
        <div class="svc-right"><span class="svc-icon">💎</span><span class="svc-arrow">↗</span></div>
      </div>
    </div>
  </div>
</section>

<!-- ══ CAPABILITIES ══ -->
<section id="capabilities">
  <div class="container section-pad">
    <div class="label-row reveal"><div class="label-line"></div><span class="label-text">Capabilities</span><span class="label-num">02/07</span></div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:end;margin-bottom:4rem;" class="reveal">
      <h2 class="section-title">Everything<br>You Need,<br><em>Under One Roof</em></h2>
      <p style="font-family:'Fraunces',serif;font-style:italic;font-size:.95rem;color:var(--white-60);line-height:1.9;">From first wireframe to post-launch growth — PixelForge handles every layer of your digital strategy. No juggling multiple agencies. One team. Total ownership.</p>
    </div>
    <div class="cap-grid stagger">
      <div class="cap-card">
        <div class="cap-num">CAP 01</div>
        <span class="cap-icon">📐</span>
        <div class="cap-title">Strategic Planning</div>
        <div class="cap-text">We map your entire digital strategy before touching design. Competitor analysis, audience research, conversion architecture, and content planning.</div>
        <div class="cap-hover-reveal">Learn more →</div>
      </div>
      <div class="cap-card">
        <div class="cap-num">CAP 02</div>
        <span class="cap-icon">✏️</span>
        <div class="cap-title">Custom Design</div>
        <div class="cap-text">100% bespoke designs in Figma. Every pixel intentional. Design systems built for scalability. Never a template, never a shortcut.</div>
        <div class="cap-hover-reveal">Learn more →</div>
      </div>
      <div class="cap-card">
        <div class="cap-num">CAP 03</div>
        <span class="cap-icon">💻</span>
        <div class="cap-title">Precision Development</div>
        <div class="cap-text">Clean, performant, accessible code. React, Next.js, Webflow, Shopify — we build on whatever stack best serves your project and future growth.</div>
        <div class="cap-hover-reveal">Learn more →</div>
      </div>
      <div class="cap-card">
        <div class="cap-num">CAP 04</div>
        <span class="cap-icon">🚀</span>
        <div class="cap-title">Launch & Optimize</div>
        <div class="cap-text">QA testing, performance audits, SEO verification, and a smooth launch day. Then 6 months of monitoring and optimization included.</div>
        <div class="cap-hover-reveal">Learn more →</div>
      </div>
      <div class="cap-card">
        <div class="cap-num">CAP 05</div>
        <span class="cap-icon">📊</span>
        <div class="cap-title">Analytics & CRO</div>
        <div class="cap-text">We set up full analytics stacks — GA4, Hotjar, Mixpanel — and run ongoing A/B tests to continually improve your conversion rates.</div>
        <div class="cap-hover-reveal">Learn more →</div>
      </div>
      <div class="cap-card">
        <div class="cap-num">CAP 06</div>
        <span class="cap-icon">🔧</span>
        <div class="cap-title">Ongoing Support</div>
        <div class="cap-text">Every project comes with a dedicated support window. Updates, bug fixes, performance reviews — we're your long-term digital partner, not a one-time vendor.</div>
        <div class="cap-hover-reveal">Learn more →</div>
      </div>
      <div class="cap-card">
        <div class="cap-num">CAP 07</div>
        <span class="cap-icon">🤝</span>
        <div class="cap-title">Dedicated PM</div>
        <div class="cap-text">Every client gets a named project manager. Real-time updates via Notion, weekly calls, and a client portal with full visibility into your project status.</div>
        <div class="cap-hover-reveal">Learn more →</div>
      </div>
      <div class="cap-card">
        <div class="cap-num">CAP 08</div>
        <span class="cap-icon">🌐</span>
        <div class="cap-title">Global Reach</div>
        <div class="cap-text">With clients across 18 countries, we understand localization, multi-language setups, regional SEO, and building for diverse global audiences.</div>
        <div class="cap-hover-reveal">Learn more →</div>
      </div>
    </div>
  </div>
</section>

<!-- ══ PROOF ══ -->
<section id="proof">
  <div class="container section-pad">
    <div class="proof-layout">
      <div class="proof-text reveal-l">
        <div class="label-row"><div class="label-line"></div><span class="label-text">Why PixelForge</span><span class="label-num">03/07</span></div>
        <h2 class="section-title">Real Results.<br><em>Real Numbers.</em><br><span class="outline">No Fluff.</span></h2>
        <p>We don't win design awards and hope clients are happy. We measure success in revenue generated, leads captured, and conversion rates improved — then we share that data with you every month.</p>
        <p>The average PixelForge client sees a 340% increase in qualified leads within the first 6 months. That's a methodology built over 8 years and 240+ projects, not luck.</p>
        <ul class="proof-checklist stagger">
          <li>100% custom design — never templates or page builders</li>
          <li>You own all code, assets, and intellectual property</li>
          <li>6-month post-launch support included in every plan</li>
          <li>Dedicated project manager on every build</li>
          <li>Delivery in 3–6 weeks, guaranteed in writing</li>
          <li>Transparent, flat-rate pricing — zero hidden fees</li>
          <li>Weekly progress calls and Notion project board</li>
          <li>Full mobile optimization + WCAG accessibility compliance</li>
          <li>Post-launch analytics and performance reporting</li>
        </ul>
      </div>
      <div class="proof-metrics stagger reveal-r">
        <div class="proof-card">
          <div><span class="proof-val" data-target="340">0</span><span class="proof-unit">%</span></div>
          <div class="proof-label">Avg. Lead Increase</div>
          <div class="proof-sub">Measured across all 2024–2025 sites</div>
        </div>
        <div class="proof-card">
          <div><span class="proof-val" data-target="4.2" data-float="true">0</span><span class="proof-unit">%</span></div>
          <div class="proof-label">Avg. Conversion Rate</div>
          <div class="proof-sub">Double the 2.1% industry standard</div>
        </div>
        <div class="proof-card">
          <div><span class="proof-val" data-target="21">0</span><span class="proof-unit">d</span></div>
          <div class="proof-label">Average Turnaround</div>
          <div class="proof-sub">Kickoff to live launch</div>
        </div>
        <div class="proof-card">
          <div><span class="proof-val" data-target="98">0</span><span class="proof-unit">%</span></div>
          <div class="proof-label">Client Satisfaction</div>
          <div class="proof-sub">Based on 240+ post-project surveys</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ══ PROCESS ══ -->
<section id="process">
  <div class="container section-pad">
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:end;margin-bottom:5rem;">
      <div class="reveal-l">
        <div class="label-row"><div class="label-line"></div><span class="label-text">How We Work</span><span class="label-num">04/07</span></div>
        <h2 class="section-title">Our Proven<br><em>5-Step Process</em></h2>
      </div>
      <p class="reveal-r" style="font-family:'Fraunces',serif;font-style:italic;font-size:.95rem;color:var(--white-60);line-height:1.9;">Clear milestones. Real communication. A process refined over 240+ projects so nothing falls through the cracks — and you always know exactly where we are.</p>
    </div>
    <div class="process-track">
      <div class="process-line"></div>
      <div class="process-progress-line" id="processLine"></div>
      <div class="process-steps stagger" id="processSteps">
        <div class="process-step">
          <div class="step-bubble">01</div>
          <div class="step-icon">🔎</div>
          <div class="step-title">Discovery</div>
          <div class="step-desc">Deep-dive into your business, goals, audience, and competitors. We build the strategy before we touch design.</div>
        </div>
        <div class="process-step">
          <div class="step-bubble">02</div>
          <div class="step-icon">🗺️</div>
          <div class="step-title">Strategy</div>
          <div class="step-desc">Sitemap, wireframes, and conversion architecture. Every page planned for maximum impact before any visual work begins.</div>
        </div>
        <div class="process-step">
          <div class="step-bubble">03</div>
          <div class="step-icon">🎨</div>
          <div class="step-title">Design</div>
          <div class="step-desc">Full visual design in Figma. Custom, never templated. You approve every screen before a single line of code is written.</div>
        </div>
        <div class="process-step">
          <div class="step-bubble">04</div>
          <div class="step-icon">⚙️</div>
          <div class="step-title">Build</div>
          <div class="step-desc">Pixel-perfect development. Fast, accessible, SEO-ready. Tested across devices and browsers before it ever reaches you.</div>
        </div>
        <div class="process-step">
          <div class="step-bubble">05</div>
          <div class="step-icon">🚀</div>
          <div class="step-title">Launch & Grow</div>
          <div class="step-desc">QA, launch day support, analytics setup, and 6 months of post-launch optimization included in every plan.</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ══ PRICING ══ -->
<section id="pricing">
  <div class="container section-pad">
    <div class="pricing-header">
      <div class="reveal-l">
        <div class="label-row"><div class="label-line"></div><span class="label-text">Transparent Pricing</span><span class="label-num">05/07</span></div>
        <h2 class="section-title">Plans That <em>Fit</em><br>Every Business</h2>
      </div>
      <div class="reveal-r">
        <p style="font-family:'Fraunces',serif;font-style:italic;font-size:.95rem;color:var(--white-60);line-height:1.9;">No hidden fees. No confusing hourly rates. Flat-rate project pricing so you know exactly what you're getting — and what you'll pay. Every plan includes full code ownership and post-launch support.</p>
        <div class="pricing-toggle">
          <span class="toggle-label">Monthly</span>
          <div class="toggle-switch" id="billingToggle" onclick="toggleBilling()"><div class="toggle-knob"></div></div>
          <span class="toggle-label">Annual</span>
          <span class="toggle-badge">Save 20%</span>
        </div>
      </div>
    </div>
    <div class="plans-grid stagger" id="plansGrid">
      <div class="plan">
        <div class="plan-tier">Starter</div>
        <div class="plan-name">Launch</div>
        <p class="plan-desc">Perfect for startups, freelancers, and small businesses that need a professional, trustworthy online presence without the enterprise price tag.</p>
        <div class="plan-price-wrap">
          <div class="plan-price plan-price-monthly"><sup>$</sup>2,500<span class="period">/project</span></div>
          <div class="plan-price plan-price-annual"><sup>$</sup>2,000<span class="period">/project</span></div>
          <div class="plan-save">✦ You save $500 with annual billing</div>
        </div>
        <ul class="plan-features">
          <li class="yes">Up to 6 custom pages</li>
          <li class="yes">Mobile-responsive design</li>
          <li class="yes">Working contact form</li>
          <li class="yes">Basic on-page SEO</li>
          <li class="yes">CMS / blog integration</li>
          <li class="yes">2 revision rounds</li>
          <li class="yes">3-week delivery</li>
          <li class="yes">3-month support</li>
          <li class="no">E-commerce functionality</li>
          <li class="no">Custom animations</li>
          <li class="no">Analytics dashboard</li>
          <li class="no">Dedicated project manager</li>
        </ul>
        <button class="plan-cta" onclick="selectPlan('Launch', '$2,500')">Get Started →</button>
      </div>
      <div class="plan featured">
        <div class="plan-glow"></div>
        <div class="plan-badge">Most Popular</div>
        <div class="plan-tier">Growth</div>
        <div class="plan-name">Scale</div>
        <p class="plan-desc">For established businesses ready to grow. Comprehensive design with advanced features, real backend functionality, and full analytics setup.</p>
        <div class="plan-price-wrap">
          <div class="plan-price plan-price-monthly"><sup>$</sup>7,500<span class="period">/project</span></div>
          <div class="plan-price plan-price-annual"><sup>$</sup>6,000<span class="period">/project</span></div>
          <div class="plan-save">✦ You save $1,500 with annual billing</div>
        </div>
        <ul class="plan-features">
          <li class="yes">Up to 20 custom pages</li>
          <li class="yes">Mobile-responsive design</li>
          <li class="yes">Working forms + lead capture</li>
          <li class="yes">Full SEO + schema markup</li>
          <li class="yes">Advanced CMS integration</li>
          <li class="yes">5 revision rounds</li>
          <li class="yes">4-week delivery</li>
          <li class="yes">6-month support</li>
          <li class="yes">Custom animations & interactions</li>
          <li class="yes">Google Analytics 4 setup</li>
          <li class="yes">Heatmap & session recording</li>
          <li class="yes">Dedicated project manager</li>
        </ul>
        <button class="plan-cta" onclick="selectPlan('Scale', '$7,500')">Get Started →</button>
      </div>
      <div class="plan">
        <div class="plan-tier">Enterprise</div>
        <div class="plan-name">Dominate</div>
        <p class="plan-desc">Complete digital systems for companies that need more — e-commerce, web apps, user accounts, and enterprise-grade performance at scale.</p>
        <div class="plan-price-wrap">
          <div class="plan-price plan-price-monthly"><sup>$</sup>18k<span class="period">+</span></div>
          <div class="plan-price plan-price-annual"><sup>$</sup>14.4k<span class="period">+</span></div>
          <div class="plan-save">✦ You save $3,600+ with annual billing</div>
        </div>
        <ul class="plan-features">
          <li class="yes">Unlimited pages</li>
          <li class="yes">E-commerce + payment integration</li>
          <li class="yes">Custom web app features</li>
          <li class="yes">Advanced SEO & content strategy</li>
          <li class="yes">Unlimited revisions</li>
          <li class="yes">6-week delivery</li>
          <li class="yes">12-month priority support</li>
          <li class="yes">User auth & accounts</li>
          <li class="yes">Full 3D / immersive design</li>
          <li class="yes">Custom analytics dashboard</li>
          <li class="yes">CRO program & A/B testing</li>
          <li class="yes">Dedicated senior team</li>
        </ul>
        <button class="plan-cta" onclick="selectPlan('Dominate', '$18,000+')">Get Started →</button>
      </div>
    </div>

    <!-- COMPARISON TABLE -->
    <div class="comparison-section reveal">
      <h3 style="font-family:'Syne',sans-serif;font-weight:700;font-size:1.4rem;color:var(--white);margin-bottom:2rem;letter-spacing:-.01em;">Full Feature Comparison</h3>
      <table class="comparison-table">
        <thead>
          <tr>
            <th>Feature</th>
            <th>Launch $2,500</th>
            <th class="highlight">Scale $7,500</th>
            <th>Dominate $18k+</th>
            <th>Freelancer</th>
          </tr>
        </thead>
        <tbody>
          <tr><td class="feature-name">Custom Design</td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-partial">~</span></td></tr>
          <tr><td class="feature-name">Mobile Responsive</td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-partial">~</span></td></tr>
          <tr><td class="feature-name">CMS Integration</td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-no">✗</span></td></tr>
          <tr><td class="feature-name">Full SEO Package</td><td><span class="check-partial">~</span></td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-no">✗</span></td></tr>
          <tr><td class="feature-name">Custom Animations</td><td><span class="check-no">✗</span></td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-no">✗</span></td></tr>
          <tr><td class="feature-name">Analytics Setup</td><td><span class="check-no">✗</span></td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-no">✗</span></td></tr>
          <tr><td class="feature-name">Dedicated PM</td><td><span class="check-no">✗</span></td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-no">✗</span></td></tr>
          <tr><td class="feature-name">E-Commerce</td><td><span class="check-no">✗</span></td><td><span class="check-partial">~</span></td><td><span class="check-yes">✓</span></td><td><span class="check-no">✗</span></td></tr>
          <tr><td class="feature-name">Post-Launch Support</td><td>3 months</td><td>6 months</td><td>12 months</td><td><span class="check-no">✗</span></td></tr>
          <tr><td class="feature-name">Code Ownership</td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-yes">✓</span></td><td><span class="check-partial">~</span></td></tr>
        </tbody>
      </table>
    </div>
  </div>
</section>

<!-- ══ PORTFOLIO ══ -->
<section id="portfolio">
  <div class="container section-pad">
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:end;margin-bottom:3rem;">
      <div class="reveal-l">
        <div class="label-row"><div class="label-line"></div><span class="label-text">Our Work</span><span class="label-num">06/07</span></div>
        <h2 class="section-title">Selected<br><em>Projects</em></h2>
      </div>
      <p class="reveal-r" style="font-family:'Fraunces',serif;font-style:italic;font-size:.95rem;color:var(--white-60);line-height:1.9;">Every project here is measured by results: leads generated, revenue grown, rankings improved. We're proud of the design — but we're prouder of the outcomes.</p>
    </div>
    <div class="portfolio-filter stagger">
      <button class="filter-btn active" onclick="filterPortfolio('all', this)">All Projects</button>
      <button class="filter-btn" onclick="filterPortfolio('web', this)">Business Web</button>
      <button class="filter-btn" onclick="filterPortfolio('ecom', this)">E-Commerce</button>
      <button class="filter-btn" onclick="filterPortfolio('saas', this)">SaaS / Apps</button>
      <button class="filter-btn" onclick="filterPortfolio('brand', this)">Branding</button>
    </div>
    <div class="portfolio-masonry stagger" id="portfolioGrid">
      <!-- LARGE CARD -->
      <div class="port-card large" data-cat="web">
        <svg class="port-art" style="height:640px;display:block;" viewBox="0 0 700 640" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <linearGradient id="pc1" x1="0" y1="0" x2="1" y2="1"><stop offset="0%" stop-color="#0d1b2a"/><stop offset="100%" stop-color="#0a2015"/></linearGradient>
            <radialGradient id="pcg1" cx="60%" cy="40%" r="60%"><stop offset="0%" stop-color="rgba(184,255,0,0.12)"/><stop offset="100%" stop-color="transparent"/></radialGradient>
          </defs>
          <rect width="700" height="640" fill="url(#pc1)"/>
          <rect width="700" height="640" fill="url(#pcg1)"/>
          <!-- Browser chrome -->
          <rect x="50" y="70" width="600" height="440" rx="8" fill="rgba(255,255,255,0.03)" stroke="rgba(255,255,255,0.07)" stroke-width="1"/>
          <rect x="50" y="70" width="600" height="36" rx="8" fill="rgba(255,255,255,0.05)"/>
          <circle cx="78" cy="88" r="5" fill="rgba(255,100,100,0.5)"/>
          <circle cx="98" cy="88" r="5" fill="rgba(255,200,0,0.5)"/>
          <circle cx="118" cy="88" r="5" fill="rgba(100,255,100,0.5)"/>
          <rect x="148" y="82" width="200" height="12" rx="6" fill="rgba(255,255,255,0.05)"/>
          <!-- Nav -->
          <rect x="68" y="120" width="560" height="28" rx="2" fill="rgba(255,255,255,0.03)"/>
          <rect x="80" y="128" width="60" height="10" rx="2" fill="rgba(184,255,0,0.5)"/>
          <rect x="400" y="128" width="50" height="10" rx="2" fill="rgba(255,255,255,0.08)"/>
          <rect x="460" y="128" width="50" height="10" rx="2" fill="rgba(255,255,255,0.08)"/>
          <rect x="520" y="124" width="60" height="18" rx="2" fill="rgba(184,255,0,0.6)"/>
          <!-- Hero area -->
          <rect x="68" y="165" width="260" height="16" rx="3" fill="rgba(184,255,0,0.4)"/>
          <rect x="68" y="190" width="360" height="10" rx="2" fill="rgba(255,255,255,0.15)"/>
          <rect x="68" y="208" width="280" height="10" rx="2" fill="rgba(255,255,255,0.1)"/>
          <rect x="68" y="226" width="220" height="10" rx="2" fill="rgba(255,255,255,0.07)"/>
          <rect x="68" y="256" width="100" height="28" rx="2" fill="rgba(184,255,0,0.7)"/>
          <rect x="178" y="258" width="90" height="24" rx="2" fill="transparent" stroke="rgba(255,255,255,0.2)" stroke-width="1"/>
          <!-- Hero image block -->
          <rect x="400" y="160" width="220" height="150" rx="6" fill="rgba(184,255,0,0.06)"/>
          <text x="510" y="248" text-anchor="middle" font-size="50" fill="rgba(184,255,0,0.25)">🌿</text>
          <!-- Stat bar -->
          <rect x="68" y="310" width="555" height="1" fill="rgba(255,255,255,0.06)"/>
          <rect x="68" y="320" width="120" height="60" rx="3" fill="rgba(255,255,255,0.02)"/>
          <rect x="210" y="320" width="120" height="60" rx="3" fill="rgba(255,255,255,0.02)"/>
          <rect x="352" y="320" width="120" height="60" rx="3" fill="rgba(255,255,255,0.02)"/>
          <rect x="494" y="320" width="120" height="60" rx="3" fill="rgba(255,255,255,0.02)"/>
          <text x="128" y="345" text-anchor="middle" font-family="monospace" font-size="16" fill="rgba(184,255,0,0.8)" font-weight="bold">340%</text>
          <text x="128" y="360" text-anchor="middle" font-family="monospace" font-size="8" fill="rgba(255,255,255,0.2)">TRAFFIC UP</text>
          <text x="270" y="345" text-anchor="middle" font-family="monospace" font-size="16" fill="rgba(184,255,0,0.8)" font-weight="bold">4.8%</text>
          <text x="270" y="360" text-anchor="middle" font-family="monospace" font-size="8" fill="rgba(255,255,255,0.2)">CVR</text>
          <text x="412" y="345" text-anchor="middle" font-family="monospace" font-size="16" fill="rgba(184,255,0,0.8)" font-weight="bold">3wk</text>
          <text x="412" y="360" text-anchor="middle" font-family="monospace" font-size="8" fill="rgba(255,255,255,0.2)">DELIVERY</text>
          <!-- Label -->
          <text x="70" y="540" font-family="monospace" font-size="11" fill="rgba(184,255,0,0.6)" letter-spacing="2">WELLNESS · E-COMMERCE</text>
          <text x="70" y="568" font-family="sans-serif" font-size="30" fill="white" font-weight="bold">VitaRoot Health Co.</text>
          <text x="70" y="590" font-family="monospace" font-size="10" fill="rgba(255,255,255,0.3)">340% organic traffic increase · Shopify Plus · 2025</text>
        </svg>
        <div class="port-overlay">
          <span class="port-cat">E-Commerce · Health & Wellness</span>
          <div class="port-title">VitaRoot Health Co.</div>
          <div class="port-meta">Shopify Plus · 340% Traffic Increase · 4.8% CVR</div>
          <div class="port-stats">
            <div><div class="port-stat-val">340%</div><div class="port-stat-lbl">Traffic</div></div>
            <div><div class="port-stat-val">4.8%</div><div class="port-stat-lbl">Conversion</div></div>
            <div><div class="port-stat-val">3wk</div><div class="port-stat-lbl">Delivery</div></div>
          </div>
        </div>
        <div class="port-link-btn" onclick="showToast('Opening VitaRoot case study...', 'info')">↗</div>
      </div>
      <!-- SMALL CARDS -->
      <div class="port-card" data-cat="saas">
        <svg class="port-art port-art-sm" viewBox="0 0 500 295" xmlns="http://www.w3.org/2000/svg">
          <defs><linearGradient id="pc2" x1="0" y1="0" x2="1" y2="1"><stop offset="0%" stop-color="#080f20"/><stop offset="100%" stop-color="#0a1526"/></linearGradient></defs>
          <rect width="500" height="295" fill="url(#pc2)"/>
          <!-- Dashboard -->
          <rect x="25" y="20" width="450" height="255" rx="6" fill="rgba(255,255,255,0.02)" stroke="rgba(255,255,255,0.05)" stroke-width="1"/>
          <rect x="25" y="20" width="90" height="255" rx="6" fill="rgba(255,255,255,0.04)"/>
          <rect x="40" y="40" width="60" height="8" rx="2" fill="rgba(184,255,0,0.5)"/>
          <rect x="40" y="58" width="50" height="5" rx="2" fill="rgba(255,255,255,0.1)"/>
          <rect x="40" y="70" width="55" height="5" rx="2" fill="rgba(255,255,255,0.07)"/>
          <rect x="40" y="82" width="45" height="5" rx="2" fill="rgba(255,255,255,0.07)"/>
          <rect x="40" y="94" width="50" height="5" rx="2" fill="rgba(255,255,255,0.07)"/>
          <!-- Chart -->
          <rect x="130" y="40" width="320" height="80" rx="3" fill="rgba(255,255,255,0.02)"/>
          <polyline points="145,110 175,82 215,92 255,65 295,75 335,50 375,62 415,40" fill="none" stroke="rgba(184,255,0,0.7)" stroke-width="2.5"/>
          <polyline points="145,110 175,82 215,92 255,65 295,75 335,50 375,62 415,40 415,120 145,120" fill="rgba(184,255,0,0.06)"/>
          <!-- Mini cards row -->
          <rect x="130" y="135" width="95" height="55" rx="3" fill="rgba(255,255,255,0.03)"/>
          <rect x="235" y="135" width="95" height="55" rx="3" fill="rgba(255,255,255,0.03)"/>
          <rect x="340" y="135" width="95" height="55" rx="3" fill="rgba(255,255,255,0.03)"/>
          <text x="177" y="158" text-anchor="middle" font-family="monospace" font-size="14" fill="rgba(184,255,0,0.9)" font-weight="bold">$48k</text>
          <text x="177" y="172" text-anchor="middle" font-family="monospace" font-size="7" fill="rgba(255,255,255,0.25)">MRR</text>
          <text x="282" y="158" text-anchor="middle" font-family="monospace" font-size="14" fill="rgba(184,255,0,0.9)" font-weight="bold">1,240</text>
          <text x="282" y="172" text-anchor="middle" font-family="monospace" font-size="7" fill="rgba(255,255,255,0.25)">USERS</text>
          <text x="387" y="158" text-anchor="middle" font-family="monospace" font-size="14" fill="rgba(184,255,0,0.9)" font-weight="bold">92%</text>
          <text x="387" y="172" text-anchor="middle" font-family="monospace" font-size="7" fill="rgba(255,255,255,0.25)">RETENTION</text>
          <text x="40" y="248" font-family="monospace" font-size="8" fill="rgba(184,255,0,0.5)" letter-spacing="1">SAAS · FINTECH</text>
          <text x="40" y="265" font-family="sans-serif" font-size="15" fill="white" font-weight="bold">LedgerAI Dashboard</text>
        </svg>
        <div class="port-overlay">
          <span class="port-cat">SaaS · FinTech Dashboard</span>
          <div class="port-title">LedgerAI Platform</div>
          <div class="port-meta">React / Next.js · 2025</div>
        </div>
        <div class="port-link-btn" onclick="showToast('Opening LedgerAI case study...', 'info')">↗</div>
      </div>
      <div class="port-card" data-cat="ecom">
        <svg class="port-art port-art-sm" viewBox="0 0 500 295" xmlns="http://www.w3.org/2000/svg">
          <defs><linearGradient id="pc3" x1="0" y1="0" x2="1" y2="1"><stop offset="0%" stop-color="#1a0d00"/><stop offset="100%" stop-color="#0f0800"/></linearGradient></defs>
          <rect width="500" height="295" fill="url(#pc3)"/>
          <!-- Product grid -->
          <rect x="25" y="20" width="135" height="170" rx="4" fill="rgba(245,200,66,0.06)" stroke="rgba(245,200,66,0.08)" stroke-width="1"/>
          <rect x="25" y="20" width="135" height="110" rx="4" fill="rgba(245,200,66,0.1)"/>
          <text x="92" y="85" text-anchor="middle" font-size="36" fill="rgba(245,200,66,0.5)">☕</text>
          <rect x="35" y="140" width="80" height="6" rx="2" fill="rgba(255,255,255,0.2)"/>
          <rect x="35" y="154" width="55" height="6" rx="2" fill="rgba(245,200,66,0.6)"/>
          <rect x="35" y="170" width="70" height="14" rx="2" fill="rgba(184,255,0,0.5)"/>
          <rect x="172" y="20" width="135" height="170" rx="4" fill="rgba(184,255,0,0.05)" stroke="rgba(184,255,0,0.1)" stroke-width="1"/>
          <rect x="172" y="20" width="135" height="110" rx="4" fill="rgba(184,255,0,0.08)"/>
          <text x="239" y="85" text-anchor="middle" font-size="36" fill="rgba(184,255,0,0.4)">🍵</text>
          <rect x="182" y="140" width="80" height="6" rx="2" fill="rgba(255,255,255,0.2)"/>
          <rect x="182" y="154" width="55" height="6" rx="2" fill="rgba(184,255,0,0.6)"/>
          <rect x="182" y="170" width="70" height="14" rx="2" fill="rgba(184,255,0,0.5)"/>
          <rect x="320" y="20" width="155" height="255" rx="4" fill="rgba(255,255,255,0.03)" stroke="rgba(255,255,255,0.06)" stroke-width="1"/>
          <text x="397" y="50" text-anchor="middle" font-family="monospace" font-size="9" fill="rgba(255,255,255,0.3)" letter-spacing="1">YOUR CART</text>
          <rect x="335" y="60" width="125" height="1" fill="rgba(255,255,255,0.06)"/>
          <text x="397" y="100" text-anchor="middle" font-family="monospace" font-size="20" fill="rgba(184,255,0,0.9)" font-weight="bold">$124</text>
          <rect x="335" y="200" width="125" height="28" rx="2" fill="rgba(184,255,0,0.8)"/>
          <text x="397" y="219" text-anchor="middle" font-family="sans-serif" font-size="11" fill="#0a0a0a" font-weight="bold">CHECKOUT</text>
          <text x="40" y="240" font-family="monospace" font-size="8" fill="rgba(245,200,66,0.6)" letter-spacing="1">E-COMMERCE · F&B</text>
          <text x="40" y="258" font-family="sans-serif" font-size="15" fill="white" font-weight="bold">BrewCraft Artisan Store</text>
          <text x="40" y="272" font-family="monospace" font-size="8" fill="rgba(255,255,255,0.2)">$2.1M GMV Year One</text>
        </svg>
        <div class="port-overlay">
          <span class="port-cat">E-Commerce · F&B</span>
          <div class="port-title">BrewCraft Artisan</div>
          <div class="port-meta">Shopify Plus · $2.1M GMV Year One</div>
        </div>
        <div class="port-link-btn" onclick="showToast('Opening BrewCraft case study...', 'info')">↗</div>
      </div>
    </div>
    <div style="text-align:center;margin-top:3rem" class="reveal">
      <a href="#contact" class="btn btn-secondary">View Full Portfolio (24 Projects) →</a>
    </div>
  </div>
</section>

<!-- ══ TESTIMONIALS ══ -->
<section id="testimonials">
  <div class="container section-pad">
    <div class="testi-layout">
      <div class="reveal-l">
        <div class="label-row"><div class="label-line"></div><span class="label-text">Client Reviews</span></div>
        <div class="testi-rating-big">4.9</div>
        <div class="testi-stars-row">★★★★★</div>
        <div class="testi-review-count">Based on 240+ verified reviews</div>
        <div class="testi-platforms stagger">
          <div class="platform-badge"><span class="platform-icon">⭐</span><div><div class="platform-name">Clutch</div><div class="platform-rating">4.9/5 · 86 reviews</div></div></div>
          <div class="platform-badge"><span class="platform-icon">🏆</span><div><div class="platform-name">Google</div><div class="platform-rating">5.0/5 · 124 reviews</div></div></div>
          <div class="platform-badge"><span class="platform-icon">💼</span><div><div class="platform-name">Upwork</div><div class="platform-rating">Top Rated Plus · 30+ reviews</div></div></div>
        </div>
        <div style="margin-top:3rem">
          <h2 class="section-title" style="font-size:clamp(2rem,3vw,3.5rem)">What Our<br><em>Clients Say</em></h2>
        </div>
      </div>
      <div class="testi-cards stagger reveal-r">
        <div class="testi-card">
          <div class="testi-stars">★★★★★</div>
          <div class="testi-text-content">PixelForge completely transformed our business. Our new site generates 3× more leads than our old one, and it launched in exactly 3 weeks as promised. Best investment we've made.</div>
          <div class="testi-author-row">
            <div class="testi-avatar">SR</div>
            <div><div class="testi-name">Sarah Richardson</div><div class="testi-role">CEO · VitaRoot Health · London</div></div>
          </div>
        </div>
        <div class="testi-card">
          <div class="testi-stars">★★★★★</div>
          <div class="testi-text-content">I've worked with 4 agencies before PixelForge. The difference? They understood conversion goals, not just aesthetics. Our checkout rate went up 62% in the first month.</div>
          <div class="testi-author-row">
            <div class="testi-avatar">MK</div>
            <div><div class="testi-name">Marcus Klein</div><div class="testi-role">Founder · BrewCraft Artisan · Berlin</div></div>
          </div>
        </div>
        <div class="testi-card">
          <div class="testi-stars">★★★★★</div>
          <div class="testi-text-content">The animations and scroll effects stopped people in their tracks. Three investors reached out after seeing our new site. That's the ROI of great design — and great execution.</div>
          <div class="testi-author-row">
            <div class="testi-avatar">AP</div>
            <div><div class="testi-name">Anika Patel</div><div class="testi-role">CTO · LedgerAI · San Francisco</div></div>
          </div>
        </div>
        <div class="testi-card">
          <div class="testi-stars">★★★★★</div>
          <div class="testi-text-content">Zero surprises. They delivered exactly what was scoped, on time, on budget. The 6-month post-launch support is genuinely exceptional. Highly, highly recommended.</div>
          <div class="testi-author-row">
            <div class="testi-avatar">TN</div>
            <div><div class="testi-name">Thomas Ng</div><div class="testi-role">Director · Meridian Real Estate · Singapore</div></div>
          </div>
        </div>
        <div class="testi-card">
          <div class="testi-stars">★★★★★</div>
          <div class="testi-text-content">We went from page 4 to page 1 on Google in 3 months. The SEO foundation they built is incredible. Organic traffic up 290%. I can't recommend these guys enough.</div>
          <div class="testi-author-row">
            <div class="testi-avatar">JL</div>
            <div><div class="testi-name">Julia Laurent</div><div class="testi-role">Marketing Director · EcoPack · Paris</div></div>
          </div>
        </div>
        <div class="testi-card">
          <div class="testi-stars">★★★★★</div>
          <div class="testi-text-content">The mobile experience they built cut our bounce rate in half. Every button, every form, every interaction works perfectly. This is what true craftsmanship looks like.</div>
          <div class="testi-author-row">
            <div class="testi-avatar">RO</div>
            <div><div class="testi-name">Ryan O'Brien</div><div class="testi-role">Owner · Prestige Fitness · Dublin</div></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ══ TEAM ══ -->
<section id="team">
  <div class="container section-pad">
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:end;margin-bottom:4rem;">
      <div class="reveal-l">
        <div class="label-row"><div class="label-line"></div><span class="label-text">Our Team</span></div>
        <h2 class="section-title">The Minds<br>Behind <em>Every Pixel</em></h2>
      </div>
      <p class="reveal-r" style="font-family:'Fraunces',serif;font-style:italic;font-size:.95rem;color:var(--white-60);line-height:1.9;">Every person on our team was hired for obsession, not credentials. We're designers who code, developers who care about UX, and strategists who think in conversion funnels — 24 people, one standard: excellence.</p>
    </div>
    <div class="team-grid stagger">
      <div class="team-card">
        <div class="team-avatar-wrap"><div class="team-avatar" style="background:rgba(184,255,0,0.1);color:var(--lime);">JM<div class="team-role-dot"></div></div></div>
        <div class="team-name">James Morgan</div>
        <div class="team-role">Founder & Creative Director</div>
        <div class="team-bio">8 years building digital experiences. Former design lead at two Y Combinator startups. Obsessed with the intersection of beauty and function.</div>
        <div class="team-socials">
          <a href="#" class="team-social" onclick="showToast('Opening Twitter...','info')">𝕏</a>
          <a href="#" class="team-social" onclick="showToast('Opening LinkedIn...','info')">in</a>
          <a href="#" class="team-social" onclick="showToast('Opening Dribbble...','info')">Db</a>
        </div>
      </div>
      <div class="team-card">
        <div class="team-avatar-wrap"><div class="team-avatar" style="background:rgba(255,92,0,0.1);color:var(--orange);">LC<div class="team-role-dot"></div></div></div>
        <div class="team-name">Lisa Chen</div>
        <div class="team-role">Head of Development</div>
        <div class="team-bio">Senior full-stack engineer with a design eye. Built products used by 2M+ users. Specializes in React, Next.js, and performance engineering.</div>
        <div class="team-socials">
          <a href="#" class="team-social" onclick="showToast('Opening GitHub...','info')">GH</a>
          <a href="#" class="team-social" onclick="showToast('Opening LinkedIn...','info')">in</a>
        </div>
      </div>
      <div class="team-card">
        <div class="team-avatar-wrap"><div class="team-avatar" style="background:rgba(240,238,234,0.05);color:var(--white);">SK<div class="team-role-dot"></div></div></div>
        <div class="team-name">Sarah Kim</div>
        <div class="team-role">Lead UX Strategist</div>
        <div class="team-bio">Former Google UX researcher. Brings data-driven design thinking to every project. Has conducted 400+ user interviews and 80+ usability tests.</div>
        <div class="team-socials">
          <a href="#" class="team-social" onclick="showToast('Opening LinkedIn...','info')">in</a>
          <a href="#" class="team-social" onclick="showToast('Opening Medium...','info')">Md</a>
        </div>
      </div>
      <div class="team-card">
        <div class="team-avatar-wrap"><div class="team-avatar" style="background:rgba(184,255,0,0.07);color:var(--lime);">AR<div class="team-role-dot"></div></div></div>
        <div class="team-name">Arjun Rao</div>
        <div class="team-role">SEO & Growth Lead</div>
        <div class="team-bio">Built and ranked 60+ websites to page one. Expert in technical SEO, Core Web Vitals, and data-driven content strategy that generates compounding organic growth.</div>
        <div class="team-socials">
          <a href="#" class="team-social" onclick="showToast('Opening LinkedIn...','info')">in</a>
          <a href="#" class="team-social" onclick="showToast('Opening Twitter...','info')">𝕏</a>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ══ FAQ ══ -->
<section id="faq">
  <div class="container section-pad">
    <div class="faq-layout">
      <div class="reveal-l">
        <div class="label-row"><div class="label-line"></div><span class="label-text">FAQ</span></div>
        <h2 class="section-title">Questions<br>We <em>Always</em><br>Get Asked</h2>
        <p>Still have questions? Email us directly at <span style="color:var(--lime)">hello@pixelforge.studio</span> or book a free 30-minute strategy call — no strings attached.</p>
        <div style="margin-top:2rem">
          <a href="#" class="btn btn-secondary" onclick="openModal(event)">Book Strategy Call →</a>
        </div>
      </div>
      <div class="faq-list stagger">
        <div class="faq-item open">
          <div class="faq-question" onclick="toggleFaq(this)">
            <span class="faq-q-text">How long does a project take?</span>
            <div class="faq-plus">+</div>
          </div>
          <div class="faq-answer">
            <div class="faq-answer-inner">Most projects are completed in 3–6 weeks from kickoff. The Launch plan typically delivers in 3 weeks, Scale in 4 weeks, and Dominate in 5–6 weeks depending on complexity. We commit to delivery timelines in writing — if we miss it, you get a discount on your next project.</div>
          </div>
        </div>
        <div class="faq-item">
          <div class="faq-question" onclick="toggleFaq(this)">
            <span class="faq-q-text">Do I own the website after it's built?</span>
            <div class="faq-plus">+</div>
          </div>
          <div class="faq-answer">
            <div class="faq-answer-inner">100%. You own everything — the code, the design files, the domain, the hosting account. We hand over complete ownership at launch. We don't lock you in or charge ongoing licensing fees. The only exception is third-party software (like Shopify or Webflow subscriptions) which you'd pay directly.</div>
          </div>
        </div>
        <div class="faq-item">
          <div class="faq-question" onclick="toggleFaq(this)">
            <span class="faq-q-text">What if I need changes after launch?</span>
            <div class="faq-plus">+</div>
          </div>
          <div class="faq-answer">
            <div class="faq-answer-inner">All plans include a post-launch support period (3, 6, or 12 months). During this time, bug fixes and minor content updates are included at no extra cost. For larger changes or new features, we scope and quote separately — always transparently, always fairly.</div>
          </div>
        </div>
        <div class="faq-item">
          <div class="faq-question" onclick="toggleFaq(this)">
            <span class="faq-q-text">How does payment work?</span>
            <div class="faq-plus">+</div>
          </div>
          <div class="faq-answer">
            <div class="faq-answer-inner">We work on a 50/50 structure: 50% due at project kickoff, 50% due at launch. For larger enterprise projects, we can arrange a 3-stage payment milestone schedule. We accept bank transfer, credit card, and Stripe. No hidden fees, ever.</div>
          </div>
        </div>
        <div class="faq-item">
          <div class="faq-question" onclick="toggleFaq(this)">
            <span class="faq-q-text">Do you work with international clients?</span>
            <div class="faq-plus">+</div>
          </div>
          <div class="faq-answer">
            <div class="faq-answer-inner">Absolutely. We currently have active clients in 18 countries. Our team spans NYC, London, and Singapore — which means we have team members in your timezone almost anywhere in the world. All communication is in English, and we use Notion + Loom for async collaboration.</div>
          </div>
        </div>
        <div class="faq-item">
          <div class="faq-question" onclick="toggleFaq(this)">
            <span class="faq-q-text">Can you help with copy and content?</span>
            <div class="faq-plus">+</div>
          </div>
          <div class="faq-answer">
            <div class="faq-answer-inner">Yes — copywriting is available as an add-on service. Our conversion copywriters specialize in website copy that's built to sell. We've found that clients who use our copywriting service see up to 40% better conversion rates versus those who provide their own copy.</div>
          </div>
        </div>
        <div class="faq-item">
          <div class="faq-question" onclick="toggleFaq(this)">
            <span class="faq-q-text">What information do you need to start?</span>
            <div class="faq-plus">+</div>
          </div>
          <div class="faq-answer">
            <div class="faq-answer-inner">To get started, we need: a brief description of your project and goals, your target audience, any examples of sites you like, your timeline, and your budget range. We handle everything else — research, strategy, design, and development. Our discovery call questionnaire makes this process easy.</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ══ CONTACT ══ -->
<section id="contact">
  <div class="container section-pad">
    <div class="contact-layout">
      <div class="contact-left reveal-l">
        <div class="label-row"><div class="label-line"></div><span class="label-text">Get In Touch</span><span class="label-num">07/07</span></div>
        <h2 class="section-title">Let's Build<br><em>Something</em><br>Extraordinary</h2>
        <p>Ready to turn your website into your best salesperson? Fill out the form and we'll send you a detailed proposal within 24 hours — no commitment, no pressure.</p>
        <div class="contact-info-cards stagger">
          <div class="contact-card">
            <span class="contact-card-icon">📧</span>
            <div><div class="contact-card-label">Email</div><div class="contact-card-val">hello@pixelforge.studio</div></div>
          </div>
          <div class="contact-card">
            <span class="contact-card-icon">📞</span>
            <div><div class="contact-card-label">Phone</div><div class="contact-card-val">+1 (555) 847-2931</div></div>
          </div>
          <div class="contact-card">
            <span class="contact-card-icon">📍</span>
            <div><div class="contact-card-label">Offices</div><div class="contact-card-val">New York · London · Singapore</div></div>
          </div>
          <div class="contact-card">
            <span class="contact-card-icon">⏰</span>
            <div><div class="contact-card-label">Response Time</div><div class="contact-card-val">Within 24 hours — guaranteed</div></div>
          </div>
          <div class="contact-card">
            <span class="contact-card-icon">📅</span>
            <div><div class="contact-card-label">Current Availability</div><div class="contact-card-val">3 client spots open — April 2026</div></div>
          </div>
        </div>
      </div>
      <div class="contact-right reveal-r">
        <div class="contact-form-box" id="contactFormBox">
          <div id="contactFormInner">
            <div class="form-title">Send Us a Message</div>
            <div class="form-subtitle">ALL FIELDS MARKED * ARE REQUIRED · WE RESPOND IN 24 HOURS</div>
            <div class="form-grid">
              <div class="form-group">
                <label class="form-label">First Name *</label>
                <input class="form-input" id="cfFirst" type="text" placeholder="First name" autocomplete="given-name">
              </div>
              <div class="form-group">
                <label class="form-label">Last Name *</label>
                <input class="form-input" id="cfLast" type="text" placeholder="Last name" autocomplete="family-name">
              </div>
            </div>
            <div class="form-group">
              <label class="form-label">Email Address *</label>
              <input class="form-input" id="cfEmail" type="email" placeholder="you@company.com" autocomplete="email">
            </div>
            <div class="form-group">
              <label class="form-label">Company / Website URL</label>
              <input class="form-input" id="cfCompany" type="text" placeholder="Your company or current website">
            </div>
            <div class="form-grid">
              <div class="form-group">
                <label class="form-label">Service Needed *</label>
                <select class="form-select" id="cfService">
                  <option value="">Select a service...</option>
                  <option>Business Website</option>
                  <option>E-Commerce Store</option>
                  <option>SaaS / Web App</option>
                  <option>Landing Page</option>
                  <option>UI/UX Design</option>
                  <option>SEO & Performance</option>
                  <option>Brand Identity</option>
                  <option>Full Digital Package</option>
                  <option>Not Sure Yet</option>
                </select>
              </div>
              <div class="form-group">
                <label class="form-label">Budget Range</label>
                <select class="form-select" id="cfBudget">
                  <option value="">Select range...</option>
                  <option>Under $2,000</option>
                  <option>$2,000 – $5,000</option>
                  <option>$5,000 – $15,000</option>
                  <option>$15,000 – $30,000</option>
                  <option>$30,000+</option>
                </select>
              </div>
            </div>
            <div class="form-group">
              <label class="form-label">Tell Us About Your Project *</label>
              <textarea class="form-textarea" id="cfMsg" placeholder="Describe your project, goals, timeline, and any other details..." maxlength="1000"></textarea>
              <div class="char-count"><span id="charCount">0</span>/1000</div>
            </div>
            <div class="form-checkbox">
              <input type="checkbox" id="cfPrivacy">
              <div class="checkbox-custom" onclick="document.getElementById('cfPrivacy').click()"></div>
              <label for="cfPrivacy">I agree to the <a href="#">Privacy Policy</a> and consent to being contacted about my project. No spam, ever.</label>
            </div>
            <button class="btn btn-primary btn-submit" id="cfSubmitBtn" onclick="submitContact()">
              <div class="btn-submit-text">
                <div class="loading-ring"></div>
                <span>Send Message →</span>
              </div>
            </button>
            <p class="form-note">🔒 Your info is 100% private and secure. We never sell or share your data.</p>
          </div>
          <div class="form-success-msg" id="contactSuccess">
            <div class="success-check">🚀</div>
            <div class="success-title">Message Sent!</div>
            <div class="success-body">Your project brief has been received by our team. A senior strategist will review it and respond with a tailored proposal within 24 hours. Check your inbox — including spam, just in case.</div>
            <div style="margin-top:2.5rem"><a href="#pricing" class="btn btn-secondary" style="display:inline-flex">← Review Our Pricing</a></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ══ CTA FINAL ══ -->
<section id="cta-final">
  <div class="cta-final-layout">
    <div class="cta-final-text reveal-l">
      <h2>READY TO<br>DOMINATE<br>YOUR MARKET?</h2>
      <p>Join 240+ businesses that chose PixelForge to power their growth. 3 client spots available this April.</p>
    </div>
    <div class="cta-final-actions reveal-r">
      <a href="#" class="btn-cta-dark" onclick="openModal(event)">Get Free Quote →</a>
      <a href="#services" class="btn-cta-outline">Explore Services</a>
    </div>
  </div>
</section>

<!-- ══ FOOTER ══ -->
<footer>
  <div class="footer-grid">
    <div class="footer-brand">
      <div class="footer-logo"><div class="footer-logo-mark"></div><span class="footer-logo-text">PIXELFORGE</span></div>
      <p>Premium web design agency crafting high-converting digital experiences for ambitious businesses worldwide. 240+ projects. 8 years. 18 countries.</p>
      <div class="footer-newsletter">
        <p>Get weekly web design tips & industry insights:</p>
        <div class="footer-nl-form">
          <input class="footer-nl-input" id="nlEmail" type="email" placeholder="your@email.com">
          <button class="footer-nl-btn" onclick="subscribeNewsletter()">JOIN</button>
        </div>
      </div>
    </div>
    <div>
      <div class="footer-col-title">Services</div>
      <ul class="footer-links">
        <li><a href="#services">Business Websites</a></li>
        <li><a href="#services">E-Commerce Stores</a></li>
        <li><a href="#services">SaaS & Web Apps</a></li>
        <li><a href="#services">Landing Pages</a></li>
        <li><a href="#services">UI/UX Design</a></li>
        <li><a href="#services">SEO & Performance</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-col-title">Company</div>
      <ul class="footer-links">
        <li><a href="#intro">About Us</a></li>
        <li><a href="#team">Our Team</a></li>
        <li><a href="#portfolio">Our Work</a></li>
        <li><a href="#process">Our Process</a></li>
        <li><a href="#testimonials">Reviews</a></li>
        <li><a href="#" onclick="showToast('Opening careers page...','info')">Careers</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-col-title">Resources</div>
      <ul class="footer-links">
        <li><a href="#pricing">Pricing</a></li>
        <li><a href="#faq">FAQ</a></li>
        <li><a href="#" onclick="showToast('Opening blog...','info')">Blog & Insights</a></li>
        <li><a href="#" onclick="showToast('Opening client portal...','info')">Client Portal</a></li>
        <li><a href="#" onclick="showToast('Opening project checker...','info')">Project Checker</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-col-title">Connect</div>
      <ul class="footer-links">
        <li><a href="#" onclick="showToast('Opening Twitter/X...','info')">Twitter / X</a></li>
        <li><a href="#" onclick="showToast('Opening LinkedIn...','info')">LinkedIn</a></li>
        <li><a href="#" onclick="showToast('Opening Dribbble...','info')">Dribbble</a></li>
        <li><a href="#" onclick="showToast('Opening Instagram...','info')">Instagram</a></li>
        <li><a href="#" onclick="showToast('Opening YouTube...','info')">YouTube</a></li>
        <li><a href="#" onclick="showToast('Opening Discord...','info')">Discord</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <div class="footer-copy">© 2026 PixelForge Studio Ltd. All rights reserved. Crafted with obsession.</div>
    <div class="footer-legal">
      <a href="#" onclick="showToast('Opening Privacy Policy...','info')">Privacy Policy</a>
      <a href="#" onclick="showToast('Opening Terms...','info')">Terms of Service</a>
      <a href="#" onclick="showToast('Opening Cookie Policy...','info')">Cookies</a>
    </div>
    <div class="footer-socials">
      <a href="#" class="footer-social" onclick="showToast('Opening Twitter/X...','info')">𝕏</a>
      <a href="#" class="footer-social" onclick="showToast('Opening LinkedIn...','info')">in</a>
      <a href="#" class="footer-social" onclick="showToast('Opening Dribbble...','info')">Db</a>
      <a href="#" class="footer-social" onclick="showToast('Opening Instagram...','info')">📸</a>
    </div>
  </div>
</footer>

<!-- ═══════════════════════════════════════════════
     JAVASCRIPT — FULL ENGINE
═══════════════════════════════════════════════ -->
<script>
'use strict';

/* ══ PARTICLE CANVAS ENGINE ══ */
(function() {
  const canvas = document.getElementById('particle-canvas');
  const ctx = canvas.getContext('2d');
  let W, H, particles = [], mouseX = 0, mouseY = 0, frame = 0;

  function resize() { W = canvas.width = window.innerWidth; H = canvas.height = window.innerHeight; }
  resize();
  window.addEventListener('resize', resize, { passive: true });

  class Particle {
    constructor() { this.reset(); }
    reset() {
      this.x = Math.random() * W;
      this.y = Math.random() * H;
      this.vx = (Math.random() - 0.5) * 0.3;
      this.vy = (Math.random() - 0.5) * 0.3;
      this.size = Math.random() * 1.5 + 0.3;
      this.alpha = Math.random() * 0.4 + 0.05;
      this.color = Math.random() > 0.85 ? 'rgba(184,255,0,' : Math.random() > 0.5 ? 'rgba(240,238,234,' : 'rgba(255,92,0,';
    }
    update() {
      const dx = mouseX - this.x, dy = mouseY - this.y;
      const dist = Math.sqrt(dx * dx + dy * dy);
      if (dist < 120) {
        this.vx -= dx / dist * 0.04;
        this.vy -= dy / dist * 0.04;
      }
      this.vx *= 0.99; this.vy *= 0.99;
      this.x += this.vx; this.y += this.vy;
      if (this.x < 0 || this.x > W || this.y < 0 || this.y > H) this.reset();
    }
    draw() {
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
      ctx.fillStyle = this.color + this.alpha + ')';
      ctx.fill();
    }
  }

  for (let i = 0; i < 120; i++) particles.push(new Particle());

  function drawConnections() {
    for (let i = 0; i < particles.length; i++) {
      for (let j = i + 1; j < particles.length; j++) {
        const dx = particles[i].x - particles[j].x;
        const dy = particles[i].y - particles[j].y;
        const d = Math.sqrt(dx * dx + dy * dy);
        if (d < 100) {
          ctx.beginPath();
          ctx.moveTo(particles[i].x, particles[i].y);
          ctx.lineTo(particles[j].x, particles[j].y);
          ctx.strokeStyle = `rgba(184,255,0,${0.04 * (1 - d / 100)})`;
          ctx.lineWidth = 0.5;
          ctx.stroke();
        }
      }
    }
  }

  function loop() {
    ctx.clearRect(0, 0, W, H);
    particles.forEach(p => { p.update(); p.draw(); });
    drawConnections();
    frame++;
    requestAnimationFrame(loop);
  }
  loop();

  document.addEventListener('mousemove', e => { mouseX = e.clientX; mouseY = e.clientY; }, { passive: true });
})();

/* ══ HERO CANVAS BG ══ */
(function() {
  const canvas = document.getElementById('heroCanvas');
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  let W, H;
  function resize() { W = canvas.width = canvas.offsetWidth; H = canvas.height = canvas.offsetHeight; }
  resize();
  const resizeObs = new ResizeObserver(resize);
  resizeObs.observe(canvas);

  const rings = Array.from({length: 5}, (_, i) => ({
    r: 80 + i * 80, alpha: 0.03 - i * 0.004, speed: 0.0003 + i * 0.0001, angle: 0
  }));

  function draw(ts) {
    ctx.clearRect(0, 0, W, H);
    const cx = W * 0.65, cy = H * 0.35;
    rings.forEach((ring, i) => {
      ring.angle += ring.speed;
      ctx.beginPath();
      ctx.arc(cx, cy, ring.r, 0, Math.PI * 2);
      ctx.strokeStyle = `rgba(184,255,0,${ring.alpha})`;
      ctx.lineWidth = 1;
      ctx.stroke();
      const dotX = cx + Math.cos(ring.angle) * ring.r;
      const dotY = cy + Math.sin(ring.angle) * ring.r;
      ctx.beginPath();
      ctx.arc(dotX, dotY, 2, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(184,255,0,${ring.alpha * 5})`;
      ctx.fill();
    });
    requestAnimationFrame(draw);
  }
  requestAnimationFrame(draw);
})();

/* ══ CURSOR ══ */
const curDot = document.getElementById('cursor-dot');
const curRing = document.getElementById('cursor-ring');
const curText = document.getElementById('cursor-text');
let cx = 0, cy = 0, rx = 0, ry = 0;

document.addEventListener('mousemove', e => { cx = e.clientX; cy = e.clientY; }, { passive: true });

(function animCursor() {
  curDot.style.left = cx + 'px'; curDot.style.top = cy + 'px';
  rx += (cx - rx) * 0.13; ry += (cy - ry) * 0.13;
  curRing.style.left = rx + 'px'; curRing.style.top = ry + 'px';
  if (curText) { curText.style.left = cx + 'px'; curText.style.top = (cy - 36) + 'px'; }
  requestAnimationFrame(animCursor);
})();

document.querySelectorAll('a, button, .svc-item, .plan, .testi-card, .cap-card, .proof-card, .port-card, .team-card, .contact-card, input, select, textarea').forEach(el => {
  el.addEventListener('mouseenter', () => document.body.classList.add('cursor-hover'));
  el.addEventListener('mouseleave', () => document.body.classList.remove('cursor-hover'));
});
document.querySelectorAll('a').forEach(a => {
  a.addEventListener('mouseenter', () => document.body.classList.add('cursor-link'));
  a.addEventListener('mouseleave', () => document.body.classList.remove('cursor-link'));
});

/* ══ MAGNETIC BUTTONS ══ */
document.querySelectorAll('.magnetic-wrap').forEach(wrap => {
  const btn = wrap.querySelector('a, button');
  if (!btn) return;
  wrap.addEventListener('mousemove', e => {
    const r = wrap.getBoundingClientRect();
    const mx = e.clientX - r.left - r.width / 2;
    const my = e.clientY - r.top - r.height / 2;
    btn.style.transform = `translate(${mx * 0.3}px, ${my * 0.4}px)`;
  });
  wrap.addEventListener('mouseleave', () => { btn.style.transform = ''; });
});

/* ══ RIPPLE EFFECT ══ */
document.querySelectorAll('.btn').forEach(btn => {
  btn.addEventListener('click', function(e) {
    const r = this.getBoundingClientRect();
    const ripple = document.createElement('span');
    ripple.classList.add('ripple');
    const size = Math.max(r.width, r.height) * 2;
    ripple.style.cssText = `width:${size}px;height:${size}px;left:${e.clientX - r.left - size/2}px;top:${e.clientY - r.top - size/2}px`;
    this.appendChild(ripple);
    setTimeout(() => ripple.remove(), 700);
  });
});

/* ══ SCROLL PROGRESS ══ */
const progressBar = document.getElementById('progress-bar');
window.addEventListener('scroll', () => {
  const s = window.scrollY;
  const h = document.documentElement.scrollHeight - window.innerHeight;
  progressBar.style.transform = `scaleX(${s / h})`;
}, { passive: true });

/* ══ NAV SCROLL ══ */
const mainNav = document.getElementById('mainNav');
window.addEventListener('scroll', () => {
  mainNav.classList.toggle('scrolled', window.scrollY > 80);
}, { passive: true });

/* ══ HERO GRID PARALLAX ══ */
const heroGrid = document.getElementById('heroGrid');
window.addEventListener('scroll', () => {
  if (heroGrid) {
    const s = window.scrollY;
    heroGrid.style.transform = `perspective(1400px) rotateX(${28 + s * 0.012}deg) scale(1.5) translateY(${s * 0.18}px)`;
  }
}, { passive: true });

/* ══ SMOOTH SCROLL ══ */
document.querySelectorAll('a[href^="#"]').forEach(a => {
  a.addEventListener('click', function(e) {
    const href = this.getAttribute('href');
    if (!href || href === '#') return;
    const target = document.querySelector(href);
    if (target) { e.preventDefault(); target.scrollIntoView({ behavior: 'smooth', block: 'start' }); }
  });
});

/* ══ INTERSECTION OBSERVER ══ */
const ioOptions = { threshold: 0.08, rootMargin: '0px 0px -40px 0px' };
const io = new IntersectionObserver((entries) => {
  entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('in'); io.unobserve(e.target); } });
}, ioOptions);
document.querySelectorAll('.reveal, .reveal-l, .reveal-r, .reveal-scale, .stagger').forEach(el => io.observe(el));

/* ══ COUNTER ANIMATION ══ */
function animateNum(el, target, isFloat, duration = 1800) {
  let start = null;
  const numEl = el.querySelector('.num') || el;
  function step(ts) {
    if (!start) start = ts;
    const progress = Math.min((ts - start) / duration, 1);
    const eased = 1 - Math.pow(1 - progress, 3);
    const val = target * eased;
    if (numEl) numEl.textContent = isFloat ? val.toFixed(1) : Math.floor(val);
    else {
      const txt = el.childNodes[0];
      if (txt && txt.nodeType === 3) txt.textContent = isFloat ? val.toFixed(1) : Math.floor(val);
    }
    if (progress < 1) requestAnimationFrame(step);
  }
  requestAnimationFrame(step);
}

const counterIO = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (!e.isIntersecting) return;
    const el = e.target;
    const target = parseFloat(el.dataset.target);
    const isFloat = !!el.dataset.float;
    animateNum(el, target, isFloat);
    counterIO.unobserve(el);
  });
}, { threshold: 0.5 });

document.querySelectorAll('[data-target]').forEach(el => counterIO.observe(el));

/* ══ TYPED TEXT ══ */
const typedEl = document.getElementById('typedEl');
if (typedEl) {
  const phrases = ['E-Commerce', 'Business Sites', 'SaaS Apps', 'Landing Pages', 'Brand Identity', 'SEO Strategy', '3D Experiences', 'Web Apps'];
  let phraseIdx = 0, charIdx = 0, isDeleting = false;
  function type() {
    const phrase = phrases[phraseIdx];
    if (!isDeleting) {
      typedEl.textContent = phrase.slice(0, charIdx + 1);
      charIdx++;
      if (charIdx === phrase.length) { isDeleting = true; setTimeout(type, 2200); return; }
    } else {
      typedEl.textContent = phrase.slice(0, charIdx - 1);
      charIdx--;
      if (charIdx === 0) { isDeleting = false; phraseIdx = (phraseIdx + 1) % phrases.length; }
    }
    setTimeout(type, isDeleting ? 55 : 90);
  }
  type();
}

/* ══ MOBILE MENU ══ */
const hamburgerBtn = document.getElementById('hamburgerBtn');
const mobileNav = document.getElementById('mobileNav');
hamburgerBtn.addEventListener('click', () => {
  hamburgerBtn.classList.toggle('active');
  mobileNav.classList.toggle('open');
  document.body.style.overflow = mobileNav.classList.contains('open') ? 'hidden' : '';
});
function closeMobile() {
  hamburgerBtn.classList.remove('active');
  mobileNav.classList.remove('open');
  document.body.style.overflow = '';
}

/* ══ MODAL ══ */
const quoteModal = document.getElementById('quoteModal');
function openModal(e) {
  if (e) e.preventDefault();
  quoteModal.classList.add('open');
  document.body.style.overflow = 'hidden';
}
function closeModal() {
  quoteModal.classList.remove('open');
  document.body.style.overflow = '';
}
document.getElementById('modalCloseBtn').addEventListener('click', closeModal);
quoteModal.addEventListener('click', e => { if (e.target === quoteModal) closeModal(); });
document.addEventListener('keydown', e => { if (e.key === 'Escape') closeModal(); });

/* ══ TOAST ══ */
const toastEl = document.getElementById('toast');
let toastTimer;
function showToast(msg, type = 'success', duration = 3500) {
  document.getElementById('toast-msg').textContent = msg;
  document.getElementById('toast-icon').textContent = type === 'success' ? '✓' : type === 'error' ? '✗' : 'ℹ';
  toastEl.className = 'toast ' + type + ' show';
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => toastEl.classList.remove('show'), duration);
}

/* ══ FORM VALIDATION ══ */
function validateEmail(email) { return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(String(email).toLowerCase()); }

function highlightError(id) {
  const el = document.getElementById(id);
  if (!el) return;
  el.classList.add('error');
  el.focus();
  el.addEventListener('input', () => el.classList.remove('error'), { once: true });
}

function setLoading(btnId, loading) {
  const btn = document.getElementById(btnId);
  if (!btn) return;
  btn.classList.toggle('loading', loading);
  btn.disabled = loading;
}

/* ══ MODAL SUBMIT ══ */
function submitModal() {
  const first = document.getElementById('mFirst').value.trim();
  const last = document.getElementById('mLast').value.trim();
  const email = document.getElementById('mEmail').value.trim();
  const desc = document.getElementById('mDesc').value.trim();

  if (!first) { showToast('Please enter your first name', 'error'); highlightError('mFirst'); return; }
  if (!last) { showToast('Please enter your last name', 'error'); highlightError('mLast'); return; }
  if (!email || !validateEmail(email)) { showToast('Please enter a valid email address', 'error'); highlightError('mEmail'); return; }

  setLoading('modalSubmitBtn', true);
  setTimeout(() => {
    setLoading('modalSubmitBtn', false);
    document.getElementById('modalFormWrap').style.display = 'none';
    document.getElementById('modalSuccessMsg').classList.add('visible');
    showToast('Quote request sent! We\'ll reply within 24 hours.', 'success', 5000);
  }, 1400);
}

/* ══ CONTACT FORM SUBMIT ══ */
document.getElementById('cfMsg').addEventListener('input', function() {
  document.getElementById('charCount').textContent = this.value.length;
});

function submitContact() {
  const first = document.getElementById('cfFirst').value.trim();
  const last = document.getElementById('cfLast').value.trim();
  const email = document.getElementById('cfEmail').value.trim();
  const service = document.getElementById('cfService').value;
  const msg = document.getElementById('cfMsg').value.trim();
  const privacy = document.getElementById('cfPrivacy').checked;

  if (!first) { showToast('Please enter your first name', 'error'); highlightError('cfFirst'); return; }
  if (!last) { showToast('Please enter your last name', 'error'); highlightError('cfLast'); return; }
  if (!email || !validateEmail(email)) { showToast('Please enter a valid email address', 'error'); highlightError('cfEmail'); return; }
  if (!service) { showToast('Please select a service', 'error'); highlightError('cfService'); return; }
  if (msg.length < 15) { showToast('Please describe your project (at least 15 chars)', 'error'); highlightError('cfMsg'); return; }
  if (!privacy) { showToast('Please agree to the Privacy Policy', 'error'); return; }

  setLoading('cfSubmitBtn', true);
  setTimeout(() => {
    setLoading('cfSubmitBtn', false);
    document.getElementById('contactFormInner').style.display = 'none';
    document.getElementById('contactSuccess').classList.add('visible');
    showToast('✓ Message sent! We\'ll reply within 24 hours.', 'success', 6000);
  }, 1600);
}

/* ══ NEWSLETTER ══ */
function subscribeNewsletter() {
  const email = document.getElementById('nlEmail').value.trim();
  if (!email || !validateEmail(email)) { showToast('Please enter a valid email', 'error'); return; }
  setTimeout(() => {
    document.getElementById('nlEmail').value = '';
    showToast('✓ You\'re subscribed! Welcome to the PixelForge community.', 'success', 5000);
  }, 600);
}

/* ══ PRICING PLAN SELECT ══ */
function selectPlan(planName, price) {
  document.getElementById('mFirst').value = '';
  document.getElementById('mLast').value = '';
  document.getElementById('mEmail').value = '';
  document.getElementById('mBudget').value = price.includes('2,500') ? '$2,000 – $5,000' : price.includes('7,500') ? '$5,000 – $15,000' : '$15,000 – $30,000';
  document.getElementById('mService').value = 'Business Website';
  document.getElementById('mDesc').value = `I\'m interested in the ${planName} plan (${price}).`;
  document.getElementById('modalFormWrap').style.display = 'block';
  document.getElementById('modalSuccessMsg').classList.remove('visible');
  openModal(null);
}

/* ══ BILLING TOGGLE ══ */
let isAnnual = false;
function toggleBilling() {
  isAnnual = !isAnnual;
  document.getElementById('billingToggle').classList.toggle('on', isAnnual);
  document.getElementById('plansGrid').classList.toggle('annual', isAnnual);
  showToast(isAnnual ? '✓ Annual pricing applied — save 20%!' : 'Monthly pricing applied', 'success');
}

/* ══ FAQ ACCORDION ══ */
function toggleFaq(questionEl) {
  const item = questionEl.parentElement;
  const isOpen = item.classList.contains('open');
  document.querySelectorAll('.faq-item.open').forEach(i => i.classList.remove('open'));
  if (!isOpen) item.classList.add('open');
}

/* ══ PORTFOLIO FILTER ══ */
function filterPortfolio(cat, btn) {
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  document.querySelectorAll('.port-card').forEach(card => {
    const cardCat = card.dataset.cat;
    if (cat === 'all' || cardCat === cat) {
      card.style.opacity = '1'; card.style.transform = ''; card.style.pointerEvents = '';
    } else {
      card.style.opacity = '0.2'; card.style.transform = 'scale(0.97)'; card.style.pointerEvents = 'none';
    }
  });
  showToast(cat === 'all' ? 'Showing all projects' : `Filtering: ${cat.charAt(0).toUpperCase() + cat.slice(1)}`, 'info');
}

/* ══ PROCESS SCROLL ANIMATION ══ */
const processLine = document.getElementById('processLine');
const processStepsEl = document.getElementById('processSteps');
if (processLine && processStepsEl) {
  const processIO = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (!e.isIntersecting) return;
      let width = 0;
      const steps = processStepsEl.querySelectorAll('.process-step');
      steps.forEach((step, i) => {
        setTimeout(() => {
          step.classList.add('active');
          width = ((i + 1) / steps.length) * 100;
          processLine.style.width = width + '%';
        }, i * 300);
      });
      processIO.unobserve(e.target);
    });
  }, { threshold: 0.3 });
  processIO.observe(processStepsEl);
}

/* ══ 3D CARD TILT ══ */
document.querySelectorAll('.plan, .testi-card, .cap-card, .proof-card, .team-card').forEach(card => {
  card.addEventListener('mousemove', function(e) {
    const r = this.getBoundingClientRect();
    const x = (e.clientX - r.left) / r.width - 0.5;
    const y = (e.clientY - r.top) / r.height - 0.5;
    this.style.transform = `perspective(700px) rotateY(${x * 7}deg) rotateX(${-y * 5}deg) translateY(-6px)`;
  });
  card.addEventListener('mouseleave', function() { this.style.transform = ''; });
});
document.querySelectorAll('.port-card').forEach(card => {
  card.addEventListener('mousemove', function(e) {
    const r = this.getBoundingClientRect();
    const x = (e.clientX - r.left) / r.width - 0.5;
    const y = (e.clientY - r.top) / r.height - 0.5;
    this.style.transform = `perspective(900px) rotateY(${x * 4}deg) rotateX(${-y * 3}deg) translateY(-4px)`;
  });
  card.addEventListener('mouseleave', function() { this.style.transform = ''; });
});

/* ══ FLOATING CTA ══ */
const floatingCta = document.getElementById('floatingCta');
let floatingShown = false;
window.addEventListener('scroll', () => {
  if (!floatingShown && window.scrollY > window.innerHeight * 1.5) {
    floatingCta.classList.add('show');
    floatingShown = true;
  }
}, { passive: true });

/* ══ ORB PARALLAX FLOATS ══ */
const floatOrbs = document.querySelectorAll('.plan-glow');
window.addEventListener('scroll', () => {
  const s = window.scrollY;
  floatOrbs.forEach((orb, i) => { orb.style.transform = `translateY(${s * (0.03 + i * 0.01)}px)`; });
}, { passive: true });

/* ══ SERVICE ITEM HOVER SOUND / VIBRATION ══ */
document.querySelectorAll('.svc-item').forEach(item => {
  item.addEventListener('mouseenter', () => {
    if (navigator.vibrate) navigator.vibrate(5);
  });
});

/* ══ KEY SHORTCUTS ══ */
document.addEventListener('keydown', e => {
  if (e.altKey && e.key === 'q') openModal(null);
  if (e.altKey && e.key === 'c') { document.getElementById('contact').scrollIntoView({ behavior: 'smooth' }); }
});

/* ══ INIT ══ */
document.addEventListener('DOMContentLoaded', () => {
  // Stagger hero stats after 1.3s
  setTimeout(() => {
    document.querySelector('.hero-stats-row')?.classList.add('in');
  }, 1300);
});
</script>
</body>
</html>
