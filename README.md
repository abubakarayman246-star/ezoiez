[subway_website.html](https://github.com/user-attachments/files/28933743/subway_website.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SUBWAY® — Eat Fresh. Live Bold.</title>
<link href="https://fonts.googleapis.com/css2?family=Black+Han+Sans&family=Bebas+Neue&family=Inter:wght@400;500;700;900&display=swap" rel="stylesheet">
<style>
  *{margin:0;padding:0;box-sizing:border-box}
  :root{
    --green:#008C15;
    --yellow:#FFC600;
    --dark:#0A0A0A;
    --white:#FFFFFF;
    --gray:#1A1A1A;
  }
  html{scroll-behavior:smooth}
  body{background:var(--dark);color:var(--white);font-family:'Inter',sans-serif;overflow-x:hidden}

  /* NAV */
  nav{
    position:fixed;top:0;left:0;right:0;z-index:999;
    display:flex;align-items:center;justify-content:space-between;
    padding:18px 5%;
    background:rgba(10,10,10,0.85);
    backdrop-filter:blur(12px);
    border-bottom:2px solid var(--yellow);
  }
  .logo{
    font-family:'Bebas Neue',sans-serif;
    font-size:2.2rem;letter-spacing:4px;
    color:var(--yellow);
    text-shadow:0 0 30px rgba(255,198,0,0.5);
  }
  .logo span{color:var(--green)}
  .nav-links{display:flex;gap:36px;list-style:none}
  .nav-links a{
    color:var(--white);text-decoration:none;font-weight:600;
    font-size:.9rem;letter-spacing:2px;text-transform:uppercase;
    transition:color .2s;position:relative;
  }
  .nav-links a::after{
    content:'';position:absolute;bottom:-4px;left:0;right:0;
    height:2px;background:var(--yellow);transform:scaleX(0);
    transition:transform .2s;
  }
  .nav-links a:hover{color:var(--yellow)}
  .nav-links a:hover::after{transform:scaleX(1)}
  .nav-cta{
    background:var(--yellow);color:var(--dark);
    border:none;padding:10px 24px;font-weight:900;
    font-size:.85rem;letter-spacing:2px;text-transform:uppercase;
    cursor:pointer;transition:transform .15s,background .15s;
    clip-path:polygon(8px 0%,100% 0%,calc(100% - 8px) 100%,0% 100%);
  }
  .nav-cta:hover{transform:scale(1.05);background:#FFD740}

  /* PAGES */
  .page{min-height:100vh;display:none;flex-direction:column;padding-top:80px}
  .page.active{display:flex}

  /* === PAGE 1: HERO === */
  #home{
    background:var(--dark);
    position:relative;overflow:hidden;
    align-items:center;justify-content:center;
    text-align:center;
  }
  .hero-stripes{
    position:absolute;inset:0;
    background:repeating-linear-gradient(
      -45deg,
      transparent,transparent 40px,
      rgba(0,140,21,0.04) 40px,rgba(0,140,21,0.04) 80px
    );
  }
  .hero-circle{
    position:absolute;width:700px;height:700px;border-radius:50%;
    background:radial-gradient(circle,rgba(255,198,0,0.12) 0%,transparent 70%);
    top:50%;left:50%;transform:translate(-50%,-50%);
    animation:pulse 4s ease-in-out infinite;
  }
  @keyframes pulse{0%,100%{transform:translate(-50%,-50%) scale(1)}50%{transform:translate(-50%,-50%) scale(1.08)}}
  .hero-content{position:relative;z-index:2;max-width:900px;padding:0 20px}
  .hero-eyebrow{
    font-size:.8rem;letter-spacing:6px;text-transform:uppercase;
    color:var(--yellow);font-weight:700;margin-bottom:20px;
    display:flex;align-items:center;justify-content:center;gap:12px;
  }
  .eyebrow-line{width:40px;height:2px;background:var(--yellow)}
  .hero-title{
    font-family:'Bebas Neue',sans-serif;
    font-size:clamp(5rem,14vw,12rem);
    line-height:.9;
    color:var(--white);
    letter-spacing:-2px;
  }
  .hero-title .accent{color:var(--yellow);display:block}
  .hero-title .green{color:var(--green);display:block}
  .hero-sub{
    font-size:1.1rem;color:rgba(255,255,255,0.6);
    margin:28px 0 40px;max-width:500px;margin-left:auto;margin-right:auto;
    line-height:1.7;
  }
  .hero-btns{display:flex;gap:16px;justify-content:center;flex-wrap:wrap}
  .btn-primary{
    background:var(--yellow);color:var(--dark);
    border:none;padding:16px 40px;font-weight:900;
    font-size:1rem;letter-spacing:2px;text-transform:uppercase;
    cursor:pointer;transition:transform .15s;
    clip-path:polygon(12px 0%,100% 0%,calc(100% - 12px) 100%,0% 100%);
  }
  .btn-primary:hover{transform:scale(1.04)}
  .btn-outline{
    background:transparent;color:var(--white);
    border:2px solid rgba(255,255,255,0.3);
    padding:15px 40px;font-weight:700;
    font-size:1rem;letter-spacing:2px;text-transform:uppercase;
    cursor:pointer;transition:all .15s;
  }
  .btn-outline:hover{border-color:var(--white);background:rgba(255,255,255,0.05)}

  .hero-stats{
    position:absolute;bottom:40px;left:0;right:0;
    display:flex;justify-content:center;gap:60px;
    z-index:2;
  }
  .stat-item{text-align:center}
  .stat-num{
    font-family:'Bebas Neue',sans-serif;
    font-size:2.5rem;color:var(--yellow);display:block;
  }
  .stat-label{font-size:.75rem;letter-spacing:3px;text-transform:uppercase;color:rgba(255,255,255,0.4)}

  /* SCROLL TICKER */
  .ticker{
    background:var(--yellow);padding:12px 0;
    overflow:hidden;white-space:nowrap;
  }
  .ticker-inner{
    display:inline-block;
    animation:ticker 20s linear infinite;
    font-family:'Bebas Neue',sans-serif;
    font-size:1.2rem;letter-spacing:3px;color:var(--dark);
  }
  @keyframes ticker{from{transform:translateX(0)}to{transform:translateX(-50%)}}
  .ticker-sep{margin:0 30px;color:var(--green)}

  /* === PAGE 2: MENU === */
  #menu{background:var(--dark);padding:80px 5%}
  .section-header{text-align:center;margin-bottom:60px}
  .section-tag{
    font-size:.75rem;letter-spacing:6px;text-transform:uppercase;
    color:var(--yellow);font-weight:700;
  }
  .section-title{
    font-family:'Bebas Neue',sans-serif;
    font-size:clamp(3rem,8vw,7rem);
    line-height:1;margin-top:8px;
  }
  .section-title .hl{color:var(--green)}

  .menu-filter{
    display:flex;gap:12px;justify-content:center;
    flex-wrap:wrap;margin-bottom:50px;
  }
  .filter-btn{
    background:rgba(255,255,255,0.05);color:rgba(255,255,255,0.6);
    border:1px solid rgba(255,255,255,0.1);padding:10px 24px;
    font-size:.8rem;letter-spacing:2px;text-transform:uppercase;
    font-weight:600;cursor:pointer;transition:all .2s;border-radius:2px;
  }
  .filter-btn.active,.filter-btn:hover{
    background:var(--yellow);color:var(--dark);border-color:var(--yellow);
  }

  .menu-grid{
    display:grid;
    grid-template-columns:repeat(auto-fill,minmax(300px,1fr));
    gap:24px;
    max-width:1200px;margin:0 auto;
  }
  .menu-card{
    background:var(--gray);
    border:1px solid rgba(255,255,255,0.07);
    position:relative;overflow:hidden;cursor:pointer;
    transition:transform .2s,border-color .2s;
    border-radius:4px;
  }
  .menu-card:hover{transform:translateY(-4px);border-color:var(--yellow)}
  .menu-card-img{
    height:200px;
    display:flex;align-items:center;justify-content:center;
    font-size:5rem;
    background:linear-gradient(135deg,rgba(0,140,21,.15),rgba(255,198,0,.1));
    position:relative;overflow:hidden;
  }
  .menu-card-img::after{
    content:'';position:absolute;bottom:-20px;left:-20px;right:-20px;
    height:40px;background:var(--gray);transform:skewY(-2deg);
  }
  .card-badge{
    position:absolute;top:16px;right:16px;
    background:var(--yellow);color:var(--dark);
    font-size:.7rem;font-weight:900;letter-spacing:2px;
    padding:4px 10px;text-transform:uppercase;border-radius:2px;
  }
  .menu-card-body{padding:20px 22px 22px}
  .card-cal{
    font-size:.7rem;letter-spacing:2px;color:var(--green);
    text-transform:uppercase;font-weight:700;margin-bottom:6px;
  }
  .card-name{font-size:1.25rem;font-weight:900;margin-bottom:8px}
  .card-desc{font-size:.85rem;color:rgba(255,255,255,0.5);line-height:1.6;margin-bottom:16px}
  .card-footer{display:flex;align-items:center;justify-content:space-between}
  .card-price{font-family:'Bebas Neue',sans-serif;font-size:1.8rem;color:var(--yellow)}
  .card-add{
    background:var(--green);color:var(--white);border:none;
    padding:8px 20px;font-weight:700;font-size:.8rem;letter-spacing:1px;
    text-transform:uppercase;cursor:pointer;border-radius:2px;
    transition:background .15s;
  }
  .card-add:hover{background:#00a819}

  /* === PAGE 3: BUILD === */
  #build{background:var(--dark);padding:80px 5%}
  .builder-layout{
    display:grid;grid-template-columns:1fr 380px;
    gap:40px;max-width:1100px;margin:0 auto;
    align-items:start;
  }
  .builder-steps{display:flex;flex-direction:column;gap:4px}
  .step-block{
    border:1px solid rgba(255,255,255,0.08);
    border-radius:4px;overflow:hidden;
  }
  .step-header{
    display:flex;align-items:center;gap:16px;padding:18px 22px;
    cursor:pointer;transition:background .15s;
    background:rgba(255,255,255,0.02);
  }
  .step-header:hover{background:rgba(255,255,255,0.05)}
  .step-header.open{background:rgba(0,140,21,0.12);border-bottom:1px solid rgba(0,140,21,0.3)}
  .step-num{
    width:36px;height:36px;border-radius:50%;
    background:var(--yellow);color:var(--dark);
    display:flex;align-items:center;justify-content:center;
    font-family:'Bebas Neue',sans-serif;font-size:1.2rem;flex-shrink:0;
  }
  .step-header.open .step-num{background:var(--green);color:var(--white)}
  .step-info{flex:1}
  .step-label{font-size:.7rem;letter-spacing:3px;color:rgba(255,255,255,0.4);text-transform:uppercase}
  .step-sel{font-size:1rem;font-weight:700;margin-top:2px}
  .step-body{
    padding:20px 22px;
    display:none;
  }
  .step-body.open{display:block}
  .option-grid{display:flex;flex-wrap:wrap;gap:10px}
  .option-chip{
    background:rgba(255,255,255,0.05);
    border:1px solid rgba(255,255,255,0.1);
    padding:8px 18px;border-radius:100px;
    font-size:.85rem;cursor:pointer;transition:all .15s;color:rgba(255,255,255,0.7);
  }
  .option-chip.selected,.option-chip:hover{
    background:var(--yellow);color:var(--dark);border-color:var(--yellow);font-weight:700;
  }
  .option-chip.multi.selected{background:var(--green);border-color:var(--green);color:var(--white)}

  /* Receipt */
  .receipt{
    background:var(--gray);border:1px solid rgba(255,255,255,0.1);
    border-radius:4px;padding:28px;position:sticky;top:90px;
  }
  .receipt-title{
    font-family:'Bebas Neue',sans-serif;
    font-size:1.8rem;letter-spacing:2px;
    border-bottom:1px solid rgba(255,255,255,0.1);
    padding-bottom:16px;margin-bottom:20px;
  }
  .receipt-item{
    display:flex;justify-content:space-between;
    font-size:.85rem;padding:8px 0;
    border-bottom:1px solid rgba(255,255,255,0.05);
  }
  .receipt-item .label{color:rgba(255,255,255,0.5);font-size:.75rem;letter-spacing:1px;text-transform:uppercase}
  .receipt-item .val{font-weight:700}
  .receipt-total{
    display:flex;justify-content:space-between;
    margin-top:20px;padding-top:16px;
    border-top:2px solid var(--yellow);
  }
  .receipt-total .t-label{font-family:'Bebas Neue',sans-serif;font-size:1.5rem;letter-spacing:2px}
  .receipt-total .t-price{font-family:'Bebas Neue',sans-serif;font-size:1.8rem;color:var(--yellow)}
  .order-btn{
    width:100%;margin-top:20px;
    background:var(--yellow);color:var(--dark);border:none;
    padding:18px;font-weight:900;font-size:1rem;letter-spacing:3px;
    text-transform:uppercase;cursor:pointer;transition:transform .15s;
    clip-path:polygon(10px 0%,100% 0%,calc(100% - 10px) 100%,0% 100%);
  }
  .order-btn:hover{transform:scale(1.02)}

  /* === PAGE 4: ABOUT === */
  #about{background:var(--dark);padding:80px 5%}
  .about-hero{
    max-width:1100px;margin:0 auto;
    display:grid;grid-template-columns:1fr 1fr;gap:80px;
    align-items:center;margin-bottom:80px;
  }
  .about-big-text{
    font-family:'Bebas Neue',sans-serif;
    font-size:clamp(4rem,9vw,8rem);line-height:.95;
    letter-spacing:-1px;
  }
  .about-big-text .line2{color:var(--yellow)}
  .about-big-text .line3{color:var(--green)}
  .about-right p{
    font-size:1.05rem;color:rgba(255,255,255,0.6);
    line-height:1.8;margin-bottom:24px;
  }
  .about-right p strong{color:var(--white);font-weight:700}

  .values-grid{
    max-width:1100px;margin:0 auto;
    display:grid;grid-template-columns:repeat(4,1fr);gap:2px;
  }
  .value-card{
    padding:40px 28px;
    background:rgba(255,255,255,0.02);
    border:1px solid rgba(255,255,255,0.06);
    transition:background .2s;
  }
  .value-card:hover{background:rgba(255,198,0,0.05);border-color:rgba(255,198,0,0.2)}
  .value-icon{font-size:2.5rem;margin-bottom:20px}
  .value-title{
    font-family:'Bebas Neue',sans-serif;font-size:1.6rem;
    letter-spacing:2px;color:var(--yellow);margin-bottom:10px;
  }
  .value-text{font-size:.85rem;color:rgba(255,255,255,0.5);line-height:1.7}

  .about-cta-strip{
    max-width:1100px;margin:80px auto 0;
    background:var(--green);padding:60px;
    display:flex;align-items:center;justify-content:space-between;
    gap:40px;flex-wrap:wrap;
    clip-path:polygon(0 0,100% 0,100% 80%,98% 100%,2% 100%,0 80%);
  }
  .strip-text h2{
    font-family:'Bebas Neue',sans-serif;font-size:3rem;letter-spacing:2px;line-height:1;
  }
  .strip-text p{margin-top:8px;color:rgba(255,255,255,0.7);font-size:.95rem}

  /* FOOTER */
  footer{
    background:#050505;border-top:1px solid rgba(255,255,255,0.06);
    padding:50px 5%;
    display:flex;align-items:center;justify-content:space-between;
    flex-wrap:wrap;gap:24px;
  }
  .foot-logo{font-family:'Bebas Neue',sans-serif;font-size:2rem;color:var(--yellow);letter-spacing:4px}
  .foot-links{display:flex;gap:28px;flex-wrap:wrap}
  .foot-links a{color:rgba(255,255,255,0.4);text-decoration:none;font-size:.8rem;letter-spacing:1px;transition:color .15s}
  .foot-links a:hover{color:var(--yellow)}
  .foot-copy{color:rgba(255,255,255,0.2);font-size:.75rem}

  /* TOAST */
  .toast{
    position:fixed;bottom:30px;right:30px;
    background:var(--green);color:white;
    padding:14px 24px;font-weight:700;font-size:.9rem;
    border-radius:4px;opacity:0;pointer-events:none;
    transition:all .3s;transform:translateY(10px);
    z-index:9999;
  }
  .toast.show{opacity:1;transform:translateY(0)}

  @media(max-width:768px){
    .nav-links{display:none}
    .hero-stats{gap:24px}
    .stat-num{font-size:1.8rem}
    .builder-layout{grid-template-columns:1fr}
    .values-grid{grid-template-columns:1fr 1fr}
    .about-hero{grid-template-columns:1fr;gap:40px}
    .receipt{position:static}
  }
</style>
</head>
<body>

<nav>
  <div class="logo">SUB<span>WAY</span></div>
  <ul class="nav-links">
    <li><a href="#" onclick="showPage('home')">Home</a></li>
    <li><a href="#" onclick="showPage('menu')">Menu</a></li>
    <li><a href="#" onclick="showPage('build')">Build</a></li>
    <li><a href="#" onclick="showPage('about')">About</a></li>
  </ul>
  <button class="nav-cta" onclick="showPage('build')">Order Now</button>
</nav>

<!-- ===== PAGE 1: HOME ===== -->
<section id="home" class="page active">
  <div class="hero-stripes"></div>
  <div class="hero-circle"></div>
  <div class="hero-content">
    <div class="hero-eyebrow">
      <span class="eyebrow-line"></span>
      Since 1965 · Over 37,000 Locations Worldwide
      <span class="eyebrow-line"></span>
    </div>
    <h1 class="hero-title">
      EAT
      <span class="accent">FRESH.</span>
      <span class="green">LIVE BOLD.</span>
    </h1>
    <p class="hero-sub">Real ingredients. Real flavors. Your sub, your rules. Build something legendary — every single day.</p>
    <div class="hero-btns">
      <button class="btn-primary" onclick="showPage('menu')">Explore Menu</button>
      <button class="btn-outline" onclick="showPage('build')">Build My Sub</button>
    </div>
  </div>
  <div class="hero-stats">
    <div class="stat-item">
      <span class="stat-num">37K+</span>
      <span class="stat-label">Locations</span>
    </div>
    <div class="stat-item">
      <span class="stat-num">100+</span>
      <span class="stat-label">Countries</span>
    </div>
    <div class="stat-item">
      <span class="stat-num">∞</span>
      <span class="stat-label">Combos</span>
    </div>
  </div>
</section>

<div class="ticker" id="ticker-home" style="display:none">
  <span class="ticker-inner">
    🥖 FRESH BAKED BREAD DAILY <span class="ticker-sep">★</span> VEGGIE DELITE <span class="ticker-sep">★</span> MEATBALL MARINARA <span class="ticker-sep">★</span> TURKEY CLUB <span class="ticker-sep">★</span> THE MONSTER <span class="ticker-sep">★</span> FOOTLONG DEALS <span class="ticker-sep">★</span> BUILD YOUR OWN SUB <span class="ticker-sep">★</span> FRESH. BOLD. SUBWAY. <span class="ticker-sep">★</span>
    🥖 FRESH BAKED BREAD DAILY <span class="ticker-sep">★</span> VEGGIE DELITE <span class="ticker-sep">★</span> MEATBALL MARINARA <span class="ticker-sep">★</span> TURKEY CLUB <span class="ticker-sep">★</span> THE MONSTER <span class="ticker-sep">★</span> FOOTLONG DEALS <span class="ticker-sep">★</span> BUILD YOUR OWN SUB <span class="ticker-sep">★</span> FRESH. BOLD. SUBWAY. <span class="ticker-sep">★</span>
  </span>
</div>

<!-- ===== PAGE 2: MENU ===== -->
<section id="menu" class="page">
  <div class="section-header">
    <p class="section-tag">What we serve</p>
    <h2 class="section-title">THE <span class="hl">LINEUP</span></h2>
  </div>
  <div class="menu-filter" id="filter-bar">
    <button class="filter-btn active" onclick="filterMenu('all',this)">All</button>
    <button class="filter-btn" onclick="filterMenu('classic',this)">Classics</button>
    <button class="filter-btn" onclick="filterMenu('premium',this)">Premium</button>
    <button class="filter-btn" onclick="filterMenu('veggie',this)">Veggie</button>
    <button class="filter-btn" onclick="filterMenu('new',this)">New</button>
  </div>
  <div class="menu-grid" id="menu-grid"></div>
</section>

<!-- ===== PAGE 3: BUILD ===== -->
<section id="build" class="page">
  <div class="section-header">
    <p class="section-tag">Craft your masterpiece</p>
    <h2 class="section-title">BUILD <span class="hl">YOUR SUB</span></h2>
  </div>
  <div class="builder-layout">
    <div class="builder-steps" id="builder-steps"></div>
    <div class="receipt">
      <div class="receipt-title">🧾 Your Order</div>
      <div id="receipt-items"></div>
      <div class="receipt-total">
        <span class="t-label">TOTAL</span>
        <span class="t-price" id="receipt-total">$0.00</span>
      </div>
      <button class="order-btn" onclick="placeOrder()">Place Order →</button>
    </div>
  </div>
</section>

<!-- ===== PAGE 4: ABOUT ===== -->
<section id="about" class="page">
  <div class="about-hero">
    <div class="about-big-text">
      BORN<br>
      <span class="line2">TO BE</span><br>
      <span class="line3">FRESH.</span>
    </div>
    <div class="about-right">
      <p>It all started in <strong>1965</strong> with a 17-year-old kid named Fred DeLuca and a $1,000 loan from family friend Dr. Peter Buck. The goal? Open a submarine sandwich shop in Bridgeport, Connecticut.</p>
      <p>What happened next changed the way the world eats. Subway grew from a single corner shop into the <strong>world's largest fast-food chain by number of locations</strong> — powered by one simple idea: fresh ingredients, made your way.</p>
      <p>Today, <strong>37,000+ restaurants</strong> in 100+ countries serve millions of people every day. The ingredients change, the recipes evolve — but the mission stays the same: <strong>Eat Fresh.</strong></p>
    </div>
  </div>

  <div class="values-grid">
    <div class="value-card">
      <div class="value-icon">🌱</div>
      <div class="value-title">Fresh Daily</div>
      <div class="value-text">Bread baked fresh in-store every single day. No compromises on quality, ever.</div>
    </div>
    <div class="value-card">
      <div class="value-icon">🎛️</div>
      <div class="value-title">Your Way</div>
      <div class="value-text">Thousands of possible combinations. Customize every ingredient, every topping, every sauce.</div>
    </div>
    <div class="value-card">
      <div class="value-icon">🌍</div>
      <div class="value-title">Global Soul</div>
      <div class="value-text">From New York to Tokyo, Subway adapts to local tastes while keeping that signature freshness.</div>
    </div>
    <div class="value-card">
      <div class="value-icon">💪</div>
      <div class="value-title">Better For You</div>
      <div class="value-text">Lower calorie options, plant-based choices, and nutrient-rich ingredients — for every lifestyle.</div>
    </div>
  </div>

  <div class="about-cta-strip">
    <div class="strip-text">
      <h2>HUNGRY YET?</h2>
      <p>Your perfect sub is 30 seconds away.</p>
    </div>
    <button class="btn-primary" style="padding:18px 48px;font-size:1rem" onclick="showPage('build')">Build It Now</button>
  </div>
</section>

<footer>
  <div class="foot-logo">SUBWAY</div>
  <div class="foot-links">
    <a href="#">Privacy Policy</a>
    <a href="#">Terms of Use</a>
    <a href="#">Nutrition Info</a>
    <a href="#">Careers</a>
    <a href="#">Franchising</a>
    <a href="#">Contact</a>
  </div>
  <div class="foot-copy">© 2025 Subway IP LLC. All rights reserved.</div>
</footer>

<div class="toast" id="toast"></div>

<script>
const SUBS = [
  {id:1,name:"Italian B.M.T.",emoji:"🥖",cal:"480 cal",desc:"Genoa salami, spicy pepperoni, ham — the OG Italian classic.",price:8.99,cat:"classic"},
  {id:2,name:"Meatball Marinara",emoji:"🍝",cal:"530 cal",desc:"Juicy meatballs smothered in zesty marinara. Melted cheese on top.",price:7.49,cat:"classic"},
  {id:3,name:"Turkey Breast",emoji:"🦃",cal:"280 cal",desc:"Lean oven-roasted turkey with crisp veggies. Light and legendary.",price:8.29,cat:"classic"},
  {id:4,name:"The Monster",emoji:"🦴",cal:"900 cal",desc:"ALL the meats. All the cheese. For when you mean business.",price:12.99,cat:"premium",badge:"BEAST MODE"},
  {id:5,name:"Steak & Cheese",emoji:"🥩",cal:"640 cal",desc:"Tender steak strips with melted American cheese. Pure fire.",price:10.49,cat:"premium"},
  {id:6,name:"Veggie Delite",emoji:"🥬",cal:"200 cal",desc:"A rainbow of fresh vegetables on your choice of bread. Crisp, light, satisfying.",price:6.99,cat:"veggie"},
  {id:7,name:"Subway Club",emoji:"🏆",cal:"410 cal",desc:"Roast beef, turkey, ham — triple stacked and triple tasty.",price:9.49,cat:"premium"},
  {id:8,name:"Spicy Italian",emoji:"🌶️",cal:"500 cal",desc:"Pepperoni and salami with a kick. For those who like it hot.",price:8.79,cat:"classic"},
  {id:9,name:"Beyond Meatball",emoji:"🌿",cal:"490 cal",desc:"Plant-based meatballs in rich marinara. Zero compromise on flavor.",price:9.99,cat:"veggie",badge:"NEW"},
  {id:10,name:"BBQ Brisket",emoji:"🔥",cal:"720 cal",desc:"Slow-smoked brisket with tangy BBQ sauce. Limited time legend.",price:13.49,cat:"new",badge:"LIMITED"},
  {id:11,name:"Tuna",emoji:"🐟",cal:"480 cal",desc:"Real tuna, creamy mayo. A classic for a reason.",price:7.99,cat:"classic"},
  {id:12,name:"Rotisserie Chicken",emoji:"🍗",cal:"370 cal",desc:"Tender rotisserie-style chicken. Clean, fresh, next level.",price:10.99,cat:"new",badge:"NEW"},
];

const STEPS = [
  {id:"size",label:"Size",icon:"📏",type:"single",options:[{l:"6\" Half",v:"6-inch",p:0},{l:"Footlong",v:"footlong",p:2.50},{l:"XL Wrap",v:"wrap",p:1.50}]},
  {id:"bread",label:"Bread",icon:"🥖",type:"single",options:[{l:"Italian White",v:"Italian White",p:0},{l:"Honey Oat",v:"Honey Oat",p:0},{l:"Multigrain",v:"Multigrain",p:0},{l:"Flatbread",v:"Flatbread",p:0},{l:"Wrap",v:"Wrap",p:0.50}]},
  {id:"protein",label:"Protein",icon:"🥩",type:"single",options:[{l:"Turkey Breast",v:"Turkey Breast",p:0},{l:"Italian B.M.T.",v:"Italian B.M.T.",p:0},{l:"Meatball Marinara",v:"Meatball Marinara",p:0},{l:"Steak",v:"Steak",p:1.50},{l:"Tuna",v:"Tuna",p:0},{l:"Beyond Meat™",v:"Beyond Meat™",p:1.50}]},
  {id:"cheese",label:"Cheese",icon:"🧀",type:"single",options:[{l:"American",v:"American",p:0},{l:"Swiss",v:"Swiss",p:0},{l:"Provolone",v:"Provolone",p:0},{l:"Cheddar",v:"Cheddar",p:0},{l:"No Cheese",v:"No Cheese",p:0}]},
  {id:"veggies",label:"Veggies",icon:"🥗",type:"multi",options:[{l:"Lettuce",v:"Lettuce"},{l:"Tomato",v:"Tomato"},{l:"Cucumber",v:"Cucumber"},{l:"Onion",v:"Onion"},{l:"Green Pepper",v:"Green Pepper"},{l:"Jalapeños",v:"Jalapeños"},{l:"Olives",v:"Olives"},{l:"Spinach",v:"Spinach"},{l:"Avocado",v:"Avocado"}]},
  {id:"sauce",label:"Sauce",icon:"🫙",type:"multi",options:[{l:"Mayonnaise",v:"Mayonnaise"},{l:"Ranch",v:"Ranch"},{l:"Honey Mustard",v:"Honey Mustard"},{l:"Southwest",v:"Southwest"},{l:"Marinara",v:"Marinara"},{l:"Oil & Vinegar",v:"Oil & Vinegar"},{l:"Hot Sauce",v:"Hot Sauce"}]},
];

let selections = {size:null,bread:null,protein:null,cheese:null,veggies:[],sauce:[]};
let basePrice = 7.49;
let activeStep = 0;
let currentMenu = 'all';

// --- NAVIGATION ---
function showPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  const ticker = document.getElementById('ticker-home');
  ticker.style.display = id==='home' ? 'block' : 'none';
  window.scrollTo(0,0);
}

// --- MENU ---
function renderMenu(cat){
  const grid = document.getElementById('menu-grid');
  const items = cat==='all' ? SUBS : SUBS.filter(s=>s.cat===cat);
  grid.innerHTML = items.map(s=>`
    <div class="menu-card">
      <div class="menu-card-img">${s.emoji}
        ${s.badge?`<div class="card-badge">${s.badge}</div>`:''}
      </div>
      <div class="menu-card-body">
        <div class="card-cal">${s.cal}</div>
        <div class="card-name">${s.name}</div>
        <div class="card-desc">${s.desc}</div>
        <div class="card-footer">
          <div class="card-price">$${s.price.toFixed(2)}</div>
          <button class="card-add" onclick="quickAdd('${s.name}',${s.price})">+ Add</button>
        </div>
      </div>
    </div>
  `).join('');
}

function filterMenu(cat,btn){
  currentMenu = cat;
  document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  renderMenu(cat);
}

function quickAdd(name,price){
  showToast(`✅ ${name} added to cart!`);
}

// --- BUILDER ---
function renderBuilder(){
  const container = document.getElementById('builder-steps');
  container.innerHTML = STEPS.map((step,i)=>`
    <div class="step-block" id="block-${i}">
      <div class="step-header ${i===0?'open':''}" onclick="toggleStep(${i})">
        <div class="step-num ${i===0?'open':''}">${i+1}</div>
        <div class="step-info">
          <div class="step-label">Step ${i+1} · ${step.icon} ${step.label}</div>
          <div class="step-sel" id="sel-${i}">${i===0?'Choose your size':'—'}</div>
        </div>
        <span style="color:rgba(255,255,255,.3);font-size:1.2rem">${i===0?'▲':'▼'}</span>
      </div>
      <div class="step-body ${i===0?'open':''}" id="body-${i}">
        <div class="option-grid">
          ${step.options.map(opt=>`
            <button class="option-chip ${step.type==='multi'?'multi':''}"
              onclick="selectOption(${i},'${opt.v}',${step.type==='multi'?'true':'false'},${opt.p||0})">
              ${opt.l}${opt.p?` <span style="color:var(--green);font-size:.75rem">+$${opt.p.toFixed(2)}</span>`:''}
            </button>
          `).join('')}
        </div>
      </div>
    </div>
  `).join('');
}

function toggleStep(i){
  document.querySelectorAll('.step-header').forEach((h,idx)=>{
    h.classList.toggle('open', idx===i);
    h.querySelector('.step-num').classList.toggle('open', idx===i);
    h.querySelector('span').textContent = idx===i?'▲':'▼';
  });
  document.querySelectorAll('.step-body').forEach((b,idx)=>{
    b.classList.toggle('open', idx===i);
  });
  activeStep = i;
}

function selectOption(stepIdx, val, isMulti, extraPrice){
  const step = STEPS[stepIdx];
  if(isMulti){
    const arr = selections[step.id];
    const idx = arr.indexOf(val);
    if(idx>-1) arr.splice(idx,1); else arr.push(val);
    const chips = document.querySelectorAll(`#body-${stepIdx} .option-chip`);
    chips.forEach(c=>{
      const label = c.textContent.trim().split('+')[0].trim();
      c.classList.toggle('selected', arr.some(v=>v===val && c.textContent.includes(val)));
    });
    // re-mark all
    chips.forEach(c=>{
      const chipVal = STEPS[stepIdx].options.find(o=>c.textContent.includes(o.l))?.v;
      c.classList.toggle('selected', arr.includes(chipVal));
    });
  } else {
    selections[step.id] = val;
    document.querySelectorAll(`#body-${stepIdx} .option-chip`).forEach(c=>{
      c.classList.remove('selected');
      if(c.textContent.includes(val.split(' ')[0])) c.classList.add('selected');
    });
    // auto next
    if(stepIdx < STEPS.length - 1){
      setTimeout(()=>toggleStep(stepIdx+1), 300);
    }
  }
  const selEl = document.getElementById(`sel-${stepIdx}`);
  if(isMulti){
    selEl.textContent = selections[step.id].length ? selections[step.id].join(', ') : '—';
  } else {
    selEl.textContent = val;
  }
  updateReceipt();
}

function updateReceipt(){
  const items = document.getElementById('receipt-items');
  const rows = STEPS.map(step=>{
    const val = Array.isArray(selections[step.id])
      ? (selections[step.id].length ? selections[step.id].join(', ') : '—')
      : (selections[step.id] || '—');
    return `<div class="receipt-item"><span class="label">${step.label}</span><span class="val">${val}</span></div>`;
  }).join('');
  items.innerHTML = rows;

  let total = basePrice;
  STEPS.forEach(step=>{
    if(!Array.isArray(selections[step.id]) && selections[step.id]){
      const opt = step.options.find(o=>o.v===selections[step.id]);
      if(opt && opt.p) total += opt.p;
    }
  });
  document.getElementById('receipt-total').textContent = `$${total.toFixed(2)}`;
}

function placeOrder(){
  if(!selections.size || !selections.bread || !selections.protein){
    showToast('⚠️ Please choose size, bread & protein first!');
    return;
  }
  showToast('🎉 Order placed! Your sub is being made!');
  setTimeout(()=>{
    selections = {size:null,bread:null,protein:null,cheese:null,veggies:[],sauce:[]};
    renderBuilder();
    updateReceipt();
  }, 2000);
}

function showToast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'), 3000);
}

// INIT
renderMenu('all');
renderBuilder();
updateReceipt();
</script>
</body>
</html>
