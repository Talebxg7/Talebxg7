<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Taleb Jarrar — Full Stack Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#10141f;
    --bg-alt:#141a29;
    --card:#1a2033;
    --card-border:#262e46;
    --hairline:#262e46;
    --text:#ecedf3;
    --text-dim:#9aa2b8;
    --text-faint:#5c6580;
    --gold:#e8a33d;
    --gold-dim:#8a6529;
    --teal:#3fa796;
    --teal-dim:#2b5a52;
  }
  *{margin:0;padding:0;box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--bg);
    color:var(--text);
    font-family:'Inter',sans-serif;
    line-height:1.6;
    -webkit-font-smoothing:antialiased;
  }
  a{color:inherit;text-decoration:none;}
  .wrap{max-width:920px;margin:0 auto;padding:0 28px;}
  h1,h2,h3{font-family:'Space Grotesk',sans-serif;letter-spacing:-0.01em;}
  .mono{font-family:'JetBrains Mono',monospace;}

  /* subtle grid-paper texture nodding to the Sudoku solver project */
  .grid-texture{
    position:fixed; inset:0; pointer-events:none; z-index:0; opacity:0.05;
    background-image:
      linear-gradient(var(--teal) 1px, transparent 1px),
      linear-gradient(90deg, var(--teal) 1px, transparent 1px);
    background-size:42px 42px;
    mask-image: radial-gradient(ellipse 70% 50% at 50% 0%, black 40%, transparent 90%);
  }

  header{
    position:sticky; top:0; z-index:10;
    background:rgba(16,20,31,0.85);
    backdrop-filter:blur(8px);
    border-bottom:1px solid var(--hairline);
  }
  nav{display:flex; justify-content:space-between; align-items:center; padding:18px 28px; max-width:920px; margin:0 auto;}
  .logo{font-family:'Space Grotesk',sans-serif; font-weight:700; font-size:18px;}
  .logo span{color:var(--gold);}
  nav ul{display:flex; gap:28px; list-style:none;}
  nav ul li a{font-size:14px; color:var(--text-dim); transition:color .2s;}
  nav ul li a:hover{color:var(--text);}

  /* HERO */
  .hero{padding:100px 0 60px; position:relative; z-index:1;}
  .eyebrow{
    font-family:'JetBrains Mono',monospace; font-size:13px; color:var(--gold);
    letter-spacing:.08em; text-transform:uppercase; margin-bottom:18px;
    display:flex; align-items:center; gap:10px;
  }
  .eyebrow::before{content:''; width:8px; height:8px; background:var(--gold); border-radius:50%; display:inline-block;}
  .hero h1{font-size:56px; font-weight:700; line-height:1.05; max-width:680px;}
  .hero p.tagline{font-size:19px; color:var(--text-dim); margin-top:20px; max-width:560px;}
  .hero-links{display:flex; gap:14px; margin-top:34px; flex-wrap:wrap;}
  .btn{
    padding:12px 22px; border-radius:6px; font-size:14px; font-weight:600;
    font-family:'JetBrains Mono',monospace; transition:all .2s; border:1px solid transparent;
  }
  .btn-primary{background:var(--gold); color:#191305;}
  .btn-primary:hover{background:#f0b256;}
  .btn-ghost{border-color:var(--card-border); color:var(--text);}
  .btn-ghost:hover{border-color:var(--teal); color:var(--teal);}

  /* SCOREBOARD — signature element, nods to the prediction-app leaderboard */
  .scoreboard{
    margin-top:56px; border:1px solid var(--card-border); border-radius:10px;
    background:var(--card); overflow:hidden;
  }
  .scoreboard-head{
    display:flex; justify-content:space-between; align-items:center;
    padding:12px 20px; border-bottom:1px solid var(--hairline);
    font-family:'JetBrains Mono',monospace; font-size:12px; color:var(--text-faint);
    letter-spacing:.06em; text-transform:uppercase;
  }
  .live-dot{width:7px; height:7px; border-radius:50%; background:var(--teal); display:inline-block; margin-right:7px; box-shadow:0 0 0 0 rgba(63,167,150,.6); animation:pulse 2s infinite;}
  @keyframes pulse{
    0%{box-shadow:0 0 0 0 rgba(63,167,150,.5);}
    70%{box-shadow:0 0 0 8px rgba(63,167,150,0);}
    100%{box-shadow:0 0 0 0 rgba(63,167,150,0);}
  }
  .scoreboard-grid{display:grid; grid-template-columns:repeat(3,1fr);}
  .score-cell{padding:26px 20px; text-align:center; border-right:1px solid var(--hairline);}
  .score-cell:last-child{border-right:none;}
  .score-num{font-family:'JetBrains Mono',monospace; font-size:34px; font-weight:600; color:var(--gold);}
  .score-label{font-size:12px; color:var(--text-dim); margin-top:6px; text-transform:uppercase; letter-spacing:.04em;}

  section{padding:70px 0; position:relative; z-index:1;}
  .section-head{display:flex; align-items:baseline; gap:14px; margin-bottom:36px;}
  .section-num{font-family:'JetBrains Mono',monospace; color:var(--text-faint); font-size:14px;}
  .section-head h2{font-size:28px;}

  /* ABOUT */
  .about-text{color:var(--text-dim); font-size:16px; max-width:680px;}
  .about-text strong{color:var(--text); font-weight:600;}

  /* EXPERIENCE */
  .timeline{border-left:1px solid var(--hairline); padding-left:28px; display:flex; flex-direction:column; gap:36px;}
  .tl-item{position:relative;}
  .tl-item::before{
    content:''; position:absolute; left:-33px; top:4px; width:9px; height:9px;
    border-radius:50%; background:var(--bg); border:2px solid var(--teal);
  }
  .tl-date{font-family:'JetBrains Mono',monospace; font-size:12px; color:var(--gold); text-transform:uppercase; letter-spacing:.04em;}
  .tl-role{font-size:18px; font-weight:600; margin-top:6px;}
  .tl-org{color:var(--text-dim); font-size:14px; margin-top:2px;}
  .tl-desc{color:var(--text-dim); font-size:15px; margin-top:10px; max-width:600px;}

  /* PROJECTS */
  .projects-grid{display:grid; grid-template-columns:1fr; gap:18px;}
  .project-card{
    border:1px solid var(--card-border); background:var(--card); border-radius:10px;
    padding:26px; transition:border-color .2s, transform .2s;
  }
  .project-card:hover{border-color:var(--teal-dim); transform:translateY(-2px);}
  .project-top{display:flex; justify-content:space-between; align-items:flex-start; gap:16px;}
  .project-title{font-size:19px; font-weight:600;}
  .project-role{font-family:'JetBrains Mono',monospace; font-size:11px; color:var(--teal); text-transform:uppercase; letter-spacing:.05em; margin-top:4px;}
  .project-link{font-family:'JetBrains Mono',monospace; font-size:13px; color:var(--text-dim); white-space:nowrap; border:1px solid var(--card-border); padding:6px 12px; border-radius:6px; transition:.2s;}
  .project-link:hover{color:var(--gold); border-color:var(--gold-dim);}
  .project-desc{color:var(--text-dim); font-size:14.5px; margin-top:14px; max-width:620px;}
  .tags{display:flex; flex-wrap:wrap; gap:8px; margin-top:16px;}
  .tag{font-family:'JetBrains Mono',monospace; font-size:11.5px; color:var(--text-dim); background:var(--bg-alt); border:1px solid var(--hairline); padding:4px 10px; border-radius:4px;}

  /* TECH STACK */
  .stack-groups{display:grid; grid-template-columns:1fr 1fr; gap:28px;}
  .stack-group h3{font-size:13px; color:var(--text-faint); text-transform:uppercase; letter-spacing:.06em; font-family:'JetBrains Mono',monospace; font-weight:500; margin-bottom:14px;}
  .stack-tags{display:flex; flex-wrap:wrap; gap:8px;}
  .stack-tag{font-size:13.5px; padding:6px 13px; border-radius:20px; border:1px solid var(--card-border); color:var(--text-dim);}

  /* EDUCATION / LANG */
  .ed-row{display:flex; justify-content:space-between; align-items:baseline; flex-wrap:wrap; gap:8px;}
  .ed-school{font-size:18px; font-weight:600;}
  .ed-date{font-family:'JetBrains Mono',monospace; font-size:12px; color:var(--gold);}
  .ed-degree{color:var(--text-dim); margin-top:4px; font-size:15px;}
  .lang-row{display:flex; gap:28px; margin-top:22px;}
  .lang-item{font-family:'JetBrains Mono',monospace; font-size:14px; color:var(--text-dim);}
  .lang-item strong{color:var(--text); font-family:'Inter',sans-serif;}

  footer{border-top:1px solid var(--hairline); padding:50px 0 40px; position:relative; z-index:1;}
  .footer-inner{display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:20px;}
  .footer-title{font-size:22px; font-weight:600; font-family:'Space Grotesk',sans-serif;}
  .footer-sub{color:var(--text-dim); font-size:14px; margin-top:6px;}
  .footer-links{display:flex; gap:16px; flex-wrap:wrap;}
  .footer-links a{font-family:'JetBrains Mono',monospace; font-size:13px; color:var(--text-dim); border:1px solid var(--card-border); padding:9px 16px; border-radius:6px; transition:.2s;}
  .footer-links a:hover{color:var(--gold); border-color:var(--gold-dim);}
  .copyright{margin-top:36px; font-size:12px; color:var(--text-faint); font-family:'JetBrains Mono',monospace;}

  .reveal{opacity:0; transform:translateY(16px); transition:opacity .6s ease, transform .6s ease;}
  .reveal.visible{opacity:1; transform:translateY(0);}

  @media(max-width:640px){
    .hero h1{font-size:38px;}
    .scoreboard-grid{grid-template-columns:1fr;}
    .score-cell{border-right:none; border-bottom:1px solid var(--hairline);}
    .score-cell:last-child{border-bottom:none;}
    .stack-groups{grid-template-columns:1fr;}
    nav ul{gap:16px;}
    nav ul li a{font-size:12.5px;}
  }
  :focus-visible{outline:2px solid var(--teal); outline-offset:3px;}
  @media (prefers-reduced-motion: reduce){
    *{animation:none !important; transition:none !important;}
  }
</style>
</head>
<body>

<div class="grid-texture"></div>

<header>
  <nav>
    <div class="logo">TJ<span>.</span></div>
    <ul>
      <li><a href="#about">About</a></li>
      <li><a href="#experience">Experience</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#stack">Stack</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>
</header>

<div class="wrap">

  <section class="hero">
    <div class="eyebrow">Amman, Jordan · Open to opportunities</div>
    <h1>Taleb Jarrar</h1>
    <p class="tagline">Full stack developer building across React, Flutter, and applied AI — from live prediction platforms to intelligent agents.</p>
    <div class="hero-links">
      <a class="btn btn-primary" href="mailto:talibjarrar@gmail.com">Get in touch</a>
      <a class="btn btn-ghost" href="https://github.com/Talebxg7" target="_blank" rel="noopener">GitHub ↗</a>
      <a class="btn btn-ghost" href="https://www.linkedin.com/in/taleb-jarrar-7ba384335" target="_blank" rel="noopener">LinkedIn ↗</a>
    </div>

    <div class="scoreboard reveal">
      <div class="scoreboard-head">
        <span><span class="live-dot"></span>Current standings</span>
        <span>SEASON 2026</span>
      </div>
      <div class="scoreboard-grid">
        <div class="score-cell">
          <div class="score-num">03</div>
          <div class="score-label">Shipped Projects</div>
        </div>
        <div class="score-cell">
          <div class="score-num">150+</div>
          <div class="score-label">Contributions</div>
        </div>
        <div class="score-cell">
          <div class="score-num">03</div>
          <div class="score-label">Languages Spoken</div>
        </div>
      </div>
    </div>
  </section>

  <section id="about">
    <div class="section-head reveal">
      <span class="section-num mono">01</span>
      <h2>About</h2>
    </div>
    <p class="about-text reveal">
      I'm a <strong>Software Engineering graduate from Istinye University, Istanbul</strong>, working across the
      full stack — <strong>React, Flutter, Node.js/Express, FastAPI, and PostgreSQL</strong>. I've contributed
      production code to a live sports-prediction platform, built an AI agent that solves Sudoku by combining
      logic, mathematics, and optimization, and shipped a full-stack dental diagnosis app spanning mobile,
      backend, and machine learning. I like projects where a real technical problem meets a real user need.
    </p>
  </section>

  <section id="experience">
    <div class="section-head reveal">
      <span class="section-num mono">02</span>
      <h2>Experience</h2>
    </div>
    <div class="timeline">
      <div class="tl-item reveal">
        <div class="tl-date">2025 — Present</div>
        <div class="tl-role">Full Stack Contributor</div>
        <div class="tl-org">Who Will Win — whowillwinapp.com</div>
        <p class="tl-desc">
          Contributed to a live sports-prediction platform, originally built in Flutter/Dart/Firebase and later
          rebuilt on React, Vite, Tailwind CSS, Express, and PostgreSQL. Wrote and edited front-end code, reviewed
          the production codebase, and worked directly with the founding engineer on feature direction.
        </p>
      </div>
      <div class="tl-item reveal">
        <div class="tl-date">Jul 2025 — Oct 2025</div>
        <div class="tl-role">Software Engineering Intern</div>
        <div class="tl-org">GCE Soft — Amman, Jordan</div>
        <p class="tl-desc">
          Worked with C#, ASP.NET Core, and Entity Framework Core alongside Flutter mobile UI and backend API
          development for a food and grocery delivery app ahead of its production launch.
        </p>
      </div>
    </div>
  </section>

  <section id="projects">
    <div class="section-head reveal">
      <span class="section-num mono">03</span>
      <h2>Featured Projects</h2>
    </div>
    <div class="projects-grid">

      <div class="project-card reveal">
        <div class="project-top">
          <div>
            <div class="project-title">Who Will Win</div>
            <div class="project-role">Full stack contributor</div>
          </div>
          <a class="project-link" href="https://whowillwinapp.com" target="_blank" rel="noopener">Visit ↗</a>
        </div>
        <p class="project-desc">
          A sports-prediction platform where users predict match outcomes and compete on live leaderboards —
          private leagues, real-time rank updates, and season-long champion/top-scorer challenges.
        </p>
        <div class="tags">
          <span class="tag">React</span><span class="tag">Vite</span><span class="tag">Tailwind CSS</span>
          <span class="tag">Express</span><span class="tag">PostgreSQL</span><span class="tag">Drizzle ORM</span>
        </div>
      </div>

      <div class="project-card reveal">
        <div class="project-top">
          <div>
            <div class="project-title">Intelligent Sudoku Solver Agent</div>
            <div class="project-role">Principles of AI — course project</div>
          </div>
          <a class="project-link" href="https://github.com/ipeknrercn/principles-of-ai-sudoku-solver-project" target="_blank" rel="noopener">Repo ↗</a>
        </div>
        <p class="project-desc">
          A rational AI agent solving Sudoku by combining three pillars: propositional logic (CSP, AC-3,
          backtracking), the mathematics of AI (linear algebra, entropy scoring), and heuristic optimization
          (Simulated Annealing, Genetic Algorithms) — with a live step-by-step web visualizer.
        </p>
        <div class="tags">
          <span class="tag">Python</span><span class="tag">Flask</span><span class="tag">NumPy</span>
          <span class="tag">CSP</span><span class="tag">Genetic Algorithm</span>
        </div>
      </div>

      <div class="project-card reveal">
        <div class="project-top">
          <div>
            <div class="project-title">Smart Dental Diagnosis System</div>
            <div class="project-role">Solo project — mobile, backend &amp; AI/ML</div>
          </div>
          <a class="project-link" href="https://github.com/Talebxg7/Smart-Dental-Diagnosis-System-For-Oral" target="_blank" rel="noopener">Repo ↗</a>
        </div>
        <p class="project-desc">
          An AI-powered mobile app that analyzes intraoral images to detect conditions like caries, tartar, and
          gingivitis, returning instant results with confidence scores and scan history.
        </p>
        <div class="tags">
          <span class="tag">Flutter</span><span class="tag">FastAPI</span><span class="tag">PostgreSQL</span>
          <span class="tag">PyTorch</span><span class="tag">JWT Auth</span><span class="tag">Docker</span>
        </div>
      </div>

    </div>
  </section>

  <section id="stack">
    <div class="section-head reveal">
      <span class="section-num mono">04</span>
      <h2>Tech Stack</h2>
    </div>
    <div class="stack-groups">
      <div class="stack-group reveal">
        <h3>Frontend &amp; Mobile</h3>
        <div class="stack-tags">
          <span class="stack-tag">React</span><span class="stack-tag">Flutter</span><span class="stack-tag">Dart</span>
          <span class="stack-tag">JavaScript</span><span class="stack-tag">HTML/CSS</span><span class="stack-tag">Tailwind CSS</span>
        </div>
      </div>
      <div class="stack-group reveal">
        <h3>Backend &amp; Data</h3>
        <div class="stack-tags">
          <span class="stack-tag">Node.js / Express</span><span class="stack-tag">FastAPI</span>
          <span class="stack-tag">C# / ASP.NET Core</span><span class="stack-tag">Entity Framework Core</span>
          <span class="stack-tag">PostgreSQL</span><span class="stack-tag">Firebase</span>
        </div>
      </div>
      <div class="stack-group reveal">
        <h3>AI &amp; Applied ML</h3>
        <div class="stack-tags">
          <span class="stack-tag">Python</span><span class="stack-tag">PyTorch</span>
          <span class="stack-tag">Constraint Satisfaction</span><span class="stack-tag">Heuristic Search</span>
        </div>
      </div>
      <div class="stack-group reveal">
        <h3>Tools &amp; Practice</h3>
        <div class="stack-tags">
          <span class="stack-tag">Git</span><span class="stack-tag">Docker</span><span class="stack-tag">CI/CD</span>
          <span class="stack-tag">Postman</span><span class="stack-tag">Swagger</span>
        </div>
      </div>
    </div>
  </section>

  <section id="education">
    <div class="section-head reveal">
      <span class="section-num mono">05</span>
      <h2>Education &amp; Languages</h2>
    </div>
    <div class="reveal">
      <div class="ed-row">
        <div class="ed-school">Istinye University, Istanbul</div>
        <div class="ed-date">Oct 2022 — Jun 2026</div>
      </div>
      <div class="ed-degree">B.Sc., Software Engineering</div>
    </div>
    <div class="lang-row reveal">
      <div class="lang-item"><strong>Arabic</strong> · native</div>
      <div class="lang-item"><strong>English</strong> · fluent</div>
      <div class="lang-item"><strong>Turkish</strong> · conversational</div>
    </div>
  </section>

</div>

<footer id="contact">
  <div class="wrap footer-inner">
    <div>
      <div class="footer-title">Let's build something.</div>
      <div class="footer-sub">talibjarrar@gmail.com · +962 79 797 3790</div>
    </div>
    <div class="footer-links">
      <a href="mailto:talibjarrar@gmail.com">Email</a>
      <a href="https://github.com/Talebxg7" target="_blank" rel="noopener">GitHub</a>
      <a href="https://www.linkedin.com/in/taleb-jarrar-7ba384335" target="_blank" rel="noopener">LinkedIn</a>
    </div>
  </div>
  <div class="wrap copyright">© 2026 Taleb Jarrar — built with HTML, CSS &amp; a bit of curiosity.</div>
</footer>

<script>
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => { if(e.isIntersecting){ e.target.classList.add('visible'); } });
  }, {threshold:0.12});
  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));
