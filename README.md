<!doctype html>
<html lang="id">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>DEWA4EXCHANGE — Rill Market (EDUKASI)</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&family=Orbitron:wght@500;800&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#071018; --card:#0b151b; --muted:#9fb0b8; --accent:#00d084; --accent-2:#00eaff; --danger:#ff4666;
    /* Neon Colors */
    --neon-main: #00eaff;
    --neon-glow: rgba(0, 234, 255, 0.7);
    --neon-shadow: 0 0 5px var(--neon-glow), 0 0 10px var(--neon-glow), 0 0 20px var(--neon-glow);
  }
  *{box-sizing:border-box}
  body{margin:0;font-family:'Inter', system-ui, Arial;background:linear-gradient(180deg,var(--bg),#02060a);color:#e6eef2;-webkit-font-smoothing:antialiased}
  a{color:inherit}

  /* Keyframes untuk Animasi Splash */
  @keyframes neon-pulse {
      0%, 100% { text-shadow: var(--neon-shadow); transform: scale(1.0) translateY(0); }
      50% { text-shadow: 0 0 8px var(--neon-glow), 0 0 15px var(--neon-glow), 0 0 25px rgba(0, 234, 255, 0.5); transform: scale(1.02) translateY(-2px); }
  }
  @keyframes gradient-bg {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-5px); }
  }
  
  /* SPLASH SCREEN BARU */
  .intro{
    position:fixed;
    inset:0;
    display:flex;
    align-items:center;
    justify-content:center;
    flex-direction:column;
    /* Gradasi Animasi Background */
    background: linear-gradient(180deg, #02060a 0%, #071018 50%, #02060a 100%);
    z-index:9999;
    transition: opacity 0.5s ease-out; /* Untuk transisi halus */
  }
  .splash-text-wrap {
      text-align: center;
      line-height: 0.9;
      color: var(--neon-main);
      font-family: 'Orbitron', sans-serif;
      animation: float 4s ease-in-out infinite; /* Animasi pelan */
  }
  .splash-main-text {
      font-weight: 800;
      font-size: 32px;
      animation: neon-pulse 1.8s ease-in-out infinite alternate;
  }
  .splash-sub-text {
      font-weight: 500;
      font-size: 16px;
      letter-spacing: 4px;
      margin-top: 5px;
  }
  .splash-logo-placeholder {
      width: 110px;
      height: 110px;
      border-radius: 18px;
      /* Background untuk Placeholder Logo */
      background: linear-gradient(135deg, var(--accent-2), var(--accent));
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 800;
      font-size: 28px;
      color: #021;
      margin-top: 20px;
      box-shadow: var(--neon-shadow); /* Efek glow ringan */
  }
  /* END SPLASH */


  /* layout */
  .app{max-width:980px;margin:0 auto;padding-bottom:88px}
  header.main{display:flex;align-items:center;justify-content:space-between;padding:12px 16px;background:transparent;position:sticky;top:0;z-index:50}
  .brand{font-weight:800;letter-spacing:1px;color:var(--accent-2)}
  .search{flex:1;margin:0 12px}
  .btn{background:transparent;border:1px solid rgba(255,255,255,0.04);padding:8px 10px;border-radius:10px;color:var(--muted);cursor:pointer;transition: all 0.3s ease;}
  .btn-primary{background:var(--accent);color:#021;border:none}
  .card{background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);padding:12px;border-radius:10px;margin:12px;border:1px solid rgba(255,255,255,0.03)}
  .grid{display:grid;grid-template-columns:1fr;gap:12px}
  .market-top{height:320px;background:#07121a;border-radius:10px;overflow:hidden}
  .chart-wrap{width:100%;height:100%}
  .small{font-size:13px;color:var(--muted)}
  .pill{background:rgba(255,255,255,0.02);padding:6px 10px;border-radius:8px;color:var(--muted);font-size:13px}
  /* bottom nav */
  .bottom-nav{position:fixed;right:0;left:0;bottom:0;height:64px;background:linear-gradient(180deg,#07121a,#041018);display:flex;align-items:center;justify-content:space-around;border-top:1px solid rgba(255,255,255,0.03);z-index:60}
  .nav-item{display:flex;flex-direction:column;align-items:center;justify-content:center;color:var(--muted);font-size:12px}
  .nav-item.active{color:var(--accent-2)}
  /* responsive */
  @media(min-width:900px){
    .app{padding:18px}
    .grid{grid-template-columns: 1fr 420px}
    .market-top{height:420px}
  }
  /* forms */
  input,select,textarea{background:transparent;border:1px solid rgba(255,255,255,0.03);padding:10px;border-radius:8px;color:#e6eef2;width:100%;outline:none}
  .mutasi{max-height:220px;overflow:auto;padding:6px}
  .positions{max-height:220px;overflow:auto;padding:6px}
  
  /* LOGIN MODAL BARU */
  #loginModal{
    display:none;
    position:fixed;
    inset:0;
    background:rgba(0,0,0,0.8); /* Background gelap untuk fokus */
    align-items:center;
    justify-content:center;
    z-index:999;
    transition: opacity 0.4s ease-in;
  }
  .login-card{
    background: linear-gradient(145deg, #051a1a, #010808); /* Gradasi hijau tua/gelap */
    padding: 24px;
    border-radius: 16px;
    width: 90%;
    max-width: 380px;
    border: 1px solid rgba(0, 234, 255, 0.1);
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5);
  }
  .login-logo-sm {
      width: 40px;
      height: 40px;
      margin: 0 auto 10px;
      border-radius: 8px;
      background: linear-gradient(135deg, var(--accent-2), var(--accent));
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 800;
      font-size: 18px;
      color: #021;
      box-shadow: 0 0 8px rgba(0, 234, 255, 0.4);
  }
  .login-title{
      text-align: center;
      font-family: 'Orbitron', sans-serif;
      color: var(--neon-main);
      font-size: 20px;
      font-weight: 800;
      text-shadow: 0 0 5px var(--neon-glow);
      margin-bottom: 20px;
  }
  .btn-modern {
      padding: 10px 15px;
      border-radius: 20px; /* Lebih rounded */
      font-weight: 600;
      border: none;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
  }
  .btn-login-primary {
      background: var(--accent);
      color: #021;
      border: 1px solid var(--accent);
  }
  .btn-login-primary:hover {
      background: #00ff99;
      box-shadow: 0 0 15px #00ff99; /* Glowing */
  }
  .btn-register {
      background: transparent;
      color: var(--neon-main);
      border: 1px solid var(--neon-main);
  }
  .btn-register:hover {
      background: rgba(0, 234, 255, 0.1);
      box-shadow: 0 0 10px var(--neon-glow); /* Glowing */
  }
  /* END LOGIN MODAL */
  
  /* helper colors */
  .pnl-pos{color:var(--accent);font-weight:800}
  .pnl-neg{color:var(--danger);font-weight:800}
  /* custom PNL colors */
  .pnl-green{color:#00FF00;font-weight:800}
  .pnl-red{color:#FF4747;font-weight:800}
  .pnl-neutral{color:#e6eef2;font-weight:800}
  /* compact */
  .row{display:flex;gap:8px;align-items:center}
  .col{flex:1}
  .mini{font-size:12px;color:var(--muted)}
  .logo-sm{width:34px;height:34px;border-radius:8px;background:linear-gradient(135deg,var(--accent-2),var(--accent));display:flex;align-items:center;justify-content:center;font-weight:800}
  
  /* --- NEW HOME CSS --- */
  .home-profile {
      padding: 20px;
      display: flex;
      justify-content: center;
  }
  .home-card {
      background: linear-gradient(145deg, #0a1b12, #0d2a1b);
      padding: 22px;
      border-radius: 14px;
      width: 90%;
      max-width: 500px;
      box-shadow: 0 0 18px rgba(0,255,128,0.25);
      border: 1px solid rgba(0,255,120,0.3);
  }
  .home-avatar {
      width: 80px;
      height: 80px;
      object-fit: cover;
      border-radius: 50%;
      border: 3px solid #00ff80;
      box-shadow: 0 0 15px rgba(0,255,128,0.5);
      margin-bottom: 15px;
      margin-left: auto;
      margin-right: auto;
      display: block; /* Agar margin auto bekerja */
  }
  .home-info {
      text-align: center;
  }
  .home-name {
      font-size: 22px;
      font-weight: bold;
      color: #00ff95;
  }
  .home-role {
      font-size: 14px;
      opacity: 0.7;
  }
  .home-desc {
      font-size: 14px;
      margin-top: 10px;
      opacity: 0.8;
      line-height: 1.6;
  }
  /* --- END NEW HOME CSS --- */
  
  /* --- ADDED MARKET CSS (TUGAS 1) --- */
  #market-chart-container {
      animation: fadeIn 0.4s ease-in-out;
  }
  @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
  }
  /* --- END ADDED MARKET CSS --- */

/* --- START ADDED TOP MOVERS CSS (TUGAS 2) --- */
.top-movers {
    margin-top: 20px;
    padding: 15px;
    background: #0d1117;
    border-radius: 12px;
}

.title-tm {
    color: #ffffff;
    font-size: 18px;
    margin-bottom: 15px;
    font-weight: bold;
}

.mover-item {
    margin-bottom: 15px;
}

.mover-header {
    display: flex;
    justify-content: space-between;
    color: #fff;
    font-size: 14px;
    margin-bottom: 5px;
}

.mover-bar {
    width: 100%;
    height: 8px;
    border-radius: 8px;
    transition: width 0.15s linear;
}

.mover-green {
    background: #0ecb81;
}

.mover-red {
    background: #f6465d;
}
/* --- END ADDED TOP MOVERS CSS (TUGAS 2) --- */
</style>
</head>
<body>

<div id="intro" class="intro">
  <div class="splash-logo-placeholder">D4</div>
  
  <div class="splash-text-wrap">
    <div class="splash-main-text">DEWA4</div>
    <div class="splash-sub-text">EXCHANGE</div>
  </div>
  <small style="margin-top:20px; color:var(--muted)">Loading Rill Market...</small>
</div>
<div class="app" id="app" style="display:none">
  <header class="main">
    <div style="display:flex;align-items:center;gap:12px">
      <div class="logo-sm">D4</div>
      <div class="brand">DEWA4EXCHANGE</div>
    </div>
    <div style="display:flex;gap:8px;align-items:center">
      <div class="pill" id="uiNet">Rp 0</div>
      <button id="loginBtnTop" class="btn">Login ▾</button>
    </div>
  </header>

  <main id="mainContent">
    </main>

</div>

<nav class="bottom-nav" id="bottomNav" style="display:none">
  <div class="nav-item active" data-page="home" onclick="navTo('home')">
    <div>🏠</div><div>Beranda</div>
  </div>
  <div class="nav-item" data-page="market" onclick="navTo('market')">
    <div>📈</div><div>Pasar</div>
  </div>
  <div class="nav-item" data-page="trade" onclick="navTo('trade')">
    <div>⚡</div><div>Perdagangan</div>
  </div>
  <div class="nav-item" data-page="futures" onclick="navTo('futures')">
    <div>📊</div><div>Futures</div>
  </div>
  <div class="nav-item" data-page="wallet" onclick="navTo('wallet')">
    <div>👛</div><div>Aset</div>
  </div>
</nav>

<div id="loginModal">
  <div class="login-card">
    <div class="login-logo-sm">D4</div>
    <div class="login-title">DEWA4EXCHANGE</div>
    <div class="small" style="text-align:center;margin-top:-10px">Akun tersimpan di browser (localStorage) — edukasi saja.</div>
    <div style="margin-top:16px">
      <input id="loginUser" placeholder="Username">
      <input id="loginPass" placeholder="Password" type="password" style="margin-top:12px">
      <div style="display:flex;gap:10px;margin-top:20px">
        <button class="btn-modern btn-login-primary" id="doLogin" style="flex:1">MASUK</button>
        <button class="btn-modern btn-register" id="doRegister" style="flex:1">DAFTAR</button>
      </div>
      <div style="display:flex;gap:8px;margin-top:10px">
        <button class="btn" id="closeLogin" style="flex:1;background:rgba(255,255,255,0.05)">Tutup</button>
        <button class="btn" id="quickGuest" style="flex:1;background:rgba(0, 234, 255, 0.1);color:var(--neon-main)">Quick Guest</button>
      </div>
      <div class="mini" style="margin-top:10px;text-align:center">Tip: Gunakan Quick Guest untuk mencoba simulasi dengan cepat.</div>
    </div>
  </div>
</div>

<script src="https://s3.tradingview.com/tv.js"></script>
<script>
let tvWidget = null;

function loadMarketChart(pair) {
    // Mapping pair default (dari instruksi)
    const symbolMap = {
        "BTCUSD": "BINANCE:BTCUSDT",
        "ETHUSD": "BINANCE:ETHUSDT",
        "BNBUSD": "BINANCE:BNBUSDT",
        "SOLUSD": "BINANCE:SOLUSDT",
        "XRPUSD": "BINANCE:XRPUSDT",
    };
    const symbol = symbolMap[pair] || "BINANCE:BTCUSDT";

    if (tvWidget) {
        // Hapus widget lama sebelum membuat yang baru jika ada (sebelum TradingView.widget yang baru)
        if (tvWidget.remove) {
            tvWidget.remove();
        }
    }
    
    // Inisialisasi TradingView.widget yang baru
    tvWidget = new TradingView.widget({
        "width": "100%",
        "height": 420,
        "symbol": symbol, // Menggunakan symbol yang sudah di-map
        "interval": "1",
        "timezone": "Asia/Jakarta",
        "theme": "dark",
        "style": "1",
        "locale": "id",
        "toolbar_bg": "#0d1117", // Agar serasi dengan background dark
        "enable_publishing": false,
        "allow_symbol_change": true, // Perlu di set true
        "container_id": "marketChart"
    });
}

document.addEventListener("DOMContentLoaded", function () {
    // Memastikan TradingView diinisialisasi setelah DOMContentLoaded
    // Fungsi ini akan dipanggil ulang di renderMarket()
    // loadMarketChart("BTCUSD"); // Komentar/hapus karena akan dipanggil di renderMarket()
});
</script>
<script>
/* ========== CONFIG ========== */
const FX_IDR_PER_USD = 15000;
// 1. Ubah semua saldo awal menjadi 0
const DEFAULT_BAL = 0; // default Rill balance for new users
const STORAGE_USERS = 'db_Rill_users';
const STORAGE_CUR = 'db_Rill_current';
const PAIRS = ['BTC/USDT','ETH/USDT','TSLA:NASDAQ','SPX:INDEX','BTCUSD'];
const MIN_DEPOSIT = 100000; // Minimal deposit Rp100.000 (untuk instruksi 3)

/* ========== HELPERS ========== */
const $ = id => document.getElementById(id);
function fmtRp(x){ return 'Rp ' + Number(x).toLocaleString('id-ID'); }
function toast(msg, t=2200){ const d=document.createElement('div'); d.style.position='fixed';d.style.right='12px';d.style.bottom='82px';d.style.background='rgba(0,0,0,0.75)';d.style.padding='8px 12px';d.style.borderRadius='8px';d.style.color='#fff';d.textContent=msg;document.body.appendChild(d); setTimeout(()=>d.remove(),t); }

/* localStorage users */
function loadUsers(){ try { return JSON.parse(localStorage.getItem(STORAGE_USERS)||'{}'); } catch(e){ return {}; } }
// 4. Pastikan saldo tersimpan di localStorage per user (saldo tidak berubah ke user lain).
// Fungsi saveUsers/loadUsers sudah bekerja dengan benar.
function saveUsers(u){ localStorage.setItem(STORAGE_USERS, JSON.stringify(u)); }
function setCurrent(u){ localStorage.setItem(STORAGE_CUR, u||''); }
function getCurrent(){ return localStorage.getItem(STORAGE_CUR) || ''; }

/* PNL calculation */
function calcPnl(position, currentPrice){
  let diff = 0;
  if(position.side === 'Buy'){
    diff = currentPrice - position.entryPrice;
  } else { // Sell
    diff = position.entryPrice - currentPrice;
  }
  const pnlUSD = diff * position.units * position.leverage;
  const pnlIDR = Math.round(pnlUSD * FX_IDR_PER_USD);
  const pnlPercent = (pnlUSD / (position.amountIDR / (position.entryPrice * FX_IDR_PER_USD)) / position.leverage) * 100;
  return { pnlUSD, pnlIDR, pnlPercent };
}
function getPnlColorClass(pnlIDR){
  if(pnlIDR > 0) return 'pnl-green';
  if(pnlIDR < 0) return 'pnl-red';
  return 'pnl-neutral';
}
function fmtPnlPercent(pnlPercent){
  const sign = pnlPercent >= 0 ? '+' : '';
  return `(${sign}${pnlPercent.toFixed(2)}%)`;
}

/* ========== SIM PRICES (fallback) ========== */
const simSeries = {}; const volMap = {'BTC/USDT':700,'ETH/USDT':30,'TSLA:NASDAQ':2,'SPX:INDEX':1,'BTCUSD':700};
const baseMap = {'BTC/USDT':85000,'ETH/USDT':3400,'TSLA:NASDAQ':320,'SPX:INDEX':4300,'BTCUSD':85000};
function genSim(pair){
  const arr=[]; let p = baseMap[pair]||100;
  for(let i=0;i<200;i++){ const o=p+(Math.random()-0.5)*(volMap[pair]||1); const c=o+(Math.random()-0.5)*(volMap[pair]||1); arr.push({o,c,h:Math.max(o,c)+Math.random(),l:Math.min(o,c)-Math.random()}); p=c; }
  simSeries[pair]=arr;
}
PAIRS.forEach(p=>genSim(p));

/* Try fetch price from Binance (only for symbols like BINANCE:BTCUSDT) */
async function fetchPriceBinance(symbol){
  try{
    const s = symbol.replace(/.*:/,'');
    const r = await fetch('https://api.binance.com/api/v3/ticker/price?symbol=' + s);
    if(!r.ok) return null;
    const j = await r.json(); return Number(j.price);
  }catch(e){return null;}
}

/* get price (prefers remote for crypto when priceMode=realtime) */
async function getPrice(pair){
  const map = {'BTC/USDT':'BINANCE:BTCUSDT','ETH/USDT':'BINANCE:ETHUSDT','BTCUSD':'COINBASE:BTCUSD','TSLA:NASDAQ':'NASDAQ:TSLA','SPX:INDEX':'INDEX:SPX'};
  const sym = map[pair] || pair;
  if(window.priceMode === 'realtime' && (sym.includes('BINANCE'))){
    const r = await fetchPriceBinance(sym);
    if(r) return r;
  }
  const s = simSeries[pair]; const last = s[s.length-1]; return (last.o + last.c)/2;
}

/* ========== UI: SPA Navigation ========== */
let currentPage = 'home';
window.priceMode = 'sim'; // sim or realtime
const mainContent = $('mainContent');

function navTo(page){
  currentPage = page;
  // update bottom nav active
  document.querySelectorAll('.nav-item').forEach(n=> n.classList.toggle('active', n.dataset.page === page));
  renderPage(page);
}

/* ========== PAGES ========== */
async function renderPage(page){
  if(page==='home') return renderHome();
  if(page==='market') return renderMarket();
  if(page==='trade') return renderTrade();
  if(page==='futures') return renderFutures();
  if(page==='wallet') return renderWallet();
}

/* HOME */
function renderHome(){
  // START MODIFIED HOME CONTENT
  mainContent.innerHTML = `
    <div class="home-profile">
        <div class="home-card">
            <img src="https://i.ibb.co.com/Y43GswQS/Screenshot-20251202-184042-Gallery.jpg"
     alt="CEO Dewa Exchange"
     style="
        width: 120px;
        height: 120px;
        border-radius: 50%;
        object-fit: cover;
        display: block;
        margin: 0 auto;
        border: 3px solid #00FF80;
        box-shadow: 0 0 15px #00FF80;
     ">
            <div class="home-info">
                <div class="home-name">Dewangga</div>
                <div class="home-role">Founder & CEO — D4EXCHANGE</div>
                <div class="home-desc">
                    Selamat datang di D4EXCHANGE — Platform edukasi trading modern 
                    dengan tampilan premium ala Bloomberg.
                </div>
            </div>
        </div>
    </div>
    <div class="grid" style="margin-top:12px; display:none;">
      <div>
        <div class="card" id="hiddenHomeCard1">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div>
              <div class="small">Market</div>
              <div style="font-weight:800" id="marketLabelHome">BTC/USDT</div>
            </div>
            <div style="text-align:right">
              <div id="priceMainHome" style="font-size:20px;font-weight:800">--</div>
              <div class="small" id="subPriceHome">--</div>
            </div>
          </div>
          <div style="height:220px;margin-top:10px;background:#07121a;border-radius:10px;overflow:hidden" id="homeChartWrap">
            </div>
          <div style="display:flex;gap:8px;margin-top:10px;align-items:center">
            <div class="pill" id="hlInfoHome">H:- • L:-</div><div style="flex:1"></div><div class="small">Mode: <strong id="modeLabelHome"></strong></div>
          </div>
        </div>
        <div class="card" id="quickTradeCardHidden">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div><div class="small">Quick Trade</div><div style="font-weight:800" id="qt_pair">BTC/USDT</div></div>
            <div><button class="btn btn-primary" onclick="navTo('trade')">Go to Trade</button></div>
          </div>
          <div style="margin-top:10px" class="small">Contoh Rill: lihat potensi PnL untuk <b>0.01 unit</b> (0.01 lot) di panel Trade.</div>
        </div>
      </div>
      <div>
        <div class="card" id="sideBalanceCard">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div><div class="small">Saldo</div><div id="sideBalance" style="font-weight:800">Rp 0</div></div>
            <div><button class="btn" id="openDepBtnSide">Deposit</button></div>
          </div>
          <div style="margin-top:12px">
            <div class="small">Open Positions</div>
            <div class="positions" id="sidePositions">Belum ada posisi</div>
          </div>
        </div>
        <div class="card" id="sideMutasiCard">
          <div class="small">Riwayat / Mutasi</div>
          <div class="mutasi" id="sideMutasi">Belum ada mutasi</div>
        </div>
      </div>
    </div>
  `;
  // END MODIFIED HOME CONTENT
  // set initial chart embed for home (use same as market but smaller)
  // Menjaga agar elemen ID yang digunakan oleh JS lain tetap ada (meskipun disembunyikan) dan fungsinya tetap dipanggil.
  initTViframe('BTC/USDT', 'homeChartWrap');
  updateMarketHeaderDisplays('BTC/USDT');
  bindSideButtons();
  renderPositionsUI('sidePositions');
}

/* MARKET page */
// Kode inisialisasi TradingView lama dihapus dan diganti dengan loadMarketChart
let currentTVSymbol = '';
function initTViframe(pair, targetId){
  // initTViframe (hanya digunakan untuk chart di Beranda)
  const tvmap = {'BTC/USDT':'BINANCE:BTCUSDT','ETH/USDT':'BINANCE:ETHUSDT','BTCUSD':'COINBASE:BTCUSD','TSLA:NASDAQ':'NASDAQ:TSLA','SPX:INDEX':'OANDA:SPX'};
  const sym = tvmap[pair] || 'BINANCE:BTCUSDT';
  if(currentTVSymbol === sym && document.getElementById(targetId)) return;
  currentTVSymbol = sym;
  // TradingView embed with correct parameters for stability
  const iframe = `<iframe src="https://s.tradingview.com/widgetembed/?symbol=${encodeURIComponent(sym)}&interval=60&theme=dark&style=1&timezone=Asia%2FJakarta&toolbar_bg=f1f3f6&allow_symbol_change=1&save_image=1&locale=id" style="width:100%;height:100%;border:0"></iframe>`;
  const target = document.getElementById(targetId);
  if(target) target.innerHTML = iframe;
}

async function renderMarket(){
  mainContent.innerHTML = `
    <div class="grid">
      <div>
        <div class="card market-top" style="height:420px; padding:0; border:none; background:transparent;">
          <div id="market-chart-container" style="width:100%; height:420px; border-radius:14px; overflow:hidden; background:#0a0f12;">
              <div id="marketChart"></div>
          </div>
        </div>
        <div class="card" style="margin-top:12px">
          <div style="display:flex;gap:8px;align-items:center">
            <label class="small">Pair:</label>
            <select id="marketPair" onchange="loadMarketChart(this.value); updateMarketHeaderDisplays(this.value); renderMarketSnapshot(this.value);">
                <option value="BTCUSD">BTC/USDT</option>
                <option value="ETHUSD">ETH/USDT</option>
                <option value="BNBUSD">BNB/USDT</option>
                <option value="SOLUSD">SOL/USDT</option>
                <option value="XRPUSD">XRP/USDT</option>
            </select>
            <div style="flex:1"></div>
            <label class="small">Mode:</label>
            <select id="modeSelectMarket"><option value="sim">Simulasi</option><option value="realtime">Realtime</option></select>
          </div>
          <div style="margin-top:10px" class="small">Ganti pair untuk memuat chart TradingView.</div>
        </div>

        <div class="card" style="margin-top:12px">
          <div class="small">Market snapshot / contoh perhitungan</div>
          <div style="margin-top:8px" id="marketSnapshot">--</div>
        </div>
      </div>

      <div>
        <div class="card" style="margin-top:12px">
          <div class="top-movers fast-movers">
              <h3 class="title-tm">Top Movers</h3>
              <div id="topMoversList"></div>
          </div>
        </div>
        <div class="card" style="margin-top:12px">
          <div class="small">Penjelasan lot & PnL (contoh)</div>
          <div class="small" style="margin-top:8px">Formula PnL: <code>pnl = units × (price_now - entry_price) × leverage</code></div>
          <div style="margin-top:8px" id="lotHelp">Contoh: 0.01 unit → perubahan harga 100 USD dengan leverage 1 memberi PnL = 0.01 × 100 × 1 = 1 USD</div>
        </div>
      </div>
    </div>
  `;
  // set events
  const initialPair = 'BTCUSD'; // Gunakan BTCUSD sebagai default untuk TradingView baru
  
  // Set nilai awal dropdown dan panggil chart
  $('marketPair').value = initialPair;
  loadMarketChart(initialPair);
  
  $('modeSelectMarket').value = window.priceMode;
  
  // Update header dan snapshot menggunakan pair yang sudah di-map (BTC/USDT)
  updateMarketHeaderDisplays('BTC/USDT'); 
  renderMarketSnapshot('BTC/USDT');
  
  // Event handler untuk mode (tetap menggunakan pair Sim/Realtime di logic lama)
  $('modeSelectMarket').onchange = function(){ 
    window.priceMode = this.value; 
    toast('Mode: '+this.value); 
    // Menggunakan pair default dari logic lama untuk display di header
    updateMarketHeaderDisplays('BTC/USDT'); 
    renderMarketSnapshot('BTC/USDT');
  };
}

/* MARKET snapshot */
async function renderMarketSnapshot(pair){
  const price = await getPrice(pair);
  const last = simSeries[pair][simSeries[pair].length-1];
  $('marketSnapshot').innerHTML = `<div style="display:flex;justify-content:space-between"><div style="font-weight:800">${pair}</div><div>${Number(price).toLocaleString()}</div></div>
    <div class="small">H: ${last.h.toFixed(2)} • L: ${last.l.toFixed(2)}</div>`;
}

/* TRADE page */
function renderTrade(){
  mainContent.innerHTML = `
    <div class="grid">
      <div>
        <div class="card">
          <div class="small">ORDER — Open Position (Rill)</div>
          <div style="display:flex;gap:8px;margin-top:8px">
            <div style="flex:1">
              <label class="small">Pair</label>
              <select id="pairSelectTrade">${PAIRS.map(p=>`<option>${p}</option>`).join('')}</select>
            </div>
            <div style="width:120px">
              <label class="small">Leverage</label>
              <select id="leverageTrade"><option>1</option><option>2</option><option>5</option><option>10</option></select>
            </div>
          </div>

          <div style="display:flex;gap:8px;margin-top:8px">
            <div style="flex:1">
              <label class="small">Input</label>
              <select id="inputModeTrade"><option value="nominal">Nominal (IDR)</option><option value="units">Units</option></select>
            </div>
            <div style="width:140px">
              <label class="small">Amount</label>
              <input id="openAmountTrade" placeholder="Contoh: 200000">
            </div>
          </div>

          <div style="display:flex;gap:8px;margin-top:12px">
            <button class="btn btn-primary" id="btnBuyTrade">Buy</button>
            <button class="btn" id="btnSellTrade">Sell</button>
            <div style="flex:1"></div>
            <div class="small" id="tradePriceInfo">--</div>
          </div>

          <div style="margin-top:10px" class="small">Estimasi PnL untuk 0.01 unit: <span id="estPnl">--</span></div>
        </div>

        <div class="card" style="margin-top:12px">
          <div class="small">Open Positions</div>
          <div class="positions" id="tradePositions">Belum ada posisi</div>
        </div>
      </div>

      <div>
        <div class="card">
          <div class="small">Portfolio (Rill)</div>
          <div id="tradePortfolio" style="margin-top:8px">--</div>
        </div>

        <div class="card" style="margin-top:12px">
          <div class="small">Mutasi</div>
          <div class="mutasi" id="tradeMutasi">--</div>
        </div>
      </div>
    </div>
  `;
  // bind events
  updateTradePriceInfo();
  $('pairSelectTrade').onchange = updateTradePriceInfo;
  $('leverageTrade').onchange = updateTradePriceInfo; // update PnL estimation if leverage changes
  $('inputModeTrade').onchange = ()=> $('openAmountTrade').value='';
  $('btnBuyTrade').onclick = ()=> openPosition('Buy');
  $('btnSellTrade').onclick = ()=> openPosition('Sell');
  renderPositionsUI('tradePositions');
  renderPortfolioUI();
  renderMutasiUI('tradeMutasi');
}

/* FUTURES (simple placeholder) */
function renderFutures(){
  mainContent.innerHTML = `
    <div class="card">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <div><b>Futures (Rill)</b><div class="small">Kasarnya sama seperti Trade tapi fitur leverage lebih advanced.</div></div>
        <div><button class="btn" onclick="toast('Rill only')">Info</button></div>
      </div>
    </div>
  `;
}

/* WALLET */
function renderWallet(){
  mainContent.innerHTML = `
    <div class="grid">
      <div>
        <div class="card">
          <div class="small">Saldo</div>
          <div style="font-weight:800;font-size:18px;margin-top:8px" id="walletBalance">Rp 0</div>
          <div style="display:flex;gap:8px;margin-top:10px">
            <button class="btn btn-primary" id="depBtnWallet">Deposit</button>
            <button class="btn" id="witBtnWallet">Withdraw</button>
            <button class="btn" id="exportBtn">Export Mutasi</button>
          </div>
          <div class="small" style="margin-top: 10px; color: #ffeb3b;">Minimal Deposit: ${fmtRp(MIN_DEPOSIT)}</div> </div>

        <div class="card" style="margin-top:12px">
          <div class="small">Riwayat</div>
          <div class="mutasi" id="walletMutasi">Tidak ada mutasi</div>
        </div>
      </div>

      <div>
        <div class="card">
          <div class="small">Akun & Alamat (Rill)</div>
          <div style="margin-top:8px"><b id="walletUser">—</b></div>
          <div class="small" style="margin-top:8px">Alamat: <span id="walletAddr">—</span></div>
        </div>
      </div>
    </div>
  `;
  $('depBtnWallet').onclick = ()=> openDepositModal();
  $('witBtnWallet').onclick = ()=> openWithdrawModal();
  $('exportBtn').onclick = exportMutasi;
  renderWalletData();
  renderMutasiUI('walletMutasi');
}

/* ========== User / Session helpers ========== */
function loadCurrentData(){
  const cur = getCurrent();
  if(!cur) return null;
  const users = loadUsers();
  return users[cur] ? users[cur].data : null;
}
function ensureUserExists(u){
  const users = loadUsers();
  if(!users[u]) {
    // 2. Pastikan setelah register user baru memiliki saldo awal 0.
    users[u] = { pass:'', data:{ balance: DEFAULT_BAL, history:[], positions:[], portfolio:[], addr:'ADDR_'+Math.random().toString(36).slice(2,8) } };
    saveUsers(users);
  }
}

/* ========== Actions: positions, deposit, withdraw ========== */
async function openPosition(side){
  const cur = getCurrent();
  if(!cur) return alert('Login dulu');
  const users = loadUsers(); const data = users[cur].data;
  // Tambahkan pengecekan saldo sebelum membuka posisi
  if (data.balance <= 0) {
      alert('Saldo Anda 0. Silakan deposit minimal Rp100.000 untuk memulai perdagangan.');
      return;
  }
  
  const pair = $('pairSelectTrade').value;
  const mode = $('inputModeTrade').value;
  const raw = Number($('openAmountTrade').value || 0);
  const lev = Number($('leverageTrade').value || 1);
  if(raw <= 0) return alert('Masukkan nominal / units');
  // price
  const now = await getPrice(pair);
  const fx = pair.includes('USDT')||pair.includes('USD') ? FX_IDR_PER_USD : 150; // Simplified FX for stocks (very rough estimate)
  let units = 0, amountIDR = 0;
  if(mode==='nominal'){ amountIDR = Math.round(raw); units = amountIDR / (now * fx); } else { units = raw; amountIDR = Math.round(units * now * fx); }
  
  if(amountIDR > data.balance) return alert('Saldo tidak cukup untuk membuka posisi ini.');
  
  // debit/credit - for Rill, Buy debits, Sell doesn't credit/debit until close (since it uses margin/leverage)
  if(side==='Buy' || side==='Sell') data.balance -= amountIDR; // FIX BUG: Ensure margin is debited for both BUY and SELL.
  // Note: For a proper Rill, Sell should also use margin from balance, but we keep it simple as per original logic.

  const pos = { id:'pos_'+Date.now()+'_'+Math.random().toString(36).slice(2,6), pair, side, entryPrice: now, units, leverage: lev, amountIDR, pnl:0, pnlPercent:0, time:new Date().toLocaleString() };
  data.positions = data.positions || []; data.positions.push(pos);
  data.history = data.history || []; data.history.push({ type: side+' '+pair, amount: -amountIDR, time: pos.time }); // debit for open position
  users[cur].data = data; saveUsers(users);
  toast('Posisi dibuka: ' + pair + ' ' + side);
  renderPositionsUI('tradePositions'); renderWalletData(); renderMutasiUI('tradeMutasi');
}

async function closePositionById(id){
  const cur = getCurrent();
  if(!cur) return alert('Login dulu');
  const users = loadUsers(); const data = users[cur].data;
  const idx = data.positions.findIndex(p=>p.id===id); if(idx===-1) return;
  const p = data.positions[idx];
  const now = await getPrice(p.pair);
  
  const { pnlIDR } = calcPnl(p, now);
  
  // Credit amountIDR (margin) + PnL. This logic now works correctly for both BUY and SELL
  // because the margin (p.amountIDR) was debited on open.
  const credit = p.amountIDR + pnlIDR;
  data.balance += credit;
  
  data.history.push({ type: 'Close '+p.side+' '+p.pair, amount: credit, time: new Date().toLocaleString() }); // credit for close
  data.positions.splice(idx,1);
  
  users[cur].data = data; saveUsers(users);
  toast('Posisi ditutup. PnL: ' + fmtRp(pnlIDR));
  renderPositionsUI('tradePositions'); renderPositionsUI('sidePositions'); renderWalletData(); renderMutasiUI('tradeMutasi'); renderMutasiUI('sideMutasi'); renderMutasiUI('walletMutasi');
}

/* deposit / withdraw modals (simple prompt) */
function openDepositModal(){ 
  const v = Number(prompt('Deposit Nominal IDR (Minimal ' + fmtRp(MIN_DEPOSIT) + ')','100000')); 
  if(!v||v<=0) return; 
  doDeposit(v);
}
function doDeposit(v){ 
  const cur=getCurrent(); 
  if(!cur) return alert('Login dulu'); 
  // 3. Pastikan saldo hanya bisa bertambah setelah user melakukan deposit minimal Rp100.000.
  if(v < MIN_DEPOSIT) return alert('Deposit minimal adalah ' + fmtRp(MIN_DEPOSIT));
  
  const users=loadUsers(); 
  users[cur].data.balance += v; 
  users[cur].data.history.push({type:'Deposit', amount:v, time:new Date().toLocaleString()}); 
  saveUsers(users); 
  renderWalletData(); 
  renderMutasiUI('tradeMutasi'); renderMutasiUI('sideMutasi'); renderMutasiUI('walletMutasi'); 
  toast('Deposit +'+fmtRp(v)); 
}
function openWithdrawModal(){ 
  const v = Number(prompt('Withdraw Nominal IDR','100000')); 
  if(!v||v<=0) return; 
  doWithdraw(v);
}
function doWithdraw(v){ 
  const cur=getCurrent(); 
  if(!cur) return alert('Login dulu'); 
  const users=loadUsers(); 
  if(v>users[cur].data.balance) return alert('Saldo tidak cukup'); 
  users[cur].data.balance -= v; 
  users[cur].data.history.push({type:'Withdraw', amount:-v, time:new Date().toLocaleString()}); 
  saveUsers(users); 
  renderWalletData(); 
  renderMutasiUI('tradeMutasi'); renderMutasiUI('sideMutasi'); renderMutasiUI('walletMutasi'); 
  toast('Withdraw -'+fmtRp(v)); 
}
function exportMutasi(){ const cur=getCurrent(); if(!cur) return alert('Login dulu'); const users=loadUsers(); const hist = users[cur].data.history||[]; if(hist.length===0) return alert('Belum ada mutasi'); let csv='timestamp,desc,amount\n'; hist.forEach(h=> csv += `"${h.time}","${h.type.replace(/"/g,'')}",${h.amount}\n`); const blob=new Blob([csv],{type:'text/csv'}); const url=URL.createObjectURL(blob); const a=document.createElement('a'); a.href=url; a.download='mutasi_'+cur+'.csv'; a.click(); URL.revokeObjectURL(url); }

/* ========== RENDER helpers ========= */
function renderPositionsUI(targetId='tradePositions'){
  const cur = getCurrent(); if(!cur) return;
  const data = loadUsers()[cur].data;
  const box = document.getElementById(targetId);
  if(!box) return;
  if(!data.positions || data.positions.length===0){ box.innerHTML='Belum ada posisi'; return; }
  box.innerHTML = '';
  data.positions.slice().reverse().forEach(p=>{
    const pnlIDR = p.pnl || 0;
    const pnlPercent = p.pnlPercent || 0;
    const pnlColor = getPnlColorClass(pnlIDR);
    const el = document.createElement('div');
    el.setAttribute('data-pos-id', p.id); // for live update
    el.style.padding='8px 0'; el.style.borderBottom='1px dashed rgba(255,255,255,0.03)';
    el.innerHTML = `<div style="display:flex;justify-content:space-between">
        <div><b>${p.pair}</b> • ${p.side} (${fmtRp(Math.round(p.amountIDR))})</div>
        <div class="${pnlColor}" data-pnl-id="${p.id}">
          ${fmtRp(pnlIDR)} <span class="mini">${fmtPnlPercent(pnlPercent)}</span>
        </div>
      </div>
      <div class="small">Entry: ${Number(p.entryPrice).toFixed(6)} • Units: ${Number(p.units).toFixed(6)} • Lev: ${p.leverage}x</div>
      <div style="display:flex;gap:8px;margin-top:6px"><button class="btn" onclick="closePositionById('${p.id}')">Close</button></div>`;
    box.appendChild(el);
  });
}

async function updatePositionsPnL(){
  const cur = getCurrent(); if(!cur) return;
  const users = loadUsers(); const data = users[cur].data;
  
  if(!data.positions || data.positions.length===0) return;
  
  const uniquePairs = [...new Set(data.positions.map(p=>p.pair))];
  const prices = {};
  for(const pair of uniquePairs){
    prices[pair] = await getPrice(pair);
  }
  
  data.positions.forEach(p=>{
    const now = prices[p.pair];
    if(!now) return;
    const { pnlIDR, pnlPercent } = calcPnl(p, now);
    p.pnl = pnlIDR; // update object for persistence/close
    p.pnlPercent = pnlPercent;
    
    // update UI for tradePositions and sidePositions
    ['tradePositions', 'sidePositions'].forEach(targetId => {
      const pnlEl = document.querySelector(`#${targetId} [data-pnl-id="${p.id}"]`);
      if(pnlEl){
        pnlEl.className = getPnlColorClass(pnlIDR);
        pnlEl.innerHTML = `${fmtRp(pnlIDR)} <span class="mini">${fmtPnlPercent(pnlPercent)}</span>`;
      }
    });
  });
  
  users[cur].data = data; saveUsers(users); // save updated PnL
}


function renderPortfolioUI(){
  const cur = getCurrent(); if(!cur) return;
  const data = loadUsers()[cur].data;
  const box = $('tradePortfolio');
  if(!box) return;
  if(!data.portfolio || data.portfolio.length===0) return box.innerHTML = '<div class="small">Belum ada aset Rill</div>';
  box.innerHTML = data.portfolio.map(p=>`<div style="display:flex;justify-content:space-between;padding:8px 0">${p.label}<div class="mini">${p.units}</div></div>`).join('');
}

function renderMutasiUI(targetId='tradeMutasi'){
  const cur = getCurrent(); if(!cur) return;
  const data = loadUsers()[cur].data;
  const box = document.getElementById(targetId);
  if(!box) return;
  if(!data.history || data.history.length===0) return box.innerHTML = '<div class="small">Belum ada mutasi</div>';
  box.innerHTML = '';
  data.history.slice().reverse().forEach(h=>{
    const el = document.createElement('div'); el.style.padding='8px 0'; el.style.borderBottom='1px dashed rgba(255,255,255,0.03)';
    el.innerHTML = `<div><b>${h.type}</b></div><div class="small">${h.time} • ${fmtRp(h.amount)}</div>`;
    box.appendChild(el);
  });
}

/* wallet data */
function renderWalletData(){
  const cur = getCurrent();
  if(!cur) { $('uiNet').textContent = fmtRp(0); return; }
  const data = loadUsers()[cur].data;
  $('uiNet').textContent = fmtRp(data.balance);
  if($('sideBalance')) $('sideBalance').textContent = fmtRp(data.balance);
  if($('walletBalance')) $('walletBalance').textContent = fmtRp(data.balance);
  if($('walletUser')) $('walletUser').textContent = cur;
  if($('walletAddr')) $('walletAddr').textContent = data.addr || '—';
}

/* market header displays */
async function updateMarketHeaderDisplays(pair){
  const price = await getPrice(pair);
  if($('marketLabelHome')) $('marketLabelHome').textContent = pair;
  if($('priceMainHome')) $('priceMainHome').textContent = Number(price).toFixed(6);
  if($('modeLabelHome')) $('modeLabelHome').textContent = window.priceMode === 'realtime' ? 'Realtime' : 'Simulasi';
  if($('hlInfoHome')) { const last = simSeries[pair][simSeries[pair].length-1]; $('hlInfoHome').textContent = `H: ${last.h.toFixed(2)} • L: ${last.l.toFixed(2)}`; }
}

/* trade price info and example pnl */
async function updateTradePriceInfo(){
  const pair = $('pairSelectTrade') ? $('pairSelectTrade').value : 'BTC/USDT';
  const price = await getPrice(pair);
  if($('tradePriceInfo')) $('tradePriceInfo').textContent = Number(price).toFixed(6);
  // example for 0.01 unit
  const exampleUnits = 0.01;
  const lev = Number($('leverageTrade') ? $('leverageTrade').value : 1);
  const estPnlUSD = exampleUnits * 1 * lev; // per 1 USD move
  if($('estPnl')) $('estPnl').textContent = `Per 1 USD move → ${exampleUnits}×1×${lev} = ${estPnlUSD.toFixed(2)} USD (× ${FX_IDR_PER_USD} => ${fmtRp(estPnlUSD*FX_IDR_PER_USD)})`;
}

/* bind side buttons */
function bindSideButtons(){
  const depBtn = $('openDepBtnSide');
  if(depBtn) depBtn.onclick = ()=> openDepositModal();
}

/* ========== LOGOUT Function ========== */
function doLogout(){
  const users = loadUsers();
  const cur = getCurrent();
  // Simpan data user terakhir sebelum logout
  if(cur){
    // Pastikan data terakhir tersimpan jika ada perubahan PnL, dll.
    users[cur].data = loadCurrentData(); // Muat ulang & simpan
    saveUsers(users);
  }
  
  setCurrent(''); // Kosongkan user aktif
  $('loginModal').style.display='flex'; // Tampilkan modal login
  $('bottomNav').style.display = 'none'; // Sembunyikan nav bar
  $('loginBtnTop').textContent = 'Login ▾'; // Set kembali teks tombol header
  $('loginBtnTop').onclick = ()=> $('loginModal').style.display='flex'; // Set kembali aksi tombol header
  $('uiNet').textContent = fmtRp(0); // Reset UI Balance
  $('loginUser').value=''; $('loginPass').value=''; // Reset input
  navTo('home'); // Kembali ke Beranda (atau tetap di halaman saat ini dengan data kosong)
  toast('Logout berhasil');
}

/* ========== LOGIN / REGISTER ========== */
// Mengganti style.display='flex' (buka modal) menjadi simulasi klik tombol loginBtnTop
$('loginBtnTop').onclick = ()=> {
  if(!getCurrent()){
    $('loginModal').style.display='flex';
  } else {
    // Jika sudah login, klik tombol header adalah logout
    doLogout();
  }
};
$('closeLogin').onclick = ()=> $('loginModal').style.display='none';

$('doRegister').onclick = ()=>{
  const u = $('loginUser').value.trim(); const p = $('loginPass').value;
  if(!u||!p) return alert('Isi username & password');
  const users = loadUsers();
  if(users[u]) return alert('Username sudah ada');
  // 2. Pastikan setelah register user baru memiliki saldo awal 0.
  users[u] = { pass:p, data:{ balance:DEFAULT_BAL, history:[], positions:[], portfolio:[], addr:'ADDR_'+Math.random().toString(36).slice(2,8) } };
  saveUsers(users); setCurrent(u); $('loginModal').style.display='none'; toast('Register & login: '+u); postLogin();
};
$('doLogin').onclick = ()=>{
  const u = $('loginUser').value.trim(); const p = $('loginPass').value;
  if(!u||!p) return alert('Isi username & password');
  const users = loadUsers();
  if(!users[u] || users[u].pass !== p) return alert('Username/password salah');
  
  // Pastikan data lengkap ada (untuk user lama/migrasi)
  if(!users[u].data.history) users[u].data.history = [];
  if(!users[u].data.positions) users[u].data.positions = [];
  if(!users[u].data.portfolio) users[u].data.portfolio = [];
  // Pastikan saldo awal 0 untuk user lama yang belum punya
  if(users[u].data.balance === undefined) users[u].data.balance = DEFAULT_BAL;


  setCurrent(u); $('loginModal').style.display='none'; toast('Login berhasil: '+u); postLogin();
};
$('quickGuest').onclick = ()=>{
  const u = 'guest_'+Math.random().toString(36).slice(2,6);
  // Tambahkan quick guest dengan pengecekan, agar tidak error di loadUsers()
  ensureUserExists(u); // Memastikan user guest baru dibuat
  setCurrent(u); $('loginModal').style.display='none'; toast('Masuk sebagai '+u); postLogin();
};

function postLogin(){
  const cur = getCurrent();
  $('loginUser').value=''; $('loginPass').value='';
  renderWalletData();
  renderMutasiUI('tradeMutasi'); renderMutasiUI('sideMutasi'); renderMutasiUI('walletMutasi');
  renderPositionsUI('tradePositions'); renderPositionsUI('sidePositions');
  renderPortfolioUI();
  // show wallet & bottom nav
  $('bottomNav').style.display = 'flex';
  // Ubah tombol Login menjadi tombol User/Logout
  $('loginBtnTop').textContent = cur; // Tampilkan username aktif
  $('loginBtnTop').onclick = doLogout; // Aksi tombol menjadi Logout
  // navigate to home
  navTo('home');
}

/* ========== INIT app ======= */
async function startApp(){
  // JANGAN UBAH SISTEM INI
  // Tampilkan splash screen, kemudian transisi ke login modal setelah 3 detik.
  const cur = getCurrent();
  if(!cur){
    $('app').style.display='block'; // Tampilkan app wrapper agar loginModal bisa muncul di tengah
    $('bottomNav').style.display='none'; // Sembunyikan nav bar
    $('loginBtnTop').textContent = 'Login ▾'; // Pastikan tombol login tetap ada
    $('loginBtnTop').onclick = ()=> $('loginModal').style.display='flex'; // Set ulang handler klik
  } else {
    // Jika sudah login, langsung ke postLogin
    $('app').style.display='block';
    postLogin();
    $('loginModal').style.display='none';
  }

  // Transisi Splash -> Login
  setTimeout(()=>{ 
    $('intro').style.opacity='0'; // Transisi halus fade out
    setTimeout(()=>{
        $('intro').style.display='none';
        // Tampilkan login modal jika belum login (tanpa mengganggu alur postLogin)
        if(!cur) $('loginModal').style.display='flex';
    }, 400); // Tunggu hingga fade out selesai
  }, 3000); // Tampilkan splash selama 3 detik
  
  // init default view
  renderPage('home');
  renderWalletData();
  // start market loop to tick simSeries (but DO NOT reload iframe repeatedly)
  marketLoop();
  // update trade price info periodically
  setInterval(()=>{ 
    if(currentPage==='trade') updateTradePriceInfo();
    // Re-check PnL if needed, but marketLoop handles the main update
  }, 3000);
}
let marketTimer = null;
async function marketLoop(){
  // tick sim series
  PAIRS.forEach(p=>{
    if(Math.random()<0.6){
      const arr = simSeries[p];
      const last = arr[arr.length-1];
      const o = last.c;
      const ch = (Math.random()-0.5)*(volMap[p]||1);
      const c = Math.max((o+ch), 0.0001);
      const h = Math.max(o,c) + Math.abs(Math.random() * (volMap[p]||1));
      const l = Math.min(o,c) - Math.abs(Math.random() * (volMap[p]||1));
      arr.push({o,c,h,l});
      if(arr.length>900) arr.shift();
    }
  });
  // update small headers if on home or market
  if(currentPage === 'home') updateMarketHeaderDisplays('BTC/USDT');
  if(currentPage === 'market'){
    // Ganti: Ambil nilai dari dropdown marketPair (BTCUSD/ETHUSD) lalu konversikan ke pair lama (BTC/USDT)
    const marketPairValue = $('marketPair') ? $('marketPair').value : 'BTCUSD';
    const oldPair = (marketPairValue === 'BTCUSD' ? 'BTC/USDT' : (marketPairValue === 'ETHUSD' ? 'ETH/USDT' : 'BTC/USDT'));
    updateMarketHeaderDisplays(oldPair);
  }
  // update open positions PnL
  const cur = getCurrent();
  if(cur) updatePositionsPnL();
  
  marketTimer = setTimeout(marketLoop, 1000 + Math.random()*800);
}

/* finally start */
// JANGAN UBAH SISTEM INI
window.onload = startApp;
</script>
<script>
// --- START ADDED TOP MOVERS SCRIPT (TUGAS 2) ---
const moversData = [
    { pair: "BTC/USDT", base: 0.3 },
    { pair: "ETH/USDT", base: -0.2 },
    { pair: "SOL/USDT", base: 0.8 },
    { pair: "XRP/USDT", base: -0.4 }
];

function renderTopMovers() {
    const box = document.getElementById("topMoversList");
    if(!box) return; // Guard clause
    box.innerHTML = "";

    moversData.forEach(m => {
        let randomMove = (Math.random() * 2 - 1) * 0.4;
        let percent = m.base + randomMove;
        let colorClass = percent >= 0 ? "mover-green" : "mover-red";
        // Batasi width agar tidak lebih dari 100% dan minimal 1% untuk visual
        let width = Math.min(Math.abs(percent) * 25, 100); 
        width = Math.max(width, 1); // Minimal 1% untuk terlihat

        box.innerHTML += `
            <div class="mover-item">
                <div class="mover-header">
                    <span>${m.pair}</span>
                    <span>${percent.toFixed(2)}%</span>
                </div>
                <div class="mover-bar ${colorClass}" style="width:${width}%"></div>
            </div>
        `;
    });
}

setInterval(renderTopMovers, 1000);
renderTopMovers();
// --- END ADDED TOP MOVERS SCRIPT (TUGAS 2) ---
</script>
</body>
</html>
