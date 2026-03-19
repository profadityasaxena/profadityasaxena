<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Aditya Saxena — AI Systems Portfolio</title>
  <style>
    :root {
      --bg: #07111f;
      --bg-2: #0b1728;
      --panel: rgba(255,255,255,0.06);
      --panel-2: rgba(255,255,255,0.08);
      --line: rgba(255,255,255,0.12);
      --text: #e9f0fb;
      --muted: #9fb0c8;
      --accent: #57a6ff;
      --accent-2: #8cc4ff;
      --glow: rgba(87,166,255,0.35);
      --shadow: 0 20px 60px rgba(0,0,0,0.35);
      --radius: 24px;
      --max: 1220px;
    }

    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body {
      margin: 0;
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      color: var(--text);
      background:
        radial-gradient(circle at 10% 20%, rgba(87,166,255,0.12), transparent 0 28%),
        radial-gradient(circle at 90% 10%, rgba(140,196,255,0.10), transparent 0 24%),
        linear-gradient(180deg, #08111f 0%, #091423 40%, #08111f 100%);
      overflow-x: hidden;
    }

    .noise,
    .grid,
    .aurora,
    .orbits {
      position: fixed;
      inset: 0;
      pointer-events: none;
      z-index: 0;
    }

    .grid {
      background-image:
        linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
      background-size: 48px 48px;
      mask-image: linear-gradient(180deg, rgba(0,0,0,0.75), transparent 92%);
    }

    .noise {
      opacity: 0.05;
      background-image:
        radial-gradient(circle at 25% 25%, white 0.7px, transparent 0.8px),
        radial-gradient(circle at 75% 75%, white 0.7px, transparent 0.8px);
      background-size: 12px 12px, 16px 16px;
      mix-blend-mode: soft-light;
    }

    .aurora::before,
    .aurora::after {
      content: "";
      position: absolute;
      width: 42vw;
      height: 42vw;
      border-radius: 50%;
      filter: blur(80px);
      opacity: 0.24;
      animation: floatBlob 16s ease-in-out infinite;
    }

    .aurora::before {
      background: radial-gradient(circle, rgba(87,166,255,0.9), transparent 60%);
      top: -8vw;
      left: -8vw;
    }

    .aurora::after {
      background: radial-gradient(circle, rgba(92,128,255,0.75), transparent 58%);
      right: -10vw;
      top: 8vh;
      animation-delay: -6s;
    }

    .orbits::before,
    .orbits::after {
      content: "";
      position: absolute;
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: 999px;
      inset: auto;
    }

    .orbits::before {
      width: 900px;
      height: 900px;
      left: 60%;
      top: -280px;
      transform: translateX(-50%);
      animation: spinSlow 38s linear infinite;
    }

    .orbits::after {
      width: 620px;
      height: 620px;
      left: 16%;
      top: 220px;
      transform: translateX(-50%);
      animation: spinSlowReverse 30s linear infinite;
    }

    a { color: inherit; text-decoration: none; }

    .container {
      width: min(calc(100% - 40px), var(--max));
      margin: 0 auto;
      position: relative;
      z-index: 2;
    }

    .nav {
      position: sticky;
      top: 14px;
      z-index: 20;
      padding-top: 18px;
    }

    .nav-inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 14px 18px;
      border: 1px solid var(--line);
      border-radius: 999px;
      background: rgba(7,17,31,0.6);
      backdrop-filter: blur(20px);
      box-shadow: var(--shadow);
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
      font-weight: 700;
      letter-spacing: 0.02em;
    }

    .brand-mark {
      width: 34px;
      height: 34px;
      border-radius: 12px;
      background: linear-gradient(135deg, var(--accent), #c7e2ff);
      box-shadow: 0 12px 28px rgba(87,166,255,0.45);
      position: relative;
      overflow: hidden;
    }

    .brand-mark::before {
      content: "";
      position: absolute;
      inset: 1px;
      border-radius: 11px;
      background: linear-gradient(180deg, rgba(255,255,255,0.35), rgba(255,255,255,0.08));
    }

    .nav-links {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
    }

    .nav-links a {
      color: var(--muted);
      padding: 10px 14px;
      border-radius: 999px;
      transition: 180ms ease;
      font-size: 14px;
    }

    .nav-links a:hover {
      color: var(--text);
      background: rgba(255,255,255,0.06);
    }

    .hero {
      min-height: 94vh;
      display: grid;
      grid-template-columns: 1.15fr 0.85fr;
      gap: 28px;
      align-items: center;
      padding: 42px 0 34px;
    }

    .eyebrow {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      padding: 8px 12px;
      border-radius: 999px;
      border: 1px solid rgba(255,255,255,0.1);
      background: rgba(255,255,255,0.04);
      color: var(--accent-2);
      font-size: 13px;
      letter-spacing: 0.08em;
      text-transform: uppercase;
    }

    .eyebrow::before {
      content: "";
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: var(--accent);
      box-shadow: 0 0 16px var(--glow);
      animation: pulse 2s infinite;
    }

    h1 {
      font-size: clamp(48px, 7.2vw, 88px);
      line-height: 0.94;
      letter-spacing: -0.045em;
      margin: 18px 0 18px;
      max-width: 11ch;
    }

    .hero-copy {
      font-size: clamp(18px, 2vw, 22px);
      line-height: 1.7;
      color: var(--muted);
      max-width: 62ch;
      margin: 0 0 30px;
    }

    .hero-actions {
      display: flex;
      gap: 14px;
      flex-wrap: wrap;
      margin-bottom: 24px;
    }

    .button {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      padding: 14px 18px;
      border-radius: 16px;
      border: 1px solid transparent;
      transition: transform 180ms ease, box-shadow 180ms ease, background 180ms ease;
      font-weight: 600;
    }

    .button.primary {
      background: linear-gradient(135deg, var(--accent), #86c2ff);
      color: #07111f;
      box-shadow: 0 18px 36px rgba(87,166,255,0.28);
    }

    .button.secondary {
      background: rgba(255,255,255,0.04);
      border-color: rgba(255,255,255,0.1);
      color: var(--text);
      backdrop-filter: blur(12px);
    }

    .button:hover {
      transform: translateY(-2px);
    }

    .hero-meta {
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
    }

    .pill {
      padding: 10px 12px;
      border-radius: 999px;
      background: rgba(255,255,255,0.04);
      border: 1px solid rgba(255,255,255,0.08);
      color: var(--muted);
      font-size: 14px;
    }

    .hero-visual {
      position: relative;
      min-height: 620px;
      display: grid;
      place-items: center;
    }

    .system-shell {
      width: min(100%, 560px);
      aspect-ratio: 1 / 1.08;
      border-radius: 30px;
      border: 1px solid rgba(255,255,255,0.1);
      background: linear-gradient(180deg, rgba(255,255,255,0.08), rgba(255,255,255,0.03));
      box-shadow: var(--shadow);
      backdrop-filter: blur(20px);
      position: relative;
      overflow: hidden;
    }

    .system-shell::before {
      content: "";
      position: absolute;
      inset: 0;
      background: linear-gradient(120deg, transparent 20%, rgba(255,255,255,0.09) 40%, transparent 62%);
      transform: translateX(-120%);
      animation: sheen 7s linear infinite;
    }

    .system-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 18px 20px;
      border-bottom: 1px solid rgba(255,255,255,0.08);
    }

    .dots { display: flex; gap: 8px; }
    .dots span {
      width: 10px; height: 10px; border-radius: 50%;
      background: rgba(255,255,255,0.22);
    }

    .system-grid {
      display: grid;
      grid-template-columns: 1.05fr 0.95fr;
      gap: 14px;
      padding: 18px;
      height: calc(100% - 64px);
    }

    .panel {
      border-radius: 22px;
      background: var(--panel);
      border: 1px solid rgba(255,255,255,0.08);
      position: relative;
      overflow: hidden;
    }

    .panel.pad { padding: 18px; }

    .panel-title {
      font-size: 13px;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      color: var(--accent-2);
      margin-bottom: 12px;
    }

    .diagram {
      height: 100%;
      display: grid;
      gap: 12px;
      grid-template-rows: 1fr 1fr 1fr 1fr;
    }

    .node {
      position: relative;
      border-radius: 18px;
      padding: 16px;
      background: linear-gradient(180deg, rgba(255,255,255,0.08), rgba(255,255,255,0.04));
      border: 1px solid rgba(255,255,255,0.08);
      transform: translateY(18px);
      opacity: 0;
      animation: riseIn 700ms forwards;
    }

    .node:nth-child(2) { animation-delay: 120ms; }
    .node:nth-child(3) { animation-delay: 240ms; }
    .node:nth-child(4) { animation-delay: 360ms; }

    .node strong {
      display: block;
      font-size: 14px;
      margin-bottom: 6px;
    }

    .node span {
      display: block;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.5;
    }

    .node::after {
      content: "";
      position: absolute;
      left: 28px;
      bottom: -12px;
      width: 2px;
      height: 14px;
      background: linear-gradient(180deg, rgba(87,166,255,0.5), transparent);
    }

    .node:last-child::after { display: none; }

    .insight-top {
      height: 52%;
      padding: 18px;
      border-bottom: 1px solid rgba(255,255,255,0.08);
      position: relative;
    }

    .chart {
      position: absolute;
      left: 18px;
      right: 18px;
      bottom: 18px;
      top: 62px;
      border-radius: 18px;
      background:
        linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.01)),
        radial-gradient(circle at 30% 30%, rgba(87,166,255,0.13), transparent 60%);
      overflow: hidden;
    }

    .chart svg {
      width: 100%;
      height: 100%;
    }

    .insight-bottom {
      height: 48%;
      padding: 18px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
    }

    .metric {
      border-radius: 18px;
      background: rgba(255,255,255,0.04);
      border: 1px solid rgba(255,255,255,0.07);
      padding: 16px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }

    .metric label {
      color: var(--muted);
      font-size: 12px;
      text-transform: uppercase;
      letter-spacing: 0.08em;
    }

    .metric strong {
      font-size: 30px;
      letter-spacing: -0.04em;
      margin-top: 10px;
    }

    .metric small {
      color: var(--accent-2);
      font-size: 12px;
      margin-top: 6px;
    }

    section {
      padding: 42px 0 10px;
    }

    .section-head {
      display: flex;
      justify-content: space-between;
      align-items: end;
      gap: 18px;
      margin-bottom: 24px;
    }

    h2 {
      font-size: clamp(28px, 4vw, 52px);
      line-height: 1;
      letter-spacing: -0.045em;
      margin: 0;
    }

    .section-head p {
      max-width: 640px;
      margin: 0;
      color: var(--muted);
      line-height: 1.7;
    }

    .projects {
      display: grid;
      grid-template-columns: repeat(12, 1fr);
      gap: 18px;
    }

    .card {
      grid-column: span 6;
      min-height: 320px;
      border-radius: 28px;
      padding: 24px;
      position: relative;
      overflow: hidden;
      border: 1px solid rgba(255,255,255,0.1);
      background: linear-gradient(180deg, rgba(255,255,255,0.07), rgba(255,255,255,0.035));
      box-shadow: var(--shadow);
      backdrop-filter: blur(14px);
      transform-style: preserve-3d;
      transition: transform 220ms ease, border-color 220ms ease, background 220ms ease;
    }

    .card:hover {
      border-color: rgba(140,196,255,0.36);
      background: linear-gradient(180deg, rgba(255,255,255,0.09), rgba(255,255,255,0.04));
    }

    .card.large { grid-column: span 8; }
    .card.tall { min-height: 360px; }
    .card.small { grid-column: span 4; }

    .card::before {
      content: "";
      position: absolute;
      inset: auto -20% -30% auto;
      width: 240px;
      height: 240px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(87,166,255,0.18), transparent 65%);
      filter: blur(10px);
      transition: transform 260ms ease;
    }

    .card:hover::before {
      transform: scale(1.08);
    }

    .kicker {
      color: var(--accent-2);
      font-size: 12px;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      margin-bottom: 14px;
    }

    .card h3 {
      font-size: 30px;
      line-height: 1;
      letter-spacing: -0.04em;
      margin: 0 0 12px;
      max-width: 16ch;
    }

    .card p {
      color: var(--muted);
      line-height: 1.7;
      margin: 0 0 18px;
      max-width: 56ch;
    }

    .tags {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      margin-top: auto;
    }

    .tags span {
      font-size: 12px;
      padding: 9px 11px;
      border-radius: 999px;
      background: rgba(255,255,255,0.06);
      border: 1px solid rgba(255,255,255,0.08);
      color: #d7e6ff;
    }

    .impact {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      margin: 18px 0 2px;
    }

    .impact strong {
      font-size: 13px;
      font-weight: 600;
      padding: 10px 12px;
      border-radius: 14px;
      background: rgba(87,166,255,0.12);
      border: 1px solid rgba(87,166,255,0.16);
      color: #dff0ff;
    }

    .stack-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 18px;
    }

    .stack-box {
      padding: 22px;
      border-radius: 24px;
      border: 1px solid rgba(255,255,255,0.09);
      background: linear-gradient(180deg, rgba(255,255,255,0.06), rgba(255,255,255,0.03));
      min-height: 240px;
      box-shadow: var(--shadow);
    }

    .stack-box h4 {
      margin: 0 0 14px;
      font-size: 18px;
      letter-spacing: -0.03em;
    }

    .stack-box ul {
      list-style: none;
      padding: 0;
      margin: 0;
      display: grid;
      gap: 10px;
    }

    .stack-box li {
      color: var(--muted);
      line-height: 1.5;
      padding-left: 14px;
      position: relative;
    }

    .stack-box li::before {
      content: "";
      position: absolute;
      width: 6px;
      height: 6px;
      border-radius: 50%;
      left: 0;
      top: 10px;
      background: var(--accent);
      box-shadow: 0 0 12px var(--glow);
    }

    .links-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 18px;
    }

    .link-card {
      padding: 22px;
      min-height: 180px;
      border-radius: 24px;
      border: 1px solid rgba(255,255,255,0.09);
      background: linear-gradient(180deg, rgba(255,255,255,0.06), rgba(255,255,255,0.03));
      box-shadow: var(--shadow);
      transition: transform 180ms ease, border-color 180ms ease;
    }

    .link-card:hover {
      transform: translateY(-3px);
      border-color: rgba(140,196,255,0.34);
    }

    .link-card h4 {
      margin: 0 0 10px;
      font-size: 22px;
      letter-spacing: -0.04em;
    }

    .link-card p {
      margin: 0 0 18px;
      color: var(--muted);
      line-height: 1.7;
    }

    .link-card a {
      color: var(--accent-2);
      font-weight: 600;
    }

    footer {
      padding: 44px 0 80px;
      color: var(--muted);
    }

    .footer-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 18px;
      padding: 18px 0;
      border-top: 1px solid rgba(255,255,255,0.1);
    }

    .reveal {
      opacity: 0;
      transform: translateY(30px);
      transition: opacity 700ms ease, transform 700ms ease;
    }

    .reveal.in {
      opacity: 1;
      transform: translateY(0);
    }

    @keyframes floatBlob {
      0%, 100% { transform: translate3d(0,0,0) scale(1); }
      50% { transform: translate3d(24px,18px,0) scale(1.06); }
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); opacity: 1; }
      50% { transform: scale(1.2); opacity: 0.78; }
    }

    @keyframes spinSlow {
      from { transform: translateX(-50%) rotate(0deg); }
      to { transform: translateX(-50%) rotate(360deg); }
    }

    @keyframes spinSlowReverse {
      from { transform: translateX(-50%) rotate(360deg); }
      to { transform: translateX(-50%) rotate(0deg); }
    }

    @keyframes sheen {
      0% { transform: translateX(-120%); }
      100% { transform: translateX(140%); }
    }

    @keyframes riseIn {
      to { transform: translateY(0); opacity: 1; }
    }

    @media (max-width: 1100px) {
      .hero { grid-template-columns: 1fr; padding-top: 26px; }
      .hero-visual { order: -1; min-height: 520px; }
      .projects .card,
      .projects .card.large,
      .projects .card.small { grid-column: span 12; }
      .stack-grid { grid-template-columns: repeat(2, 1fr); }
      .links-grid { grid-template-columns: 1fr; }
    }

    @media (max-width: 720px) {
      .container { width: min(calc(100% - 24px), var(--max)); }
      .nav-inner { border-radius: 24px; align-items: start; flex-direction: column; gap: 12px; }
      .nav-links { width: 100%; }
      .hero { min-height: auto; }
      .system-grid { grid-template-columns: 1fr; }
      .system-shell { aspect-ratio: auto; min-height: 640px; }
      .insight-top { min-height: 220px; }
      .insight-bottom { grid-template-columns: 1fr; }
      .stack-grid { grid-template-columns: 1fr; }
      .section-head { flex-direction: column; align-items: start; }
      h1 { max-width: 10ch; }
    }
  </style>
