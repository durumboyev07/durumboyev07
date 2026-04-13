<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Durumboy — Backend Developer</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  background: #070711;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  min-height: 100vh;
  padding: 30px 16px;
}

.wrap {
  width: 100%;
  max-width: 680px;
  background: #070711;
  color: #c8d0ff;
  font-family: 'Courier New', monospace;
  padding: 28px 24px 36px;
  position: relative;
  overflow: hidden;
  border: 1px solid #00f5ff20;
}

.grid-bg {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(0,245,255,0.04) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,245,255,0.04) 1px, transparent 1px);
  background-size: 40px 40px;
  pointer-events: none;
}

.corner { position: absolute; width: 20px; height: 20px; border-color: #00f5ff; border-style: solid; }
.tl { top: 10px; left: 10px; border-width: 2px 0 0 2px; }
.tr { top: 10px; right: 10px; border-width: 2px 2px 0 0; }
.bl { bottom: 10px; left: 10px; border-width: 0 0 2px 2px; }
.br { bottom: 10px; right: 10px; border-width: 0 2px 2px 0; }

.top-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
  font-size: 10px;
  color: #ffffff30;
  letter-spacing: 2px;
  position: relative;
  z-index: 1;
}
.online { display: flex; align-items: center; gap: 6px; color: #00ff90; }
.dot { width: 7px; height: 7px; border-radius: 50%; background: #00ff90; animation: pulse 2s infinite; }
@keyframes pulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:0.4;transform:scale(0.8)} }

.hero { text-align: center; margin-bottom: 32px; position: relative; z-index: 1; }

.avatar-ring {
  width: 90px; height: 90px;
  border-radius: 50%;
  border: 2px solid #00f5ff;
  display: flex; align-items: center; justify-content: center;
  margin: 0 auto 16px;
  font-size: 36px;
  background: #0d0d20;
  position: relative;
  box-shadow: 0 0 0 4px #00f5ff15, 0 0 0 8px #00f5ff08, 0 0 30px #00f5ff20;
}
.avatar-ring::before {
  content: '';
  position: absolute;
  inset: -6px;
  border-radius: 50%;
  border: 1px dashed #00f5ff40;
  animation: spin 12s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }

.name {
  font-size: 30px;
  font-weight: 700;
  color: #00f5ff;
  letter-spacing: 6px;
  text-transform: uppercase;
  text-shadow: 0 0 20px #00f5ff60, 0 0 60px #00f5ff20;
  margin-bottom: 8px;
}
.title-tag {
  display: inline-block;
  border: 1px solid #ff006e60;
  color: #ff84b7;
  font-size: 10px;
  letter-spacing: 4px;
  padding: 5px 16px;
  text-shadow: 0 0 10px #ff006e50;
  clip-path: polygon(0 0, calc(100% - 8px) 0, 100% 8px, 100% 100%, 8px 100%, 0 calc(100% - 8px));
}

