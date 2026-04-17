<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>How Long Have You Been You?</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=EB+Garamond:ital,wght@0,400;0,500;1,400;1,500&family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300;1,400&family=Jost:wght@200;300;400&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --ink: #1a1a18;
    --warm-white: #f7f5f0;
    --mid: #8a8780;
    --light-rule: rgba(26,26,24,0.12);
    --accent: #3a3935;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--warm-white);
    color: var(--ink);
    font-family: 'EB Garamond', Georgia, serif;
    overflow-x: hidden;
  }

  /* ─────────────────────────────────────────
     INTRO
  ───────────────────────────────────────── */
  #intro {
    min-height: 100svh;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: 0 6vw 8vh;
    position: relative;
    z-index: 1;
  }

  #intro-bg {
    position: absolute;
    inset: 0;
    overflow: hidden;
    opacity: 0.07;
    pointer-events: none;
  }

  #intro-bg img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: right center;
  }

  .title-block {
    position: relative;
    z-index: 1;
    max-width: 780px;
  }

  .eyebrow {
    font-family: 'Jost', sans-serif;
    font-weight: 300;
    font-size: clamp(11px, 1.4vw, 15px);
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--ink);
    margin-bottom: 2rem;
  }

  h1 {
    font-family: 'Cormorant Garamond', Georgia, serif;
    font-weight: 300;
    font-style: italic;
    font-size: clamp(40px, 7.5vw, 98px);
    line-height: 1.0;
    letter-spacing: -0.01em;
    color: var(--ink);
    margin-bottom: 2.5rem;
  }

  .subtitle {
    font-size: clamp(15px, 1.4vw, 20px);
    line-height: 1.75;
    color: var(--mid);
    max-width: 520px;
    font-style: italic;
  }

  .scroll-cue {
    font-family: 'Jost', sans-serif;
    font-weight: 200;
    font-size: 11px;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--mid);
    margin-top: 3.5rem;
    display: flex;
    align-items: center;
    gap: 12px;
    opacity: 0;
    animation: fadein 1.2s 1.8s forwards;
  }

  .scroll-cue::after {
    content: '';
    display: block;
    width: 40px;
    height: 1px;
    background: var(--mid);
  }

  @keyframes fadein { to { opacity: 1; } }

  /* ─────────────────────────────────────────
     SCROLL-ROTATING BACKGROUND
  ───────────────────────────────────────── */
  #scroll-bg {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 0;
    overflow: hidden;
    opacity: 0;
    transition: opacity 0.4s ease;
  }
  #scroll-bg.active { opacity: 1; }
  #scroll-bg img {
    position: absolute;
    top: 50%;
    left: 50%;
    transform-origin: center center;
    opacity: 0.07;
  }

  /* ─────────────────────────────────────────
     PROGRESS BAR
  ───────────────────────────────────────── */
  #progress-bar {
    position: fixed;
    top: 0; left: 0;
    height: 2px;
    width: 0%;
    background: var(--ink);
    z-index: 100;
    transition: width 0.1s linear;
  }

  /* ─────────────────────────────────────────
     ARTWORK SECTION — desktop sticky sidebar
  ───────────────────────────────────────── */
  #artwork-section {
    position: relative;
    z-index: 1;
  }

  #art-sticky {
    position: sticky;
    top: 0;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    overflow: hidden;
    pointer-events: none;
    z-index: 0;
  }

  #art-wrap {
    position: relative;
    width: 42vw;
    height: 100vh;
    overflow: hidden;
    flex-shrink: 0;
  }

  #art-inner {
    position: absolute;
    top: 0; right: 0;
    width: 100%; height: 100%;
  }

  #svg-rotated {
    display: block;
    position: absolute;
    transform-origin: top left;
  }

  /* ─────────────────────────────────────────
     NARRATIVE PANELS
  ───────────────────────────────────────── */
  #scroll-narrative {
    position: relative;
    z-index: 1;
  }

  .panel {
    min-height: 100vh;
    display: flex;
    align-items: center;
    padding: 0 6vw;
    justify-content: flex-start;
  }

  .panel-inner {
    max-width: 460px;
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.9s ease, transform 0.9s ease;
  }

  .panel-inner.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .panel-label {
    font-family: 'Jost', sans-serif;
    font-weight: 200;
    font-size: 10px;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: var(--mid);
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .panel-label::before {
    content: '';
    display: block;
    width: 24px;
    height: 1px;
    background: var(--mid);
  }

  .panel h2 {
    font-family: 'Cormorant Garamond', Georgia, serif;
    font-weight: 300;
    font-size: clamp(26px, 3vw, 40px);
    line-height: 1.2;
    margin-bottom: 1.5rem;
    letter-spacing: -0.01em;
  }

  .panel h2 em { font-style: italic; }

  .panel p {
    font-size: clamp(15px, 1.2vw, 18px);
    line-height: 1.85;
    color: #4a4845;
  }

  .panel p + p { margin-top: 1.2em; }

  .rule {
    width: 40px; height: 1px;
    background: var(--light-rule);
    margin: 2rem 0;
  }

  /* ─────────────────────────────────────────
     MOBILE ART STRIPS — hidden everywhere
     (artwork shown only in the full-artwork
     section at the end of the page)
  ───────────────────────────────────────── */
  .mobile-art-strip {
    display: none !important;
  }

  /* ─────────────────────────────────────────
     FULL ARTWORK
  ───────────────────────────────────────── */
  #full-artwork {
    padding: 14vh 6vw;
    text-align: center;
    position: relative;
    z-index: 1;
  }

  .full-art-label {
    font-family: 'Jost', sans-serif;
    font-weight: 200;
    font-size: 10px;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: var(--mid);
    margin-bottom: 3rem;
  }

  #full-svg-container {
    display: inline-block;
    width: 100%;
    max-width: 960px;
    border: 1px solid var(--light-rule);
    padding: 3vw;
    background: #fafaf8;
    overflow: hidden;
  }

  #full-svg-container img {
    width: 100%; height: auto;
    display: block;
  }

  .caption {
    margin-top: 2rem;
    font-size: 13px;
    font-style: italic;
    color: var(--mid);
    font-family: 'EB Garamond', serif;
  }

  /* ─────────────────────────────────────────
     CLOSING
  ───────────────────────────────────────── */
  #closing {
    padding: 12vh 6vw 16vh;
    max-width: 680px;
    position: relative;
    z-index: 1;
  }

  #closing h2 {
    font-family: 'Cormorant Garamond', Georgia, serif;
    font-weight: 300;
    font-style: italic;
    font-size: clamp(28px, 3.5vw, 46px);
    line-height: 1.2;
    margin-bottom: 2rem;
  }

  #closing p {
    font-size: clamp(15px, 1.2vw, 18px);
    line-height: 1.9;
    color: #4a4845;
  }

  #closing p + p { margin-top: 1.4em; }

  /* ─────────────────────────────────────────
     FOOTER
  ───────────────────────────────────────── */
  footer {
    border-top: 1px solid var(--light-rule);
    padding: 3rem 6vw;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
    position: relative;
    z-index: 1;
  }

  footer span {
    font-family: 'Jost', sans-serif;
    font-weight: 200;
    font-size: 11px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--mid);
  }

  /* ═════════════════════════════════════════
     TABLET  768–1023px
     Narrower sidebar, adjusted type
  ═════════════════════════════════════════ */
  @media (max-width: 1023px) {
    #art-wrap { width: 38vw; }
    .panel { padding: 0 5vw; }
    .panel-inner { max-width: 400px; }
    .panel h2 { font-size: clamp(24px, 3.5vw, 36px); }
    .panel p  { font-size: clamp(15px, 1.6vw, 17px); }
  }

  /* ═════════════════════════════════════════
     MOBILE  ≤767px
     Single column. Sticky sidebar hidden.
     Artwork shown as horizontal strips.
  ═════════════════════════════════════════ */
  @media (max-width: 767px) {

    /* Hide desktop sticky sidebar */
    #art-sticky { display: none !important; }

    /* Panels: full width, block layout */
    .panel {
      min-height: auto;
      padding: 11vw 7vw 9vw;
      display: block;
    }

    /* Always visible on mobile — no JS fade needed */
    .panel-inner {
      max-width: 100%;
      opacity: 1 !important;
      transform: none !important;
      transition: none !important;
    }

    .panel h2 { font-size: clamp(26px, 6.5vw, 40px); }
    .panel p  { font-size: clamp(16px, 4vw, 18px); line-height: 1.85; }

    /* Intro */
    #intro { padding: 0 7vw 10vw; }
    h1 { font-size: clamp(38px, 10vw, 64px); margin-bottom: 1.5rem; }
    .eyebrow { font-size: 10px; margin-bottom: 1.5rem; }
    .subtitle { font-size: clamp(16px, 4vw, 19px); }
    .scroll-cue { margin-top: 2.5rem; }

    /* Full artwork */
    #full-artwork { padding: 10vw 7vw; }
    #full-svg-container { padding: 5vw; }
    .caption { font-size: 12px; }

    /* Closing */
    #closing {
      padding: 10vw 7vw 14vw;
      max-width: 100%;
    }
    #closing h2 { font-size: clamp(26px, 7vw, 38px); }
    #closing p  { font-size: clamp(15px, 4.2vw, 18px); }

    /* Footer */
    footer {
      flex-direction: column;
      align-items: flex-start;
      padding: 2.5rem 7vw;
      gap: 0.5rem;
    }
  }

  /* ═════════════════════════════════════════
     SMALL PHONES  ≤390px
  ═════════════════════════════════════════ */
  @media (max-width: 390px) {
    h1 { font-size: clamp(32px, 10vw, 46px); }
  }