</script>

</body>
</html>


## 🌐 Socials:
[![Facebook](https://img.shields.io/badge/Facebook-%231877F2.svg?logo=Facebook&logoColor=white)](https://facebook.com/Whowillwin App) [![Instagram](https://img.shields.io/badge/Instagram-%23E4405F.svg?logo=Instagram&logoColor=white)](https://instagram.com/Talebxg7__) [![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://linkedin.com/in/taleb-jarrar-7ba384335) [![X](https://img.shields.io/badge/X-black.svg?logo=X&logoColor=white)](https://x.com/Talebhas) [![email](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white)](mailto:talibjarrar@gmail.com) 

# 💻 Tech Stack:
![C](https://img.shields.io/badge/c-%2300599C.svg?style=for-the-badge&logo=c&logoColor=white) ![C#](https://img.shields.io/badge/c%23-%23239120.svg?style=for-the-badge&logo=csharp&logoColor=white) ![C++](https://img.shields.io/badge/c++-%2300599C.svg?style=for-the-badge&logo=c%2B%2B&logoColor=white) ![Dart](https://img.shields.io/badge/dart-%230175C2.svg?style=for-the-badge&logo=dart&logoColor=white) ![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white) ![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white) ![PHP](https://img.shields.io/badge/php-%23777BB4.svg?style=for-the-badge&logo=php&logoColor=white) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white) ![Swift](https://img.shields.io/badge/swift-F54A2A?style=for-the-badge&logo=swift&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Dart](https://img.shields.io/badge/dart-%230175C2.svg?style=for-the-badge&logo=dart&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![Flutter](https://img.shields.io/badge/Flutter-%2302569B.svg?style=for-the-badge&logo=Flutter&logoColor=white) ![Render](https://img.shields.io/badge/Render-%46E3B7.svg?style=for-the-badge&logo=render&logoColor=white) ![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=for-the-badge&logo=Cloudflare&logoColor=white) ![Firebase](https://img.shields.io/badge/firebase-%23039BE5.svg?style=for-the-badge&logo=firebase) ![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB) ![Firebase](https://img.shields.io/badge/firebase-a08021?style=for-the-badge&logo=firebase&logoColor=ffcd34) ![CrateDB](https://img.shields.io/badge/CrateDB-009DC7?style=for-the-badge&logo=CrateDB&logoColor=white) ![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white) ![React Native](https://img.shields.io/badge/react_native-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB) ![Blender](https://img.shields.io/badge/blender-%23F5792A.svg?style=for-the-badge&logo=blender&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Swagger](https://img.shields.io/badge/-Swagger-%23Clojure?style=for-the-badge&logo=swagger&logoColor=white) ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=for-the-badge&logo=javascript&logoColor=%23F7DF1E) ![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white) ![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi)
# 📊 GitHub Stats:
![](https://github-readme-stats.shion.dev/api?username=Talebxg7&theme=dark&hide_border=false&include_all_commits=false&count_private=false)<br/>
![](https://streak-stats.demolab.com/?user=Talebxg7&theme=dark&hide_border=false)<br/>
![](https://github-readme-stats.shion.dev/api/top-langs/?username=Talebxg7&theme=dark&hide_border=false&include_all_commits=false&count_private=false&layout=compact)

## 🏆 GitHub Trophies
![](https://github-profile-trophy.vercel.app/?username=Talebxg7&theme=radical&no-frame=false&no-bg=false&margin-w=4)

### 🔝 Top Contributed Repo
![](https://github-contributor-stats.vercel.app/api?username=Talebxg7&limit=5&theme=dark&combine_all_yearly_contributions=true)

---
[![](https://komarev.com/ghpvc/?username=Talebxg7&icon=0&color=0)](https://visitcount.itsvg.in)

<!-- Proudly created with GPRM ( https://gprm.itsvg.in ) -->

<!---
Talebxg7/Talebxg7 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
