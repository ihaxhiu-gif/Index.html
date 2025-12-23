<!DOCTYPE html>
<html lang="sq">
<head>
<meta charset="UTF-8">
<title>POS Market – FINAL ABSOLUT (perditesuar)</title>

<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">

<style>
body{margin:0;font-family:Segoe UI;background:#eef2f7}
header{background:#1e293b;color:#fff;padding:15px}
nav button{margin:4px;padding:10px;border:none;border-radius:10px;background:#334155;color:#fff}
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
.modal-content.small-modal{max-width:420px;padding:12px;text-align:left}
.modal-content.small-modal h4{margin:6px 0}
.txn-list{margin:6px 0;padding-left:18px}
.txn-summary{margin-top:8px;font-weight:600}
</style>

<script src="https://unpkg.com/@ericblade/quagga2/dist/quagga.js"></script>
</head>
<body>

<header>
<h2>🛒 POS Market</h2>
<nav id="menu" style="display:none">
<button onclick="openSec('prod')" class="admin">Stok</button>
<button onclick="openSec('sale')">Shitje</button>
<button onclick="openSec('bil')" class="admin">Bilanc</button>
<button onclick="openSec('hist')">Historik</button>
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
  <input id="pb" placeholder="Barkodi" class="col">
</div>
<div class="row" style="margin-top:8px">
  <input id="pp" type="number" placeholder="Çmimi" class="col">
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
/* ======= DATA & STATE ======= */
const users=[{u:'admin',p:'admin',r:'admin'},{u:'kasier',p:'kasier',r:'kasier'}];
let role=null, scanTarget=null, scanLock=false, camMode='environment';
let quaggaHandler = null;
let quaggaRunning = false;

/* Load persistent data */
let products = JSON.parse(localStorage.getItem('p') || '[]');
let sales = []; // current basket
let salesHistory = JSON.parse(localStorage.getItem('salesHistory') || '[]');
let daily = +localStorage.getItem('daily') || 0;

/* Element refs (avoid relying on implicit globals) */
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
const viewModalEl = document.getElementById('viewModal');
const settleAmountEl = document.getElementById('settleAmount');
const txnModalEl = document.getElementById('txnModal');
const txnMsgEl = document.getElementById('txnMsg');
const txnTitleEl = document.getElementById('txnTitle');

/* ======= LOGIN ======= */
function doLogin(){
  let f=users.find(x=>x.u===u.value&&x.p===p.value);
  if(!f) return msg.textContent='Gabim login';
  role=f.r;
  loginSec.style.display='none';
  menu.style.display='block';
  document.querySelectorAll('.admin').forEach(e=>e.style.display=role==='admin'?'block':'none');
  openSec('sale'); renderProducts(); updateDaily(); renderHistory();
}
function logout(){ location.reload(); }
function openSec(id){
  document.querySelectorAll('section').forEach(s=>s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

/* ======= STOK ======= */
function addProduct(){
  products.push({n:pn.value||'Pa emër',b:pb.value||'',p:+pp.value||0,s:+ps.value||0});
  store();
  pn.value=pb.value=pp.value=ps.value='';
  renderProducts();
}
function renderProducts(){
  prodTableEl.innerHTML = '<tr><th>Emër</th><th>Barkod</th><th>Çmim</th><th>Stok</th><th>❌</th></tr>';
  products.forEach((p,i)=>{
    prodTableEl.innerHTML += `
    <tr>
      <td><input value="${escapeHtml(p.n)}" onchange="products[${i}].n=this.value;store()"></td>
      <td><input value="${escapeHtml(p.b)}" onchange="products[${i}].b=this.value;store()"></td>
      <td><input type="number" value="${p.p}" onchange="products[${i}].p=+this.value;store()"></td>
      <td><input type="number" value="${p.s}" onchange="products[${i}].s=+this.value;store()"></td>
      <td><button onclick="products.splice(${i},1);store();renderProducts()">🗑️</button></td>
    </tr>`;
  });
}

/* ======= SHITJE ======= */
function addToSale(p){
  if(p.s<1) return alert('Stoku = 0');
  let s = sales.find(x=>x.b===p.b);
  if(s){ if(s.q+1>p.s) return alert('Sasia tejkalon stoqen'); s.q++; }
  else sales.push({b:p.b,n:p.n,p:p.p,q:1});
  drawSale();
}
function manualAdd(){
  let v = saleScanEl.value.trim().toLowerCase();
  if(!v) return;
  let p = products.find(x=>x.b===v || x.n.toLowerCase().includes(v));
  if(!p) return alert('Nuk u gjet');
  addToSale(p); saleScanEl.value=''; saleScanEl.focus();
}
saleScanEl.addEventListener('keydown', e=>{ if(e.key==='Enter') manualAdd(); });

/* ======= SHITJE + LLOGARITJE ======= */
function drawSale(){
  saleTableEl.innerHTML = '<tr><th>Produkt</th><th>Sasi</th><th>Çmim</th><th>Total</th><th></th></tr>';
  sales.forEach((x,i)=>{
    saleTableEl.innerHTML += `
    <tr>
      <td>${escapeHtml(x.n)}</td>
      <td>
        <button class="qtyBtn" onclick="changeQty(${i},-1)">➖</button>
        ${x.q}
        <button class="qtyBtn" onclick="changeQty(${i},1)">➕</button>
      </td>
      <td>${x.p}</td>
      <td>${x.q*x.p}</td>
      <td><button onclick="sales.splice(${i},1);drawSale();">🗑️</button></td>
    </tr>`;
  });
  recalc();
}
function changeQty(i,delta){
  const item = sales[i];
  if(!item) return;
  const prod = products.find(p=>p.b===item.b);
  item.q += delta;
  if(item.q < 1) { sales.splice(i,1); }
  if(prod && item.q > prod.s){ item.q = prod.s; alert('Sasia tejkalon stoqen'); }
  drawSale();
}
function recalc(){
  let total=0; sales.forEach(x=>total+=x.q*x.p);
  totEl.textContent = total;
  let cash = (+paidEl.value||0);
  let diff = cash - total;
  if(diff < 0){
    changeEl.textContent = `Mungojnë ${Math.abs(diff)} ALL`;
    changeEl.style.color='red';
  } else {
    changeEl.textContent = `Kusur ${diff} ALL`;
    changeEl.style.color='green';
  }
}
paidEl.addEventListener('input', recalc);

/* ======= CAMERA (improve close handling + defensive Quagga use) ======= */
camCloseBtn.addEventListener('click', stopCam);
// Close when clicking the backdrop
camEl.addEventListener('click', (e)=>{
  if(e.target === camEl) stopCam();
});
// Close on Escape
document.addEventListener('keydown', (e)=>{
  if(e.key === 'Escape'){
    if(camEl.style.display === 'block') stopCam();
    if(viewModalEl.style.display === 'block') closeView();
    if(txnModalEl.style.display === 'block') closeTxn();
  }
});

function openCam(target, mode){
  scanTarget = target;
  camMode = mode;
  scanLock = false;
  camEl.style.display = 'block';

  // Ensure any previous run is stopped cleanly
  if(quaggaHandler && window.Quagga){
    try{
      if(Quagga.offDetected) Quagga.offDetected(quaggaHandler);
      else if(Quagga.off) Quagga.off('detected', quaggaHandler);
    }catch(e){}
    quaggaHandler = null;
  }
  // Init Quagga and set handler only after init success
  if(!window.Quagga){
    alert('Quagga nuk u gjet'); camEl.style.display='none'; return;
  }
  Quagga.init({
    inputStream:{
      type:"LiveStream",
      target: scannerEl,
      constraints:{
        facingMode: { ideal: camMode },
        width: { ideal: 640 },
        height: { ideal: 480 }
      }
    },
    locator:{patchSize:"medium",halfSample:true},
    decoder:{readers:["ean_reader","ean_8_reader","code_128_reader","upc_reader"]},
    locate:true
  }, err => {
    if(err){ alert("Kamera nuk u hap (HTTPS / leje): " + (err.message||err)); camEl.style.display='none'; return; }
    try{ Quagga.start(); quaggaRunning = true; }catch(e){ alert("Gabim duke nisur kamerën: "+(e.message||e)); camEl.style.display='none'; return; }

    // Assign handler now
    quaggaHandler = function(d){
      if(scanLock) return;
      scanLock = true;
      let code = d && d.codeResult && (d.codeResult.code || d.codeResult.codeResult);
      if(!code){ scanLock = false; return; }
      if(scanTarget === 'stock') {
        pb.value = code;
      } else if(scanTarget === 'sale'){
        let p = products.find(x=>x.b===code);
        if(p) addToSale(p);
        else alert('Barkodi nuk u gjet: ' + code);
      }
      // Close a bit later so user can see scanner result
      setTimeout(stopCam, 400);
    };

    // Attach detection listener (defensive)
    try{
      if(Quagga.onDetected) Quagga.onDetected(quaggaHandler);
      else if(Quagga.on) Quagga.on('detected', quaggaHandler);
    }catch(e){ /* ignore */ }
  });
}

function stopCam(){
  // Hide UI first (avoid blocked clicks)
  camEl.style.display = 'none';
  scanLock = false;

  // Remove detector and stop Quagga (defensive)
  try{
    if(quaggaHandler && window.Quagga){
      if(Quagga.offDetected) Quagga.offDetected(quaggaHandler);
      else if(Quagga.off) Quagga.off('detected', quaggaHandler);
    }
  }catch(e){ /* ignore */ }

  try{
    if(window.Quagga && quaggaRunning){
      Quagga.stop();
    }
  }catch(e){ /* ignore */ }

  quaggaHandler = null;
  quaggaRunning = false;
}

/* ======= PAGESA & BILANC ======= */
function pay(){
  let total = +totEl.textContent || 0;
  let cash = +paidEl.value || 0;
  if(sales.length===0) return alert('Shporta është bosh');

  const clientName = (client.value||'').trim();

  // compute change and net collected (net is what stays in register)
  let changeAmount = Math.max(0, cash - total);
  let netCollected = Math.min(cash, total); // this is what should be added to daily
  let due = Math.max(0, total - cash);
  let status = cash >= total ? 'paid' : 'owed';

  // Update stock immediately and persist
  for(let item of sales){
    let prod = products.find(p=>p.b===item.b);
    if(prod) prod.s = Math.max(0, prod.s - item.q);
  }
  store(); // persist products right away

  const timestamp = new Date().toISOString();
  const record = {
    id: timestamp + '_' + Math.random().toString(36).slice(2,7),
    timestamp,
    client: clientName || null,
    items: JSON.parse(JSON.stringify(sales)),
    total,
    // store amountPaid as the actual collected amount (net), and also keep raw cashGiven
    amountPaid: netCollected,
    cashGiven: cash,
    change: changeAmount,
    due,
    status
  };
  // Add to history and persist
  salesHistory.unshift(record);
  localStorage.setItem('salesHistory', JSON.stringify(salesHistory));

  // Update daily with the amount actually collected now (netCollected)
  daily += netCollected;
  localStorage.setItem('daily', daily);

  // Clear current basket and UI
  store(); cancel(); updateDaily(); renderHistory();

  // Show success modal with details (products, amount given, change)
  if(status==='paid'){
    // Build product list HTML
    let prodHtml = '<ul class="txn-list">';
    record.items.forEach(it=>{
      prodHtml += `<li>${escapeHtml(it.n)} x${it.q} = ${it.q * it.p} ALL</li>`;
    });
    prodHtml += '</ul>';

    const html = `
      <div style="color:green;font-weight:700;margin-bottom:6px">Transaksioni u mbyll me sukses</div>
      <div><b>Produkte:</b>${prodHtml}</div>
      <div class="txn-summary">Total: ${record.total} ALL</div>
      <div>Klienti dha: ${record.cashGiven} ALL</div>
      <div>Kusur: ${record.change} ALL</div>
      <div class="small" style="margin-top:6px">Shuma e shtuar në arkë (neto): ${record.amountPaid} ALL</div>
    `;
    txnTitleEl.textContent = 'Shitje e plotë';
    showTxn(html);
  } else {
    const html = `
      <div style="color:#b45f00;font-weight:700;margin-bottom:6px">Shitja u regjistrua si BORXH</div>
      <div><b>Produkte:</b><ul class="txn-list">${record.items.map(it=>`<li>${escapeHtml(it.n)} x${it.q} = ${it.q*it.p} ALL</li>`).join('')}</ul></div>
      <div class="txn-summary">Total: ${record.total} ALL</div>
      <div>Paguat tani (neto): ${record.amountPaid} ALL</div>
      <div>Mbetje (borxh): ${record.due} ALL</div>
    `;
    txnTitleEl.textContent = 'Shitje me borxh';
    showTxn(html);
  }
}

/* Cancel current sale (keeps products/state persisted) */
function cancel(){
  sales = []; saleTableEl.innerHTML=''; totEl.textContent=0; paidEl.value=''; changeEl.textContent=0; client.value='';
}

/* ======= HISTORIK ======= */
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
  // store current viewed id on modal
  viewModalEl.dataset.currentId = id;
  // Pre-fill settle amount with due
  settleAmountEl.value = r.due || '';
  viewModalEl.style.display='block';
}
function closeView(){
  viewModalEl.style.display='none';
  delete viewModalEl.dataset.currentId;
}
function deleteSale(id){
  if(!confirm('Fshi këtë regjistrim?')) return;
  salesHistory = salesHistory.filter(x=>x.id!==id);
  localStorage.setItem('salesHistory', JSON.stringify(salesHistory));
  renderHistory();
}

/* ======= SHLYERJE BORXHI ======= */
function settleDebt(){
  const id = viewModalEl.dataset.currentId;
  if(!id) return alert('Nuk ka shitje të zgjedhur');
  const r = salesHistory.find(x=>x.id===id);
  if(!r) return alert('Nuk u gjet shitja');
  let amt = +settleAmountEl.value || 0;
  if(amt <= 0) return alert('Shuma duhet > 0');
  if(r.due <= 0) return alert('Nuk ka borxh për këtë shitje');

  const payNow = Math.min(amt, r.due);
  r.amountPaid += payNow;
  r.due -= payNow;
  if(r.due <= 0) { r.status = 'paid'; r.due = 0; }
  else r.status = 'owed';

  // Update daily with collected amount
  daily += payNow;
  localStorage.setItem('daily', daily);

  // Persist history
  localStorage.setItem('salesHistory', JSON.stringify(salesHistory));
  updateDaily(); renderHistory(); viewSale(id); // re-open modal with updated values
  showTxn(`<div style="color:green;font-weight:700">Transaksioni u mbyll me sukses</div><div>U faturua shuma: ${payNow} ALL</div>`);
}

/* ======= EXPORT CSV ======= */
function exportCSV(){
  if(!salesHistory.length) return alert('Nuk ka të dhëna për eksport');
  const rows = [];
  const header = ['id','timestamp','client','total','amountPaid','cashGiven','change','due','status','items'];
  rows.push(header.join(','));
  salesHistory.slice().reverse().forEach(r=>{
    const itemsText = r.items.map(i=>`${i.n} x${i.q}=${i.q*i.p}`).join(' | ');
    const row = [
      `"${r.id}"`,
      `"${r.timestamp}"`,
      `"${(r.client||'')}"`,
      r.total,
      r.amountPaid,
      r.cashGiven !== undefined ? r.cashGiven : '',
      r.change,
      r.due,
      r.status,
      `"${itemsText}"`
    ];
    rows.push(row.join(','));
  });
  const csv = rows.join('\n');
  const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'sales_history.csv';
  a.click();
  URL.revokeObjectURL(url);
}

/* ======= CLEAR ALL (lokal) ======= */
function clearOld(){
  if(!confirm('Je i sigurt? Kjo do fshij historikun lokal.')) return;
  salesHistory = [];
  localStorage.removeItem('salesHistory');
  renderHistory();
}

/* ======= BILANCI / MBYLL DITA ======= */
function updateDaily(){ dailyEl.textContent = daily; }
cashRealEl.addEventListener('input', ()=>{
  let d = (+cashRealEl.value||0) - daily;
  diffEl.textContent = d + ' ALL'; diffEl.style.color = d < 0 ? 'red' : 'green';
});
function closeDay(){
  const sys = daily;
  const arka = +cashRealEl.value || 0;
  const diffv = arka - sys;

  // store closure record
  const closures = JSON.parse(localStorage.getItem('dayClosures')||'[]');
  const closure = {timestamp:new Date().toISOString(), system:sys, cash:arka, diff:diffv};
  closures.push(closure);
  localStorage.setItem('dayClosures', JSON.stringify(closures));

  // reset daily
  daily = 0; localStorage.setItem('daily',0);
  cashRealEl.value=''; updateDaily(); diffEl.textContent=0;

  // Build modal html (same style as txn modal)
  const html = `
    <div style="color:green;font-weight:700;margin-bottom:6px">Transaksioni u mbyll me sukses</div>
    <div><b>Bilanci i mbyllur:</b></div>
    <div>Shuma në sistem (duhet në arkë): ${closure.system} ALL</div>
    <div>Arka (me dore): ${closure.cash} ALL</div>
    <div style="margin-top:6px"><b>Diferenca:</b> ${closure.diff} ALL</div>
    <div class="small" style="margin-top:8px">Koha: ${closure.timestamp.replace('T',' ').slice(0,19)}</div>
  `;
  txnTitleEl.textContent = 'Mbyllje dite';
  showTxn(html);
}

/* ======= TRANSACTION MODAL UTILS ======= */
function showTxn(html){
  // Accept HTML string and display in txn modal
  txnMsgEl.innerHTML = html;
  txnModalEl.style.display = 'block';
}
function closeTxn(){
  txnModalEl.style.display = 'none';
  txnMsgEl.innerHTML = '';
}

/* ======= UTIL ======= */
function store(){ localStorage.setItem('p',JSON.stringify(products)); renderProducts(); }
// simple html escaper
function escapeHtml(str){ return (''+str).replace(/[&<>"']/g, s=>({ '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[s])); }

/* ======= SYNC BETWEEN TABS ======= */
/* When data changes in another tab, update current UI in real time */
window.addEventListener('storage', (e)=>{
  if(e.key === 'p'){
    products = JSON.parse(e.newValue || '[]');
    renderProducts();
  }
  if(e.key === 'salesHistory'){
    salesHistory = JSON.parse(e.newValue || '[]');
    renderHistory();
  }
  if(e.key === 'daily'){
    daily = +e.newValue || 0;
    updateDaily();
  }
});

/* ======= INITIAL RENDER ======= */
renderProducts();
renderHistory();
updateDaily();
</script>

</body>
</html>