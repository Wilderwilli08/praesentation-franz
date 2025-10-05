<!doctype html>
<html lang="de">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Kritischer Systemhinweis</title>
  <style>
    :root{--bg:#0b1020;--accent:#ff5555;--panel:#0f1724;--text:#e6eef8}
    html,body{height:100%;margin:0;font-family:Inter,Segoe UI,Roboto,Arial}
    body{background:linear-gradient(180deg,#071129 0%, #0b0f1a 100%);color:var(--text);display:flex;align-items:center;justify-content:center;overflow:hidden}
    .card{width:92%;max-width:820px;background:radial-gradient(circle at 10% 10%, rgba(255,255,255,0.02), transparent), var(--panel);border-radius:12px;padding:26px;box-shadow:0 8px 40px rgba(2,6,23,0.7);position:relative;overflow:hidden;z-index:5}
    h1{margin:0 0 6px 0;font-size:20px}
    p.lead{margin:0 0 16px 0;color:#bcd0ea}
    .terminal{background:#000;border-radius:8px;padding:14px;font-family:monospace;font-size:13px;line-height:1.5;color:#7efc82;min-height:140px;box-shadow:inset 0 0 40px rgba(0,255,128,0.02)}
    .btns{margin-top:14px;display:flex;gap:10px}
    button{padding:10px 14px;border-radius:8px;border:none;background:#172134;color:var(--text);cursor:pointer}
    button.secondary{background:transparent;border:1px solid rgba(255,255,255,0.06)}
    .overlay{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;background:linear-gradient(180deg, rgba(3,7,18,0.66), rgba(3,7,18,0.66));backdrop-filter:blur(2px);z-index:10}
    .big-warning{font-size:34px;color:var(--accent);font-weight:700;letter-spacing:0.5px}
    .reveal{display:none;padding:20px;text-align:center;z-index:20}
    .confetti{position:absolute;inset:0;pointer-events:none;z-index:15}
    #blackout {position: fixed;inset: 0;background: black;z-index: 9999;display: none;color:white;font-size:22px;display:flex;align-items:center;justify-content:center;font-family:monospace;}
    #matrixCanvas {position: fixed;inset: 0;z-index: 50;background:black;display:none;}
    #thankyou {position: fixed;inset: 0;display:none;align-items:center;justify-content:center;background:black;color:red;font-size:80px;font-weight:bold;z-index:2000;}
  </style>
</head>
<body>
  <div id="blackout">System wird heruntergefahren…</div>
  <canvas id="matrixCanvas"></canvas>
  <div id="thankyou">THANK YOU</div>
  <div class="card" id="card">
    <h1>Kritischer Systemhinweis</h1>
    <p class="lead">Ungewöhnliche Aktivität erkannt. Eine Prüfung läuft...</p>
    <div class="terminal" id="term" aria-live="polite"></div>
    <div class="btns">
      <button id="revealBtn">Schnell prüfen</button>
      <button class="secondary" id="closeBtn">Schließen</button>
    </div>
    <div class="overlay" id="overlay" style="display:flex;flex-direction:column;gap:12px;">
      <div class="big-warning">‼️ WARNUNG ‼️</div>
      <div style="color:#d0d7ee;max-width:700px;text-align:center">
        Systemintegrität möglicherweise gefährdet. Weitere Schritte werden automatisch ausgeführt. ‼️Bitte nichts Drücken‼️
      </div>
    </div>
    <div class="reveal" id="reveal">
      <h2> System rebooting </h2>
      <p>⚠️System wurde gehackt, keine Daten entwendet.⚠️</p>
      <button id="okBtn">Ruben ist ein Sigam skibidi wap wap</button>
    </div>
    <canvas class="confetti" id="confetti"></canvas>
  </div>
<script>
  const term = document.getElementById('term');
  const overlay = document.getElementById('overlay');
  const reveal = document.getElementById('reveal');
  const revealBtn = document.getElementById('revealBtn');
  const closeBtn = document.getElementById('closeBtn');
  const okBtn = document.getElementById('okBtn');
  const blackout = document.getElementById('blackout');
  const matrixCanvas = document.getElementById('matrixCanvas');
  const thankyou = document.getElementById('thankyou');
  const lines = [
    "Verbindung prüfen...",
    "Authentifizierung: OK",
    "Protokolle analysieren...",
    "Ungewöhnliche Anfrage: gefunden",
    "Sicherheitslevel: EVALUATION",
    "Maßnahmen: Automatische Prüfung läuft...",
    "Prüfung abgeschlossen."
  ];
  let i = 0;
  function writeLine() {
    if(i < lines.length) {
      term.textContent += "> " + lines[i] + "\n";
      i++;
      setTimeout(writeLine, 900 + Math.random()*700);
    } else {
      setTimeout(triggerBlackout, 700);
    }
  }
  setTimeout(writeLine, 900);
  function triggerBlackout() {
    blackout.style.display = 'flex';
    setTimeout(() => {
      blackout.style.display = 'none';
      startMatrix();
    }, 2000);
  }
  function startMatrix() {
    matrixCanvas.style.display = "block";
    const ctx = matrixCanvas.getContext("2d");
    matrixCanvas.width = window.innerWidth;
    matrixCanvas.height = window.innerHeight;
    const letters = "01";
    const fontSize = 14;
    const columns = matrixCanvas.width/fontSize;
    const drops = Array(Math.floor(columns)).fill(1);
    function draw() {
      ctx.fillStyle = "rgba(0,0,0,0.05)";
      ctx.fillRect(0,0,matrixCanvas.width,matrixCanvas.height);
      ctx.fillStyle = "#0F0";
      ctx.font = fontSize + "px monospace";
      for(let i=0;i<drops.length;i++){
        const text = letters[Math.floor(Math.random()*letters.length)];
        ctx.fillText(text,i*fontSize,drops[i]*fontSize);
        if(drops[i]*fontSize > matrixCanvas.height && Math.random() > 0.975) drops[i]=0;
        drops[i]++;
      }
    }
    let interval = setInterval(draw,33);
    setTimeout(()=>{
      clearInterval(interval);
      matrixCanvas.style.display="none";
      showRevealOverlay();
    },10000);
  }
  function showRevealOverlay(){
    overlay.style.display = 'flex';
    setTimeout(()=>overlay.style.display='none', 5000);
    setTimeout(()=>{ reveal.style.display='block'; startConfetti(); endWithThankYou(); }, 2400);
  }
  revealBtn.onclick = triggerBlackout;
  closeBtn.onclick = ()=>{ window.close?.() || alert("Fenster schließen nicht erlaubt im Browser. Einfach Tab schließen."); };
  okBtn.onclick = ()=>{ reveal.style.display='none'; stopConfetti(); term.textContent += "\n[Hinweis] Dies war ein harmloser Streich.\n"; };
  const canvas = document.getElementById('confetti');
  const ctx = canvas.getContext('2d');
  let confettiItems = [], anim;
  function resize() { canvas.width = canvas.clientWidth; canvas.height = canvas.clientHeight; }
  window.addEventListener('resize', resize);
  resize();
  function startConfetti(){
    confettiItems = Array.from({length:40}).map(_=>({
      x: Math.random()*canvas.width,
      y: Math.random()*canvas.height - canvas.height/2,
      r: (Math.random()*6)+4,
      dx: (Math.random()-0.5)*2,
      dy: Math.random()*3+1,
      c: ['#f44336','#ffeb3b','#4caf50','#2196f3','#ff9800','#9c27b0'][Math.floor(Math.random()*6)]
    }));
    draw();
  }
  function stopConfetti(){ confettiItems = []; cancelAnimationFrame(anim); ctx.clearRect(0,0,canvas.width,canvas.height); }
  function draw(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    confettiItems.forEach(p=>{
      ctx.fillStyle = p.c;
      ctx.beginPath();
      ctx.ellipse(p.x,p.y,p.r,p.r*0.6,0,0,Math.PI*2);
      ctx.fill();
      p.x += p.dx; p.y += p.dy; p.dy += 0.02;
      if(p.y > canvas.height + 10) p.y = -20;
      if(p.x < -20) p.x = canvas.width + 20;
      if(p.x > canvas.width + 20) p.x = -20;
    });
    anim = requestAnimationFrame(draw);
  }
  function endWithThankYou(){
    setTimeout(()=>{
      reveal.style.display="none";
      stopConfetti();
      thankyou.style.display="flex";
    },15000);
  }
</script>
</body>
</html>