.stats-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
  margin-bottom: 24px;
  position: relative;
  z-index: 1;
}
.stat-card {
  background: #0d0d20;
  border: 1px solid #00f5ff25;
  padding: 14px 8px;
  text-align: center;
  clip-path: polygon(0 0, calc(100% - 8px) 0, 100% 8px, 100% 100%, 0 100%);
}
.stat-val { font-size: 22px; font-weight: 700; color: #00f5ff; display: block; text-shadow: 0 0 10px #00f5ff50; }
.stat-lbl { font-size: 9px; color: #ffffff40; letter-spacing: 2px; display: block; margin-top: 4px; }

.section { margin-bottom: 22px; position: relative; z-index: 1; }

.sec-head {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 12px;
  font-size: 10px;
  letter-spacing: 4px;
  color: #ff006e;
  text-shadow: 0 0 8px #ff006e50;
}
.sec-head::before { content: '//'; color: #ffffff20; }
.sec-head::after { content: ''; flex: 1; height: 1px; background: linear-gradient(90deg, #ff006e40, transparent); }

.badges { display: flex; flex-wrap: wrap; gap: 8px; }

.badge {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  padding: 7px 14px;
  font-size: 11px;
  letter-spacing: 1.5px;
  font-weight: 700;
  font-family: 'Courier New', monospace;
  clip-path: polygon(0 0, calc(100% - 7px) 0, 100% 7px, 100% 100%, 7px 100%, 0 calc(100% - 7px));
  transition: opacity 0.2s, transform 0.15s;
  cursor: default;
}
.badge:hover { opacity: 0.75; transform: translateY(-1px); }
.badge-icon { font-size: 14px; }

.b-cyan   { background: #00f5ff12; border: 1px solid #00f5ff45; color: #00f5ff; }
.b-pink   { background: #ff006e12; border: 1px solid #ff006e45; color: #ff84b7; }
.b-yellow { background: #ffe60012; border: 1px solid #ffe60045; color: #ffe600; }
.b-green  { background: #00ff9012; border: 1px solid #00ff9045; color: #00ff90; }
.b-purple { background: #bf5fff12; border: 1px solid #bf5fff45; color: #d49aff; }

.divider {
  border: none;
  border-top: 1px solid #ffffff10;
  margin: 24px 0;
  position: relative;
  z-index: 1;
}
.divider::after {
  content: '◆';
  position: absolute;
  top: -9px; left: 50%;
  transform: translateX(-50%);
  background: #070711;
  padding: 0 10px;
  color: #ff006e80;
  font-size: 11px;
}

.contact-section { position: relative; z-index: 1; }
.contact-label {
  text-align: center;
  font-size: 10px;
  color: #ffffff25;
  letter-spacing: 3px;
  margin-bottom: 14px;
}
.contact-row { display: flex; flex-wrap: wrap; gap: 10px; justify-content: center; }

.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 22px;
  font-family: 'Courier New', monospace;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 2px;
  text-decoration: none;
  clip-path: polygon(0 0, calc(100% - 10px) 0, 100% 10px, 100% 100%, 10px 100%, 0 calc(100% - 10px));
  transition: opacity 0.2s, transform 0.15s;
}
.btn:hover { opacity: 0.8; transform: translateY(-2px); }
.btn-tg { background: #00f5ff18; border: 1px solid #00f5ff55; color: #00f5ff; }
.btn-li { background: #bf5fff18; border: 1px solid #bf5fff55; color: #d49aff; }
.btn-gm { background: #ff006e18; border: 1px solid #ff006e55; color: #ff84b7; }

.footer {
  text-align: center;
  margin-top: 28px;
  font-size: 9px;
  color: #ffffff18;
  letter-spacing: 3px;
  position: relative;
  z-index: 1;
}

.scanline {
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(0deg, transparent, transparent 3px, rgba(0,245,255,0.012) 3px, rgba(0,245,255,0.012) 4px);
  pointer-events: none;
  z-index: 0;
}
</style>
</head>
<body>

<div class="wrap">
  <div class="grid-bg"></div>
  <div class="scanline"></div>

  <div class="corner tl"></div>
  <div class="corner tr"></div>
  <div class="corner bl"></div>
  <div class="corner br"></div>

  <div class="top-bar">
    <span>SYS::GITHUB_PROFILE_v2.1</span>
    <span class="online"><span class="dot"></span>ONLINE &nbsp;·&nbsp; TASHKENT-01</span>
  </div>

  <div class="hero">
    <div class="avatar-ring">👾</div>
    <div class="name">Durumboy</div>
    <div style="margin-top:10px;">
      <span class="title-tag">&#9658; BACKEND DEVELOPER &#9668;</span>
    </div>
  </div>

  <div class="stats-row">
    <div class="stat-card">
      <span class="stat-val">3+</span>
      <span class="stat-lbl">YEARS EXP</span>
    </div>
    <div class="stat-card">
      <span class="stat-val">10+</span>
      <span class="stat-lbl">TECHNOLOGIES</span>
    </div>
    <div class="stat-card">
      <span class="stat-val">UZ</span>
      <span class="stat-lbl">LOCATION</span>
    </div>
  </div>

  <div class="section">
    <div class="sec-head">BACKEND CORE</div>
    <div class="badges">
      <span class="badge b-cyan"><span class="badge-icon">🐍</span>PYTHON</span>
      <span class="badge b-cyan"><span class="badge-icon">⚗️</span>FLASK</span>
      <span class="badge b-cyan"><span class="badge-icon">🦄</span>DJANGO</span>
      <span class="badge b-cyan"><span class="badge-icon">⚙️</span>C</span>
      <span class="badge b-cyan"><span class="badge-icon">⚙️</span>C++</span>
    </div>
  </div>

  <div class="section">
    <div class="sec-head">FRONTEND LAYER</div>
    <div class="badges">
      <span class="badge b-pink"><span class="badge-icon">🌐</span>HTML5</span>
      <span class="badge b-pink"><span class="badge-icon">🎨</span>CSS3</span>
      <span class="badge b-pink"><span class="badge-icon">⚡</span>JAVASCRIPT</span>
      <span class="badge b-pink"><span class="badge-icon">🅱️</span>BOOTSTRAP</span>
      <span class="badge b-pink"><span class="badge-icon">🔧</span>JINJA2</span>
    </div>
  </div>

  <div class="section">
    <div class="sec-head">DATABASE</div>
    <div class="badges">
      <span class="badge b-yellow"><span class="badge-icon">🐘</span>POSTGRESQL</span>
      <span class="badge b-yellow"><span class="badge-icon">🐬</span>MYSQL</span>
      <span class="badge b-yellow"><span class="badge-icon">🗃️</span>SQLITE</span>
    </div>
  </div>

  <div class="section">
    <div class="sec-head">DEVOPS &amp; TOOLS</div>
    <div class="badges">
      <span class="badge b-green"><span class="badge-icon">🐧</span>LINUX</span>
      <span class="badge b-green"><span class="badge-icon">⚡</span>REDIS</span>
      <span class="badge b-green"><span class="badge-icon">🐳</span>DOCKER</span>
      <span class="badge b-purple"><span class="badge-icon">📌</span>GIT</span>
      <span class="badge b-purple"><span class="badge-icon">🐙</span>GITHUB</span>
    </div>
  </div>

  <hr class="divider">

  <div class="contact-section">
    <div class="contact-label">// CONTACT PROTOCOLS</div>
    <div class="contact-row">
      <a href="https://t.me/into_dz" class="btn btn-tg">&#9654; TELEGRAM</a>
      <a href="https://www.linkedin.com/in/durumboy-durumboyev-4891533a0/" class="btn btn-li">&#9654; LINKEDIN</a>
      <a href="mailto:ddurumboy2197@gmail.com" class="btn btn-gm">&#9654; GMAIL</a>
    </div>
  </div>

  <div class="footer">ACCESS GRANTED &nbsp;·&nbsp; NODE: TASHKENT-01 &nbsp;·&nbsp; 2025</div>
</div>

</body>
</html>