</style>
</head>
<body>

<div id="progress-bar"></div>

<!-- SCROLL-ROTATING BACKGROUND -->
<div id="scroll-bg" aria-hidden="true">
  <img id="scroll-bg-img" src="hex_pattern_svg.svg" alt="">
</div>

<!-- ── INTRO ── -->
<section id="intro">
  <div id="intro-bg">
    <img src="hex_pattern_svg.svg" alt="" aria-hidden="true">
  </div>
  <div class="title-block">
    <p class="eyebrow">Etched aluminum &nbsp;·&nbsp; 2026</p>
    <h1>How Long Have<br>You Been You?</h1>
    <p class="subtitle">A meditation on identity, continuity, and the strange persistence of the self across time.</p>
    <p class="scroll-cue">Scroll to explore</p>
  </div>
</section>

<!-- ── MAIN SCROLLYTELLING AREA ── -->
<div id="artwork-section">

  <!-- Desktop/tablet: sticky rotated strip on right -->
  <div id="art-sticky" aria-hidden="true">
    <div id="art-wrap">
      <div id="art-inner">
        <img id="svg-rotated" src="hex_pattern_svg.svg" alt="Hex pattern artwork">
      </div>
    </div>
  </div>

  <!-- Narrative panels -->
  <div id="scroll-narrative">

    <div class="panel" data-progress="0">
      <div class="panel-inner">
        <p class="panel-label">Origin</p>
        <h2>You began as<br><em>one thing.</em></h2>
        <div class="rule"></div>
        <p>Look at a photograph of yourself as a child. The face is familiar, yet foreign. You share a body — a lineage of cells — with that small person. And yet you know something they do not, have been shaped by things they never experienced, carry losses they couldn't yet imagine.</p>
        <p>Are you the same person?</p>
      </div>
    </div>

    <!-- Mobile art strip: shows leftmost (simplest) portion -->
    <div class="mobile-art-strip" data-strip="0" aria-hidden="true">
      <img src="hex_pattern_svg.svg" alt="">
    </div>

    <div class="panel" data-progress="0.2">
      <div class="panel-inner">
        <p class="panel-label">The past self</p>
        <h2>Looking backward<br>feels <em>obvious.</em></h2>
        <div class="rule"></div>
        <p>When we look behind us, the transformation seems natural. Of course we changed. We can trace the path: the formative years, the decisive moments, the slow accumulations. The journey from then to now feels legible — even inevitable.</p>
        <p>We grant our past selves the permission to have been different.</p>
      </div>
    </div>

    <div class="mobile-art-strip" data-strip="1" aria-hidden="true">
      <img src="hex_pattern_svg.svg" alt="">
    </div>

    <div class="panel" data-progress="0.42">
      <div class="panel-inner">
        <p class="panel-label">The present self</p>
        <h2>But now<br><em>feels fixed.</em></h2>
        <div class="rule"></div>
        <p>Something strange happens when we look forward. The future self — the person you will be in ten, twenty, forty years — feels like a continuation of who you are right now. We make plans for them, make sacrifices for them, as though they are us.</p>
        <p>We assume our future self will want what we want now. Believe what we believe now. Be, essentially, who we are now.</p>
      </div>
    </div>

    <div class="mobile-art-strip" data-strip="2" aria-hidden="true">
      <img src="hex_pattern_svg.svg" alt="">
    </div>

    <div class="panel" data-progress="0.64">
      <div class="panel-inner">
        <p class="panel-label">The future self</p>
        <h2>The pattern<br><em>keeps changing.</em></h2>
        <div class="rule"></div>
        <p>Research consistently shows that people underestimate how much they will change. Psychologists call this the "end of history illusion" — the persistent feeling that you have finally become the person you were always becoming, and that the story is now stable.</p>
        <p>But the pattern never stops evolving. Complexity grows in ways you cannot yet see from where you stand.</p>
      </div>
    </div>

    <div class="mobile-art-strip" data-strip="3" aria-hidden="true">
      <img src="hex_pattern_svg.svg" alt="">
    </div>

    <div class="panel" data-progress="0.85">
      <div class="panel-inner">
        <p class="panel-label">Continuity</p>
        <h2>And yet — <br><em>still you.</em></h2>
        <div class="rule"></div>
        <p>The philosopher Derek Parfit spent his life on this question. He came to believe that personal identity is not what matters — that the thread connecting your past, present, and future selves is thinner than we imagine, and stranger.</p>
        <p>And somehow, that thought is not frightening. It is freeing. To hold your past and future selves with a lighter grip. To let the pattern be what it is.</p>
      </div>
    </div>

  </div><!-- /scroll-narrative -->
