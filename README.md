<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mo Samir · Dev Terminal</title>
  <!-- Fonts & Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: #0a0e14;
      font-family: 'Fira Code', monospace;
      color: #c9d1d9;
      padding: 2rem 1.5rem;
      display: flex;
      justify-content: center;
      line-height: 1.6;
    }

    .terminal {
      max-width: 1000px;
      width: 100%;
      background: #0D1117;
      border-radius: 24px;
      padding: 2rem 2rem 2.5rem;
      box-shadow: 0 20px 60px rgba(0, 0, 0, 0.8), 0 0 0 1px rgba(57, 255, 20, 0.08);
      border: 1px solid rgba(57, 255, 20, 0.15);
      backdrop-filter: blur(2px);
      transition: all 0.2s ease;
    }

    /* ---- scrollbar ---- */
    ::-webkit-scrollbar { width: 6px; }
    ::-webkit-scrollbar-track { background: #0D1117; }
    ::-webkit-scrollbar-thumb { background: #39FF14; border-radius: 12px; }

    /* ---- glitch / blink ---- */
    .blink {
      animation: blink 1.2s step-end infinite;
    }
    @keyframes blink {
      0%, 100% { opacity: 1; }
      50% { opacity: 0; }
    }

    .pulse {
      animation: pulse 2.2s ease-in-out infinite;
    }
    @keyframes pulse {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.65; transform: scale(1.02); }
    }

    .slide-up {
      animation: slideUp 0.6s cubic-bezier(0.23, 1, 0.32, 1) forwards;
      opacity: 0;
      transform: translateY(18px);
    }
    .slide-up:nth-child(2) { animation-delay: 0.08s; }
    .slide-up:nth-child(3) { animation-delay: 0.15s; }
    .slide-up:nth-child(4) { animation-delay: 0.22s; }

    @keyframes slideUp {
      to { opacity: 1; transform: translateY(0); }
    }

    .flicker {
      animation: flicker 3.2s infinite alternate;
    }
    @keyframes flicker {
      0% { opacity: 0.95; text-shadow: 0 0 2px #39FF14; }
      100% { opacity: 1; text-shadow: 0 0 12px #39FF14, 0 0 30px #39ff1433; }
    }

    .typing-cursor {
      display: inline-block;
      width: 2px;
      height: 1.1em;
      background: #39FF14;
      margin-left: 6px;
      animation: blink 0.9s step-end infinite;
      vertical-align: text-bottom;
    }

    /* ---- header ---- */
    .header-typing {
      font-size: 1.4rem;
      font-weight: 500;
      letter-spacing: 0.5px;
      color: #39FF14;
      background: #0D1117;
      padding: 0.2rem 0.8rem;
      border-radius: 40px;
      display: inline-block;
      border: 1px solid #39ff1433;
      box-shadow: 0 0 12px #39ff1410;
      margin-bottom: 1.8rem;
    }

    .bash-line {
      font-size: 0.95rem;
      color: #8b949e;
      margin: 1.2rem 0 0.3rem;
      display: flex;
      align-items: center;
      gap: 6px;
    }
    .bash-line i {
      color: #39FF14;
      width: 20px;
      font-size: 0.9rem;
    }
    .bash-line span {
      color: #c9d1d9;
    }

    .divider {
      border: 0;
      height: 1px;
      background: linear-gradient(90deg, transparent, #39ff1440, #39ff1470, #39ff1440, transparent);
      margin: 1.6rem 0;
    }

    /* ---- about box ---- */
    .about-box {
      background: #0f141b;
      border-radius: 16px;
      padding: 1.2rem 1.8rem;
      border-left: 4px solid #39FF14;
      box-shadow: inset 0 0 0 1px #1c262f;
      margin: 0.5rem 0 1.2rem;
      font-size: 0.95rem;
    }
    .about-box > div {
      display: flex;
      flex-wrap: wrap;
      gap: 0.2rem 1.8rem;
    }
    .about-box .label {
      color: #8b949e;
      min-width: 100px;
    }
    .about-box .value {
      color: #e6edf3;
      font-weight: 400;
    }
    .about-box .highlight {
      color: #39FF14;
    }
    .status-badge {
      display: inline-block;
      background: #39ff1418;
      padding: 0.1rem 0.9rem;
      border-radius: 30px;
      color: #39FF14;
      border: 1px solid #39ff1433;
      font-size: 0.8rem;
      letter-spacing: 0.3px;
      margin-top: 0.4rem;
    }

    /* ---- badges ---- */
    .badge-group {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 0.8rem 1.2rem;
      margin: 1.2rem 0 1rem;
    }
    .badge-group .badge {
      background: #0D1117;
      padding: 0.3rem 1.2rem;
      border-radius: 40px;
      font-size: 0.8rem;
      font-weight: 500;
      color: #39FF14;
      border: 1px solid #39ff1430;
      box-shadow: 0 0 6px #39ff1408;
      transition: 0.2s ease;
      letter-spacing: 0.4px;
    }
    .badge-group .badge i {
      margin-right: 6px;
      opacity: 0.7;
    }
    .badge-group .badge:hover {
      background: #39ff1410;
      border-color: #39ff1470;
      transform: translateY(-2px);
      box-shadow: 0 8px 20px #39ff1405;
    }

    /* ---- tech table ---- */
    .tech-grid {
      display: flex;
      flex-wrap: wrap;
      gap: 1.5rem 2rem;
      background: #0f141b;
      border-radius: 20px;
      padding: 1.6rem 1.8rem;
      margin: 0.5rem 0 0.8rem;
      border: 1px solid #1c262f;
    }
    .tech-col {
      flex: 1 1 180px;
    }
    .tech-col h4 {
      font-size: 0.8rem;
      text-transform: uppercase;
      letter-spacing: 1.2px;
      color: #8b949e;
      margin-bottom: 0.4rem;
      border-bottom: 1px dashed #2d3843;
      padding-bottom: 0.3rem;
    }
    .tech-col .code-block {
      font-size: 0.9rem;
      color: #c9d1d9;
      background: #0a0e14;
      padding: 0.4rem 0.8rem;
      border-radius: 10px;
      border-left: 2px solid #39FF14;
      white-space: pre-wrap;
      line-height: 1.7;
    }

    /* ---- skill bars ---- */
    .skill-bars {
      margin: 1.2rem 0 0.2rem;
      background: #0f141b;
      padding: 1.4rem 1.8rem;
      border-radius: 20px;
      border: 1px solid #1c262f;
    }
    .skill-item {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-bottom: 0.5rem;
    }
    .skill-item .name {
      min-width: 100px;
      font-size: 0.9rem;
      color: #c9d1d9;
      font-weight: 400;
    }
    .skill-item .bar-bg {
      flex: 1;
      height: 8px;
      background: #1c262f;
      border-radius: 20px;
      overflow: hidden;
      box-shadow: inset 0 0 4px #00000055;
    }
    .skill-item .bar-fill {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, #39FF14, #7bff5e);
      border-radius: 20px;
      box-shadow: 0 0 12px #39ff1440;
      transition: width 1.8s cubic-bezier(0.22, 1, 0.36, 1);
    }
    .skill-item .pct {
      min-width: 44px;
      font-size: 0.8rem;
      color: #8b949e;
      text-align: right;
    }

    /* ---- project cards ---- */
    .project-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
      gap: 1.5rem;
      margin: 0.8rem 0 0.2rem;
    }
    .project-card {
      background: #0f141b;
      border-radius: 18px;
      padding: 1.2rem 1.4rem;
      border: 1px solid #1c262f;
      transition: 0.25s ease;
      box-shadow: 0 4px 12px rgba(0,0,0,0.3);
      position: relative;
      overflow: hidden;
    }
    .project-card:hover {
      transform: translateY(-6px);
      border-color: #39ff1460;
      box-shadow: 0 12px 30px #00000060, 0 0 0 1px #39ff1420;
    }
    .project-card .emoji-big {
      font-size: 1.8rem;
      line-height: 1;
      margin-bottom: 0.2rem;
      display: inline-block;
    }
    .project-card h4 {
      font-size: 1rem;
      color: #e6edf3;
      margin: 0.2rem 0 0.1rem;
    }
    .project-card .desc {
      font-size: 0.82rem;
      color: #8b949e;
      margin: 0.3rem 0 0.5rem;
      line-height: 1.5;
    }
    .project-card .tech-tags {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
      margin: 0.3rem 0 0.4rem;
    }
    .project-card .tech-tags span {
      background: #0D1117;
      padding: 0.1rem 0.7rem;
      border-radius: 30px;
      font-size: 0.7rem;
      border: 1px solid #2d3843;
      color: #c9d1d9;
      letter-spacing: 0.2px;
    }
    .project-card .link-icon {
      color: #39FF14;
      opacity: 0.6;
      transition: 0.2s;
      font-size: 0.9rem;
      margin-left: 4px;
    }
    .project-card .link-icon:hover {
      opacity: 1;
    }
    .project-card .feature-list {
      font-size: 0.78rem;
      color: #b1bac4;
      list-style: none;
      padding-left: 0;
      margin: 0.2rem 0 0;
    }
    .project-card .feature-list li {
      padding: 0.08rem 0;
      display: flex;
      align-items: baseline;
      gap: 6px;
    }
    .project-card .feature-list li::before {
      content: "›";
      color: #39FF14;
      font-weight: 600;
    }

    /* ---- stats ---- */
    .stats-row {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 1.2rem;
      margin: 0.6rem 0 0.2rem;
    }
    .stats-row img {
      border-radius: 16px;
      border: 1px solid #1c262f;
      background: #0D1117;
      box-shadow: 0 4px 20px rgba(0,0,0,0.4);
      transition: 0.2s ease;
      max-width: 100%;
      height: auto;
    }
    .stats-row img:hover {
      transform: scale(1.01);
      border-color: #39ff1430;
    }
    .streak-wrap {
      margin: 1rem 0 0.8rem;
      text-align: center;
    }
    .streak-wrap img {
      border-radius: 16px;
      border: 1px solid #1c262f;
      max-width: 100%;
    }
    .activity-graph {
      margin: 1rem 0 1.2rem;
      border-radius: 20px;
      overflow: hidden;
      border: 1px solid #1c262f;
      background: #0D1117;
      padding: 0.2rem;
    }
    .activity-graph img {
      width: 100%;
      display: block;
      border-radius: 12px;
    }

    /* ---- contact ---- */
    .contact-links {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 1rem 1.6rem;
      margin: 0.8rem 0 0.2rem;
    }
    .contact-links a {
      color: #c9d1d9;
      text-decoration: none;
      font-size: 0.9rem;
      background: #0f141b;
      padding: 0.3rem 1.4rem;
      border-radius: 40px;
      border: 1px solid #2d3843;
      transition: 0.2s;
      display: inline-flex;
      align-items: center;
      gap: 8px;
    }
    .contact-links a i {
      color: #39FF14;
      width: 18px;
    }
    .contact-links a:hover {
      border-color: #39FF14;
      background: #39ff1408;
      transform: translateY(-2px);
      box-shadow: 0 6px 16px #39ff1405;
    }
    .visitor-badge {
      margin: 1rem 0 0.4rem;
      text-align: center;
      opacity: 0.7;
      font-size: 0.8rem;
    }

    .final-status {
      text-align: center;
      font-size: 0.95rem;
      color: #8b949e;
      margin-top: 1.8rem;
      border-top: 1px solid #1c262f;
      padding-top: 1.6rem;
      letter-spacing: 0.2px;
    }
    .final-status .cursor-block {
      display: inline-block;
      width: 10px;
      height: 18px;
      background: #39FF14;
      margin-left: 6px;
      vertical-align: text-bottom;
      animation: blink 1s step-end infinite;
    }

    /* responsive */
    @media (max-width: 640px) {
      .terminal { padding: 1.2rem 1rem; }
      .about-box > div { flex-direction: column; gap: 0.1rem; }
      .tech-grid { flex-direction: column; gap: 1rem; }
      .skill-item { flex-wrap: wrap; }
      .skill-item .name { min-width: 80px; }
    }
  </style>
</head>
<body>
<div class="terminal">

  <!-- header with typing -->
  <div class="header-typing slide-up">
    <i class="fas fa-terminal" style="margin-right: 10px; opacity:0.8;"></i>
    <span id="typewriter"></span><span class="typing-cursor"></span>
  </div>

  <!-- bash: about -->
  <div class="bash-line slide-up"><i class="fas fa-chevron-right"></i> <span>mo@dev:~$ cat about.txt</span></div>
  <div class="about-box slide-up">
    <div>
      <span class="label"><i class="far fa-user" style="color:#39FF14;width:20px;"></i> Name</span>
      <span class="value">Mo Samir <span style="color:#39FF14;font-weight:400;">·</span> <span class="highlight">Web Developer</span></span>
    </div>
    <div>
      <span class="label"><i class="fas fa-graduation-cap" style="color:#39FF14;width:20px;"></i> Education</span>
      <span class="value">MCA Graduate — Web Technologies & Database Systems</span>
    </div>
    <div>
      <span class="label"><i class="fas fa-briefcase" style="color:#39FF14;width:20px;"></i> Experience</span>
      <span class="value">Backup Support Systems @ SRF Limited</span>
    </div>
    <div>
      <span class="label"><i class="fas fa-bullseye" style="color:#39FF14;width:20px;"></i> Focus</span>
      <span class="value">Secure Auth · RBAC · Scalable Backend</span>
    </div>
    <div>
      <span class="label"><i class="fas fa-chess-king" style="color:#39FF14;width:20px;"></i> Hobby</span>
      <span class="value">Chess ♟️ | Debugging at 2 AM 🐛</span>
    </div>
    <div style="margin-top:8px;">
      <span class="status-badge"><i class="fas fa-circle" style="font-size:0.5rem; vertical-align:middle; margin-right:6px; color:#39FF14;"></i> ONLINE · building, breaking, fixing</span>
    </div>
  </div>

  <!-- badges -->
  <div class="badge-group slide-up">
    <span class="badge"><i class="fas fa-code"></i> WEB DEVELOPER</span>
    <span class="badge"><i class="fas fa-user-graduate"></i> MCA GRADUATE</span>
    <span class="badge"><i class="fas fa-layer-group"></i> FULL STACK</span>
    <span class="badge"><i class="fas fa-shield-alt"></i> SECURITY FOCUSED</span>
  </div>

  <!-- tech stack -->
  <div class="bash-line slide-up"><i class="fas fa-chevron-right"></i> <span>mo@dev:~$ ls tech_stack/</span></div>
  <div class="tech-grid slide-up">
    <div class="tech-col">
      <h4><i class="fas fa-laptop-code" style="color:#39FF14;margin-right:6px;"></i> frontend</h4>
      <div class="code-block">HTML5 · CSS3 · JavaScript<br>Bootstrap · jQuery · Tailwind</div>
    </div>
    <div class="tech-col">
      <h4><i class="fas fa-server" style="color:#39FF14;margin-right:6px;"></i> backend</h4>
      <div class="code-block">PHP · Laravel · Node.js<br>Python · REST APIs</div>
    </div>
    <div class="tech-col">
      <h4><i class="fas fa-database" style="color:#39FF14;margin-right:6px;"></i> database</h4>
      <div class="code-block">MySQL · MongoDB<br>SQLite · PostgreSQL</div>
    </div>
    <div class="tech-col">
      <h4><i class="fas fa-tools" style="color:#39FF14;margin-right:6px;"></i> tools</h4>
      <div class="code-block">Git · GitHub · Docker<br>VSCode · Postman · Composer · Linux</div>
    </div>
  </div>

  <!-- skill bars with animation on load -->
  <div class="skill-bars slide-up" id="skillBars">
    <div class="skill-item"><span class="name">PHP</span><div class="bar-bg"><div class="bar-fill" data-width="90"></div></div><span class="pct">90%</span></div>
    <div class="skill-item"><span class="name">Laravel</span><div class="bar-bg"><div class="bar-fill" data-width="85"></div></div><span class="pct">85%</span></div>
    <div class="skill-item"><span class="name">MySQL</span><div class="bar-bg"><div class="bar-fill" data-width="88"></div></div><span class="pct">88%</span></div>
    <div class="skill-item"><span class="name">JavaScript</span><div class="bar-bg"><div class="bar-fill" data-width="75"></div></div><span class="pct">75%</span></div>
  </div>

  <!-- projects -->
  <div class="bash-line slide-up"><i class="fas fa-chevron-right"></i> <span>mo@dev:~$ ls -la projects/</span></div>
  <div class="project-grid slide-up">
    <div class="project-card">
      <span class="emoji-big">🏠</span>
      <h4>all-home-services</h4>
      <div class="tech-tags"><span>PHP</span><span>MySQL</span><span>Bootstrap</span></div>
      <div class="desc">Enterprise service booking platform</div>
      <ul class="feature-list">
        <li>Auth & authorization</li>
        <li>Real-time booking</li>
        <li>Admin dashboard w/ analytics</li>
        <li>Payment gateway ready</li>
      </ul>
    </div>
    <div class="project-card">
      <span class="emoji-big">🔐</span>
      <h4>otp-verification</h4>
      <div class="tech-tags"><span>PHP</span><span>AJAX</span><span>MySQL</span></div>
      <div class="desc">Secure 2FA authentication system</div>
      <ul class="feature-list">
        <li>Time-based OTP generation</li>
        <li>Secure session management</li>
        <li>Rate limiting & brute-force guard</li>
        <li>SMS/Email gateway architecture</li>
      </ul>
    </div>
    <div class="project-card">
      <span class="emoji-big">🧑‍💼</span>
      <h4>rbac-admin-panel</h4>
      <div class="tech-tags"><span>Laravel</span><span>MySQL</span><span>Bootstrap</span></div>
      <div class="desc">Role-based access control system</div>
      <ul class="feature-list">
        <li>Multi-role permission hierarchy</li>
        <li>Dynamic role-based menus</li>
        <li>Audit logs & activity tracking</li>
        <li>Secure hashing & reset flows</li>
      </ul>
    </div>
    <div class="project-card">
      <span class="emoji-big">📘</span>
      <h4>academic-repo</h4>
      <div class="tech-tags"><span>DBMS</span><span>Web Dev</span><span>Algorithms</span></div>
      <div class="desc">MCA curriculum implementations</div>
      <ul class="feature-list">
        <li>Database normalization projects</li>
        <li>Algorithms in PHP / Python</li>
        <li>Full-stack mini-projects</li>
        <li>Clean code & design patterns</li>
      </ul>
    </div>
    <div class="project-card">
      <span class="emoji-big">🧮</span>
      <h4>loan-calculator</h4>
      <div class="tech-tags"><span>JavaScript</span><span>HTML5</span><span>CSS3</span></div>
      <div class="desc">Interactive EMI & loan calculation tool</div>
      <ul class="feature-list">
        <li>Real-time EMI & interest calc</li>
        <li>Clean, responsive UI</li>
        <li>Dynamic input validation</li>
        <li><a href="https://mosamir-05.github.io/LoanCalc/" target="_blank" style="color:#39FF14;text-decoration:none;">🔗 ./run --live</a></li>
      </ul>
    </div>
    <div class="project-card">
      <span class="emoji-big">🌐</span>
      <h4>portfolio</h4>
      <div class="tech-tags"><span>HTML5</span><span>CSS3</span><span>JavaScript</span></div>
      <div class="desc">Personal developer portfolio</div>
      <ul class="feature-list">
        <li>Skills, projects & experience</li>
        <li>Fully responsive design</li>
        <li>Contact & resume sections</li>
        <li><a href="https://mosamir-05.github.io/my_portfolio/" target="_blank" style="color:#39FF14;text-decoration:none;">🔗 ./run --live</a></li>
      </ul>
    </div>
  </div>

  <!-- stats -->
  <div class="bash-line slide-up"><i class="fas fa-chevron-right"></i> <span>mo@dev:~$ git log --stats</span></div>
  <div class="stats-row slide-up">
    <img width="45%" src="https://github-readme-stats.vercel.app/api?username=MoSamir-05&show_icons=true&theme=chartreuse-dark&include_all_commits=true&count_private=true&border_radius=6&bg_color=0D1117&title_color=39FF14&icon_color=39FF14&text_color=c9d1d9" alt="stats" />
    <img width="45%" src="https://github-readme-stats.vercel.app/api/top-langs/?username=MoSamir-05&layout=compact&langs_count=8&theme=chartreuse-dark&border_radius=6&bg_color=0D1117&title_color=39FF14&text_color=c9d1d9" alt="top langs" />
  </div>
  <div class="streak-wrap slide-up">
    <img width="80%" src="https://github-readme-streak-stats.herokuapp.com/?user=MoSamir-05&theme=dark&border_radius=6&background=0D1117&ring=39FF14&fire=39FF14&currStreakLabel=39FF14&currStreakNum=c9d1d9&sideLabels=c9d1d9&dates=8b949e" alt="streak" />
  </div>
  <div class="activity-graph slide-up">
    <img src="https://github-readme-activity-graph.vercel.app/graph?username=MoSamir-05&theme=react-dark&hide_border=true&area=true&bg_color=0D1117&color=39FF14&line=39FF14&point=c9d1d9" width="100%" alt="activity graph" />
  </div>

  <!-- contact -->
  <div class="bash-line slide-up"><i class="fas fa-chevron-right"></i> <span>mo@dev:~$ cat contact.txt</span></div>
  <div class="contact-links slide-up">
    <a href="mailto:mo.samir.sitponwala@gmail.com"><i class="fas fa-envelope"></i> mo.samir.sitponwala</a>
    <a href="https://github.com/MoSamir-05" target="_blank"><i class="fab fa-github"></i> MoSamir-05</a>
    <a href="https://mosamir-05.github.io/my_portfolio/" target="_blank"><i class="fas fa-globe"></i> portfolio</a>
  </div>
  <div class="visitor-badge slide-up">
    <img src="https://komarev.com/ghpvc/?username=MoSamir-05&label=visitors&color=39FF14&style=flat-square&labelColor=0D1117" alt="visitors" />
  </div>

  <!-- final status -->
  <div class="final-status slide-up">
    <span style="color:#39FF14;">mo@dev:~$</span> echo $STATUS<br>
    <span style="color:#e6edf3;">> Building clean, scalable web applications. Always shipping.</span>
    <span class="cursor-block"></span>
  </div>

</div>

<script>
  (function(){
    // ---- typewriter effect ----
    const text = "$ whoami  •  Mo Samir — Web Developer  •  $ cat skills.txt  •  PHP | Laravel | MySQL";
    const el = document.getElementById('typewriter');
    let index = 0;
    function type() {
      if (index < text.length) {
        el.textContent += text.charAt(index);
        index++;
        setTimeout(type, 45 + Math.random()*25);
      }
    }
    setTimeout(type, 300);

    // ---- animate skill bars (on load) ----
    const fills = document.querySelectorAll('.bar-fill');
    function animateBars() {
      fills.forEach(bar => {
        const w = bar.getAttribute('data-width');
        if (w) {
          bar.style.width = w + '%';
        }
      });
    }
    // start after a small delay to let the page settle
    setTimeout(animateBars, 500);

    // ---- re-animate on scroll (optional) using Intersection Observer ----
    if ('IntersectionObserver' in window) {
      const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            const target = entry.target;
            if (target.id === 'skillBars') {
              // reset to 0 then animate again
              fills.forEach(bar => { bar.style.width = '0%'; });
              setTimeout(animateBars, 200);
            }
          }
        });
      }, { threshold: 0.3 });
      const skillSection = document.getElementById('skillBars');
      if (skillSection) observer.observe(skillSection);
    }

    // ---- additional flicker effect on badges (random) ----
    document.querySelectorAll('.badge-group .badge').forEach((badge, i) => {
      badge.style.animationDelay = (i * 0.2) + 's';
    });
  })();
</script>
</body>
</html>
