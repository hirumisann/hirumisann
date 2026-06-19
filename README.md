
<!DOCTYPE html>
<html>
<head>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

  * { box-sizing: border-box; margin: 0; padding: 0; image-rendering: pixelated; }

  body {
    background: #0a0f1e;
    font-family: 'Press Start 2P', monospace;
    color: #e0e8ff;
    overflow-x: hidden;
  }

  :root {
    --gold: #ffb454;
    --gold2: #ffd089;
    --blue: #3a7bd5;
    --blue2: #6fa3f7;
    --dark: #0a1130;
    --mid: #111a3a;
    --panel: #151f40;
    --border: #2a3a6a;
    --text: #9aa3c7;
    --white: #e0e8ff;
    --green: #4ade80;
    --pink: #f472b6;
    --cyan: #22d3ee;
    --red: #f87171;
    --purple: #a855f7;
  }

  /* Scanline overlay */
  body::before {
    content: '';
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.04) 2px, rgba(0,0,0,0.04) 4px);
    pointer-events: none;
    z-index: 9999;
  }

  .page {
    max-width: 860px;
    margin: 0 auto;
    padding: 20px 12px 40px;
  }

  /* ---- HEADER ---- */
  .header {
    text-align: center;
    padding: 24px 12px 20px;
    border: 3px solid var(--gold);
    background: var(--panel);
    image-rendering: pixelated;
    position: relative;
    margin-bottom: 16px;
    box-shadow: 0 0 0 3px var(--dark), 0 0 0 6px var(--border);
  }

  .header::before {
    content: '◆ ◆ ◆';
    position: absolute;
    top: -12px;
    left: 50%;
    transform: translateX(-50%);
    background: var(--panel);
    padding: 0 8px;
    color: var(--gold);
    font-size: 8px;
    letter-spacing: 4px;
  }

  .moon-pixel {
    display: block;
    margin: 0 auto 12px;
    width: 48px;
    height: 48px;
  }

  .hero-name {
    font-size: 13px;
    color: var(--gold);
    letter-spacing: 2px;
    text-shadow: 3px 3px 0 #7a3a00, -1px -1px 0 #3a1a00;
    margin-bottom: 8px;
    animation: blink-cursor 1s step-end infinite;
  }

  @keyframes blink-cursor { 50% { opacity: 0.7; } }

  .typing-box {
    display: inline-block;
    border: 2px solid var(--gold);
    padding: 6px 14px;
    background: var(--dark);
    font-size: 7px;
    color: var(--gold2);
    margin-top: 8px;
    position: relative;
    overflow: hidden;
    min-width: 280px;
    min-height: 22px;
  }

  .typing-text {
    display: inline-block;
    white-space: nowrap;
    overflow: hidden;
  }

  .cursor-blink {
    display: inline-block;
    width: 7px;
    height: 12px;
    background: var(--gold);
    vertical-align: middle;
    animation: blink 0.7s step-end infinite;
    margin-left: 2px;
  }

  @keyframes blink { 50% { opacity: 0; } }

  /* PIXEL character walking */
  .pixel-char-row {
    display: flex;
    justify-content: center;
    margin: 12px 0 0;
    gap: 16px;
  }

  /* ---- GRID LAYOUT ---- */
  .grid-2 {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-bottom: 12px;
  }

  .grid-3 {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 10px;
    margin-bottom: 12px;
  }

  @media (max-width: 600px) {
    .grid-2 { grid-template-columns: 1fr; }
    .grid-3 { grid-template-columns: 1fr 1fr; }
    .hero-name { font-size: 9px; }
  }

  /* ---- PANEL BOXES ---- */
  .pixel-box {
    border: 3px solid var(--border);
    background: var(--panel);
    padding: 12px;
    position: relative;
  }

  .pixel-box::before {
    content: attr(data-title);
    position: absolute;
    top: -10px;
    left: 10px;
    background: var(--panel);
    padding: 0 6px;
    font-size: 6px;
    color: var(--gold);
    letter-spacing: 1px;
    border: 1px solid var(--gold);
  }

  .pixel-box.gold-border { border-color: var(--gold); }
  .pixel-box.blue-border { border-color: var(--blue2); }
  .pixel-box.cyan-border { border-color: var(--cyan); }
  .pixel-box.green-border { border-color: var(--green); }
  .pixel-box.pink-border { border-color: var(--pink); }
  .pixel-box.purple-border { border-color: var(--purple); }

  /* ---- ABOUT SECTION ---- */
  .about-grid {
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 12px;
    align-items: start;
    margin-top: 8px;
  }

  .about-text {
    font-size: 6px;
    line-height: 2.2;
    color: var(--text);
  }

  .about-text .highlight { color: var(--gold); }

  .yaml-block {
    font-size: 6px;
    line-height: 2.0;
    background: var(--dark);
    border: 2px solid var(--border);
    padding: 8px;
    margin-top: 6px;
    border-left: 3px solid var(--green);
  }

  .yaml-key { color: var(--blue2); }
  .yaml-val { color: var(--gold2); }
  .yaml-str { color: var(--green); }
  .yaml-bool { color: var(--pink); }
  .yaml-comment { color: #444e7a; }

  /* ---- STATS ---- */
  .stat-bar-wrap {
    margin: 6px 0;
  }

  .stat-label {
    display: flex;
    justify-content: space-between;
    font-size: 6px;
    color: var(--text);
    margin-bottom: 3px;
  }

  .stat-bar-outer {
    height: 10px;
    background: var(--dark);
    border: 2px solid var(--border);
    position: relative;
    overflow: hidden;
  }

  .stat-bar-fill {
    height: 100%;
    position: relative;
    transition: width 1.5s steps(20, end);
    animation: grow-bar 1.5s steps(20, end) forwards;
  }

  @keyframes grow-bar {
    from { width: 0 !important; }
  }

  .stat-bar-fill::after {
    content: '';
    position: absolute;
    right: 0; top: 0; bottom: 0;
    width: 3px;
    background: rgba(255,255,255,0.5);
    animation: shimmer 1s step-end infinite;
  }

  @keyframes shimmer { 50% { opacity: 0; } }

  /* ---- TECH BADGES ---- */
  .badge-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    margin-top: 8px;
  }

  .tech-badge {
    font-size: 6px;
    padding: 4px 8px;
    border: 2px solid;
    background: var(--dark);
    letter-spacing: 1px;
    cursor: default;
    transition: all 0.1s step-end;
    position: relative;
  }

  .tech-badge:hover {
    transform: translate(-2px, -2px);
    box-shadow: 3px 3px 0;
  }

  .badge-js { color: #f0db4f; border-color: #f0db4f; }
  .badge-js:hover { box-shadow: 3px 3px 0 #f0db4f; }
  .badge-html { color: #e34c26; border-color: #e34c26; }
  .badge-html:hover { box-shadow: 3px 3px 0 #e34c26; }
  .badge-css { color: #264de4; border-color: #5b7fff; }
  .badge-css:hover { box-shadow: 3px 3px 0 #5b7fff; }
  .badge-cf { color: #f38020; border-color: #f38020; }
  .badge-cf:hover { box-shadow: 3px 3px 0 #f38020; }
  .badge-cursor { color: var(--cyan); border-color: var(--cyan); }
  .badge-cursor:hover { box-shadow: 3px 3px 0 var(--cyan); }
  .badge-ai { color: var(--green); border-color: var(--green); }
  .badge-ai:hover { box-shadow: 3px 3px 0 var(--green); }
  .badge-claude { color: var(--purple); border-color: var(--purple); }
  .badge-claude:hover { box-shadow: 3px 3px 0 var(--purple); }
  .badge-api { color: var(--gold); border-color: var(--gold); }
  .badge-api:hover { box-shadow: 3px 3px 0 var(--gold); }

  /* ---- PROJECTS ---- */
  .project-card {
    border: 3px solid var(--border);
    background: var(--dark);
    padding: 10px;
    margin-bottom: 8px;
    position: relative;
    transition: all 0.1s step-end;
    cursor: pointer;
  }

  .project-card:hover {
    transform: translate(-3px, -3px);
    box-shadow: 4px 4px 0 var(--gold);
    border-color: var(--gold);
  }

  .project-card.film:hover {
    box-shadow: 4px 4px 0 #e8746a;
    border-color: #e8746a;
  }

  .project-title {
    font-size: 8px;
    color: var(--gold);
    margin-bottom: 4px;
  }

  .project-title.film-title { color: #e8746a; }

  .project-desc {
    font-size: 6px;
    color: var(--text);
    line-height: 1.8;
  }

  .project-tag {
    display: inline-block;
    font-size: 5px;
    padding: 2px 5px;
    border: 1px solid var(--gold);
    color: var(--gold);
    margin-top: 5px;
    margin-right: 3px;
  }

  .project-tag.film-tag { border-color: #e8746a; color: #e8746a; }

  /* ---- PIXEL SPRITE ANIMATION ---- */
  .sprite-area {
    display: flex;
    justify-content: center;
    align-items: flex-end;
    gap: 20px;
    padding: 8px 0;
  }

  /* ---- CONTRIBUTION GRID ---- */
  .contrib-grid {
    display: grid;
    grid-template-columns: repeat(52, 1fr);
    gap: 2px;
    margin-top: 8px;
  }

  .contrib-cell {
    aspect-ratio: 1;
    border-radius: 0;
  }

  /* ---- SOCIAL LINKS ---- */
  .social-row {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin-top: 8px;
  }

  .social-btn {
    font-family: 'Press Start 2P', monospace;
    font-size: 6px;
    padding: 6px 10px;
    border: 2px solid var(--text);
    background: var(--dark);
    color: var(--text);
    cursor: pointer;
    transition: all 0.1s step-end;
    text-decoration: none;
    display: inline-block;
  }

  .social-btn:hover {
    background: var(--text);
    color: var(--dark);
    transform: translate(-2px, -2px);
    box-shadow: 3px 3px 0 var(--gold);
  }

  /* ---- SNAKE GRID ---- */
  #snake-canvas {
    display: block;
    margin: 8px auto 0;
    image-rendering: pixelated;
    border: 2px solid var(--border);
  }

  /* ---- FOOTER QUOTE ---- */
  .footer-quote {
    text-align: center;
    margin-top: 20px;
    padding: 16px;
    border: 3px solid var(--border);
    background: var(--panel);
    font-size: 6px;
    color: var(--gold2);
    line-height: 2.5;
    position: relative;
  }

  .footer-quote::before {
    content: '★ ★ ★ ★ ★';
    display: block;
    color: var(--gold);
    margin-bottom: 8px;
    letter-spacing: 4px;
    animation: twinkle 2s step-end infinite;
  }

  @keyframes twinkle {
    0%, 100% { opacity: 1; }
    33% { opacity: 0.3; }
    66% { opacity: 0.7; }
  }

  /* ---- PIXEL GIF CHAR ---- */
  .pixel-walk {
    position: relative;
    height: 48px;
  }

  .walk-char {
    position: absolute;
    bottom: 0;
    left: 0;
    animation: walk-across 6s linear infinite;
  }

  @keyframes walk-across {
    0% { left: -32px; }
    100% { left: calc(100% + 32px); }
  }

  /* Section divider */
  .divider {
    text-align: center;
    font-size: 7px;
    color: var(--border);
    margin: 6px 0;
    letter-spacing: 4px;
  }

  /* Achievement badges */
  .achievement {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 6px 8px;
    border: 2px solid var(--border);
    background: var(--dark);
    margin-bottom: 6px;
    transition: all 0.1s step-end;
  }

  .achievement:hover {
    border-color: var(--gold);
    transform: translateX(3px);
  }

  .achiev-icon {
    font-size: 14px;
    width: 24px;
    text-align: center;
    flex-shrink: 0;
  }

  .achiev-text {
    font-size: 6px;
    color: var(--text);
    line-height: 1.8;
  }

  .achiev-text strong {
    color: var(--gold);
    display: block;
    margin-bottom: 2px;
  }

  /* EXP level bar */
  .level-up {
    text-align: center;
    margin-bottom: 10px;
  }
  .level-num {
    font-size: 20px;
    color: var(--gold);
    text-shadow: 3px 3px 0 #7a3a00;
    display: block;
  }
  .level-label {
    font-size: 6px;
    color: var(--text);
    margin-top: 2px;
  }

  /* animated stars in header */
  .stars-row {
    display: flex;
    justify-content: center;
    gap: 6px;
    margin-top: 6px;
  }

  .star {
    font-size: 10px;
    color: var(--gold);
    animation: star-pulse 1.5s step-end infinite;
  }

  .star:nth-child(2) { animation-delay: 0.5s; }
  .star:nth-child(3) { animation-delay: 1s; }

  @keyframes star-pulse { 50% { opacity: 0.2; color: #ffd089; } }
</style>
</head>
<body>
<div class="page">

<!-- ====== HEADER ====== -->
<div class="header" style="margin-bottom:16px;">
  <svg class="moon-pixel" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
    <rect x="5" y="1" width="6" height="1" fill="#ffd089"/>
    <rect x="3" y="2" width="2" height="1" fill="#ffd089"/>
    <rect x="11" y="2" width="2" height="1" fill="#ffd089"/>
    <rect x="2" y="3" width="1" height="6" fill="#ffd089"/>
    <rect x="13" y="3" width="1" height="6" fill="#ffd089"/>
    <rect x="3" y="9" width="1" height="2" fill="#ffd089"/>
    <rect x="4" y="11" width="1" height="1" fill="#ffd089"/>
    <rect x="5" y="12" width="1" height="1" fill="#ffd089"/>
    <rect x="6" y="13" width="5" height="1" fill="#ffd089"/>
    <rect x="11" y="12" width="1" height="1" fill="#ffd089"/>
    <rect x="12" y="11" width="1" height="1" fill="#ffd089"/>
    <rect x="13" y="9" width="1" height="2" fill="#ffd089"/>
    <rect x="3" y="3" width="10" height="6" fill="#ffd089"/>
    <rect x="3" y="9" width="10" height="3" fill="#ffd089"/>
    <!-- crescent cutout -->
    <rect x="6" y="3" width="5" height="8" fill="#0a0f1e"/>
    <rect x="5" y="4" width="1" height="6" fill="#0a0f1e"/>
    <!-- star accent -->
    <rect x="1" y="1" width="1" height="1" fill="#ffb454"/>
    <rect x="14" y="6" width="1" height="1" fill="#ffb454"/>
    <rect x="0" y="8" width="1" height="1" fill="#ffd089"/>
  </svg>

  <div class="hero-name">★ MUHAMMAD HILMY ★</div>

  <div class="typing-box">
    <span class="typing-text" id="typing-text"></span><span class="cursor-blink"></span>
  </div>

  <div class="stars-row">
    <span class="star">✦</span><span class="star">✦</span><span class="star">✦</span>
  </div>

  <!-- Pixel character row in header -->
  <div class="pixel-walk" style="margin-top:12px; overflow:hidden;">
    <svg class="walk-char" viewBox="0 0 16 24" width="32" height="48" xmlns="http://www.w3.org/2000/svg">
      <!-- body -->
      <rect x="4" y="0" width="8" height="8" fill="#ffd089"/>
      <rect x="3" y="1" width="1" height="6" fill="#ffd089"/>
      <rect x="12" y="1" width="1" height="6" fill="#ffd089"/>
      <!-- eyes -->
      <rect x="5" y="2" width="2" height="2" fill="#0a0f1e"/>
      <rect x="9" y="2" width="2" height="2" fill="#0a0f1e"/>
      <!-- mouth -->
      <rect x="6" y="5" width="4" height="1" fill="#0a0f1e"/>
      <!-- body shirt -->
      <rect x="3" y="8" width="10" height="8" fill="#ffb454"/>
      <rect x="2" y="9" width="1" height="5" fill="#ffb454"/>
      <rect x="13" y="9" width="1" height="5" fill="#ffb454"/>
      <!-- legs -->
      <rect x="4" y="16" width="3" height="6" fill="#3a7bd5"/>
      <rect x="9" y="16" width="3" height="6" fill="#3a7bd5"/>
      <!-- shoes -->
      <rect x="3" y="21" width="4" height="2" fill="#0a0f1e"/>
      <rect x="9" y="21" width="4" height="2" fill="#0a0f1e"/>
      <!-- cup of tea -->
      <rect x="14" y="9" width="4" height="3" fill="#c47c5a" x2="14"/>
      <rect x="13" y="10" width="1" height="2" fill="#c47c5a"/>
    </svg>
  </div>
</div>

<!-- ====== ROW 1: ABOUT + YAML ====== -->
<div class="grid-2" style="margin-bottom:12px;">

  <div class="pixel-box gold-border" data-title="▶ TENTANG AKU">
    <div style="margin-top:8px;">
      <div class="about-text">
        <span class="highlight">▸</span> Pelajar yang menghabiskan<br>
        &nbsp;&nbsp;malam dengan kode<br>
        <span class="highlight">▸</span> Secangkir teh ☕ + hujan rintik 🌧<br>
        <span class="highlight">▸</span> Teknik <span class="highlight">VIBE CODING</span><br>
        &nbsp;&nbsp;fokus gambaran besar<br>
        <span class="highlight">▸</span> AI handles the details ✓
      </div>
      <div style="margin-top:10px;">
        <div class="achievement">
          <span class="achiev-icon">🌙</span>
          <div class="achiev-text"><strong>NIGHT OWL CODER</strong>Code after midnight</div>
        </div>
        <div class="achievement">
          <span class="achiev-icon">🤖</span>
          <div class="achiev-text"><strong>AI COLLABORATOR</strong>Cursor + Claude + GPT</div>
        </div>
        <div class="achievement">
          <span class="achiev-icon">🌐</span>
          <div class="achiev-text"><strong>WEB BUILDER</strong>REST API + UI/UX</div>
        </div>
      </div>
    </div>
  </div>

  <div class="pixel-box cyan-border" data-title="▶ PLAYER.YAML">
    <div class="yaml-block" style="margin-top:8px;">
      <div><span class="yaml-comment"># player config</span></div>
      <div><span class="yaml-key">name:</span> <span class="yaml-str">"Muhammad Hilmy"</span></div>
      <div><span class="yaml-key">role:</span> <span class="yaml-str">"Pelajar"</span></div>
      <div><span class="yaml-key">class:</span> <span class="yaml-str">"Web Dev"</span></div>
      <div><span class="yaml-key">focus:</span></div>
      <div>&nbsp;<span class="yaml-comment">- Web Development</span></div>
      <div>&nbsp;<span class="yaml-comment">- REST API</span></div>
      <div>&nbsp;<span class="yaml-comment">- UI/UX Design</span></div>
      <div><span class="yaml-key">vibe_coding:</span> <span class="yaml-bool">true</span></div>
      <div><span class="yaml-key">location:</span> <span class="yaml-str">"Indonesia 🇮🇩"</span></div>
      <div><span class="yaml-key">tools:</span></div>
      <div>&nbsp;<span class="yaml-comment">- Cursor</span></div>
      <div>&nbsp;<span class="yaml-comment">- Claude</span></div>
      <div>&nbsp;<span class="yaml-comment">- ChatGPT</span></div>
      <div><span class="yaml-key">status:</span> <span class="yaml-str">"online 🟢"</span></div>
    </div>
  </div>
</div>

<!-- ====== STATS ROW ====== -->
<div class="pixel-box gold-border" data-title="▶ STATUS PEMAIN" style="margin-bottom:12px;">
  <div style="margin-top:10px; display:grid; grid-template-columns:1fr 1fr; gap:12px;">

    <div>
      <div class="level-up">
        <span class="level-num">42</span>
        <span class="level-label">CURRENT LEVEL</span>
      </div>
      <div class="stat-bar-wrap">
        <div class="stat-label"><span>⚔ Web Dev</span><span>87 / 100</span></div>
        <div class="stat-bar-outer"><div class="stat-bar-fill" style="width:87%;background:linear-gradient(90deg,#ffb454,#ffd089);"></div></div>
      </div>
      <div class="stat-bar-wrap">
        <div class="stat-label"><span>🛡 REST API</span><span>72 / 100</span></div>
        <div class="stat-bar-outer"><div class="stat-bar-fill" style="width:72%;background:linear-gradient(90deg,#3a7bd5,#6fa3f7);"></div></div>
      </div>
      <div class="stat-bar-wrap">
        <div class="stat-label"><span>✨ UI/UX</span><span>65 / 100</span></div>
        <div class="stat-bar-outer"><div class="stat-bar-fill" style="width:65%;background:linear-gradient(90deg,#a855f7,#c084fc);"></div></div>
      </div>
      <div class="stat-bar-wrap">
        <div class="stat-label"><span>🤖 AI Collab</span><span>95 / 100</span></div>
        <div class="stat-bar-outer"><div class="stat-bar-fill" style="width:95%;background:linear-gradient(90deg,#22d3ee,#67e8f9);"></div></div>
      </div>
      <div class="stat-bar-wrap">
        <div class="stat-label"><span>☕ Tea Magic</span><span>100 / 100</span></div>
        <div class="stat-bar-outer"><div class="stat-bar-fill" style="width:100%;background:linear-gradient(90deg,#4ade80,#86efac);"></div></div>
      </div>
    </div>

    <div>
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:6px;margin-bottom:8px;">
        <div style="border:2px solid var(--gold);background:var(--dark);padding:8px;text-align:center;">
          <div style="font-size:14px;color:var(--gold);">247</div>
          <div style="font-size:5px;color:var(--text);margin-top:3px;">COMMITS</div>
        </div>
        <div style="border:2px solid var(--blue2);background:var(--dark);padding:8px;text-align:center;">
          <div style="font-size:14px;color:var(--blue2);">12</div>
          <div style="font-size:5px;color:var(--text);margin-top:3px;">REPOS</div>
        </div>
        <div style="border:2px solid var(--green);background:var(--dark);padding:8px;text-align:center;">
          <div style="font-size:14px;color:var(--green);">🔥 8</div>
          <div style="font-size:5px;color:var(--text);margin-top:3px;">STREAK</div>
        </div>
        <div style="border:2px solid var(--cyan);background:var(--dark);padding:8px;text-align:center;">
          <div style="font-size:14px;color:var(--cyan);">5★</div>
          <div style="font-size:5px;color:var(--text);margin-top:3px;">RATING</div>
        </div>
      </div>

      <!-- top langs mini chart -->
      <div style="font-size:6px;color:var(--text);margin-bottom:4px;">TOP LANGUAGES</div>
      <div style="height:16px;border:2px solid var(--border);display:flex;overflow:hidden;margin-bottom:4px;">
        <div style="background:#f0db4f;width:45%;position:relative;"></div>
        <div style="background:#e34c26;width:25%;"></div>
        <div style="background:#264de4;width:20%;"></div>
        <div style="background:#3a7bd5;width:10%;"></div>
      </div>
      <div style="display:flex;gap:6px;flex-wrap:wrap;">
        <span style="font-size:5px;color:#f0db4f;">■ JS 45%</span>
        <span style="font-size:5px;color:#e34c26;">■ HTML 25%</span>
        <span style="font-size:5px;color:#5b7fff;">■ CSS 20%</span>
        <span style="font-size:5px;color:#6fa3f7;">■ Other 10%</span>
      </div>
    </div>
  </div>
</div>

<!-- ====== TECH STACK ====== -->
<div class="pixel-box blue-border" data-title="▶ TECH STACK & TOOLS" style="margin-bottom:12px;">
  <div class="badge-grid" style="margin-top:8px;">
    <span class="tech-badge badge-js">⚡ JAVASCRIPT</span>
    <span class="tech-badge badge-html">🔶 HTML5</span>
    <span class="tech-badge badge-css">💎 CSS3</span>
    <span class="tech-badge badge-cf">🌊 CLOUDFLARE</span>
    <span class="tech-badge badge-cursor">🎯 CURSOR</span>
    <span class="tech-badge badge-ai">🤖 CHATGPT</span>
    <span class="tech-badge badge-claude">🟣 CLAUDE</span>
    <span class="tech-badge badge-api">📡 REST API</span>
  </div>

  <!-- pixel sprite tech icons row -->
  <div class="sprite-area" style="margin-top:12px;">
    <svg viewBox="0 0 16 16" width="28" height="28" title="JS">
      <rect width="16" height="16" fill="#f0db4f"/>
      <rect x="10" y="3" width="2" height="8" fill="#0a0f1e"/>
      <rect x="8" y="9" width="2" height="2" fill="#0a0f1e"/>
      <rect x="4" y="3" width="2" height="10" fill="#0a0f1e"/>
      <rect x="3" y="11" width="5" height="2" fill="#0a0f1e"/>
    </svg>
    <svg viewBox="0 0 16 16" width="28" height="28" title="HTML">
      <rect width="16" height="16" fill="#e34c26"/>
      <rect x="3" y="2" width="10" height="2" fill="#fff"/>
      <rect x="4" y="5" width="8" height="1" fill="#fff"/>
      <rect x="5" y="7" width="6" height="1" fill="#fff"/>
      <rect x="3" y="9" width="4" height="1" fill="#fff"/>
      <rect x="9" y="9" width="4" height="1" fill="#fff"/>
      <rect x="4" y="11" width="3" height="1" fill="#fff"/>
      <rect x="9" y="11" width="3" height="1" fill="#fff"/>
      <rect x="5" y="13" width="6" height="1" fill="#fff"/>
    </svg>
    <svg viewBox="0 0 16 16" width="28" height="28" title="CSS">
      <rect width="16" height="16" fill="#264de4"/>
      <rect x="4" y="2" width="8" height="2" fill="#fff"/>
      <rect x="3" y="5" width="9" height="1" fill="#fff"/>
      <rect x="4" y="7" width="8" height="1" fill="#fff"/>
      <rect x="8" y="9" width="5" height="1" fill="#fff"/>
      <rect x="7" y="11" width="6" height="1" fill="#fff"/>
      <rect x="4" y="13" width="5" height="1" fill="#fff"/>
    </svg>
    <svg viewBox="0 0 16 16" width="28" height="28" title="CF">
      <rect width="16" height="16" fill="#f38020"/>
      <rect x="2" y="10" width="12" height="3" fill="#fff" rx="1"/>
      <rect x="4" y="7" width="8" height="3" fill="#fff" rx="1"/>
      <rect x="6" y="4" width="4" height="3" fill="#fff" rx="1"/>
    </svg>
    <svg viewBox="0 0 16 16" width="28" height="28" title="API">
      <rect width="16" height="16" fill="#ffb454"/>
      <rect x="2" y="4" width="12" height="2" fill="#0a0f1e"/>
      <rect x="2" y="7" width="8" height="2" fill="#0a0f1e"/>
      <rect x="2" y="10" width="10" height="2" fill="#0a0f1e"/>
    </svg>
  </div>
</div>

<!-- ====== PROJECTS ====== -->
<div class="pixel-box pink-border" data-title="▶ PROYEK UTAMA" style="margin-bottom:12px;">
  <div style="margin-top:10px; display:grid; grid-template-columns:1fr 1fr; gap:8px;">

    <div class="project-card" onclick="openLink('https://github.com/hirumisann')">
      <!-- pixel anime icon -->
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:6px;">
        <svg viewBox="0 0 16 16" width="24" height="24">
          <rect x="2" y="1" width="12" height="13" fill="#ffb454" rx="1"/>
          <rect x="4" y="3" width="8" height="6" fill="#0a1130"/>
          <rect x="5" y="4" width="6" height="4" fill="#3a7bd5"/>
          <rect x="5" y="4" width="2" height="4" fill="#6fa3f7" opacity="0.5"/>
          <rect x="3" y="10" width="10" height="2" fill="#151f40"/>
          <rect x="4" y="10" width="2" height="2" fill="#ffb454"/>
          <rect x="7" y="10" width="2" height="2" fill="#ffd089"/>
        </svg>
        <div class="project-title">ANIMESAKU</div>
      </div>
      <div class="project-desc">Platform streaming anime<br>dengan REST API backend.<br>Built with vibe coding ✨</div>
      <div>
        <span class="project-tag">STREAMING</span>
        <span class="project-tag">ANIME</span>
        <span class="project-tag">REST API</span>
      </div>
    </div>

    <div class="project-card film" onclick="openLink('https://github.com/hirumisann')">
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:6px;">
        <svg viewBox="0 0 16 16" width="24" height="24">
          <rect x="1" y="2" width="14" height="12" fill="#e8746a" rx="1"/>
          <rect x="2" y="3" width="12" height="8" fill="#0a1130"/>
          <rect x="3" y="4" width="10" height="6" fill="#1a0a0a"/>
          <polygon points="6,5 6,9 11,7" fill="#e8746a"/>
          <rect x="2" y="12" width="2" height="2" fill="#0a1130"/>
          <rect x="5" y="12" width="2" height="2" fill="#0a1130"/>
          <rect x="8" y="12" width="2" height="2" fill="#0a1130"/>
          <rect x="11" y="12" width="2" height="2" fill="#0a1130"/>
        </svg>
        <div class="project-title film-title">FILMSAKU</div>
      </div>
      <div class="project-desc">Platform streaming film<br>dengan UI/UX modern.<br>Pixel perfect 🎬</div>
      <div>
        <span class="project-tag film-tag">STREAMING</span>
        <span class="project-tag film-tag">FILM</span>
        <span class="project-tag film-tag">UI/UX</span>
      </div>
    </div>
  </div>
</div>

<!-- ====== CONTRIBUTION SNAKE (canvas-based pixel grid) ====== -->
<div class="pixel-box green-border" data-title="▶ CONTRIBUTION SNAKE" style="margin-bottom:12px;">
  <div style="margin-top:10px; text-align:center;">
    <canvas id="snake-canvas" width="600" height="100" style="max-width:100%;"></canvas>
    <div style="font-size:6px;color:var(--text);margin-top:6px;">[ press SPACE or tap to reset snake ]</div>
  </div>
</div>

<!-- ====== CONNECT ====== -->
<div class="pixel-box purple-border" data-title="▶ TERHUBUNG DENGAN SAYA" style="margin-bottom:12px;">
  <div class="social-row" style="margin-top:8px;">

    <a class="social-btn" href="https://github.com/hirumisann" target="_blank">
      <svg viewBox="0 0 16 16" width="14" height="14" style="vertical-align:middle;margin-right:4px;">
        <rect x="5" y="0" width="6" height="1" fill="currentColor"/>
        <rect x="3" y="1" width="2" height="1" fill="currentColor"/>
        <rect x="11" y="1" width="2" height="1" fill="currentColor"/>
        <rect x="2" y="2" width="1" height="8" fill="currentColor"/>
        <rect x="13" y="2" width="1" height="8" fill="currentColor"/>
        <rect x="3" y="10" width="1" height="2" fill="currentColor"/>
        <rect x="12" y="10" width="1" height="2" fill="currentColor"/>
        <rect x="4" y="12" width="1" height="1" fill="currentColor"/>
        <rect x="11" y="12" width="1" height="1" fill="currentColor"/>
        <rect x="5" y="13" width="6" height="1" fill="currentColor"/>
        <rect x="3" y="2" width="10" height="8" fill="currentColor"/>
        <rect x="5" y="4" width="2" height="4" fill="#0a0f1e"/>
        <rect x="9" y="4" width="2" height="4" fill="#0a0f1e"/>
        <rect x="6" y="6" width="4" height="3" fill="#0a0f1e"/>
        <rect x="7" y="7" width="2" height="2" fill="currentColor"/>
      </svg>
      GITHUB
    </a>

    <a class="social-btn" href="https://instagram.com/hirumisann" target="_blank">
      <svg viewBox="0 0 16 16" width="14" height="14" style="vertical-align:middle;margin-right:4px;">
        <rect x="2" y="2" width="12" height="12" rx="3" fill="none" stroke="currentColor" stroke-width="1.5"/>
        <rect x="5" y="5" width="6" height="6" rx="1" fill="none" stroke="currentColor" stroke-width="1.2"/>
        <rect x="11" y="3" width="2" height="2" rx="0.5" fill="currentColor"/>
        <circle cx="8" cy="8" r="2" fill="none" stroke="currentColor" stroke-width="1.2"/>
      </svg>
      INSTAGRAM
    </a>

  </div>
</div>

<!-- ====== FOOTER ====== -->
<div class="footer-quote">
  "DIBUAT DENGAN SECANGKIR TEH ☕<br>
  DAN BANYAK BARIS KODE DI MALAM HARI 🌙"<br><br>
  <span style="color:var(--text);font-size:5px;">— MUHAMMAD HILMY — INDONESIA — 2025 —</span>
</div>

</div><!-- end .page -->

<script>
// ---- TYPING ANIMATION ----
const phrases = [
  'Pelajar | Web Developer',
  'REST API Builder',
  'UI/UX Explorer',
  'Vibe Coding Enjoyer',
  'Night Coder 🌙'
];
let pi = 0, ci = 0, deleting = false;
const el = document.getElementById('typing-text');

function typeLoop() {
  const cur = phrases[pi];
  if (!deleting) {
    el.textContent = cur.slice(0, ci + 1);
    ci++;
    if (ci === cur.length) { deleting = true; setTimeout(typeLoop, 1800); return; }
  } else {
    el.textContent = cur.slice(0, ci - 1);
    ci--;
    if (ci === 0) { deleting = false; pi = (pi + 1) % phrases.length; }
  }
  setTimeout(typeLoop, deleting ? 60 : 100);
}
typeLoop();

// ---- CONTRIBUTION SNAKE GAME ----
const canvas = document.getElementById('snake-canvas');
const ctx = canvas.getContext('2d');
const W = canvas.width, H = canvas.height;
const SZ = 10;
const COLS = Math.floor(W / SZ);
const ROWS = Math.floor(H / SZ);

// Generate a static contribution grid underneath
const contribColors = ['#1a2040', '#1a2040', '#0f3a2a', '#1a5c3a', '#27a060', '#4ade80'];

function randContrib(x, y) {
  const seed = (x * 37 + y * 13 + x * y) % 100;
  if (seed < 40) return contribColors[0];
  if (seed < 55) return contribColors[1];
  if (seed < 70) return contribColors[2];
  if (seed < 82) return contribColors[3];
  if (seed < 92) return contribColors[4];
  return contribColors[5];
}

// Draw static grid
function drawGrid() {
  for (let r = 0; r < ROWS; r++) {
    for (let c = 0; c < COLS; c++) {
      ctx.fillStyle = randContrib(c, r);
      ctx.fillRect(c * SZ + 1, r * SZ + 1, SZ - 2, SZ - 2);
    }
  }
}

// Snake state
let snake = [{x: 5, y: 2}];
let dir = {x: 1, y: 0};
let nextDir = {x: 1, y: 0};
let food = {x: 30, y: 4};
let score = 0;
let gameOver = false;

function placeFood() {
  food = {
    x: Math.floor(Math.random() * COLS),
    y: Math.floor(Math.random() * ROWS)
  };
}

function resetGame() {
  snake = [{x: 5, y: 2}];
  dir = {x: 1, y: 0};
  nextDir = {x: 1, y: 0};
  score = 0;
  gameOver = false;
  placeFood();
}

function stepSnake() {
  if (gameOver) return;
  dir = {...nextDir};
  const head = {x: (snake[0].x + dir.x + COLS) % COLS, y: (snake[0].y + dir.y + ROWS) % ROWS};

  if (snake.some(s => s.x === head.x && s.y === head.y)) {
    gameOver = true;
    return;
  }

  snake.unshift(head);
  if (head.x === food.x && head.y === food.y) {
    score++;
    placeFood();
  } else {
    snake.pop();
  }
}

function drawSnake() {
  ctx.clearRect(0, 0, W, H);
  drawGrid();

  // food (flashing)
  const flash = Math.floor(Date.now() / 300) % 2;
  ctx.fillStyle = flash ? '#f87171' : '#fca5a5';
  ctx.fillRect(food.x * SZ + 1, food.y * SZ + 1, SZ - 2, SZ - 2);

  // snake
  snake.forEach((s, i) => {
    if (i === 0) {
      ctx.fillStyle = '#ffb454';
    } else {
      const t = i / snake.length;
      ctx.fillStyle = `hsl(${200 + t * 60}, 80%, ${60 - t * 20}%)`;
    }
    ctx.fillRect(s.x * SZ + 1, s.y * SZ + 1, SZ - 2, SZ - 2);

    // eyes on head
    if (i === 0) {
      ctx.fillStyle = '#0a0f1e';
      ctx.fillRect(s.x * SZ + 2, s.y * SZ + 2, 2, 2);
      ctx.fillRect(s.x * SZ + 6, s.y * SZ + 2, 2, 2);
    }
  });

  if (gameOver) {
    ctx.fillStyle = 'rgba(10,15,30,0.75)';
    ctx.fillRect(0, 0, W, H);
    ctx.fillStyle = '#ffb454';
    ctx.font = '8px "Press Start 2P"';
    ctx.textAlign = 'center';
    ctx.fillText('GAME OVER — SPACE TO RETRY', W / 2, H / 2 - 6);
    ctx.fillStyle = '#9aa3c7';
    ctx.font = '6px "Press Start 2P"';
    ctx.fillText('SCORE: ' + score, W / 2, H / 2 + 10);
  }
}

// auto-steer toward food
function autoSteer() {
  if (gameOver) return;
  const head = snake[0];
  const dx = food.x - head.x;
  const dy = food.y - head.y;

  // prefer horizontal
  if (Math.abs(dx) >= Math.abs(dy)) {
    const nx = dx > 0 ? 1 : -1;
    if (!(nx === -dir.x && dir.x !== 0)) { nextDir = {x: nx, y: 0}; return; }
  }
  const ny = dy > 0 ? 1 : -1;
  if (!(ny === -dir.y && dir.y !== 0)) { nextDir = {x: 0, y: ny}; }
}

placeFood();

let lastTime = 0;
function gameLoop(ts) {
  if (ts - lastTime > 150) {
    lastTime = ts;
    autoSteer();
    stepSnake();
    if (gameOver) { setTimeout(resetGame, 2000); }
  }
  drawSnake();
  requestAnimationFrame(gameLoop);
}
requestAnimationFrame(gameLoop);

// space / tap to reset
document.addEventListener('keydown', e => { if (e.code === 'Space') { e.preventDefault(); resetGame(); } });
canvas.addEventListener('click', resetGame);
canvas.addEventListener('touchend', e => { e.preventDefault(); resetGame(); });

// Animate stat bars on load
document.querySelectorAll('.stat-bar-fill').forEach(bar => {
  const w = bar.style.width;
  bar.style.width = '0%';
  setTimeout(() => { bar.style.width = w; }, 300);
});
</script>
</body>
</html>