</div><!-- /artwork-section -->

<!-- FULL ARTWORK REVEAL -->
<section id="full-artwork">
  <p class="full-art-label">The work in full</p>
  <div id="full-svg-container">
    <img src="HowLongHaveYouBeenYou.jpeg" alt="How Long Have You Been You — full artwork, etched aluminum">
  </div>
  <p class="caption">Etched aluminum &nbsp;·&nbsp; The pattern moves from sparse regularity at left to dense complexity at right.</p>
</section>

<!-- CLOSING -->
<section id="closing">
  <h2>"How long have you<br>been you?"</h2>
  <p>This question does not have an answer. It is designed to sit with you, to accompany you through your day, to surface again unexpectedly when you catch your reflection or find an old letter or meet someone you used to be.</p>
  <p>The aluminum does not change. The pattern etched into it is fixed. But the person looking at it — the person asking the question — never is.</p>
  <p style="margin-top: 2.5rem; font-style: italic; color: var(--mid);">The work is in that gap.</p>
</section>

<!-- FOOTER -->
<footer>
  <span>How Long Have You Been You? &nbsp;·&nbsp; Etched Aluminum</span>
  <span>© 2026 — Craig Lewis</span>
</footer>

<script>
(function () {
  'use strict';

  const SVG_W = 1151;
  const SVG_H = 482;

  function isDesktop() { return window.innerWidth >= 1024; }
  function isTablet()  { return window.innerWidth >= 768 && window.innerWidth < 1024; }
  function isMobile()  { return window.innerWidth < 768; }

  /* ── Progress bar ── */
  const progressBar = document.getElementById('progress-bar');
  function updateProgressBar() {
    const docH = document.documentElement.scrollHeight - window.innerHeight;
    progressBar.style.width = (docH > 0 ? Math.min(100, (window.scrollY / docH) * 100) : 0) + '%';
  }

  /* ── Desktop / tablet: sticky rotated art reveal ── */
  const svgImg  = document.getElementById('svg-rotated');
  const artWrap = document.getElementById('art-wrap');

  function layoutArt() {
    if (isMobile()) return;
    const wrapW = artWrap.offsetWidth;
    const wrapH = artWrap.offsetHeight;
    const scale = wrapW / SVG_H;
    const imgW  = SVG_W * scale;
    const imgH  = SVG_H * scale;
    const visH  = SVG_W * scale;

    svgImg.style.width  = imgW + 'px';
    svgImg.style.height = imgH + 'px';
    svgImg.style.transformOrigin = '0 0';
    svgImg.style.transform = `rotate(90deg) translateX(${wrapW - imgH}px)`;
    svgImg.style.top = '0px';

    svgImg._visH  = visH;
    svgImg._wrapH = wrapH;
    svgImg._imgH  = imgH;
    svgImg._wrapW = wrapW;
  }

  function updateArtScroll() {
    if (isMobile()) return;
    if (!svgImg._visH) return;
    const artSection = document.getElementById('artwork-section');
    const rect       = artSection.getBoundingClientRect();
    const maxScroll  = artSection.offsetHeight - window.innerHeight;
    const progress   = Math.max(0, Math.min(1, -rect.top / maxScroll));
    const overflow   = Math.max(0, svgImg._visH - svgImg._wrapH);
    svgImg.style.top = (-progress * overflow) + 'px';
  }

  /* ── Scroll-rotating background ──
     Activates once the intro scrolls off screen.
     Rotates 0°→90° CW by the time "The work is in that gap." is reached.
     Image sized to 1.5× the viewport diagonal so it fills at all angles.
  ── */
  const scrollBg    = document.getElementById('scroll-bg');
  const scrollBgImg = document.getElementById('scroll-bg-img');

  function updateScrollBg() {
    const introEl   = document.getElementById('intro');
    const closingEl = document.getElementById('closing');
    const gapLine   = closingEl ? closingEl.querySelector('p[style*="italic"]') : null;

    const introBottom = introEl.getBoundingClientRect().bottom;
    const active = introBottom < 20;
    scrollBg.classList.toggle('active', active);
    if (!active) return;

    const introExitY = introEl.offsetTop + introEl.offsetHeight;
    const gapY = gapLine
      ? gapLine.getBoundingClientRect().top + window.scrollY - window.innerHeight * 0.5
      : document.body.scrollHeight;

    const t   = Math.max(0, Math.min(1, (window.scrollY - introExitY) / Math.max(1, gapY - introExitY)));
    const deg = t * 90;

    // 1.5× diagonal ensures coverage at all rotation angles
    const vw   = window.innerWidth;
    const vh   = window.innerHeight;
    const diag = Math.ceil(Math.sqrt(vw * vw + vh * vh) * 1.5);
    const imgW = diag;
    const imgH = diag / (SVG_W / SVG_H);

    scrollBgImg.style.width  = imgW + 'px';
    scrollBgImg.style.height = imgH + 'px';

    // Max opacity slightly higher on mobile so the effect reads through
    const maxOpacity = isMobile() ? 0.12 : 0.07;
    let opacity = maxOpacity;
    if (t > 0.85)      opacity = maxOpacity * (1 - (t - 0.85) / 0.15);
    else if (t < 0.08) opacity = maxOpacity * (t / 0.08);
    scrollBgImg.style.opacity = opacity;

    // Pivot from viewport center — top:50%;left:50% in CSS + translate(-50%,-50%)
    // ensures correct centering on iOS Safari fixed-position contexts
    scrollBgImg.style.transform = `translate(-50%, -50%) rotate(${deg}deg)`;
  }

  /* ── Panel fade-in (desktop/tablet only) ── */
  const panels = document.querySelectorAll('.panel-inner');
  function updatePanelFade() {
    if (isMobile()) return;
    panels.forEach(p => {
      if (p.getBoundingClientRect().top < window.innerHeight * 0.78) {
        p.classList.add('visible');
      }
    });
  }

  /* ── Intro text reveal ── */
  const titleBlock = document.querySelector('.title-block');
  titleBlock.style.cssText += 'opacity:0;transform:translateY(24px);transition:opacity 1.2s ease,transform 1.2s ease;';
  window.addEventListener('load', () => {
    setTimeout(() => {
      titleBlock.style.opacity   = '1';
      titleBlock.style.transform = 'translateY(0)';
    }, 200);
  });

  /* ── Unified handlers ── */
  function onScroll() {
    updateProgressBar();
    updateArtScroll();
    updateScrollBg();
    updatePanelFade();
  }

  let resizeTimer;
  function onResize() {
    clearTimeout(resizeTimer);
    resizeTimer = setTimeout(() => {
      layoutArt();
      onScroll();
    }, 80);
  }

  window.addEventListener('scroll',            onScroll,  { passive: true });
  window.addEventListener('resize',            onResize);
  window.addEventListener('orientationchange', onResize);

  layoutArt();
  onScroll();
  // Run again after fonts/images settle, and once more for iOS Safari
})();
</script>
</body>
</html>
