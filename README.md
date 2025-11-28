# birthday-card
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Happy Birthday Avishka</title>
  <style>
    :root{ 
      --bg:#ffe6f2;
      --pink1:#ff9ecb;
      --pink2:#ff4fa3;
      --accent:#ff4081;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:Arial, Helvetica, sans-serif;
      background:var(--bg);
      text-align:center;
      overflow-x:hidden;
      padding-bottom:80px;
    }

    h1{ margin-top:40px; font-size:2.2rem; color:var(--accent); }

    .balloons{ display:flex; justify-content:center; gap:20px; margin-top:40px; min-height:140px; }

    .balloon{
      width:90px; height:120px;
      background: radial-gradient(circle at 30% 30%, var(--pink1), var(--pink2));
      border-radius:50% 50% 45% 45%;
      position:relative;
      cursor:pointer;
      transition:transform .2s, opacity .25s;
      box-shadow: 0 10px 20px rgba(255,105,180,.35);
      display:inline-block;
    }
    .balloon::after{
      content:""; position:absolute; bottom:-20px; left:50%; transform:translateX(-50%);
      width:2px; height:40px; background:#ff4fa3;
    }
    .balloon.popped{ background:transparent; border:2px dashed #ff80ab; transform:scale(.75); opacity:.6; }

    /* Cake area */
    #cake-section{ margin-top:50px; display:none; opacity:0; transform:translateX(60px); transition: all .8s ease; }
    #cake{
      margin:auto; width:220px; height:160px; border-radius:18px; position:relative;
      box-shadow:0 6px 24px rgba(0,0,0,.18); cursor:pointer; padding-top:8px;
      background:linear-gradient(180deg,#ff9ecb,#ff7aa6);
    }
    /* cake layers */
    .layer{ width:85%; height:28px; border-radius:12px; margin:10px auto; background:white; box-shadow:inset 0 -3px 8px rgba(0,0,0,.03); }
    .layer.alt{ background:#ffe6f2; }

    /* candles */
    #candles{ position:absolute; top:-10px; left:50%; transform:translateX(-50%); display:flex; gap:12px; align-items:flex-end; }
    .candle{ width:8px; height:28px; background:#ffd1dc; border-radius:3px; position:relative; }
    .flame{
      width:12px; height:12px; background:orange; border-radius:50% 50% 40% 40%;
      position:absolute; top:-14px; left:50%; transform:translateX(-50%);
      filter:drop-shadow(0 2px 4px rgba(255,140,0,.5));
      animation:flame-flicker .35s infinite;
      transition:opacity .6s ease;
    }
    @keyframes flame-flicker {
      0%{ transform:translateX(-50%) scale(1); opacity:1; }
      50%{ transform:translateX(-48%) scale(.9); opacity:.85; }
      100%{ transform:translateX(-50%) scale(1); opacity:1; }
    }

    /* air effect */
    .air-effect {
      position: absolute;
      width: 8px;
      height: 8px;
      background: #ffc0cb;
      border-radius: 50%;
      pointer-events: none;
      animation: rise 1s forwards;
    }
    @keyframes rise {
      0% { opacity: 1; transform: translateY(0) scale(1); }
      100% { opacity: 0; transform: translateY(-80px) scale(0.5); }
    }

    /* love-note centered */
    #love-note{
      display:none; opacity:0; transform:translateX(-100px);
      transition: all .7s ease; margin:30px auto; cursor:pointer; width:300px; max-width:90%;
      display:block;
    }
    #love-note img{ width:100%; display:block; border-radius:8px; box-shadow:0 6px 20px rgba(0,0,0,.15); }

    /* final page */
    #final-page{
      display:none; opacity:0; transform:translateX(100px); transition:all .8s ease; margin-top:30px;
    }
    #final-page img{ border-radius:12px; display:block; margin:12px auto; box-shadow:0 10px 30px rgba(0,0,0,.18); }

    #emoji-row {
      margin-top: 12px;
      font-size: 1.3rem;
    }

    /* small helpers */
    .centered{ display:flex; align-items:center; justify-content:center; flex-direction:column; }
    .hint{ font-size:0.95rem; color:#b84b7a; margin-top:8px }

    /* clickable feedback */
    #cake:active{ transform:scale(.98) }
  </style>
</head>
<body>
  <h1 id="title" style="opacity:0; transform:translateX(-100px); transition:1s">Pop All 6 Balloons 🎈</h1>

  <div class="balloons" id="balloon-area"></div>

  <!-- Cake section -->
  <div id="cake-section" style="display:none">
    <h2>🎂 Click the Cake 15 Times 🎂</h2>
    <div id="cake" onclick="cakeClick()">
      <div id="candles">
        <div class="candle"><div class="flame"></div></div>
        <div class="candle"><div class="flame"></div></div>
        <div class="candle"><div class="flame"></div></div>
      </div>
      <div class="layer" style="height:22px;width:75%;"></div>
      <div class="layer alt" style="height:22px;width:80%;"></div>
      <div class="layer" style="height:22px;width:85%;"></div>
    </div>
    <div class="hint">Click the cake until the flames go out!</div>
  </div>

  <!-- mail image -->
  <div id="love-note" class="centered" onclick="openNote()">
    <img src="mail.png" alt="Love Note (click to open)">
  </div>

  <!-- final page -->
  <div id="final-page" class="centered">
    <h1>Happy Birthday Avishka 🎉💖</h1>
    <p>You are amazing, special and truly precious. Enjoy your day! 💕</p>
    
    <!-- Cats and Avishka photo -->
    <div class="photo-row" style="display:flex; align-items:center; justify-content:center; gap:12px;">
      <img src="catt.png" alt="Cat Left" style="width:100px; max-width:20%; border-radius:12px; box-shadow:0 10px 30px rgba(0,0,0,.18);">
      <img id="avishka-photo" src="npc.png" alt="Avishka's Photo" style="width:300px; max-width:40%; border-radius:12px; box-shadow:0 10px 30px rgba(0,0,0,.18);">
      <img src="catt.png" alt="Cat Right" style="width:100px; max-width:20%; border-radius:12px; box-shadow:0 10px 30px rgba(0,0,0,.18);">
    </div>

    <div id="emoji-row">🎉🎂✨🍰🥳🎂🎈🎉🥳🎉🎂🎀💗🥳🥂✨🧁</div>
  </div>

  <script>
    let popped = 0;
    let cakeClicks = 0;
    const TOTAL_BALLOONS = 6;
    const REQUIRED_CAKE_CLICKS = 15;

    function spawnBalloon() {
      const area = document.getElementById('balloon-area');
      area.innerHTML = `<div class='balloon' onclick='popBalloon(this)'></div>`;
    }

    function popBalloon(elem) {
      if (!elem) return;
      elem.classList.add('popped');
      popped++;
      if (popped < TOTAL_BALLOONS) {
        setTimeout(spawnBalloon, 350);
      }
      if (popped === TOTAL_BALLOONS) {
        const cakeSec = document.getElementById('cake-section');
        cakeSec.style.display = 'block';
        setTimeout(()=> { cakeSec.style.opacity = 1; cakeSec.style.transform = 'translateX(0)'; }, 60);
        setTimeout(()=> document.getElementById('balloon-area').style.display = 'none', 400);
      }
    }

    function cakeClick() {
      cakeClicks++;
      const cake = document.getElementById('cake');

      // shake
      cake.style.transform = 'translateY(-3px)';
      setTimeout(()=> cake.style.transform = '', 120);

      // air effect particles
      for (let i = 0; i < 5; i++) {
        const particle = document.createElement('div');
        particle.className = 'air-effect';
        particle.style.left = (Math.random() * 30 + 20) + '%';
        cake.appendChild(particle);
        setTimeout(() => particle.remove(), 1000);
      }

      if (cakeClicks === REQUIRED_CAKE_CLICKS) {
        document.querySelectorAll('.flame').forEach(f => {
          f.style.transition = 'opacity .8s ease, transform .8s ease';
          f.style.opacity = '0';
          f.style.transform = 'scale(.6)';
        });

        setTimeout(()=> {
          const ln = document.getElementById('love-note');
          ln.style.display = 'block';
          setTimeout(()=> { ln.style.opacity = 1; ln.style.transform = 'translateX(0)'; }, 60);
        }, 600);
      }
    }

    function openNote() {
      const final = document.getElementById('final-page');
      final.style.display = 'block';
      setTimeout(()=> { final.style.opacity = 1; final.style.transform = 'translateX(0)'; }, 80);
      setTimeout(()=> window.scrollTo({ top: document.body.scrollHeight, behavior: 'smooth' }), 150);
    }

    window.onload = function() {
      spawnBalloon();
      setTimeout(()=> {
        const t = document.getElementById('title');
        t.style.opacity = 1;
        t.style.transform = 'translateX(0)';
      }, 180);

      const cakeSec = document.getElementById('cake-section');
      cakeSec.style.opacity = 0;
      cakeSec.style.transform = 'translateX(60px)';
    }
  </script>

  <!-- background music -->
  <audio id="bg-music" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_7ab14f392e.mp3?filename=lofi-hip-hop-100-bpm-10977.mp3" autoplay loop></audio>
</body>
</html>
