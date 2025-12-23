<!DOCTYPE html>
<html lang="sq">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1.0,viewport-fit=cover">
<title>POS Market — Modern</title>
<meta name="description" content="POS Market — aplikacion i vogël për shitje me barkode, historik, dhe bilanc.">

<!-- Minimal styles, modern dhe responsive -->
<style>
  :root{
    --bg:#eef2f7;
    --card:#ffffff;
    --muted:#6b7280;
    --accent:#2563eb;
    --dark:#0f172a;
    --radius:12px;
    --gap:10px;
  }
  *{box-sizing:border-box}
  body{margin:0;font-family:Inter, "Segoe UI", Roboto, Arial, sans-serif;background:var(--bg);color:var(--dark);-webkit-font-smoothing:antialiased}
  header{background:linear-gradient(90deg,#0f172a,#1e293b);color:#fff;padding:14px 16px;display:flex;align-items:center;justify-content:space-between;gap:12px}
  header h1{font-size:1.05rem;margin:0;display:flex;align-items:center;gap:10px}
  .container{max-width:1100px;margin:18px auto;padding:0 16px}
  nav{display:flex;gap:8px;flex-wrap:wrap}
  .btn{display:inline-flex;align-items:center;gap:8px;padding:8px 12px;border-radius:10px;border:0;background:var(--accent);color:#fff;font-weight:600;cursor:pointer}
  .btn.ghost{background:transparent;color:#111;border:1px solid rgba(0,0,0,.06)}
  .card{background:var(--card);padding:14px;border-radius:var(--radius);box-shadow:0 8px 18px rgba(2,6,23,0.06);margin-bottom:12px}
  input[type="text"],input[type="number"],select{padding:10px;border-radius:8px;border:1px solid #e6eef8;min-height:40px}
  .row{display:flex;gap:10px;flex-wrap:wrap}
  .col{flex:1;min-width:150px}
  table{width:100%;border-collapse:collapse;margin-top:10px;font-size:0.95rem}
  th,td{padding:8px;border-bottom:1px solid #eef2f7;text-align:left}
  th{background:#f8fafc;font-weight:700}
  .qtyBtn{padding:6px 8px;border-radius:8px;border:0;background:#efefef;cursor:pointer}
  .small{font-size:0.9rem;color:var(--muted)}
  .admin{display:none} /* toggled by role */
  .hidden{display:none!important}
  .modal{display:none;position:fixed;inset:0;background:rgba(0,0,0,.55);z-index:999;align-items:center;justify-content:center;padding:12px}
  .modal.open{display:flex}
  .modal-content{background:var(--card);padding:16px;border-radius:12px;max-width:680px;width:100%;max-height:85vh;overflow:auto}
  #scanner{width:100%;background:#000;border-radius:8px;overflow:hidden;height:320px}
  footer{padding:12px;text-align:center;color:var(--muted);font-size:0.9rem}
  @media (max-width:720px){
    .row{flex-direction:column}
    #scanner{height:220px}
  }
</style>

<!-- Quagga2 for barcode scanning -->
<script src="https://unpkg.com/@ericblade/quagga2/dist/quagga.js"></script>
</head>
<body>
<header>
  <h1>🛒 POS Market</h1>
  <nav id="topNav" aria-label="Main navigation">
    <button class="btn" data-section="sale">Shitje</button>
    <button class="btn admin" data-section="prod">Stok</button>
    <button class="btn admin" data-section="bil">Bilanc</button>
    <button class="btn" data-section="hist">Historik</button>
    <button class="btn" id="logoutBtn" style="background:#ef4444">Dil</button>
  </nav>
</header>

<main class="container" id="app">
  <!-- Login -->
  <section id="loginSec" class="card" aria-labelledby="loginTitle">
    <h2 id="loginTitle">Hyr në sistem</h2>
    <div class="row" style="align-items:center;margin-top:8px">
      <input id="u" class="col" type="text" placeholder="User" aria-label="Username">
      <input id="p" class="col" type="password" placeholder="Password" aria-label="Password">
      <button id="loginBtn" class="btn">Hyr</button>
    </div>
    <p id="msg" class="small" style="color:#b91c1c;margin-top:8px"></p>
    <p class="small" style="margin-top:8px">Përdorues për testim: <b>admin/admin</b> & <b>kasier/kasier</b></p>
  </section>

  <!-- PROD (admin) -->
  <section id="prod" class="card admin hidden" aria-hidden="true">
    <h2>Shto / Menaxho Produkte</h2>
    <div class="row" style="margin-top:8px">
      <input id="pn" class="col" type="text" placeholder="Emri i produktit">
      <input id="pb" class="col" type="text" placeholder="Barkodi (opsional)">
    </div>
    <div class="row" style="margin-top:8px">
      <input id="pp" type="number" placeholder="Çmimi (ALL)" class="col">
      <input id="ps" type="number" placeholder="Sasia" class="col">
      <div style="display:flex;gap:8px;align-items:center">
        <button id="addProductBtn" class="btn">➕ Shto</button>
        <button id="openCamStockBack" class="btn ghost">📷 Mbrapa</button>
        <button id="openCamStockFront" class="btn ghost">🤳 Para</button>
      </div>
    </div>

    <div style="margin-top:12px;overflow:auto">
      <table id="prodTable" aria-live="polite"></table>
    </div>
  </section>

  <!-- SALE -->
  <section id="sale" class="card">
    <h2>Shitje</h2>
    <div class="row" style="margin-top:8px;align-items:center">
      <input id="saleScan" class="col" type="text" placeholder="Emër / Barkod / Skano USB" aria-label="Skanim ose kërkim">
      <input id="client" class="col" type="text" placeholder="Emri i klientit (opsional)">
      <button id="manualAddBtn" class="btn">➕ Shto</button>
    </div>
    <div style="margin-top:8px;display:flex;gap:8px">
      <button id="openCamSaleBack" class="btn ghost">📷 Mbrapa</button>
      <button id="openCamSaleFront" class="btn ghost">🤳 Para</button>
    </div>

    <div class="card" style="margin-top:12px">
      <table id="saleTable" aria-live="polite"></table>
      <div style="display:flex;justify-content:space-between;align-items:center;margin-top:8px;gap:8px;flex-wrap:wrap">
        <div><h3>Total: <span id="tot">0</span> ALL</h3></div>
        <div style="display:flex;gap:8px;align-items:center">
          <input id="paid" type="number" placeholder="Lekë nga klienti">
          <button id="payBtn" class="btn">Paguaj</button>
          <button id="cancelBtn" class="btn ghost">Anulo</button>
        </div>
      </div>
      <p class="small">Kusur / Mungesë: <span id="change">0</span></p>
    </div>
  </section>

  <!-- BILANCI -->
  <section id="bil" class="card admin hidden" aria-hidden="true">
    <h2>Bilanci Ditor</h2>
    <p>Sistemi: <b><span id="daily">0</span> ALL</b></p>
    <p class="small">(Kjo është shuma e parave të arkëtuara gjatë ditës)</p>
    <div class="row" style="margin-top:8px">
      <input id="cashReal" type="number" placeholder="Shuma reale në arkë" class="col">
      <div style="display:flex;gap:8px;align-items:center">
        <button id="closeDayBtn" class="btn">Mbyll Ditën</button>
      </div>
    </div>
    <p class="small">Diferenca: <b><span id="diff">0</span></b></p>
  </section>

  <!-- HISTORIK -->
  <section id="hist" class="card">
    <h2>Historiku i Shitjeve</h2>
    <div style="margin-bottom:8px;display:flex;gap:8px;flex-wrap:wrap">
      <button id="exportCsvBtn" class="btn">⬇️ Eksporto CSV</button>
      <button id="clearAllBtn" class="btn ghost">🧹 Fshi të gjitha (lokal)</button>
    </div>
    <div style="overflow:auto">
      <table id="histTable" aria-live="polite"></table>
    </div>
  </section>
</main>

<!-- CAMERA MODAL -->
<div id="cam" class="modal" role="dialog" aria-modal="true" aria-hidden="true">
  <div class="modal-content">
    <h3>Skano Barkod</h3>
    <div id="scanner" aria-label="Scanner camera"></div>
    <div style="display:flex;gap:8px;justify-content:flex-end;margin-top:12px">
      <button id="camCloseBtn" class="btn ghost">Mbyll</button>
    </div>
  </div>
</div>

<!-- VIEW SALE MODAL -->
<div id="viewModal" class="modal" role="dialog" aria-modal="true" aria-hidden="true">
  <div class="modal-content" id="viewContent">
    <h3>Detajet e Shitjes</h3>
    <div id="viewBody"></div>
    <div style="margin-top:12px;display:flex;gap:8px;align-items:center">
      <input id="settleAmount" type="number" placeholder="Shuma për të shlyer (ALL)">
      <button id="settleBtn" class="btn">Shlyej Borxh</button>
      <button id="closeViewBtn" class="btn ghost">Mbyll</button>
    </div>
  </div>
</div>

<footer>POS Market — përditësim modern (lokal, punon me localStorage)</footer>

<script>
/*
  Përmbledhje përmirësimesh:
  - Përdorim të qartë të referencave DOM (getElementById)
  - Kontroll më i mirë i localStorage (parsing i sigurt)
  - Manage Quagga start/stop me checks
  - Accessibility (aria-hidden toggles) dhe responsive styling
  - Mbrojtje të të dhënave me escapeHtml kur vendosim HTML
  - Eksport CSV me BOM për të siguruar hapje korrekte në Excel
*/

/* HELPERS */
const qs = (id) => document.getElementById(id);
const safeParse = (v, def) => {
  try { return JSON.parse(v); } catch(e) { return def; }
};
const escapeHtml = (str='') => (''+str).replace(/[&<>"']/g, s => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[s]));

/* DOM */
const loginSec = qs('loginSec');
const uInput = qs('u');
const pInput = qs('p');
const loginBtn = qs('loginBtn');
const msgEl = qs('msg');

const prodSec = qs('prod');
const pn = qs('pn'), pb = qs('pb'), pp = qs('pp'), ps = qs('ps');
const addProductBtn = qs('addProductBtn');
const prodTable = qs('prodTable');

const saleSec = qs('sale');
const saleScan = qs('saleScan'), client = qs('client');
const manualAddBtn = qs('manualAddBtn');
const saleTable = qs('saleTable'), totEl = qs('tot'), paidEl = qs('paid'), changeEl = qs('change');
const payBtn = qs('payBtn'), cancelBtn = qs('cancelBtn');

const histTable = qs('histTable');
const exportCsvBtn = qs('exportCsvBtn'), clearAllBtn = qs('clearAllBtn');

const dailyEl = qs('daily'), cashReal = qs('cashReal'), diffEl = qs('diff'), closeDayBtn = qs('closeDayBtn');

const camModal = qs('cam'), scannerEl = qs('scanner'), camCloseBtn = qs('camCloseBtn');
const openCamStockBack = qs('openCamStockBack'), openCamStockFront = qs('openCamStockFront');
const openCamSaleBack = qs('openCamSaleBack'), openCamSaleFront = qs('openCamSaleFront');

const viewModal = qs('viewModal'), viewBody = qs('viewBody'), settleAmount = qs('settleAmount');
const settleBtn = qs('settleBtn'), closeViewBtn = qs('closeViewBtn');

const logoutBtn = qs('logoutBtn');
const navButtons = Array.from(document.querySelectorAll('nav button[data-section]'));

/* State */
const users = [{u:'admin',p:'admin',r:'admin'},{u:'kasier',p:'kasier',r:'kasier'}];
let role = null;
let scanTarget = null; // 'stock' or 'sale'
let camMode = 'environment'; // 'environment' or 'user'
let scanLock = false;
let quaggaHandler = null;
let quaggaRunning = false;
let products = safeParse(localStorage.getItem('p'), []);
let sales = []; // current basket
let salesHistory = safeParse(localStorage.getItem('salesHistory'), []);
let daily = Number(localStorage.getItem('daily') || 0);

/* ---- UI / Navigation ---- */
function showSection(id){
  document.querySelectorAll('main > section').forEach(s => {
    if(s.id === id){
      s.classList.remove('hidden');
      s.setAttribute('aria-hidden','false');
    } else {
      s.classList.add('hidden');
      s.setAttribute('aria-hidden','true');
    }
  });
  // focus first input for convenience
  if(id === 'sale') saleScan.focus();
  if(id === 'loginSec') uInput.focus();
}
navButtons.forEach(btn=>{
  btn.addEventListener('click',()=> showSection(btn.dataset.section));
});

/* ---- Login ---- */
loginBtn.addEventListener('click', doLogin);
uInput.addEventListener('keydown', e=> { if(e.key==='Enter') pInput.focus(); });
pInput.addEventListener('keydown', e=> { if(e.key==='Enter') doLogin(); });

function doLogin(){
  msgEl.textContent = '';
  const uname = (uInput.value || '').trim();
  const pwd = (pInput.value || '').trim();
  const found = users.find(x => x.u === uname && x.p === pwd);
  if(!found){
    msgEl.textContent = 'Gabim login — përdorues ose fjalëkalim i pasaktë';
    return;
  }
  role = found.r;
  // Show/hide admin sections + nav
  document.querySelectorAll('.admin').forEach(el => {
    if(role === 'admin'){
      el.classList.remove('hidden');
      el.setAttribute('aria-hidden','false');
    } else {
      el.classList.add('hidden');
      el.setAttribute('aria-hidden','true');
    }
  });
  // toggle nav admin buttons
  document.querySelectorAll('nav button').forEach(b => {
    if(b.classList.contains('admin')) b.style.display = role === 'admin' ? 'inline-flex' : 'none';
  });
  loginSec.classList.add('hidden');
  showSection('sale');
  renderProducts();
  renderHistory();
  updateDailyUI();
}

/* ---- Products ---- */
function saveProducts(){
  localStorage.setItem('p', JSON.stringify(products));
  renderProducts();
}
addProductBtn.addEventListener('click', ()=>{
  const name = (pn.value || '').trim() || 'Pa emër';
  const barcode = (pb.value || '').trim();
  const price = Number(pp.value) || 0;
  const stock = Math.max(0, Number(ps.value) || 0);
  products.push({n:name,b:barcode,p:price,s:stock});
  saveProducts();
  pn.value = pb.value = pp.value = ps.value = '';
});

function renderProducts(){
  prodTable.innerHTML = '<tr><th>Emër</th><th>Barkod</th><th>Çmim</th><th>Stok</th><th>Veprime</th></tr>';
  products.forEach((p,i)=>{
    prodTable.innerHTML += `<tr>
      <td><input aria-label="Emri produktit" value="${escapeHtml(p.n)}" data-i="${i}" class="prod-name" style="width:100%"></td>
      <td><input aria-label="Barkod" value="${escapeHtml(p.b)}" data-i="${i}" class="prod-bar" style="width:100%"></td>
      <td><input aria-label="Çmim" type="number" value="${p.p}" data-i="${i}" class="prod-price" style="width:100%"></td>
      <td><input aria-label="Sasi" type="number" value="${p.s}" data-i="${i}" class="prod-stock" style="width:100%"></td>
      <td><button class="btn ghost" data-del="${i}">🗑️</button></td>
    </tr>`;
  });
  // attach listeners
  Array.from(document.querySelectorAll('.prod-name')).forEach(inp=>{
    inp.addEventListener('change', e=>{
      const i = Number(e.target.dataset.i);
      products[i].n = e.target.value;
      saveProducts();
    });
  });
  Array.from(document.querySelectorAll('.prod-bar')).forEach(inp=>{
    inp.addEventListener('change', e=>{
      const i = Number(e.target.dataset.i);
      products[i].b = e.target.value;
      saveProducts();
    });
  });
  Array.from(document.querySelectorAll('.prod-price')).forEach(inp=>{
    inp.addEventListener('change', e=>{
      const i = Number(e.target.dataset.i);
      products[i].p = Number(e.target.value) || 0;
      saveProducts();
    });
  });
  Array.from(document.querySelectorAll('.prod-stock')).forEach(inp=>{
    inp.addEventListener('change', e=>{
      const i = Number(e.target.dataset.i);
      products[i].s = Math.max(0, Number(e.target.value) || 0);
      saveProducts();
    });
  });
  Array.from(document.querySelectorAll('[data-del]')).forEach(btn=>{
    btn.addEventListener('click', e=>{
      const i = Number(e.currentTarget.dataset.del);
      products.splice(i,1);
      saveProducts();
    });
  });
}

/* ---- Sale / Basket ---- */
function findProductByQuery(q){
  if(!q) return null;
  q = q.toLowerCase();
  return products.find(p => (p.b && p.b.toLowerCase() === q) || p.n.toLowerCase().includes(q));
}

function addToSale(product){
  if(!product) return alert('Produkt i pavlefshëm');
  if(product.s < 1) return alert('Stoku = 0');
  const s = sales.find(x => x.b === product.b && x.p === product.p && x.n === product.n);
  if(s){
    if(s.q + 1 > product.s) return alert('Sasia tejkalon stoqen');
    s.q++;
  } else {
    sales.push({b:product.b,n:product.n,p:product.p,q:1});
  }
  drawSale();
}

manualAddBtn.addEventListener('click', manualAdd);
saleScan.addEventListener('keydown', e => { if(e.key === 'Enter') manualAdd(); });

function manualAdd(){
  const v = (saleScan.value || '').trim();
  if(!v) return;
  const p = findProductByQuery(v.toLowerCase());
  if(!p) return alert('Nuk u gjet');
  addToSale(p);
  saleScan.value = '';
}

function drawSale(){
  saleTable.innerHTML = '<tr><th>Produkt</th><th>Sasi</th><th>Çmim</th><th>Total</th><th>Veprime</th></tr>';
  sales.forEach((x,i)=>{
    saleTable.innerHTML += `<tr>
      <td>${escapeHtml(x.n)}</td>
      <td style="width:130px;">
        <button class="qtyBtn" data-dec="${i}">➖</button>
        <span style="margin:0 8px">${x.q}</span>
        <button class="qtyBtn" data-inc="${i}">➕</button>
      </td>
      <td>${x.p}</td>
      <td>${x.q * x.p}</td>
      <td><button class="btn ghost" data-rm="${i}">🗑️</button></td>
    </tr>`;
  });
  // listeners
  Array.from(saleTable.querySelectorAll('[data-dec]')).forEach(b => b.addEventListener('click', e => changeQty(Number(e.currentTarget.dataset.dec), -1)));
  Array.from(saleTable.querySelectorAll('[data-inc]')).forEach(b => b.addEventListener('click', e => changeQty(Number(e.currentTarget.dataset.inc), 1)));
  Array.from(saleTable.querySelectorAll('[data-rm]')).forEach(b => b.addEventListener('click', e => {
    sales.splice(Number(e.currentTarget.dataset.rm),1);
    drawSale();
  }));
  recalc();
}

function changeQty(i, delta){
  const item = sales[i];
  if(!item) return;
  const prod = products.find(p => p.b === item.b && p.n === item.n);
  item.q += delta;
  if(item.q < 1) { sales.splice(i,1); }
  if(prod && item.q > prod.s){ item.q = prod.s; alert('Sasia tejkalon stoqen'); }
  drawSale();
}

function recalc(){
  const total = sales.reduce((acc,x)=>acc + (x.q * x.p), 0);
  totEl.textContent = total.toFixed(2);
  const paid = Number(paidEl.value) || 0;
  const diff = paid - total;
  if(diff < 0){
    changeEl.textContent = `Mungojnë ${Math.abs(diff).toFixed(2)} ALL`;
    changeEl.style.color = 'red';
  } else {
    changeEl.textContent = `Kusur ${diff.toFixed(2)} ALL`;
    changeEl.style.color = 'green';
  }
}
paidEl.addEventListener('input', recalc);

/* ---- Payment ---- */
payBtn.addEventListener('click', pay);
cancelBtn.addEventListener('click', cancel);

function pay(){
  const total = Number(totEl.textContent) || 0;
  const cash = Number(paidEl.value) || 0;
  if(sales.length === 0) return alert('Shporta është bosh');

  const clientName = (client.value || '').trim() || null;
  const status = cash >= total ? 'paid' : 'owed';
  const changeAmount = Math.max(0, cash - total);
  const due = Math.max(0, total - cash);

  // Reduce stock
  for(const item of sales){
    const prod = products.find(p => p.b === item.b && p.n === item.n);
    if(prod) prod.s = Math.max(0, prod.s - item.q);
  }

  const timestamp = new Date().toISOString();
  const record = {
    id: timestamp + '_' + Math.random().toString(36).slice(2,8),
    timestamp,
    client: clientName,
    items: JSON.parse(JSON.stringify(sales)),
    total,
    amountPaid: cash,
    change: changeAmount,
    due,
    status
  };
  salesHistory.unshift(record);
  localStorage.setItem('salesHistory', JSON.stringify(salesHistory));

  daily += record.amountPaid;
  localStorage.setItem('daily', String(daily));

  saveProducts();
  cancel();
  updateDailyUI();
  renderHistory();

  if(status === 'paid'){
    alert('Shitja u krye. Kusur: ' + changeAmount.toFixed(2) + ' ALL');
  } else {
    alert('Shitja u regjistrua si BORXH. Mungojnë: ' + due.toFixed(2) + ' ALL (Paguat: ' + cash.toFixed(2) + ' ALL)');
  }
}

function cancel(){
  sales = [];
  saleTable.innerHTML = '';
  totEl.textContent = '0';
  paidEl.value = '';
  changeEl.textContent = '0';
  client.value = '';
}

/* ---- History ---- */
function renderHistory(){
  histTable.innerHTML = '<tr><th>Data</th><th>Klient</th><th>Total</th><th>Paguar</th><th>Mbetje</th><th>Status</th><th>Veprime</th></tr>';
  salesHistory.forEach(rec=>{
    histTable.innerHTML += `<tr>
      <td>${escapeHtml(rec.timestamp.replace('T',' ').slice(0,19))}</td>
      <td>${escapeHtml(rec.client || '--')}</td>
      <td>${rec.total}</td>
      <td>${rec.amountPaid}</td>
      <td>${rec.due}</td>
      <td>${escapeHtml(rec.status)}</td>
      <td>
        <button class="btn ghost" data-view="${rec.id}">Shiko</button>
        <button class="btn ghost" data-del="${rec.id}">🗑️</button>
      </td>
    </tr>`;
  });

  Array.from(histTable.querySelectorAll('[data-view]')).forEach(b => b.addEventListener('click', e => viewSale(e.currentTarget.dataset.view)));
  Array.from(histTable.querySelectorAll('[data-del]')).forEach(b => b.addEventListener('click', e => deleteSale(e.currentTarget.dataset.del)));
}

function viewSale(id){
  const r = salesHistory.find(x => x.id === id);
  if(!r) return alert('Nuk u gjet shitja');
  let html = `<p><b>Data:</b> ${escapeHtml(r.timestamp.replace('T',' ').slice(0,19))}</p>`;
  html += `<p><b>Klient:</b> ${escapeHtml(r.client || '--')}</p>`;
  html += `<p><b>Total:</b> ${r.total.toFixed(2)} ALL</p>`;
  html += `<p><b>Paguar:</b> ${r.amountPaid.toFixed(2)} ALL</p>`;
  html += `<p><b>Mbetje:</b> ${r.due.toFixed(2)} ALL</p>`;
  html += `<p><b>Status:</b> ${escapeHtml(r.status)}</p>`;
  html += '<hr><p><b>Produkte:</b></p><ul>';
  r.items.forEach(it => html += `<li>${escapeHtml(it.n)} x${it.q} = ${(it.q*it.p).toFixed(2)} ALL</li>`);
  html += '</ul>';
  viewBody.innerHTML = html;
  viewModal.dataset.currentId = id;
  settleAmount.value = r.due || '';
  openModal(viewModal);
}

function closeView(){
  closeModal(viewModal);
  delete viewModal.dataset.currentId;
}

closeViewBtn.addEventListener('click', closeView);

function deleteSale(id){
  if(!confirm('Fshi këtë regjistrim?')) return;
  salesHistory = salesHistory.filter(x => x.id !== id);
  localStorage.setItem('salesHistory', JSON.stringify(salesHistory));
  renderHistory();
}

/* ---- Settle Debt ---- */
settleBtn.addEventListener('click', settleDebt);

function settleDebt(){
  const id = viewModal.dataset.currentId;
  if(!id) return alert('Nuk ka shitje të zgjedhur');
  const r = salesHistory.find(x => x.id === id);
  if(!r) return alert('Nuk u gjet shitja');
  const amt = Number(settleAmount.value) || 0;
  if(amt <= 0) return alert('Shuma duhet > 0');
  if(r.due <= 0) return alert('Nuk ka borxh për këtë shitje');

  const payNow = Math.min(amt, r.due);
  r.amountPaid += payNow;
  r.due -= payNow;
  if(r.due <= 0){ r.status = 'paid'; r.due = 0; } else r.status = 'owed';

  daily += payNow;
  localStorage.setItem('daily', String(daily));

  localStorage.setItem('salesHistory', JSON.stringify(salesHistory));
  updateDailyUI();
  renderHistory();
  viewSale(id); // reopen updated view
  alert('U faturua shuma: ' + payNow.toFixed(2) + ' ALL');
}

/* ---- Export CSV ---- */
exportCsvBtn.addEventListener('click', exportCSV);

function exportCSV(){
  if(!salesHistory.length) return alert('Nuk ka të dhëna për eksport');
  const rows = [];
  const header = ['id','timestamp','client','total','amountPaid','due','status','items'];
  rows.push(header.join(','));
  // reverse for chronological old->new or new->old depending preference; here newest first (salesHistory is newest-first)
  salesHistory.forEach(r=>{
    const itemsText = r.items.map(i=>`${i.n} x${i.q}=${(i.q*i.p).toFixed(2)}`).join(' | ');
    const row = [
      `"${r.id}"`,
      `"${r.timestamp}"`,
      `"${(r.client||'')}"`,
      r.total.toFixed(2),
      r.amountPaid.toFixed(2),
      r.due.toFixed(2),
      r.status,
      `"${itemsText}"`
    ];
    rows.push(row.join(','));
  });
  const csvBody = rows.join('\n');
  // Add UTF-8 BOM so Excel recognizes encoding
  const blob = new Blob(["\uFEFF", csvBody], { type: 'text/csv;charset=utf-8;' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'sales_history.csv';
  a.click();
  URL.revokeObjectURL(url);
}

/* ---- Clear all local history ---- */
clearAllBtn.addEventListener('click', ()=>{
  if(!confirm('Je i sigurt? Kjo do fshij historikun lokal.')) return;
  salesHistory = [];
  localStorage.removeItem('salesHistory');
  renderHistory();
});

/* ---- Daily / Close Day ---- */
function updateDailyUI(){
  dailyEl.textContent = Number(daily).toFixed(2);
}
cashReal.addEventListener('input', ()=>{
  const d = (Number(cashReal.value) || 0) - Number(daily || 0);
  diffEl.textContent = d.toFixed(2) + ' ALL';
  diffEl.style.color = d < 0 ? 'red' : 'green';
});

closeDayBtn.addEventListener('click', closeDay);

function closeDay(){
  const sys = Number(daily) || 0;
  const cash = Number(cashReal.value) || 0;
  const diffVal = cash - sys;
  alert(`Sistemi (duhet në arkë): ${sys.toFixed(2)} ALL\nArka (me dore): ${cash.toFixed(2)} ALL\nDiferenca: ${diffVal.toFixed(2)} ALL`);
  const closures = safeParse(localStorage.getItem('dayClosures'), []);
  closures.push({timestamp:new Date().toISOString(), system:sys, cash, diff:diffVal});
  localStorage.setItem('dayClosures', JSON.stringify(closures));
  daily = 0;
  localStorage.setItem('daily', '0');
  cashReal.value = '';
  updateDailyUI();
  diffEl.textContent = '0';
}

/* ---- Camera / Quagga ---- */
function openCamera(target, mode='environment'){
  scanTarget = target; camMode = mode; scanLock = false;
  openModal(camModal);
  startQuagga();
}

openCamStockBack.addEventListener('click', ()=> openCamera('stock','environment'));
openCamStockFront.addEventListener('click', ()=> openCamera('stock','user'));
openCamSaleBack.addEventListener('click', ()=> openCamera('sale','environment'));
openCamSaleFront.addEventListener('click', ()=> openCamera('sale','user'));

camCloseBtn.addEventListener('click', stopCamera);

function startQuagga(){
  if(typeof Quagga === 'undefined'){
    alert('Quagga nuk u gjet. Sigurohu që lidhja me CDN është e disponueshme (HTTPS).');
    closeModal(camModal);
    return;
  }

  // Remove existing handler if present
  removeQuaggaHandler();

  const constraints = {
    facingMode: camMode // 'environment' or 'user'
  };

  try {
    Quagga.init({
      inputStream: {
        name: "Live",
        type: "LiveStream",
        target: scannerEl,
        constraints: constraints
      },
      locator: {patchSize:"medium", halfSample:true},
      decoder: { readers: ["ean_reader","ean_8_reader","code_128_reader","upc_reader"] },
      locate: true
    }, function(err){
      if(err){
        console.error('Quagga init error', err);
        alert("Kamera nuk u hap (kontrollo lejet / HTTPS): " + (err.message || err));
        closeModal(camModal);
        return;
      }
      try {
        Quagga.start();
        quaggaRunning = true;
      } catch(e){
        console.error('Quagga start error', e);
        alert('Gabim duke nisur kamerën: ' + e.message);
        closeModal(camModal);
      }
    });
  } catch(e){
    console.error('Quagga init exception', e);
    alert('Gabim gjatë inicializimit të skanerit: ' + e.message);
    closeModal(camModal);
    return;
  }

  // Debounced detection handler
  quaggaHandler = function(result){
    if(scanLock) return;
    scanLock = true;
    try {
      const code = result && result.codeResult && result.codeResult.code;
      if(!code){ scanLock = false; return; }
      if(scanTarget === 'stock'){
        pb.value = code;
      } else if(scanTarget === 'sale'){
        const found = products.find(x => x.b === code);
        if(found) addToSale(found);
        else alert('Barkodi nuk u gjet: ' + code);
      }
    } finally {
      setTimeout(()=>{ stopCamera(); }, 400);
    }
  };

  // Attach handler using available API
  if(typeof Quagga.onDetected === 'function'){
    Quagga.onDetected(quaggaHandler);
  } else if(typeof Quagga.addListener === 'function'){
    Quagga.addListener && Quagga.addListener('detected', quaggaHandler);
  } else {
    console.warn('Metoda për ndjekjen e detektimit nuk u gjend në Quagga.');
  }
}

function removeQuaggaHandler(){
  if(!quaggaHandler || typeof Quagga === 'undefined') return;
  try {
    if(typeof Quagga.offDetected === 'function') Quagga.offDetected(quaggaHandler);
    else if(typeof Quagga.off === 'function') Quagga.off('detected', quaggaHandler);
    else if(typeof Quagga.removeListener === 'function') Quagga.removeListener('detected', quaggaHandler);
    else if(typeof Quagga.stop === 'function') {
      // nothing to remove, will stop
    }
  } catch(e){
    console.warn('Gabim gjatë heqjes së handler-it të Quagga:', e);
  } finally {
    quaggaHandler = null;
  }
}

function stopCamera(){
  removeQuaggaHandler();
  try{
    if(typeof Quagga !== 'undefined' && quaggaRunning && typeof Quagga.stop === 'function'){
      Quagga.stop();
    }
  } catch(e){
    console.warn('Gabim ndalimi Quagga:', e);
  } finally {
    quaggaRunning = false;
    scanLock = false;
    closeModal(camModal);
  }
}

/* ---- Modal helpers ---- */
function openModal(el){
  el.classList.add('open');
  el.setAttribute('aria-hidden','false');
}
function closeModal(el){
  el.classList.remove('open');
  el.setAttribute('aria-hidden','true');
}

/* ---- Initial render / bindings ---- */
function init(){
  // default view - login
  showSection('loginSec');
  // wire logout
  logoutBtn.addEventListener('click', ()=> {
    if(confirm('Dëshironi të dilni?')) location.reload();
  });
  // If there are existing products/histories, render them
  renderProducts();
  renderHistory();
  updateDailyUI();
  // Allow clicking outside modal to close
  [camModal, viewModal].forEach(m => {
    m.addEventListener('click', e => { if(e.target === m) { closeModal(m); stopCamera(); }});
  });
  // keyboard escape to close modals
  document.addEventListener('keydown', e => {
    if(e.key === 'Escape'){
      closeModal(camModal); closeModal(viewModal); stopCamera();
    }
  });
}
init();

</script>
</body>
</html>