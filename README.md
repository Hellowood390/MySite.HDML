<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Nomma — order food from your street</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,600;9..144,700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --ink:#1c1a17; --paper:#fffaf4; --card:#ffffff;
    --chili:#e14e2e; --mango:#f4a721; --herb:#3f6b4a;
    --line:#e7ddd0; --muted:#7a6f62;
    box-sizing:border-box;
    padding-top:env(safe-area-inset-top,0px);
    padding-bottom:env(safe-area-inset-bottom,0px);
  }
  @media (prefers-color-scheme: dark){
    :root:not([data-theme="light"]){
      --ink:#f4efe7; --paper:#17140f; --card:#211d16;
      --line:#382f22; --muted:#a89a86;
    }
  }
  :root[data-theme="dark"]{
    --ink:#f4efe7; --paper:#17140f; --card:#211d16;
    --line:#382f22; --muted:#a89a86;
  }
  html{scroll-padding-top:env(safe-area-inset-top,0px);}
  *{box-sizing:border-box;}
  body{
    margin:0; background:var(--paper); color:var(--ink);
    font-family:'Inter',system-ui,sans-serif;
    -webkit-font-smoothing:antialiased;
  }
  h1,h2,.display{font-family:'Fraunces',Georgia,serif;}
  a{color:inherit;text-decoration:none;}
  .wrap{max-width:1100px;margin:0 auto;padding:0 24px;}
  header{
    position:sticky; top:env(safe-area-inset-top,0px); z-index:10;
    background:var(--paper); border-bottom:1px solid var(--line);
  }
  .nav{display:flex;align-items:center;justify-content:space-between;padding:18px 24px;}
  .logo{font-family:'Fraunces',serif;font-weight:700;font-size:22px;letter-spacing:-0.02em;}
  .logo span{color:var(--chili);}
  .navlinks{display:flex;gap:28px;font-size:15px;color:var(--muted);}
  .navlinks a:hover{color:var(--ink);}
  .btn{
    display:inline-flex;align-items:center;gap:8px;
    background:var(--chili); color:#fff; padding:11px 20px;
    border-radius:100px; font-weight:600; font-size:14px; border:none; cursor:pointer;
  }
  .btn.ghost{background:transparent;color:var(--ink);border:1px solid var(--line);}
  @media (max-width:720px){.navlinks{display:none;}}

  .hero{padding:64px 0 40px;}
  .hero .grid{display:grid;grid-template-columns:1.1fr 0.9fr;gap:48px;align-items:center;}
  @media (max-width:820px){.hero .grid{grid-template-columns:1fr;}}
  .kicker{color:var(--chili);font-weight:600;font-size:15px;margin-bottom:14px;}
  h1{font-size:clamp(34px,5vw,54px);line-height:1.05;font-weight:600;margin:0 0 20px;max-width:15ch;}
  .lede{color:var(--muted);font-size:18px;line-height:1.6;max-width:38ch;margin-bottom:32px;}
  .search{
    display:flex;gap:8px;background:var(--card);border:1px solid var(--line);
    border-radius:14px;padding:8px;max-width:460px;
  }
  .search input{
    flex:1;border:none;background:none;padding:10px 12px;font-size:15px;color:var(--ink);
    font-family:inherit;outline:none;
  }
  .stats{display:flex;gap:36px;margin-top:36px;}
  .stat b{font-family:'Fraunces',serif;font-size:26px;display:block;}
  .stat span{color:var(--muted);font-size:13px;}

  .plate{
    position:relative; aspect-ratio:1/1; border-radius:32px;
    background:linear-gradient(155deg,var(--mango),var(--chili));
    display:flex;align-items:center;justify-content:center;
    font-size:96px;
  }

  .cats{display:flex;gap:10px;overflow-x:auto;padding:28px 0;border-top:1px solid var(--line);border-bottom:1px solid var(--line);}
  .cats::-webkit-scrollbar{display:none;}
  .chip{
    flex:0 0 auto;background:var(--card);border:1px solid var(--line);
    border-radius:100px;padding:10px 18px;font-size:14px;font-weight:500;
    display:flex;align-items:center;gap:8px;white-space:nowrap;
  }

  section{padding:56px 0;}
  .sec-head{display:flex;justify-content:space-between;align-items:baseline;margin-bottom:28px;}
  .sec-head h2{font-size:28px;font-weight:600;margin:0;}
  .sec-head a{color:var(--chili);font-size:14px;font-weight:600;}

  .cards{display:grid;grid-template-columns:repeat(4,1fr);gap:20px;}
  @media (max-width:900px){.cards{grid-template-columns:repeat(2,1fr);}}
  @media (max-width:520px){.cards{grid-template-columns:1fr;}}
  .card{
    background:var(--card);border:1px solid var(--line);border-radius:18px;overflow:hidden;
  }
  .card .photo{
    height:120px;display:flex;align-items:center;justify-content:center;font-size:40px;
  }
  .card .body{padding:16px;}
  .card h3{margin:0 0 4px;font-size:16px;}
  .card p{margin:0;color:var(--muted);font-size:13px;}
  .card .meta{display:flex;justify-content:space-between;margin-top:12px;font-size:13px;color:var(--muted);}

  .steps{display:grid;grid-template-columns:repeat(3,1fr);gap:28px;}
  @media (max-width:720px){.steps{grid-template-columns:1fr;}}
  .step .num{
    font-family:'Fraunces',serif;font-size:15px;color:var(--chili);
    border:1px solid var(--chili);width:32px;height:32px;border-radius:50%;
    display:flex;align-items:center;justify-content:center;margin-bottom:16px;
  }
  .step h3{margin:0 0 8px;font-size:18px;}
  .step p{margin:0;color:var(--muted);font-size:14px;line-height:1.6;}

  .cta{
    background:var(--ink);color:var(--paper);border-radius:28px;
    padding:56px 40px;display:flex;justify-content:space-between;align-items:center;gap:24px;
  }
  @media (max-width:700px){.cta{flex-direction:column;text-align:center;}}
  .cta h2{color:var(--paper);font-size:30px;margin:0 0 10px;max-width:16ch;}
  .cta p{color:#c9c1b5;margin:0 0 0;max-width:34ch;}
  .storebtns{display:flex;gap:10px;flex-wrap:wrap;}
  .storebtns .btn.ghost{border-color:#453f34;color:var(--paper);}

  footer{border-top:1px solid var(--line);padding:32px 0;color:var(--muted);font-size:13px;
    display:flex;justify-content:space-between;flex-wrap:wrap;gap:12px;}
</style>
</head>
<body>

<header>
  <div class="nav">
    <div class="logo">nom<span>ma</span></div>
    <div class="navlinks">
      <a href="#restaurants">Restaurants</a>
      <a href="#how">How it works</a>
      <a href="#">Ride with us</a>
    </div>
    <a href="#" class="btn ghost">Sign in</a>
  </div>
</header>

<div class="wrap">
  <section class="hero">
    <div class="grid">
      <div>
        <div class="kicker">Now delivering in 40+ neighborhoods</div>
        <h1>Whatever's cooking nearby, delivered warm.</h1>
        <p class="lede">From the corner dosa cart to the place with the queue out the door — order it, track it, eat it while it's still hot.</p>
        <div class="search">
          <input type="text" placeholder="Enter your delivery address">
          <button class="btn">Find food</button>
        </div>
        <div class="stats">
          <div class="stat"><b>26 min</b><span>average delivery</span></div>
          <div class="stat"><b>3,200+</b><span>restaurants listed</span></div>
          <div class="stat"><b>4.7★</b><span>average rating</span></div>
        </div>
      </div>
      <div class="plate">🍜</div>
    </div>
  </section>

  <div class="cats">
    <div class="chip">🍛 Biryani</div>
    <div class="chip">🍕 Pizza</div>
    <div class="chip">🍔 Burgers</div>
    <div class="chip">🍣 Sushi</div>
    <div class="chip">🥗 Salads</div>
    <div class="chip">🍰 Desserts</div>
    <div class="chip">☕ Coffee</div>
    <div class="chip">🌮 Tacos</div>
  </div>

  <section id="restaurants">
    <div class="sec-head">
      <h2>Popular near you</h2>
      <a href="#">See all restaurants</a>
    </div>
    <div class="cards">
      <div class="card">
        <div class="photo" style="background:#fde3d0;">🍜</div>
        <div class="body">
          <h3>Golden Wok</h3>
          <p>Chinese · Noodles</p>
          <div class="meta"><span>4.8 ★</span><span>20–30 min</span></div>
        </div>
      </div>
      <div class="card">
        <div class="photo" style="background:#fbe3e8;">🍕</div>
        <div class="body">
          <h3>Bella Forno</h3>
          <p>Italian · Pizza</p>
          <div class="meta"><span>4.6 ★</span><span>25–35 min</span></div>
        </div>
      </div>
      <div class="card">
        <div class="photo" style="background:#e7f0e3;">🥗</div>
        <div class="body">
          <h3>Green Bowl Co.</h3>
          <p>Healthy · Salads</p>
          <div class="meta"><span>4.7 ★</span><span>15–25 min</span></div>
        </div>
      </div>
      <div class="card">
        <div class="photo" style="background:#fdeecb;">🍛</div>
        <div class="body">
          <h3>Spice Route</h3>
          <p>Indian · Curry</p>
          <div class="meta"><span>4.9 ★</span><span>30–40 min</span></div>
        </div>
      </div>
    </div>
  </section>

  <section id="how">
    <div class="sec-head"><h2>How it works</h2></div>
    <div class="steps">
      <div class="step">
        <div class="num">1</div>
        <h3>Browse what's nearby</h3>
        <p>See real menus, prices and wait times for restaurants close to you.</p>
      </div>
      <div class="step">
        <div class="num">2</div>
        <h3>Place your order</h3>
        <p>Pay in the app and the kitchen starts cooking the moment it's confirmed.</p>
      </div>
      <div class="step">
        <div class="num">3</div>
        <h3>Track it to your door</h3>
        <p>Watch your rider's route in real time, right up to the knock on your door.</p>
      </div>
    </div>
  </section>

  <section>
    <div class="cta">
      <div>
        <h2>Get Nomma on your phone</h2>
        <p>Faster reordering, live rider tracking and deals that only show up in the app.</p>
      </div>
      <div class="storebtns">
        <a href="#" class="btn ghost">App Store</a>
        <a href="#" class="btn ghost">Google Play</a>
      </div>
    </div>
  </section>
</div>

<footer>
  <div class="wrap" style="display:flex;justify-content:space-between;width:100%;flex-wrap:wrap;gap:12px;">
    <span>© 2026 Nomma</span>
    <span>Partner with us · Become a rider · Help</span>
  </div>
</footer>

</body>
</html>