</head>
<body>
  <div class="aurora"></div>
  <div class="grid"></div>
  <div class="orbits"></div>
  <div class="noise"></div>

  <div class="container nav">
    <div class="nav-inner">
      <div class="brand">
        <div class="brand-mark"></div>
        <span>Aditya Saxena</span>
      </div>
      <div class="nav-links">
        <a href="#projects">Projects</a>
        <a href="#stack">Stack</a>
        <a href="#work">Selected Work</a>
        <a href="https://www.linkedin.com/in/itsadisxnn" target="_blank" rel="noreferrer">LinkedIn</a>
        <a href="https://www.adityasaxena.xyz" target="_blank" rel="noreferrer">Portfolio</a>
      </div>
    </div>
  </div>

  <main class="container">
    <section class="hero">
      <div class="hero-text reveal in">
        <div class="eyebrow">Systems Portfolio</div>
        <h1>I build AI systems that survive contact with reality.</h1>
        <p class="hero-copy">
          Most demos look good in isolation. Real systems have messy data, imperfect environments, latency, drift, hard constraints, and people in the loop. That is the part I care about. So this portfolio is built around projects, not buzzwords.
        </p>
        <div class="hero-actions">
          <a class="button primary" href="#projects">View Systems</a>
          <a class="button secondary" href="https://github.com/profadityasaxena" target="_blank" rel="noreferrer">Open GitHub</a>
        </div>
        <div class="hero-meta">
          <span class="pill">AI Systems</span>
          <span class="pill">Machine Learning</span>
          <span class="pill">Data Platforms</span>
          <span class="pill">Full-Stack Engineering</span>
        </div>
      </div>

      <div class="hero-visual reveal in">
        <div class="system-shell" id="tilt-card">
          <div class="system-header">
            <div class="dots"><span></span><span></span><span></span></div>
            <div style="color: var(--muted); font-size: 13px;">Live systems, not slides</div>
          </div>
          <div class="system-grid">
            <div class="panel pad">
              <div class="panel-title">System Flow</div>
              <div class="diagram">
                <div class="node"><strong>Data Ingestion</strong><span>Telemetry, documents, events, APIs, distributed signals.</span></div>
                <div class="node"><strong>Feature & Context Layer</strong><span>Transformations, embeddings, graphs, rolling windows, semantics.</span></div>
                <div class="node"><strong>Decision Engine</strong><span>RL, retrieval, forecasting, optimization, policy evaluation.</span></div>
                <div class="node"><strong>Deployment & Monitoring</strong><span>APIs, orchestration, rollback, observability, continuous improvement.</span></div>
              </div>
            </div>
            <div class="panel" style="display:grid; grid-template-rows: 1fr 0.9fr;">
              <div class="insight-top">
                <div class="panel-title">Performance</div>
                <div class="chart">
                  <svg viewBox="0 0 100 60" preserveAspectRatio="none" aria-hidden="true">
                    <defs>
                      <linearGradient id="lineGlow" x1="0" y1="0" x2="1" y2="0">
                        <stop offset="0%" stop-color="#5aa8ff" stop-opacity="0.3"/>
                        <stop offset="50%" stop-color="#91c8ff" stop-opacity="1"/>
                        <stop offset="100%" stop-color="#5aa8ff" stop-opacity="0.3"/>
                      </linearGradient>
                    </defs>
                    <g opacity="0.2">
                      <path d="M0 10 H100 M0 20 H100 M0 30 H100 M0 40 H100 M0 50 H100" stroke="white" stroke-width="0.4"/>
                      <path d="M10 0 V60 M30 0 V60 M50 0 V60 M70 0 V60 M90 0 V60" stroke="white" stroke-width="0.4"/>
                    </g>
                    <path d="M0,45 C10,44 13,41 20,36 C27,31 31,33 38,28 C45,23 50,26 57,21 C63,17 69,19 76,13 C84,6 90,10 100,4" fill="none" stroke="url(#lineGlow)" stroke-width="2.2" stroke-linecap="round">
                      <animate attributeName="stroke-dasharray" values="0,200;200,0" dur="3.2s" repeatCount="indefinite"/>
                    </path>
                    <path d="M0,60 L0,45 C10,44 13,41 20,36 C27,31 31,33 38,28 C45,23 50,26 57,21 C63,17 69,19 76,13 C84,6 90,10 100,4 L100,60 Z" fill="rgba(87,166,255,0.15)"/>
                  </svg>
                </div>
              </div>
              <div class="insight-bottom">
                <div class="metric">
                  <label>Optimization uplift</label>
                  <strong>2–4%</strong>
                  <small>Sustained performance gain</small>
                </div>
                <div class="metric">
                  <label>Resolution speed</label>
                  <strong>60–70%</strong>
                  <small>Faster knowledge retrieval</small>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="projects">
      <div class="section-head reveal">
        <div>
          <div class="eyebrow">Selected Systems</div>
          <h2>Projects worth looking at.</h2>
        </div>
        <p>
          The point is not to list technologies. The point is to show what got built, how the system was structured, and why it mattered.
        </p>
      </div>

      <div class="projects">
        <article class="card large tall reveal" data-tilt>
          <div class="kicker">Machine Learning System</div>
          <h3>AI Optimization Platform</h3>
          <p>
            A reinforcement learning system running on high-frequency telemetry in live environments. It takes in 200+ signals, builds rolling features, learns policies under constraints, and supports decisions without bypassing human control.
          </p>
          <div class="impact">
            <strong>2–4% performance gain</strong>
            <strong>4–5% efficiency gain</strong>
            <strong>~15% productivity increase</strong>
          </div>
          <div class="tags">
            <span>Reinforcement Learning</span>
            <span>Feature Engineering</span>
            <span>Telemetry</span>
            <span>MLOps</span>
          </div>
        </article>

        <article class="card small tall reveal" data-tilt>
          <div class="kicker">AI Platform</div>
          <h3>Industry Mind</h3>
          <p>
            A modular intelligence platform that brings together streaming data, system context, knowledge graphs, and model outputs into one operational layer.
          </p>
          <div class="tags">
            <span>Data Platform</span>
            <span>Knowledge Graphs</span>
            <span>Decision Systems</span>
          </div>
        </article>

        <article class="card small reveal" data-tilt>
          <div class="kicker">Generative AI</div>
          <h3>RAG + Knowledge Graph System</h3>
          <p>
            Instead of guessing, this system retrieves the right context first, then reasons across relationships, then generates grounded answers.
          </p>
          <div class="impact">
            <strong>60–70% faster resolution</strong>
          </div>
          <div class="tags">
            <span>RAG</span>
            <span>FAISS</span>
            <span>Graph Reasoning</span>
          </div>
        </article>

        <article class="card small reveal" data-tilt>
          <div class="kicker">ML Operations</div>
          <h3>MLOps Lifecycle Platform</h3>
          <p>
            Versioned models, controlled rollout, parallel testing, rollback, drift detection, and retraining. Less hype, more engineering discipline.
          </p>
          <div class="tags">
            <span>MLflow</span>
            <span>Deployment</span>
            <span>Monitoring</span>
          </div>
        </article>

        <article class="card small reveal" data-tilt>
          <div class="kicker">Data Engineering</div>
          <h3>Real-Time Data Platform</h3>
          <p>
            High-throughput streaming and batch pipelines designed for low latency, reliability, observability, and downstream intelligence.
          </p>
          <div class="tags">
            <span>Spark</span>
            <span>Kafka</span>
            <span>Flink</span>
          </div>
        </article>

        <article class="card reveal" data-tilt>
          <div class="kicker">Cloud Systems</div>
          <h3>Cloud-Native AI Delivery</h3>
          <p>
            Containerized services, orchestrated deployments, CI/CD, backend APIs, frontend integration, and production-ready delivery across cloud environments.
          </p>
          <div class="tags">
            <span>Docker</span>
            <span>Kubernetes</span>
            <span>FastAPI</span>
            <span>Next.js</span>
          </div>
        </article>
      </div>
    </section>

    <section id="stack">
      <div class="section-head reveal">
        <div>
          <div class="eyebrow">Technical Stack</div>
          <h2>The tools matter less than the system, but here they are.</h2>
        </div>
        <p>
          I use whatever makes the system simpler, more reliable, and easier to scale. No attachment to complexity for its own sake.
        </p>
      </div>

      <div class="stack-grid">
        <div class="stack-box reveal">
          <h4>Machine Learning</h4>
          <ul>
            <li>PyTorch</li>
            <li>TensorFlow</li>
            <li>scikit-learn</li>
            <li>Hugging Face</li>
            <li>OpenAI</li>
            <li>LangChain</li>
          </ul>
        </div>
        <div class="stack-box reveal">
          <h4>Data & Streaming</h4>
          <ul>
            <li>Apache Spark</li>
            <li>Databricks</li>
            <li>Kafka</li>
            <li>Flink</li>
            <li>Airflow</li>
          </ul>
        </div>
        <div class="stack-box reveal">
          <h4>Backend & Platform</h4>
          <ul>
            <li>Python</li>
            <li>FastAPI</li>
            <li>Node.js</li>
            <li>REST APIs</li>
            <li>Microservices</li>
            <li>Neo4j / Knowledge Systems</li>
          </ul>
        </div>
        <div class="stack-box reveal">
          <h4>Cloud & Delivery</h4>
          <ul>
            <li>AWS</li>
            <li>Azure</li>
            <li>Docker</li>
            <li>Kubernetes</li>
            <li>Terraform</li>
            <li>CI/CD</li>
          </ul>
        </div>
      </div>
    </section>

    <section id="work">
      <div class="section-head reveal">
        <div>
          <div class="eyebrow">Selected Work</div>
          <h2>A few places to start.</h2>
        </div>
        <p>
          The repositories below are a mix of production-inspired systems, research implementations, and structured technical work.
        </p>
      </div>

      <div class="links-grid">
        <article class="link-card reveal">
          <h4>KubeChat</h4>
          <p>Question-answering system built with Kubernetes, containers, LLMs, and vector search.</p>
          <a href="https://github.com/profadityasaxena/KubeChat" target="_blank" rel="noreferrer">Open repository</a>
        </article>
        <article class="link-card reveal">
          <h4>INSIGHT-XAI</h4>
          <p>Explainable AI work exploring latent representations, interpretability, and structured evaluation.</p>
          <a href="https://github.com/profadityasaxena/Labels-to-Latents" target="_blank" rel="noreferrer">Open repository</a>
        </article>
        <article class="link-card reveal">
          <h4>Cloud Modernization</h4>
          <p>Frameworks and architecture work focused on modernizing legacy systems into scalable platforms.</p>
          <a href="https://github.com/profadityasaxena/Cloud-Legacy-to-Modern" target="_blank" rel="noreferrer">Open repository</a>
        </article>
      </div>
    </section>
  </main>

  <footer class="container">
    <div class="footer-bar">
      <div>Aditya Saxena</div>
      <div>
        <a href="https://www.linkedin.com/in/itsadisxnn" target="_blank" rel="noreferrer">LinkedIn</a>
        <span style="padding:0 10px; opacity:0.5;">/</span>
        <a href="https://www.adityasaxena.xyz" target="_blank" rel="noreferrer">Portfolio</a>
      </div>
    </div>
  </footer>

  <script>
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) entry.target.classList.add('in');
      });
    }, { threshold: 0.14 });

    document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

    const tiltCards = document.querySelectorAll('[data-tilt]');
    tiltCards.forEach((card) => {
      card.addEventListener('mousemove', (e) => {
        const rect = card.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;
        const rx = ((y / rect.height) - 0.5) * -8;
        const ry = ((x / rect.width) - 0.5) * 10;
        card.style.transform = `perspective(900px) rotateX(${rx}deg) rotateY(${ry}deg) translateY(-2px)`;
      });
      card.addEventListener('mouseleave', () => {
        card.style.transform = 'perspective(900px) rotateX(0deg) rotateY(0deg) translateY(0px)';
      });
    });

    const heroCard = document.getElementById('tilt-card');
    heroCard.addEventListener('mousemove', (e) => {
      const rect = heroCard.getBoundingClientRect();
      const x = e.clientX - rect.left;
      const y = e.clientY - rect.top;
      const rx = ((y / rect.height) - 0.5) * -5;
      const ry = ((x / rect.width) - 0.5) * 6;
      heroCard.style.transform = `perspective(1200px) rotateX(${rx}deg) rotateY(${ry}deg)`;
    });
    heroCard.addEventListener('mouseleave', () => {
      heroCard.style.transform = 'perspective(1200px) rotateX(0deg) rotateY(0deg)';
    });
  </script>
</body>
</html>
