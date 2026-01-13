<!DOCTYPE html>
<html lang="sq">
<head>
<meta charset="UTF-8">
<title>POS Market – FINAL ABSOLUT (perditesuar)</title>

<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">

<style>
body{margin:0;font-family:Segoe UI,Arial,Helvetica;background:#eef2f7}
header{background:#1e293b;color:#fff;padding:15px;display:flex;align-items:center;justify-content:space-between;gap:12px}
nav button{margin:4px;padding:10px;border:none;border-radius:10px;background:#334155;color:#fff;cursor:pointer}
section{display:none;padding:15px}
section.active{display:block}
.card{background:#fff;padding:15px;border-radius:14px;margin-bottom:12px;box-shadow:0 8px 18px rgba(0,0,0,.1)}
input,button,select{padding:8px;border-radius:8px;border:1px solid #cbd5f5}
button{background:#2563eb;color:#fff;font-weight:600;margin:3px}
table{width:100%;border-collapse:collapse;margin-top:10px}
th,td{padding:6px;border-bottom:1px solid #e5e7eb;text-align:center}
th{background:#f1f5f9}
.admin{display:none}
.qtyBtn{padding:4px 8px}
.modal{display:none;position:fixed;inset:0;background:rgba(0,0,0,.6);z-index:999}
.modal-content{background:#fff;margin:60px auto;padding:15px;width:95%;max-width:520px;border-radius:14px}
.small{font-size:0.9em;color:#374151}
.kv{font-weight:600}
.row{display:flex;gap:8px;flex-wrap:wrap}
.col{flex:1;min-width:120px}
#scanner{width:100%;background:#000;border-radius:8px;overflow:hidden}

/* small modal variant (less tall) */
.modal-content.small-modal{max-width:720px;padding:12px;text-align:left}
.modal-content.small-modal h4{margin:6px 0}
.txn-list{margin:6px 0;padding-left:18px}
.txn-summary{margin-top:8px;font-weight:600}
.suggestion{background:#f8fafc;padding:8px;border-radius:8px;margin-top:6px}

/* FINANCE specific */
.finance-top{display:flex;gap:8px;align-items:center;flex-wrap:wrap}
.finance-metrics{display:flex;gap:12px;flex-wrap:wrap;margin-top:8px}
.finance-metrics .box{background:#f8fafc;padding:10px;border-radius:8px}
#deviceTime{font-size:0.95em;color:#dbeafe}
canvas{max-width:100%;height:320px;display:block}
</style>

<!-- Chart.js CDN -->
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://unpkg.com/@ericblade/quagga2/dist/quagga.js"></script>
</head>
<body>

<header>
  <div style="display:flex;gap:12px;align-items:center">
    <h2 style="margin:0">🛒 POS Market</h2>
    <div id="deviceTime">--:--:--</div>
  </div>

  <nav id="menu" style="display:none">
    <button onclick="openSec('prod')" class="admin">Stok</button>
    <button onclick="openSec('sale')">Shitje</button>
    <button onclick="openSec('bil')" class="admin">Bilanc</button>
    <button onclick="openSec('hist')">Historik</button>
    <button onclick="openSec('fin')" class="admin">Financa</button>
    <button onclick="logout()">Dil</button>
  </nav>
</header>

<!-- LOGIN -->
<section id="loginSec" class="active">
<div class="card">
<h3>Login</h3>
<input id="u" placeholder="User">
<input id="p" type="password">
<button onclick="doLogin()">Hyr</button>
<p id="msg" style="color:red"></p>
</div>
</section>

<!-- STOK -->
<section id="prod">
<div class="card admin">
<h3>Shto Produkt</h3>
<div class="row">
<input id="pn" placeholder="Emri" class="col">
<input id="pb" placeholder="Barkodi (unik)" class="col">
</div>
<div class="row" style="margin-top:8px">
<input id="pp" type="number" placeholder="Çmimi Shitje (ALL)" class="col">
<input id="pcost" type="number" placeholder="Çmimi Blerje (ALL)" class="col">
<input id="ps" type="number" placeholder="Sasia" class="col">
</div>
<div style="margin-top:8px">
<button onclick="addProduct()">➕ Shto</button>
<button onclick="openCam('stock','environment')">📷 Mbrapa</button>
<button onclick="openCam('stock','user')">🤳 Para</button>
</div>
</div>
<table id="prodTable"></table>
</section>

<!-- SHITJE -->
<section id="sale">
<div class="card">
<div class="row">
<input id="saleScan" placeholder="Emër / Barkod / Scan USB" autofocus class="col">
<input id="client" placeholder="Emri i klientit (opsional)" class="col">
</div>
<div style="margin-top:8px">
<button onclick="manualAdd()">➕ Shto</button>
<button onclick="openCam('sale','environment')">📷 Mbrapa</button>
<button onclick="openCam('sale','user')">🤳 Para</button>
</div>
</div>

<div class="card">
<table id="saleTable"></table>
<h3>Total: <span id="tot">0</span> ALL</h3>
<input id="paid" type="number" placeholder="Lekë nga klienti">
<h3>Kusur / Mungesë: <span id="change">0</span></h3>
<button onclick="pay()">Paguaj</button>
<button onclick="cancel()">Anulo</button>
</div>
</section>

<!-- BILANC -->
<section id="bil" class="admin">
<div class="card">
<h3>Bilanci Ditor</h3>
<p>Sistemi: <b><span id="daily">0</span> ALL</b></p>
<p class="small">(Kjo është shuma e parave të arkëtuara gjatë ditës)</p>
<input id="cashReal" type="number" placeholder="Shuma reale në arkë">
<p>Diferenca: <b><span id="diff">0</span></b></p>
<button onclick="closeDay()">Mbyll Ditën</button>
<button onclick="generateReorderReport_manual()">Gjenero Sugjerime (pa mbyllje)</button>
</div>
</section>

<!-- HISTORIK -->
<section id="hist">
<div class="card">
<h3>Historiku i Shitjeve</h3>
<div style="margin-bottom:8px">
<button onclick="exportCSV()">⬇️ Eksporto CSV</button>
<button onclick="clearOld()">🧹 Fshi të gjitha (lokal)</button>
</div>
<table id="histTable"></table>
</div>
</section>

<!-- FINANCE (uses stock data & purchase price; no separate supplies) -->
<section id="fin" class="admin">
  <div class="card">
    <h3>FINANCA — Raport (nga stoku)</h3>

    <div class="finance-top">
      <div>
        <label class="small">Nga</label><br>
        <input id="finFrom" type="date">
      </div>
      <div>
        <label class="small">Deri</label><br>
        <input id="finTo" type="date">
      </div>
      <div style="margin-left:auto">
        <label class="small">Ora pajisjes</label><br>
        <div id="finDeviceTime" class="small">--:--:--</div>
      </div>
      <div><br><button onclick="updateFinance()">Përditëso Raport</button></div>
    </div>

    <div class="finance-metrics">
      <div class="box">
        <div class="small">Të ardhurat (shitjet)</div>
        <div id="finRevenue" class="kv">0 ALL</div>
      </div>
      <div class="box">
        <div class="small">COGS (nga blerja)</div>
        <div id="finCOGS" class="kv">0 ALL</div>
      </div>
      <div class="box">
        <div class="small">Fitim / Humbje</div>
        <div id="finProfit" class="kv">0 ALL</div>
        <div id="finMargin" class="small">Marginë: 0%</div>
      </div>
    </div>

    <div style="margin-top:12px">
      <h4>Grafik: Të ardhurat vs Fitimi (per periudhë)</h4>
      <canvas id="finChart"></canvas>
    </div>
  </div>
</section>

<!-- CAMERA -->
<div class="modal" id="cam">
<div class="modal-content">
<h3>Scan Barcode</h3>
<div id="scanner" style="height:260px"></div>
<button id="camCloseBtn">Mbyll</button>
</div>
</div>

<!-- VIEW / PAY DEBT MODAL -->
<div class="modal" id="viewModal">
<div class="modal-content" id="viewContent">
<h3>Detajet e Shitjes</h3>
<div id="viewBody"></div>
<div style="margin-top:12px">
<input id="settleAmount" type="number" placeholder="Shuma për të shlyer (ALL)">
<button onclick="settleDebt()">Shlyej Borxh</button>
<button onclick="closeView()">Mbyll</button>
</div>
</div>
</div>

<!-- TRANSACTION SUCCESS MODAL (small) -->
<div class="modal" id="txnModal">
<div class="modal-content small-modal">
<h4 id="txnTitle">Transaksioni</h4>
<div id="txnMsg" class="small"></div>
<div style="margin-top:12px;text-align:right">
<button onclick="closeTxn()">Mbyll</button>
</div>
</div>
</div>

<script>
/* ======= CONFIG & STORAGE KEYS ======= */
const KEY_PRODUCTS = 'p';
const KEY_SALES_HISTORY = 'salesHistory';
const KEY_DAILY = 'daily';

/* ======= STATE ======= */
const users=[{u:'admin',p:'admin',r:'admin'},{u:'kasier',p:'kasier',r:'kasier'}];
let role=null;
let products = JSON.parse(localStorage.getItem(KEY_PRODUCTS) || '[]');
let sales = [];
let salesHistory = JSON.parse(localStorage.getItem(KEY_SALES_HISTORY) || '[]');
let daily = +localStorage.getItem(KEY_DAILY) || 0;
let quaggaHandler = null, quaggaRunning = false, scanLock = false;
let finChart = null;

/* ======= ELEMENTS ======= */
const deviceTimeEl = document.getElementById('deviceTime');
const finDeviceTimeEl = document.getElementById('finDeviceTime');
const camEl = document.getElementById('cam');
const scannerEl = document.getElementById('scanner');
const camCloseBtn = document.getElementById('camCloseBtn');
const saleScanEl = document.getElementById('saleScan');
const paidEl = document.getElementById('paid');
const totEl = document.getElementById('tot');
const changeEl = document.getElementById('change');
const prodTableEl = document.getElementById('prodTable');
const saleTableEl = document.getElementById('saleTable');
const histTableEl = document.getElementById('histTable');
const dailyEl = document.getElementById('daily');
const cashRealEl = document.getElementById('cashReal');
const diffEl = document.getElementById('diff');
const txnModalEl = document.getElementById('txnModal');
const txnMsgEl = document.getElementById('txnMsg');
const txnTitleEl = document.getElementById('txnTitle');

/* ======= LOGIN ======= */
function doLogin(){
  const fu = document.getElementById('u').value.trim();
  const fp = document.getElementById('p').value;
  const f = users.find(x=>x.u===fu && x.p===fp);
  if(!f){ document.getElementById('msg').textContent = 'Gabim login'; return; }
  role = f.r;
  document.getElementById('loginSec').style.display = 'none';
  document.getElementById('menu').style.display = 'block';
  document.querySelectorAll('.admin').forEach(e=>e.style.display = role === 'admin' ? 'block' : 'none');
  openSec('sale');
  renderProducts();
  renderHistory();
  updateDaily();
  initFinanceChart();
}
function logout(){ location.reload(); }
function openSec(id){
  document.querySelectorAll('section').forEach(s=>s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

/* ======= PRODUCTS (store purchase_price in stock) ======= */
function renderProducts(){
  prodTableEl.innerHTML = '<tr><th>Emër</th><th>Barkod</th><th>Çmim Shitje</th><th>Çmimi Blerje</th><th>Stok</th><th>Veprime</th></tr>';
  products.forEach((p,i)=>{
    prodTableEl.innerHTML += `
      <tr>
        <td><input value="${escapeHtml(p.n || '')}" onchange="products[${i}].n=this.value;storeProducts()"></td>
        <td><input value="${escapeHtml(p.b || '')}" onchange="products[${i}].b=this.value;storeProducts()"></td>
        <td><input type="number" value="${p.p || 0}" onchange="products[${i}].p=+this.value;storeProducts()"></td>
        <td><input type="number" value="${p.purchase_price || 0}" onchange="products[${i}].purchase_price=+this.value;storeProducts()"></td>
        <td><input type="number" value="${p.s || 0}" onchange="products[${i}].s=+this.value;storeProducts()"></td>
        <td><button onclick="deleteProduct(${i})">🗑️</button></td>
      </tr>`;
  });
}
function addProduct(){
  const name = (document.getElementById('pn').value || '').trim();
  const barcode = (document.getElementById('pb').value || '').trim();
  const price = Number(document.getElementById('pp').value) || 0;
  const purchase_price = Number(document.getElementById('pcost').value) || 0;
  const qty = Number(document.getElementById('ps').value) || 0;
  if(!name) return alert('Emri i produktit është i detyrueshëm');
  if(price <= 0) return alert('Çmimi i shitjes duhet > 0');
  if(purchase_price <= 0) return alert('Çmimi i blerjes duhet > 0');
  if(barcode && products.find(p=>p.b === barcode)) return alert('Barkod ekziston');
  products.push({ n: name, b: barcode, p: price, purchase_price: purchase_price, s: qty });
  storeProducts();
  document.getElementById('pn').value=''; document.getElementById('pb').value=''; document.getElementById('pp').value=''; document.getElementById('pcost').value=''; document.getElementById('ps').value='';
}
function deleteProduct(i){
  if(!confirm('Fshi këtë produkt?')) return;
  products.splice(i,1);
  storeProducts();
}
function storeProducts(){
  localStorage.setItem(KEY_PRODUCTS, JSON.stringify(products));
  renderProducts();
  initFinanceChart(); // refresh chart because purchase prices or stock changed
}

/* ======= SALES ======= */
function findProductByKey(key){
  if(!key) return null;
  key = key.toString().trim().toLowerCase();
  return products.find(p => p.b && p.b.toString().toLowerCase() === key)
    || products.find(p => (p.n || '').toString().toLowerCase() === key)
    || products.find(p => (p.n || '').toString().toLowerCase().includes(key));
}
function addToSale(p){
  if(p.s < 1) return alert('Stoku = 0');
  let s = sales.find(x=>x.b===p.b);
  if(s){
    if(s.q + 1 > p.s) return alert('Sasia tejkalon stoqen');
    s.q++;
  } else {
    sales.push({ b: p.b, n: p.n, p: p.p, q: 1 });
  }
  drawSale();
}
function manualAdd(){
  let v = saleScanEl.value.trim().toLowerCase();
  if(!v) return;
  const p = findProductByKey(v);
  if(!p) return alert('Nuk u gjet');
  addToSale(p); saleScanEl.value=''; saleScanEl.focus();
}
saleScanEl.addEventListener('keydown', e=>{ if(e.key==='Enter') manualAdd(); });

function drawSale(){
  saleTableEl.innerHTML = '<tr><th>Produkt</th><th>Sasi</th><th>Çmim</th><th>Total</th><th></th></tr>';
  sales.forEach((x,i)=> {
    saleTableEl.innerHTML += `
      <tr>
        <td>${escapeHtml(x.n)}</td>
        <td><button class="qtyBtn" onclick="changeQty(${i},-1)">➖</button> ${x.q} <button class="qtyBtn" onclick="changeQty(${i},1)">➕</button></td>
        <td>${x.p}</td>
        <td>${x.q * x.p}</td>
        <td><button onclick="sales.splice(${i},1);drawSale();">🗑️</button></td>
      </tr>`;
  });
  recalc();
}
function changeQty(i,delta){
  const item = sales[i]; if(!item) return;
  const prod = products.find(p=>p.b === item.b);
  item.q += delta;
  if(item.q < 1) { sales.splice(i,1); }
  if(prod && item.q > prod.s){ item.q = prod.s; alert('Sasia tejkalon stoqen'); }
  drawSale();
}
function recalc(){
  let total = 0; sales.forEach(x=> total += x.q * x.p);
  totEl.textContent = total;
  const cash = (+paidEl.value || 0);
  const diff = cash - total;
  if(diff < 0){ changeEl.textContent = `Mungojnë ${Math.abs(diff)} ALL`; changeEl.style.color = 'red'; }
  else { changeEl.textContent = `Kusur ${diff} ALL`; changeEl.style.color = 'green'; }
}
paidEl.addEventListener('input', recalc);

/* ======= CAMERA ======= */
camCloseBtn.addEventListener('click', stopCam);
camEl.addEventListener('click', (e)=>{ if(e.target === camEl) stopCam(); });
document.addEventListener('keydown', (e)=>{ if(e.key === 'Escape'){ if(camEl.style.display === 'block') stopCam(); if(txnModalEl.style.display === 'block') closeTxn(); } });

function openCam(target, mode){
  scanLock = false;
  camEl.style.display = 'block';
  if(quaggaHandler && window.Quagga){ try{ Quagga.offDetected && Quagga.offDetected(quaggaHandler); }catch(e){} quaggaHandler = null; }
  if(!window.Quagga){ alert('Quagga nuk u gjet'); camEl.style.display='none'; return; }
  Quagga.init({
    inputStream:{ type:"LiveStream", target: scannerEl, constraints:{ facingMode: { ideal: mode }, width:{ideal:640}, height:{ideal:480} } },
    locator:{patchSize:"medium",halfSample:true},
    decoder:{readers:["ean_reader","ean_8_reader","code_128_reader","upc_reader"]},
    locate:true
  }, err => {
    if(err){ alert("Kamera nuk u hap: " + (err.message||err)); camEl.style.display='none'; return; }
    try{ Quagga.start(); quaggaRunning = true; }catch(e){ alert("Gabim duke nisur kamerën: "+(e.message||e)); camEl.style.display='none'; return; }
    quaggaHandler = function(d){
      if(scanLock) return; scanLock = true;
      const code = d && d.codeResult && (d.codeResult.code || d.codeResult.codeResult);
      if(!code){ scanLock = false; return; }
      if(target === 'stock'){ document.getElementById('pb').value = code; }
      else if(target === 'sale'){
        const p = products.find(x=>x.b === code);
        if(p) addToSale(p); else alert('Barkodi nuk u gjet: ' + code);
      }
      setTimeout(stopCam, 400);
    };
    try{ Quagga.onDetected && Quagga.onDetected(quaggaHandler); }catch(e){}
  });
}
function stopCam(){ camEl.style.display='none'; scanLock = false; try{ Quagga.offDetected && Quagga.offDetected(quaggaHandler); }catch(e){} try{ if(window.Quagga && quaggaRunning) Quagga.stop(); }catch(e){} quaggaHandler = null; quaggaRunning = false; }

/* ======= PAYMENT (fixed) ======= */
function pay(){
  try{
    const total = +totEl.textContent || 0;
    const cash = +paidEl.value || 0;
    if(sales.length === 0) { alert('Shporta është bosh'); return; }

    const clientName = (document.getElementById('client').value || '').trim();
    const changeAmount = Math.max(0, cash - total);
    const netCollected = Math.min(cash, total);
    const due = Math.max(0, total - cash);
    const status = cash >= total ? 'paid' : 'owed';

    // update product stocks (persist)
    for(const item of sales){
      const prod = products.find(p=>p.b === item.b);
      if(prod) prod.s = Math.max(0, prod.s - item.q);
    }
    storeProducts(); // persist updated stock

    const timestamp = new Date().toISOString();
    const record = {
      id: timestamp + '_' + Math.random().toString(36).slice(2,7),
      timestamp,
      client: clientName || null,
      items: JSON.parse(JSON.stringify(sales)),
      total,
      amountPaid: netCollected,
      cashGiven: cash,
      change: changeAmount,
      due,
      status
    };

    // save history atomically and update daily
    salesHistory.unshift(record);
    localStorage.setItem(KEY_SALES_HISTORY, JSON.stringify(salesHistory));

    daily += netCollected;
    localStorage.setItem(KEY_DAILY, daily);

    // clear UI
    sales = []; cancel();

    // refresh dependent UI parts
    updateDaily();
    renderHistory();
    updateFinance();
    initFinanceChart();

    // show success modal
    const prodHtml = `<ul class="txn-list">${record.items.map(it=>`<li>${escapeHtml(it.n)} x${it.q} = ${it.q*it.p} ALL</li>`).join('')}</ul>`;
    const html = status==='paid'
      ? `<div style="color:green;font-weight:700;margin-bottom:6px">Transaksioni u mbyll me sukses</div>
         <div><b>Produkte:</b>${prodHtml}</div>
         <div class="txn-summary">Total: ${record.total} ALL</div>
         <div>Klienti dha: ${record.cashGiven} ALL</div>
         <div>Kusur: ${record.change} ALL</div>
         <div class="small" style="margin-top:6px">Shuma e shtuar në arkë (neto): ${record.amountPaid} ALL</div>`
      : `<div style="color:#b45f00;font-weight:700;margin-bottom:6px">Shitja u regjistrua si BORXH</div>
         <div><b>Produkte:</b>${prodHtml}</div>
         <div class="txn-summary">Total: ${record.total} ALL</div>
         <div>Paguat tani (neto): ${record.amountPaid} ALL</div>
         <div>Mbetje (borxh): ${record.due} ALL</div>`;
    txnTitleEl.textContent = status==='paid' ? 'Shitje e plotë' : 'Shitje me borxh';
    showTxn(html);
  }catch(err){
    console.error('Pay error:', err);
    alert('Gabim gjatë pagesës. Shikoni console për detaje.');
  }
}

/* Cancel current sale */
function cancel(){ sales=[]; saleTableEl.innerHTML=''; totEl.textContent=0; paidEl.value=''; changeEl.textContent=0; document.getElementById('client').value=''; }

/* ======= HISTORY & DEBT ======= */
function renderHistory(){
  histTableEl.innerHTML = '<tr><th>Data</th><th>Klient</th><th>Total</th><th>Paguar(net)</th><th>Mbetje</th><th>Status</th><th>Veprime</th></tr>';
  salesHistory.forEach(rec=>{
    histTableEl.innerHTML += `<tr>
      <td>${rec.timestamp.replace('T',' ').slice(0,19)}</td>
      <td>${escapeHtml(rec.client||'--')}</td>
      <td>${rec.total}</td>
      <td>${rec.amountPaid}</td>
      <td>${rec.due}</td>
      <td>${rec.status}</td>
      <td>
        <button onclick='viewSale("${rec.id}")'>Shiko</button>
        <button onclick='deleteSale("${rec.id}")'>🗑️</button>
      </td>
    </tr>`;
  });
}
function viewSale(id){
  const r = salesHistory.find(x=>x.id===id);
  if(!r) return alert('Nuk u gjet shitja');
  const body = document.getElementById('viewBody');
  let html = `<p><b>Data:</b> ${r.timestamp.replace('T',' ').slice(0,19)}</p>`;
  html += `<p><b>Klient:</b> ${escapeHtml(r.client||'--')}</p>`;
  html += `<p><b>Total:</b> ${r.total} ALL</p>`;
  html += `<p><b>Paguar (neto):</b> ${r.amountPaid} ALL</p>`;
  html += `<p><b>Klienti dha:</b> ${r.cashGiven !== undefined ? r.cashGiven + ' ALL' : '--'}</p>`;
  html += `<p><b>Kusur:</b> ${r.change} ALL</p>`;
  html += `<p><b>Mbetje:</b> ${r.due} ALL</p>`;
  html += `<p><b>Status:</b> ${r.status}</p>`;
  html += '<hr><p><b>Produkte:</b></p><ul>';
  r.items.forEach(it=> html += `<li>${escapeHtml(it.n)} x${it.q} = ${it.q*it.p} ALL</li>`);
  html += '</ul>';
  body.innerHTML = html;
  document.getElementById('viewModal').dataset.currentId = id;
  document.getElementById('settleAmount').value = r.due || '';
  document.getElementById('viewModal').style.display='block';
}
function closeView(){ document.getElementById('viewModal').style.display='none'; delete document.getElementById('viewModal').dataset.currentId; }
function deleteSale(id){
  if(!confirm('Fshi këtë regjistrim?')) return;
  salesHistory = salesHistory.filter(x=>x.id !== id);
  localStorage.setItem(KEY_SALES_HISTORY, JSON.stringify(salesHistory));
  renderHistory(); updateFinance(); initFinanceChart();
}

/* debt settle */
function settleDebt(){
  const id = document.getElementById('viewModal').dataset.currentId;
  if(!id) return alert('Nuk ka shitje të zgjedhur');
  const r = salesHistory.find(x=>x.id===id);
  if(!r) return alert('Nuk u gjet shitja');
  const amt = +document.getElementById('settleAmount').value || 0;
  if(amt <= 0) return alert('Shuma duhet > 0');
  if(r.due <= 0) return alert('Nuk ka borxh');
  const payNow = Math.min(amt, r.due);
  r.amountPaid += payNow; r.due -= payNow;
  if(r.due <= 0){ r.status='paid'; r.due = 0; } else r.status='owed';
  daily += payNow; localStorage.setItem(KEY_DAILY, daily);
  localStorage.setItem(KEY_SALES_HISTORY, JSON.stringify(salesHistory));
  updateDaily(); renderHistory(); viewSale(id); updateFinance(); initFinanceChart();
  showTxn(`<div style="color:green;font-weight:700">Pagesa u regjistrua</div><div>U mbledh: ${payNow} ALL</div>`);
}

/* ======= EXPORT & CLEAR ======= */
function exportCSV(){
  if(!salesHistory.length) return alert('Nuk ka të dhëna për eksport');
  const rows = []; rows.push(['id','timestamp','client','total','amountPaid','cashGiven','change','due','status','items'].join(','));
  salesHistory.slice().reverse().forEach(r=>{
    const itemsText = r.items.map(i=>`${i.n} x${i.q}=${i.q*i.p}`).join(' | ');
    const row = [`"${r.id}"`, `"${r.timestamp}"`, `"${r.client||''}"`, r.total, r.amountPaid, r.cashGiven !== undefined ? r.cashGiven : '', r.change, r.due, r.status, `"${itemsText}"`].join(',');
    rows.push(row);
  });
  const csv = rows.join('\n');
  const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a'); a.href = url; a.download = 'sales_history.csv'; a.click(); URL.revokeObjectURL(url);
}
function clearOld(){
  if(!confirm('Je i sigurt? Kjo do fshij historikun lokal.')) return;
  salesHistory = []; localStorage.removeItem(KEY_SALES_HISTORY); renderHistory(); updateFinance(); initFinanceChart();
}

/* ======= BILANCI & REORDER (same) ======= */
function getLocalDateStr(iso){ const d = new Date(iso); return d.getFullYear() + '-' + String(d.getMonth()+1).padStart(2,'0') + '-' + String(d.getDate()).padStart(2,'0'); }
function isSameLocalDate(isoA, isoB){ return getLocalDateStr(isoA) === getLocalDateStr(isoB); }
function aggregateSales(records){ const agg = {}; records.forEach(r=>(r.items||[]).forEach(it=>{ const key = it.b || it.n; if(!agg[key]) agg[key] = {b: it.b, n: it.n, qty:0, revenue:0}; agg[key].qty += it.q; agg[key].revenue += (it.q * it.p); })); return agg; }
function getSalesSinceDays(days){ const cutoff = Date.now() - (days * 24 * 60 * 60 * 1000); return salesHistory.filter(r => new Date(r.timestamp).getTime() >= cutoff); }
function isWeeklyReportDay(date){ const d = date.getDay(); return d === 1 || d === 4; }
function generateReorderReport_inner(manual=false){
  const now = new Date(); const isWeekly = isWeeklyReportDay(now); if(!manual && !isWeekly) return null;
  const last7 = getSalesSinceDays(7); const agg7 = aggregateSales(last7);
  const last14 = getSalesSinceDays(14); const agg14 = aggregateSales(last14);
  const suggestions = [], slowItems = [];
  products.forEach(p=>{
    const key = p.b || p.n; const sold7 = agg7[key] ? agg7[key].qty : 0; const avgDaily7 = sold7 / 7; const leadDaysFactor = 3; const targetStock = Math.ceil(avgDaily7 * leadDaysFactor);
    if(avgDaily7 > 0){
      if(p.s < targetStock){ const suggestedQty = Math.max(1, Math.ceil(avgDaily7 * 7) - p.s); suggestions.push({b:p.b,n:p.n,stock:p.s,avgDaily7:avgDaily7.toFixed(2),suggest: suggestedQty}); }
    } else { if(!agg14[key] || agg14[key].qty === 0) slowItems.push({b:p.b,n:p.n,stock:p.s}); }
  });
  return {isWeekly, suggestions, slowItems};
}
function generateReorderReport_manual(){
  const rep = generateReorderReport_inner(true); if(!rep) return alert('Nuk mund të gjenerohet raporti.');
  let html = `<div style="color:#0b5cff;font-weight:700;margin-bottom:6px">Raport Riporositjeje</div>`;
  if(rep.suggestions.length === 0) html += '<div>Asnjë sugjerim për riporositje bazuar në 7-ditoren e fundit.</div>';
  else { html += '<div><b>Sugjerime blerjeje (bazuar në mesataren 7-ditore):</b></div><ul class="txn-list">'; rep.suggestions.forEach(s=> html += `<li>${escapeHtml(s.n)} — Stok aktual: ${s.stock} — Mesatare/ditë: ${s.avgDaily7} — Shto rreth: <b>${s.suggest}</b></li>`); html += '</ul>'; }
  if(rep.slowItems.length){ html += '<div style="margin-top:8px"><b>Produkte që nuk u shitën në 14 ditët e fundit:</b></div><ul class="txn-list">'; rep.slowItems.forEach(si=> html += `<li>${escapeHtml(si.n)} — Stok: ${si.stock}</li>`); html += '</ul>'; }
  txnTitleEl.textContent = 'Sugjerime Riporositjeje'; showTxn(html);
}

/* ======= CLOSE DAY (kept) ======= */
function closeDay(){
  const sys = daily; const arka = +cashRealEl.value || 0; const diffv = arka - sys;
  const closures = JSON.parse(localStorage.getItem('dayClosures')||'[]');
  const closure = {timestamp:new Date().toISOString(), system:sys, cash:arka, diff:diffv};
  closures.push(closure); localStorage.setItem('dayClosures', JSON.stringify(closures));
  daily = 0; localStorage.setItem(KEY_DAILY, 0); cashRealEl.value=''; updateDaily(); diffEl.textContent = 0;
  // Show short report
  const now = new Date(); const todayStr = getLocalDateStr(now.toISOString());
  const todaySales = salesHistory.filter(r => isSameLocalDate(r.timestamp, now.toISOString()));
  const aggToday = aggregateSales(todaySales);
  let soldHtml='', totalQty=0, totalRev=0;
  if(Object.keys(aggToday).length === 0) soldHtml = '<div>Asnjë shitje sot.</div>';
  else { soldHtml = '<ul class="txn-list">'; Object.values(aggToday).forEach(item=>{ soldHtml += `<li>${escapeHtml(item.n)} — Sasi: ${item.qty} — Të ardhura: ${item.revenue} ALL</li>`; totalQty += item.qty; totalRev += item.revenue; }); soldHtml += '</ul>'; }
  let topSellerHtml = '<div>Nuk ka të dhëna për top-seller.</div>'; const itemsArr = Object.values(aggToday); if(itemsArr.length){ itemsArr.sort((a,b)=>b.qty - a.qty); const top = itemsArr[0]; topSellerHtml = `<div class="suggestion"><b>Top Produkt i Sotëm:</b> ${escapeHtml(top.n)} — Sasi: ${top.qty} — Të ardhura: ${top.revenue} ALL</div>`; }
  const reorder = generateReorderReport_inner(false);
  let reorderHtml = '';
  if(reorder && reorder.isWeekly){ if(reorder.suggestions.length === 0) reorderHtml += '<div>Asnjë sugjerim për riporositje bazuar në 7-ditoren e fundit.</div>'; else { reorderHtml += '<div><b>Sugjerime blerjeje (bazuar në mesataren 7-ditore):</b></div><ul class="txn-list">'; reorder.suggestions.forEach(s=> reorderHtml += `<li>${escapeHtml(s.n)} — Stok aktual: ${s.stock} — Mesatare/ditë: ${s.avgDaily7} — Shto rreth: <b>${s.suggest}</b></li>`); reorderHtml += '</ul>'; } if(reorder.slowItems.length){ reorderHtml += '<div style="margin-top:8px"><b>Produkte që nuk u shitën në 14 ditët e fundit:</b></div><ul class="txn-list">'; reorder.slowItems.forEach(si=> reorderHtml += `<li>${escapeHtml(si.n)} — Stok: ${si.stock}</li>`); reorderHtml += '</ul>'; } } else { reorderHtml += `<div class="small">Sugjerime blerjeje prodhohen 2 herë në javë (e hënë & e enjte).</div>`; }
  const html = `
    <div style="color:green;font-weight:700;margin-bottom:6px">Mbyllje dite</div>
    <div>Shuma në sistem (duhet në arkë): ${closure.system} ALL</div>
    <div>Arka (me dore): ${closure.cash} ALL</div>
    <div style="margin-top:6px"><b>Diferenca:</b> ${closure.diff} ALL</div>
    <hr>
    <div><b>Raporti i Shitjeve për sot (${todayStr}):</b></div>
    ${soldHtml}
    <div><b>Totali i produkteve te shitura:</b> ${totalQty} — <b>Të ardhurat:</b> ${totalRev} ALL</div>
    ${topSellerHtml}
    <hr>
    <div><b>Raport riporositjeje (2x/javë):</b></div>
    ${reorderHtml}
  `;
  txnTitleEl.textContent = 'Mbyllje dite + Raport'; showTxn(html);
}

/* ======= FINANCE (use purchase_price from products) ======= */
function computeRevenue(from=null,to=null){
  const fromD = from ? new Date(from) : null; const toD = to ? new Date(to) : null;
  let total = 0;
  salesHistory.forEach(s=>{
    const d = new Date(s.timestamp);
    if(fromD && d < fromD) return;
    if(toD && d > new Date(toD.getTime() + 24*3600*1000 -1)) return;
    total += Number(s.total) || 0;
  });
  return total;
}
function computeCOGS_from_stock(from=null,to=null){
  const fromD = from ? new Date(from) : null; const toD = to ? new Date(to) : null;
  let cogs = 0;
  salesHistory.forEach(s=>{
    const d = new Date(s.timestamp);
    if(fromD && d < fromD) return;
    if(toD && d > new Date(toD.getTime() + 24*3600*1000 -1)) return;
    s.items.forEach(it=>{
      const prod = products.find(p=>p.b === it.b);
      const unitCost = prod ? (Number(prod.purchase_price) || 0) : 0;
      cogs += unitCost * (Number(it.q) || 0);
    });
  });
  return Math.round(cogs);
}
function updateFinance(){
  const from = document.getElementById('finFrom').value || null;
  const to = document.getElementById('finTo').value || null;
  const revenue = computeRevenue(from,to);
  const cogs = computeCOGS_from_stock(from,to);
  const profit = revenue - cogs;
  const margin = revenue > 0 ? ((profit / revenue) * 100).toFixed(2) : '0.00';
  document.getElementById('finRevenue').innerText = revenue + ' ALL';
  document.getElementById('finCOGS').innerText = cogs + ' ALL';
  document.getElementById('finProfit').innerText = Math.round(profit) + ' ALL';
  document.getElementById('finMargin').innerText = `Marginë: ${margin}%`;
  updateFinanceChart(from,to);
}

/* ======= Finance Chart (clean init & update) ======= */
function initFinanceChart(){
  const canvas = document.getElementById('finChart');
  if(!canvas) return;
  const ctx = canvas.getContext('2d');
  if(finChart){ finChart.destroy(); finChart = null; }
  finChart = new Chart(ctx, {
    type: 'line',
    data: { labels: [], datasets: [
      { label: 'Të ardhurat (ALL)', data: [], borderColor: '#2563eb', backgroundColor: 'rgba(37,99,235,0.12)', fill: true },
      { label: 'Fitim (ALL)', data: [], borderColor: '#16a34a', backgroundColor: 'rgba(16,163,74,0.12)', fill: true }
    ]},
    options: {
      responsive: true,
      scales: { x:{ title:{ display:true, text:'Datë' }}, y:{ title:{ display:true, text:'ALL' } } },
      plugins: { legend: { position:'top' } }
    }
  });
  updateFinance(); // initial populate
}

function updateFinanceChart(from=null,to=null){
  if(!finChart) initFinanceChart();
  // determine range (default last 14 days)
  let fromDate = from ? new Date(from) : null;
  let toDate = to ? new Date(to) : null;
  if(!fromDate || !toDate){ toDate = new Date(); fromDate = new Date(); fromDate.setDate(toDate.getDate() - 13); }
  if(fromDate > toDate){ const tmp = fromDate; fromDate = toDate; toDate = tmp; }
  // build day keys
  const labels = [];
  const revMap = {}, profitMap = {};
  const dayCount = Math.round((toDate - fromDate) / (24*3600*1000)) + 1;
  for(let i=0;i<dayCount;i++){
    const d = new Date(fromDate.getFullYear(), fromDate.getMonth(), fromDate.getDate() + i);
    const key = d.toISOString().slice(0,10);
    labels.push(key); revMap[key] = 0; profitMap[key] = 0;
  }
  // accumulate by day
  salesHistory.forEach(s=>{
    const day = s.timestamp.slice(0,10);
    if(!(day in revMap)) return;
    const revenue = Number(s.total) || 0;
    let cogs = 0;
    s.items.forEach(it=>{
      const prod = products.find(p=>p.b === it.b);
      const unitCost = prod ? (Number(prod.purchase_price) || 0) : 0;
      cogs += unitCost * (Number(it.q) || 0);
    });
    revMap[day] += revenue;
    profitMap[day] += (revenue - cogs);
  });
  const revData = labels.map(l=>revMap[l] || 0);
  const profitData = labels.map(l=>profitMap[l] || 0);
  finChart.data.labels = labels;
  finChart.data.datasets[0].data = revData;
  finChart.data.datasets[1].data = profitData;
  finChart.update();
}

/* ======= UTILS ======= */
function updateDaily(){ dailyEl.textContent = daily; }
function showTxn(html){ txnMsgEl.innerHTML = html; txnModalEl.style.display = 'block'; }
function closeTxn(){ txnModalEl.style.display = 'none'; txnMsgEl.innerHTML = ''; }
function escapeHtml(str){ return ('' + (str || '')).replace(/[&<>"']/g, s=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[s])); }

/* ======= STORAGE SYNC ACROSS TABS ======= */
window.addEventListener('storage', (e)=>{
  if(e.key === KEY_PRODUCTS){ products = JSON.parse(e.newValue || '[]'); renderProducts(); initFinanceChart(); }
  if(e.key === KEY_SALES_HISTORY){ salesHistory = JSON.parse(e.newValue || '[]'); renderHistory(); updateFinance(); initFinanceChart(); }
  if(e.key === KEY_DAILY){ daily = +e.newValue || 0; updateDaily(); }
});

/* ======= INITIALIZE UI ======= */
/* Pre-fill convenience login */
document.getElementById('u').value = 'admin'; document.getElementById('p').value = 'admin';
renderProducts(); renderHistory(); updateDaily(); initFinanceChart();

/* Device time display */
function updateDeviceTimeDisplays(){
  const now = new Date();
  const hh = String(now.getHours()).padStart(2,'0');
  const mm = String(now.getMinutes()).padStart(2,'0');
  const ss = String(now.getSeconds()).padStart(2,'0');
  deviceTimeEl.textContent = `${hh}:${mm}:${ss}`;
  finDeviceTimeEl.textContent = `${hh}:${mm}:${ss}`;
}
setInterval(updateDeviceTimeDisplays, 1000);
updateDeviceTimeDisplays();

</script>

</body>
</html>