<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8" />
<title>StyleLens — Conceptual Design Wireframe</title>
<style>
  :root{
    --bg:#f4f5f7;
    --surface:#ffffff;
    --line:#d9dde3;
    --ink:#1f2430;
    --muted:#8a929e;
    --soft:#eef1f5;
    --dark:#1f2430;
  }

  * { box-sizing: border-box; margin:0; padding:0; }

  body{
    font-family: "Inter", -apple-system, "Segoe UI", Roboto, sans-serif;
    background: var(--bg);
    color: var(--ink);
    padding: 40px 20px 80px;
  }

  h1.title{
    font-size: 22px;
    font-weight: 700;
    margin-bottom: 6px;
  }
  p.subtitle{
    font-size: 13px;
    color: var(--muted);
    margin-bottom: 32px;
  }

  /* Grid of screens */
  .grid{
    display: grid;
    grid-template-columns: repeat(4, 390px);
    gap: 48px 40px;
    justify-content: center;
  }

  @media (max-width: 1700px){
    .grid{ grid-template-columns: repeat(3, 390px); }
  }
  @media (max-width: 1300px){
    .grid{ grid-template-columns: repeat(2, 390px); }
  }

  /* Screen frame */
  .screen-wrap{
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  .screen-label{
    font-size: 12px;
    font-weight: 600;
    color: var(--muted);
    letter-spacing: .08em;
    text-transform: uppercase;
  }
  .screen{
    width: 390px;
    height: 844px;
    background: var(--surface);
    border: 1.5px solid var(--line);
    border-radius: 24px;
    overflow: hidden;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  /* Status bar */
  .statusbar{
    height: 32px;
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding: 0 20px;
    font-size: 11px;
    color: var(--ink);
    font-weight: 600;
  }
  .statusbar .icons{ display:flex; gap:4px; }
  .statusbar .dot{ width:5px; height:5px; background: var(--ink); border-radius:50%; }

  /* Navbar top */
  .navbar{
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding: 10px 16px;
    border-bottom: 1px solid var(--line);
  }
  .navbar .nav-left{
    display:flex; align-items:center; gap:10px;
    font-size: 14px; font-weight: 600;
  }
  .nav-icon{
    width: 28px; height:28px;
    border: 1.5px solid var(--line);
    border-radius: 8px;
    display:flex; align-items:center; justify-content:center;
    font-size: 13px;
    color: var(--ink);
    background: var(--surface);
  }
  .nav-title{ font-size: 14px; font-weight: 600; }

  /* Body content */
  .content{
    flex:1;
    padding: 16px 18px;
    overflow: hidden;
    display:flex;
    flex-direction: column;
    gap: 14px;
  }

  /* Bottom nav */
  .bottomnav{
    height: 62px;
    border-top: 1px solid var(--line);
    display:flex;
    align-items:center;
    justify-content:space-around;
    padding: 0 8px;
    background: var(--surface);
  }
  .bottomnav .nav-item{
    display:flex;
    flex-direction:column;
    align-items:center;
    gap: 4px;
    font-size: 10px;
    color: var(--muted);
  }
  .bottomnav .nav-item.active{ color: var(--ink); font-weight:600; }
  .bottomnav .nav-item .ic{
    width: 20px; height: 20px;
    border: 1.5px solid currentColor;
    border-radius: 6px;
  }

  /* Generic UI atoms */
  .search{
    height: 42px;
    background: var(--soft);
    border-radius: 10px;
    display:flex; align-items:center;
    padding: 0 14px;
    font-size: 13px;
    color: var(--muted);
    gap: 8px;
  }

  .banner{
    background: var(--soft);
    border-radius: 14px;
    padding: 16px;
    display:flex;
    flex-direction: column;
    gap: 6px;
  }
  .banner h3{ font-size: 15px; font-weight: 700; }
  .banner p{ font-size: 12px; color: var(--muted); }
  .banner .cta{
    margin-top: 8px;
    background: var(--dark);
    color: white;
    padding: 9px 14px;
    border-radius: 8px;
    font-size: 12px;
    font-weight: 600;
    align-self: flex-start;
  }

  .section-title{
    font-size: 13px;
    font-weight: 700;
    margin-top: 2px;
  }

  .chips{
    display:flex; gap: 8px; flex-wrap: wrap;
  }
  .chip{
    padding: 7px 12px;
    font-size: 11.5px;
    border: 1px solid var(--line);
    border-radius: 999px;
    background: var(--surface);
    color: var(--ink);
  }
  .chip.active{
    background: var(--dark);
    color: #fff;
    border-color: var(--dark);
  }

  .thumb-row{
    display:grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
  }
  .thumb{
    aspect-ratio: 1/1;
    background: var(--soft);
    border-radius: 12px;
    position: relative;
    overflow:hidden;
  }
  .thumb::before,
  .img-placeholder::before{
    content:"";
    position:absolute;
    inset: 0;
    background:
      linear-gradient(to top right, transparent 49.4%, var(--line) 49.4%, var(--line) 50.6%, transparent 50.6%),
      linear-gradient(to top left, transparent 49.4%, var(--line) 49.4%, var(--line) 50.6%, transparent 50.6%);
  }

  .img-placeholder{
    background: var(--soft);
    border-radius: 12px;
    position: relative;
    overflow: hidden;
    display:flex;
    align-items:center;
    justify-content:center;
    font-size: 11px;
    color: var(--muted);
  }
  .img-placeholder > span{
    position: relative;
    z-index: 1;
    background: var(--soft);
    padding: 2px 8px;
    border-radius: 4px;
  }

  .input-group{
    display:flex;
    flex-direction: column;
    gap: 6px;
  }
  .input-group label{
    font-size: 12px;
    font-weight: 600;
    color: var(--ink);
  }
  .input-group .input{
    height: 40px;
    background: var(--surface);
    border: 1px solid var(--line);
    border-radius: 10px;
    padding: 0 12px;
    display:flex; align-items:center;
    font-size: 12.5px;
    color: var(--muted);
  }

  .btn{
    height: 46px;
    border-radius: 10px;
    display:flex; align-items:center; justify-content:center;
    font-size: 13px; font-weight: 700;
    letter-spacing: .04em;
    cursor: pointer;
    border: 1.5px solid transparent;
  }
  .btn.primary{ background: var(--dark); color:#fff; }
  .btn.outline{ background: #fff; color: var(--ink); border-color: var(--line); }

  .divider{
    height: 1px; background: var(--line); margin: 2px 0;
  }

  .row{
    display:flex; align-items:center; justify-content:space-between;
    font-size: 12.5px;
  }

  .stepper{
    display:flex; align-items:center; gap: 10px;
    font-size: 11.5px; color: var(--muted);
  }
  .stepper .bar{
    flex:1; height: 6px; background: var(--soft); border-radius: 99px; overflow: hidden;
  }
  .stepper .bar > span{
    display:block; height:100%; width: 50%;
    background: var(--dark);
  }

  .product-card{
    display:flex; gap: 12px;
    background: var(--soft);
    border-radius: 12px;
    padding: 10px;
    align-items:center;
  }
  .product-card .pic{
    width: 56px; height: 56px;
    background: var(--surface);
    border-radius: 8px;
    flex-shrink: 0;
    position: relative;
    overflow: hidden;
  }
  .product-card .pic::before{
    content:"";
    position:absolute; inset:0;
    background:
      linear-gradient(to top right, transparent 49.4%, var(--line) 49.4%, var(--line) 50.6%, transparent 50.6%),
      linear-gradient(to top left, transparent 49.4%, var(--line) 49.4%, var(--line) 50.6%, transparent 50.6%);
  }
  .product-card .info{ display:flex; flex-direction:column; gap:2px; flex:1; }
  .product-card .info h4{ font-size: 13px; font-weight: 600; }
  .product-card .info span{ font-size: 12px; color: var(--muted); }

  .camera-frame{
    flex:1;
    background: var(--soft);
    border-radius: 16px;
    position: relative;
    display:flex;
    align-items:center;
    justify-content:center;
  }
  .camera-frame .corner{
    position:absolute;
    width: 22px; height: 22px;
    border: 2px solid var(--ink);
  }
  .camera-frame .c1{ top:14px; left:14px; border-right:none; border-bottom:none; }
  .camera-frame .c2{ top:14px; right:14px; border-left:none; border-bottom:none; }
  .camera-frame .c3{ bottom:14px; left:14px; border-right:none; border-top:none; }
  .camera-frame .c4{ bottom:14px; right:14px; border-left:none; border-top:none; }

  .face-oval{
    width: 140px; height: 180px;
    border: 1.5px dashed var(--line);
    border-radius: 50%;
    display:flex; align-items:center; justify-content:center;
    font-size: 10px; color: var(--muted);
    text-align:center;
    padding: 8px;
  }

  .live-badge{
    position:absolute; top: 14px; right: 14px;
    background: var(--dark); color:#fff;
    font-size: 10px; font-weight:700;
    padding: 4px 8px; border-radius: 6px;
    letter-spacing: .1em;
  }

  .check-list{
    display:flex; flex-direction: column; gap: 8px;
  }
  .check-item{
    display:flex; align-items:center; gap: 10px;
    font-size: 12.5px;
  }
  .check-item .box{
    width: 16px; height:16px;
    border: 1.5px solid var(--line);
    border-radius: 4px;
    display:flex; align-items:center; justify-content:center;
    font-size: 11px;
  }
  .check-item.checked .box{
    background: var(--dark); border-color: var(--dark); color:#fff;
  }

  .compare{
    display:grid; grid-template-columns: 1fr 1fr; gap: 10px;
  }
  .compare .side{
    display:flex; flex-direction: column; gap: 6px;
    font-size: 11px; color: var(--muted);
    text-align:center;
  }
  .compare .side .pic{
    height: 150px;
    background: var(--soft);
    border-radius: 12px;
    position: relative;
    overflow: hidden;
  }
  .compare .side .pic::before{
    content:"";
    position:absolute; inset:0;
    background:
      linear-gradient(to top right, transparent 49.4%, var(--line) 49.4%, var(--line) 50.6%, transparent 50.6%),
      linear-gradient(to top left, transparent 49.4%, var(--line) 49.4%, var(--line) 50.6%, transparent 50.6%);
  }

  .info-table{
    display:flex; flex-direction: column;
    border: 1px solid var(--line);
    border-radius: 10px;
    overflow: hidden;
  }
  .info-table .tr{
    display:flex; justify-content:space-between;
    padding: 10px 12px;
    font-size: 12px;
    background: #fff;
    border-bottom: 1px solid var(--line);
  }
  .info-table .tr:last-child{ border-bottom:none; }
  .info-table .tr span:first-child{ color: var(--muted); }
  .info-table .tr span:last-child{ font-weight: 600; }

  .color-dots{
    display:flex; gap: 10px;
  }
  .color-dots .dot-c{
    width: 26px; height: 26px;
    border-radius: 50%;
    border: 1.5px solid var(--line);
    background: var(--soft);
  }
  .color-dots .dot-c.active{
    border: 2px solid var(--ink);
  }

  .size-row{
    display:flex; gap: 8px;
  }
  .size-chip{
    width: 40px; height: 40px;
    border: 1px solid var(--line);
    border-radius: 8px;
    display:flex; align-items:center; justify-content:center;
    font-size: 12px; font-weight: 600;
  }
  .size-chip.active{
    background: var(--dark); color:#fff; border-color: var(--dark);
  }

  .qty{
    display:flex; align-items:center; gap: 14px;
    border: 1px solid var(--line);
    border-radius: 8px;
    padding: 6px 12px;
    font-size: 13px;
    align-self: flex-start;
  }

  .price-large{
    font-size: 18px; font-weight: 700;
  }

  .cart-item{
    display:flex; gap: 10px; align-items:flex-start;
    padding-bottom: 12px;
    border-bottom: 1px solid var(--line);
  }
  .cart-item:last-of-type{ border-bottom: none; padding-bottom: 0; }
  .cart-item .pic{
    width: 60px; height:60px;
    background: var(--soft);
    border-radius: 10px;
    flex-shrink: 0;
    position: relative;
    overflow: hidden;
  }
  .cart-item .pic::before{
    content:"";
    position:absolute; inset:0;
    background:
      linear-gradient(to top right, transparent 49.4%, var(--line) 49.4%, var(--line) 50.6%, transparent 50.6%),
      linear-gradient(to top left, transparent 49.4%, var(--line) 49.4%, var(--line) 50.6%, transparent 50.6%);
  }
  .cart-item .body{ flex:1; display:flex; flex-direction:column; gap: 4px; }
  .cart-item .body h4{ font-size: 13px; font-weight: 600; }
  .cart-item .body .meta{ font-size: 11.5px; color: var(--muted); }
  .cart-item .body .line{
    display:flex; align-items:center; justify-content:space-between; margin-top:4px;
  }
  .cart-item .qty-mini{
    display:flex; align-items:center; gap: 8px;
    border: 1px solid var(--line);
    border-radius: 6px;
    padding: 3px 8px;
    font-size: 11.5px;
  }

  .totals{
    display:flex; flex-direction: column; gap: 6px;
    font-size: 12.5px;
    margin-top: 4px;
  }
  .totals .row{
    display:flex; justify-content:space-between;
  }
  .totals .row.total{
    font-weight: 700;
    font-size: 14px;
    padding-top: 8px;
    border-top: 1px dashed var(--line);
  }

  .radio-group{
    display:flex; flex-direction: column; gap: 8px;
  }
  .radio{
    display:flex; align-items:center; gap: 10px;
    font-size: 12.5px;
    padding: 10px 12px;
    border: 1px solid var(--line);
    border-radius: 10px;
  }
  .radio .dot{
    width: 16px; height: 16px; border-radius:50%;
    border: 1.5px solid var(--line);
    display:flex; align-items:center; justify-content:center;
  }
  .radio.active .dot{
    border-color: var(--dark);
  }
  .radio.active .dot::after{
    content:""; width: 8px; height: 8px; border-radius:50%;
    background: var(--dark);
  }

  .success-badge{
    width: 72px; height:72px; border-radius:50%;
    background: var(--soft);
    display:flex; align-items:center; justify-content:center;
    font-size: 32px; color: var(--dark);
    align-self: center;
  }

  .profile-head{
    display:flex; align-items:center; gap: 14px;
  }
  .avatar{
    width: 56px; height:56px; border-radius:50%;
    background: var(--soft);
    display:flex; align-items:center; justify-content:center;
    font-size: 22px;
  }

  .annotation{
    background: #fff8e6;
    border-left: 3px solid #f2b705;
    padding: 10px 14px;
    border-radius: 6px;
    font-size: 11.5px;
    color: #6b5a1b;
    line-height: 1.5;
  }
  .annotation strong{ color: #4a3c0a; }
</style>
</head>
<body>

  <h1 class="title">StyleLens — Conceptual Design Wireframe</h1>
  <p class="subtitle">Low-fidelity wireframe untuk marketplace AI (Fashion, Kosmetik, Aksesoris). Import ke Figma via plugin <b>html.to.design</b>.</p>

  <div class="grid">

    <!-- 01 LOGIN -->
    <div class="screen-wrap">
      <div class="screen-label">01 · Login / Register</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="content" style="justify-content:center; gap: 22px;">
          <div style="text-align:center;">
            <h2 style="font-size:22px; font-weight:700; letter-spacing:.06em;">STYLELENS</h2>
            <p style="font-size:12px; color:var(--muted); margin-top:6px;">AI Virtual Try-On Marketplace</p>
          </div>
          <div class="input-group">
            <label>Email</label>
            <div class="input">nama@email.com</div>
          </div>
          <div class="input-group">
            <label>Password</label>
            <div class="input">••••••••</div>
          </div>
          <div class="btn primary">MASUK</div>
          <div class="btn outline">DAFTAR AKUN BARU</div>
          <div style="text-align:center; font-size:11.5px; color:var(--muted);">atau lanjutkan dengan</div>
          <div class="btn outline">G · GOOGLE</div>
        </div>
      </div>
    </div>

    <!-- 02 HOME -->
    <div class="screen-wrap">
      <div class="screen-label">02 · Home</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="navbar">
          <div class="nav-left">STYLELENS</div>
          <div style="display:flex; gap:8px;">
            <div class="nav-icon">🔔</div>
            <div class="nav-icon">👤</div>
          </div>
        </div>
        <div class="content">
          <div class="search">🔍 Cari style, brand, produk…</div>
          <div class="banner">
            <h3>AI TRY-ON</h3>
            <p>See it before you buy — coba dulu, baru beli.</p>
            <div class="cta">COBA FITUR AI</div>
          </div>
          <div class="section-title">Kategori</div>
          <div class="chips">
            <div class="chip active">Fashion</div>
            <div class="chip">Kosmetik</div>
            <div class="chip">Aksesoris</div>
          </div>
          <div class="section-title">Rekomendasi AI untuk Kamu</div>
          <div class="thumb-row">
            <div class="thumb"></div>
            <div class="thumb"></div>
            <div class="thumb"></div>
          </div>
        </div>
        <div class="bottomnav">
          <div class="nav-item active"><div class="ic"></div>Home</div>
          <div class="nav-item"><div class="ic"></div>Search</div>
          <div class="nav-item"><div class="ic"></div>Camera</div>
          <div class="nav-item"><div class="ic"></div>Cart</div>
          <div class="nav-item"><div class="ic"></div>Profile</div>
        </div>
      </div>
    </div>

    <!-- 03 PRODUCT DETAIL -->
    <div class="screen-wrap">
      <div class="screen-label">03 · Product Detail</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="navbar">
          <div class="nav-icon">←</div>
          <div class="nav-title">Detail Produk</div>
          <div class="nav-icon">♡</div>
        </div>
        <div class="content">
          <div class="img-placeholder" style="height: 220px;"><span>Foto Produk</span></div>
          <div>
            <h3 style="font-size:16px; font-weight:700;">Casual T-Shirt</h3>
            <p style="font-size:12px; color:var(--muted); margin-top:2px;">★ 4.8 · 128 ulasan</p>
            <div class="price-large" style="margin-top:6px;">Rp 199.000</div>
          </div>
          <p style="font-size:12px; color:var(--muted); line-height:1.5;">T-shirt casual berbahan cotton combed 30s, nyaman dipakai sehari-hari.</p>
          <div>
            <div class="section-title" style="margin-bottom:6px;">Warna</div>
            <div class="color-dots">
              <div class="dot-c active"></div>
              <div class="dot-c"></div>
              <div class="dot-c"></div>
            </div>
          </div>
          <div>
            <div class="section-title" style="margin-bottom:6px;">Ukuran</div>
            <div class="size-row">
              <div class="size-chip">S</div>
              <div class="size-chip active">M</div>
              <div class="size-chip">L</div>
              <div class="size-chip">XL</div>
            </div>
          </div>
          <div class="btn primary" style="margin-top:auto;">TRY WITH AI</div>
          <div class="btn outline">TAMBAH KE KERANJANG</div>
        </div>
      </div>
    </div>

    <!-- 04 AI VIRTUAL FITTING INPUT -->
    <div class="screen-wrap">
      <div class="screen-label">04 · AI Virtual Fitting — Input</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="navbar">
          <div class="nav-icon">←</div>
          <div class="nav-title">AI Virtual Fitting</div>
          <div style="width:28px;"></div>
        </div>
        <div class="content" style="overflow:auto;">
          <div class="product-card">
            <div class="pic"></div>
            <div class="info">
              <h4>Casual T-Shirt</h4>
              <span>Rp 199.000</span>
            </div>
          </div>
          <div class="stepper">
            <span>Step 1 of 2</span>
            <div class="bar"><span></span></div>
          </div>
          <div class="section-title" style="letter-spacing:.05em;">MASUKKAN DATA TUBUH</div>
          <div class="input-group">
            <label>Tinggi Badan</label>
            <div class="input">Contoh: 170 cm</div>
          </div>
          <div class="input-group">
            <label>Berat Badan</label>
            <div class="input">Contoh: 65 kg</div>
          </div>
          <div class="input-group">
            <label>Lebar Dada</label>
            <div class="input">Contoh: 90 cm</div>
          </div>
          <div>
            <div class="section-title" style="margin-bottom:6px;">Jenis Kulit</div>
            <div class="chips">
              <div class="chip">Terang</div>
              <div class="chip active">Sedang</div>
              <div class="chip">Gelap</div>
            </div>
          </div>
          <div>
            <div class="section-title" style="margin-bottom:6px;">Upload Foto Tubuh</div>
            <div class="img-placeholder" style="height:110px;"><span>Upload Foto</span></div>
          </div>
          <div class="btn primary" style="margin-top:8px;">LANJUTKAN</div>
        </div>
      </div>
    </div>

    <!-- 05 AI VIRTUAL FITTING RESULT -->
    <div class="screen-wrap">
      <div class="screen-label">05 · AI Virtual Fitting — Result</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="navbar">
          <div class="nav-icon">←</div>
          <div class="nav-title">Hasil Virtual Fitting</div>
          <div style="width:28px;"></div>
        </div>
        <div class="content">
          <div class="img-placeholder" style="flex:1;">
            <span>AVATAR 3D + Outfit</span>
          </div>
          <div class="info-table">
            <div class="tr"><span>Rekomendasi Ukuran</span><span>M</span></div>
            <div class="tr"><span>Confidence</span><span>92%</span></div>
            <div class="tr"><span>Alasan</span><span>Tinggi 160 · Berat 50</span></div>
          </div>
          <div class="btn outline">COBA UKURAN LAIN</div>
          <div class="btn primary">TAMBAH KE KERANJANG</div>
        </div>
      </div>
    </div>

    <!-- 06 AI BEAUTY TRY-ON CAMERA -->
    <div class="screen-wrap">
      <div class="screen-label">06 · AI Beauty Try-On — Camera</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="navbar">
          <div class="nav-icon">←</div>
          <div class="nav-title">AI Beauty Try-On</div>
          <div style="width:28px;"></div>
        </div>
        <div class="content">
          <div class="camera-frame">
            <div class="corner c1"></div><div class="corner c2"></div>
            <div class="corner c3"></div><div class="corner c4"></div>
            <div class="face-oval">Posisikan wajah di dalam area ini</div>
          </div>
          <div class="section-title">AI DETECTION</div>
          <div class="check-list">
            <div class="check-item checked"><div class="box">✓</div>Warna Kulit</div>
            <div class="check-item checked"><div class="box">✓</div>Struktur Wajah</div>
            <div class="check-item"><div class="box"></div>Warna Bibir</div>
          </div>
          <p style="font-size:11.5px; color:var(--muted); text-align:center;">Pastikan wajah terlihat jelas dan berada dalam area kamera.</p>
          <div class="btn primary">BUKA KAMERA</div>
          <div class="btn outline">GUNAKAN FOTO</div>
        </div>
      </div>
    </div>

    <!-- 07 HASIL BEAUTY TRY-ON -->
    <div class="screen-wrap">
      <div class="screen-label">07 · AI Beauty Try-On — Result</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="navbar">
          <div class="nav-icon">←</div>
          <div class="nav-title">Hasil Beauty Try-On</div>
          <div style="width:28px;"></div>
        </div>
        <div class="content">
          <div class="section-title">PERBANDINGAN</div>
          <div class="compare">
            <div class="side"><div class="pic"></div>BEFORE</div>
            <div class="side"><div class="pic"></div>AFTER</div>
          </div>
          <div>
            <h4 style="font-size:14px; font-weight:700;">Lipstick Nude</h4>
            <p style="font-size:12px; color:var(--muted);">Warna: Natural Nude</p>
          </div>
          <div class="info-table">
            <div class="tr"><span>Warna Kulit</span><span>Terang</span></div>
            <div class="tr"><span>Warna Produk</span><span>Natural Nude</span></div>
            <div class="tr"><span>Kompatibilitas</span><span>Sesuai ✓</span></div>
          </div>
          <div class="btn primary" style="margin-top:auto;">LIHAT DETAIL PRODUK</div>
          <div class="btn outline">TAMBAH KE KERANJANG</div>
        </div>
      </div>
    </div>

    <!-- 08 AI MIRROR TRY-ON -->
    <div class="screen-wrap">
      <div class="screen-label">08 · AI Mirror Try-On</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="navbar">
          <div class="nav-icon">←</div>
          <div class="nav-title">AI Mirror Try-On</div>
          <div style="width:28px;"></div>
        </div>
        <div class="content">
          <div class="camera-frame">
            <div class="corner c1"></div><div class="corner c2"></div>
            <div class="corner c3"></div><div class="corner c4"></div>
            <div class="live-badge">LIVE</div>
            <div class="face-oval">Overlay aksesori di wajah</div>
          </div>
          <div class="section-title">Pilih Aksesori</div>
          <div class="chips">
            <div class="chip">Kacamata</div>
            <div class="chip active">Anting</div>
            <div class="chip">Kalung</div>
          </div>
          <div class="info-table">
            <div class="tr"><span>Wajah Terdeteksi</span><span>✓</span></div>
            <div class="tr"><span>Posisi Aksesori</span><span>Sesuai</span></div>
          </div>
          <div class="btn primary" style="margin-top:auto;">AMBIL FOTO</div>
          <div class="btn outline">TAMBAH KE KERANJANG</div>
        </div>
      </div>
    </div>

    <!-- 09 CART -->
    <div class="screen-wrap">
      <div class="screen-label">09 · Cart</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="navbar">
          <div class="nav-icon">←</div>
          <div class="nav-title">Keranjang</div>
          <div style="width:28px;"></div>
        </div>
        <div class="content">
          <div class="cart-item">
            <div class="pic"></div>
            <div class="body">
              <h4>Casual T-Shirt</h4>
              <div class="meta">Ukuran M</div>
              <div class="line">
                <strong style="font-size:12.5px;">Rp 199.000</strong>
                <div class="qty-mini">- 1 +</div>
              </div>
            </div>
          </div>
          <div class="cart-item">
            <div class="pic"></div>
            <div class="body">
              <h4>Classic Sunglasses</h4>
              <div class="meta">Round Frame</div>
              <div class="line">
                <strong style="font-size:12.5px;">Rp 259.000</strong>
                <div class="qty-mini">- 1 +</div>
              </div>
            </div>
          </div>
          <div class="divider"></div>
          <div class="totals">
            <div class="row"><span>Subtotal</span><span>Rp 458.000</span></div>
            <div class="row"><span>Ongkos Kirim</span><span>Rp 15.000</span></div>
            <div class="row total"><span>Total</span><span>Rp 473.000</span></div>
          </div>
          <div class="btn primary" style="margin-top:auto;">CHECKOUT</div>
        </div>
      </div>
    </div>

    <!-- 10 CHECKOUT -->
    <div class="screen-wrap">
      <div class="screen-label">10 · Checkout</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="navbar">
          <div class="nav-icon">←</div>
          <div class="nav-title">Checkout</div>
          <div style="width:28px;"></div>
        </div>
        <div class="content" style="overflow:auto;">
          <div class="section-title">Alamat Pengiriman</div>
          <div class="input-group">
            <div class="input" style="height:auto; padding:10px 12px; line-height:1.5; display:block;">
              Salsa Amelia<br>0812-xxxx-xxxx<br>Jl. Merdeka No. 10, Jakarta
            </div>
          </div>
          <div class="section-title">Metode Pengiriman</div>
          <div class="radio-group">
            <div class="radio active"><div class="dot"></div>Reguler · Rp 15.000</div>
            <div class="radio"><div class="dot"></div>Express · Rp 25.000</div>
          </div>
          <div class="section-title">Metode Pembayaran</div>
          <div class="radio-group">
            <div class="radio active"><div class="dot"></div>Transfer Bank</div>
            <div class="radio"><div class="dot"></div>E-Wallet</div>
            <div class="radio"><div class="dot"></div>COD</div>
          </div>
          <div class="divider"></div>
          <div class="totals">
            <div class="row total"><span>Total Bayar</span><span>Rp 473.000</span></div>
          </div>
          <div class="btn primary" style="margin-top:auto;">BAYAR</div>
        </div>
      </div>
    </div>

    <!-- 11 PAYMENT STATUS -->
    <div class="screen-wrap">
      <div class="screen-label">11 · Payment Status</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="navbar">
          <div style="width:28px;"></div>
          <div class="nav-title">Status Pembayaran</div>
          <div style="width:28px;"></div>
        </div>
        <div class="content" style="justify-content:center; gap:18px;">
          <div class="success-badge">✓</div>
          <h3 style="text-align:center; font-size:16px; font-weight:700;">Pembayaran Berhasil</h3>
          <p style="text-align:center; font-size:12px; color:var(--muted);">Pesanan kamu sedang diproses</p>
          <div class="info-table">
            <div class="tr"><span>Order ID</span><span>SL-2024-0001</span></div>
            <div class="tr"><span>Total</span><span>Rp 473.000</span></div>
            <div class="tr"><span>Metode</span><span>Transfer Bank</span></div>
          </div>
          <div class="btn primary">LACAK PESANAN</div>
          <div class="btn outline">KEMBALI KE HOME</div>
        </div>
      </div>
    </div>

    <!-- 12 PROFILE -->
    <div class="screen-wrap">
      <div class="screen-label">12 · Profile</div>
      <div class="screen">
        <div class="statusbar"><span>9:41</span><div class="icons"><span class="dot"></span><span class="dot"></span><span class="dot"></span></div></div>
        <div class="navbar">
          <div class="nav-icon">←</div>
          <div class="nav-title">Profil</div>
          <div style="width:28px;"></div>
        </div>
        <div class="content" style="overflow:auto;">
          <div class="profile-head">
            <div class="avatar">👤</div>
            <div>
              <h3 style="font-size:15px; font-weight:700;">Salsa Amelia</h3>
              <p style="font-size:12px; color:var(--muted);">Mahasiswa · 20 tahun</p>
            </div>
          </div>
          <div class="section-title">Data Tubuh</div>
          <div class="info-table">
            <div class="tr"><span>Tinggi</span><span>160 cm</span></div>
            <div class="tr"><span>Berat</span><span>50 kg</span></div>
            <div class="tr"><span>Lebar Dada</span><span>85 cm</span></div>
            <div class="tr"><span>Jenis Kulit</span><span>Sedang</span></div>
          </div>
          <div class="section-title">Preferensi</div>
          <div class="chips">
            <div class="chip active">Fashion</div>
            <div class="chip active">Kosmetik</div>
            <div class="chip">Aksesoris</div>
          </div>
          <div class="section-title">Privasi & Keamanan</div>
          <div class="info-table">
            <div class="tr"><span>Izin Kamera</span><span>Aktif</span></div>
            <div class="tr"><span>Simpan Data Tubuh</span><span>Aktif</span></div>
          </div>
          <div class="btn outline" style="margin-top:auto;">LOGOUT</div>
        </div>
      </div>
    </div>

  </div>

</body>
</html>
