<!DOCTYPE html>
<html lang="sq">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="apple-mobile-web-app-capable" content="yes">
<title>POS Market Ultra Final</title>

<style>
:root{
  --bg:#eef4ff;--card:#fff;--primary:#2563eb;--primary2:#1d4ed8;
  --nav:#111827;--text:#1f2937;--muted:#6b7280;--line:#e5e7eb;
  --success:#16a34a;--danger:#dc2626;--warning:#b45309;
  --shadow:0 10px 26px rgba(15,23,42,.08);--radius:16px
}
*{box-sizing:border-box}
html,body{
  margin:0;min-height:100%;
  font-family:Segoe UI,Roboto,Arial,sans-serif;
  background:var(--bg);color:var(--text)
}
header{
  position:sticky;top:0;z-index:20;display:flex;
  align-items:center;justify-content:space-between;gap:12px;
  flex-wrap:wrap;padding:14px 18px;color:#fff;
  background:linear-gradient(135deg,var(--nav),#1f2937)
}
header h2{margin:0;font-size:1.15rem}
nav{display:flex;gap:8px;flex-wrap:wrap}
section{display:none;padding:18px}
section.active{display:block}
.card{
  padding:18px;margin-bottom:14px;background:var(--card);
  border:1px solid #94a3b82e;border-radius:var(--radius);
  box-shadow:var(--shadow)
}
.card h3{margin:0 0 12px}
.row{display:flex;gap:10px;flex-wrap:wrap}
.col{flex:1;min-width:130px}
input,select,button{
  font:inherit;padding:10px 12px;border:1px solid #cbd5e1;
  border-radius:10px;outline:0
}
input:focus,select:focus{
  border-color:var(--primary);box-shadow:0 0 0 3px #2563eb22
}
button{
  border:0;color:#fff;background:linear-gradient(135deg,var(--primary),var(--primary2));
  font-weight:700;cursor:pointer;box-shadow:0 7px 16px #2563eb33
}
button:hover{transform:translateY(-1px)}
button.secondary{background:linear-gradient(135deg,#64748b,#475569)}
button.danger{background:linear-gradient(135deg,#dc2626,#b91c1c)}
button:disabled{opacity:.55;cursor:not-allowed;transform:none}
nav button{background:#ffffff18;color:#fff}
table{width:100%;margin-top:12px;border-collapse:collapse;background:#fff}
th,td{padding:9px 7px;border-bottom:1px solid var(--line);text-align:center;vertical-align:middle}
th{background:#f8fafc;color:#334155}
tr:last-child td{border-bottom:0}
.small{color:var(--muted);font-size:.9rem}
.muted{color:var(--muted)}
.admin{display:none}
.stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(170px,1fr));gap:12px;margin-bottom:14px}
.stat{padding:14px;border:1px solid #2563eb22;border-radius:12px;background:linear-gradient(135deg,#f8fbff,#eef6ff)}
.stat-label{color:var(--muted);font-size:.8rem;text-transform:uppercase}
.stat-value{margin-top:5px;font-size:1.35rem;font-weight:800}
.loyalty{margin-top:12px;padding:12px;border:1px solid #bfdbfe;border-radius:12px;background:linear-gradient(135deg,#eff6ff,#dbeafe)}
.green{color:var(--success);font-weight:700}
.red{color:var(--danger);font-weight:700}
.warn{color:var(--warning);font-weight:700}
.alert-bell{display:inline-flex;gap:8px;align-items:center;padding:7px 12px;border-radius:999px;background:#f59e0b;color:#111827;font-weight:800;cursor:pointer}
.badge{background:#ef4444;color:#fff;border-radius:999px;min-width:20px;padding:2px 7px;text-align:center;font-size:.75rem}
.results{display:none;margin-top:8px;padding:8px;border:1px solid #bfdbfe;border-radius:10px;background:#f8fbff}
.result-row{display:flex;justify-content:space-between;align-items:center;gap:8px;padding:8px 0;border-bottom:1px solid var(--line)}
.result-row:last-child{border-bottom:0}
.expired{background:#fee2e2}.expiring{background:#fff7ed}.lowstock{background:#fff7f0}
.modal{position:fixed;inset:0;z-index:90;display:none;overflow:auto;padding:20px;background:#0f172a99}
.modal-content{width:min(95%,760px);max-height:82vh;overflow:auto;margin:40px auto;padding:18px;border-radius:18px;background:#fff;box-shadow:0 20px 45px #0003}
@media(max-width:700px){
  .row{flex-direction:column}nav{width:100%}nav button{flex:1 1 100%}
  table{display:block;overflow-x:auto;white-space:nowrap}
}
@media print{
  body *{visibility:hidden!important}
  #printArea,#printArea *{visibility:visible!important}
  #printArea{position:absolute;left:0;top:0;width:100%;padding:10px;background:#fff}
}
</style>
</head>

<body>

<header>
  <div style="display:flex;align-items:center;gap:12px;flex-wrap:wrap">
    <h2>🛒 POS Market Ultra Final</h2>
    <div class="alert-bell" onclick="openAlertsModal()">
      ALARME <span id="alertCount" class="badge">0</span>
    </div>
  </div>

  <nav id="menu" style="display:none">
    <button class="admin" onclick="openSec('prod')">Stok</button>
    <button onclick="openSec('sale')">Shitje</button>
    <button onclick="openSec('bil')">Bilanc</button>
    <button onclick="openSec('hist')">Historik</button>
    <button onclick="openSec('clients')">Klientët</button>
    <button class="admin" onclick="openSec('suppliers')">Furnitorët</button>
    <button class="admin" onclick="openSec('settings')">Cilësimet</button>
    <button onclick="logout()">Dil</button>
  </nav>
</header>

<section id="loginSec" class="active">
  <div class="card" style="max-width:440px;margin:40px auto">
    <h3>Login</h3>
    <input id="u" placeholder="User" style="width:100%;margin-bottom:8px">
    <input id="p" type="password" placeholder="Password" style="width:100%;margin-bottom:8px">
    <button onclick="doLogin()">Hyr</button>
    <p id="msg" class="red"></p>
    <p class="small">Admin: admin / admin<br>Kasier: kasier / kasier</p>
  </div>
</section>

<section id="prod">
  <div class="card admin">
    <h3>Shto Produkt</h3>

    <div class="row">
      <input id="pn" class="col" placeholder="Emri">
      <input id="pb" class="col" placeholder="Barkodi / Scanner USB">
    </div>

    <div class="row" style="margin-top:8px">
      <select id="punit" class="col">
        <option value="piece">Copë</option>
        <option value="kg">Kilogram</option>
      </select>
      <input id="pp" class="col" type="number" min="0" step=".01" placeholder="Çmimi / Çmimi për kg">
      <input id="pc" class="col" type="number" min="0" step=".01" placeholder="Kostoja e blerjes">
      <input id="ps" class="col" type="number" min="0" step=".001" placeholder="Stoku">
    </div>

    <div class="row" style="margin-top:8px">
      <select id="pcat" class="col">
        <option value="ushqim">Ushqim</option>
        <option value="pije">Pije</option>
        <option value="higjienike">Higjienike</option>
      </select>
      <input id="pexp" type="date" class="col">
      <input id="pmin" type="number" min="0" step=".001" class="col" placeholder="Min Stock">
    </div>

    <button style="margin-top:10px" onclick="addProduct()">➕ Shto Produkt</button>
    <p class="small">Për produktet me kg, çmimi është për 1 kg.</p>
  </div>

  <div class="card">
    <h3>Inventari</h3>
    <table id="prodTable"></table>
  </div>
</section>

<section id="sale">
  <div id="statsGrid" class="stats"></div>

  <div class="card">
    <div class="row">
      <input id="saleScan" class="col" placeholder="Emër ose barkod / Skaner USB" autocomplete="off">
      <input id="saleWeight" type="number" min=".001" step=".001" class="col" placeholder="Pesha në kg">
      <input id="client" class="col" placeholder="Emri i klientit">
      <input id="clientPhone" class="col" placeholder="Telefoni i klientit">
    </div>

    <div id="customerResults" class="results"></div>

    <div class="row" style="margin-top:10px">
      <div class="col">
        <label class="small">Valuta</label>
        <select id="saleCurrency" style="width:100%" onchange="recalc()">
          <option value="ALL">Lek (ALL)</option>
          <option value="EUR">Euro (EUR)</option>
        </select>
      </div>

      <div class="col">
        <label class="small">Ulje (%)</label>
        <input id="discountPct" type="number" min="0" max="100" step=".01" value="0" style="width:100%" oninput="recalc()">
      </div>

      <div class="col">
        <label class="small">Ulje fikse (ALL)</label>
        <input id="discountALL" type="number" min="0" step=".01" value="0" style="width:100%" oninput="recalc()">
      </div>

      <div class="col">
        <label class="small">Mënyra e pagesës</label>
        <select id="paymentMethod" style="width:100%" onchange="paymentChanged()">
          <option value="cash_all">Cash (LEK)</option>
          <option value="card">Kartë</option>
          <option value="cash_eur">Cash (EUR)</option>
        </select>
      </div>
    </div>

    <button style="margin-top:10px" onclick="manualAdd()">➕ Shto në shportë</button>
    <p class="small">Për produktet me kg vendos peshën para shtimit.</p>
  </div>

  <div class="card">
    <table id="saleTable"></table>

    <h3>Total: <span id="tot">0.00</span> ALL</h3>
    <div id="totInEur" class="small"></div>

    <div class="loyalty">
      <b>Programi Loyal</b>
      <div id="loyaltyInfo" class="small"></div>

      <label>
        <input id="useLoyaltyPoints" type="checkbox" onchange="recalc()">
        Përdor pikët e klientit
      </label>

      <div id="loyaltyDiscount" class="small"></div>
    </div>

    <div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:12px">
      <input id="paid" type="number" min="0" step=".01" placeholder="Shuma nga klienti" style="flex:1;min-width:180px">
      <button onclick="pay()">Paguaj</button>
      <button class="secondary" onclick="cancelSale()">Anulo</button>
    </div>

    <h3>Kusur / Mungesë: <span id="change">0.00</span></h3>
  </div>
</section>

<section id="bil">
  <div class="card">
    <h3>Hapja e Kasës</h3>

    <p class="small">
      Thyerja fillestare përdoret për kusur dhe nuk konsiderohet shitje.
    </p>

    <div class="row">
      <div class="col">
        <label class="small">Thyerja fillestare (ALL)</label>
        <input id="openingFloatInput" type="number" min="0" step=".01" placeholder="P.sh. 10000" style="width:100%">
      </div>

      <div class="col">
        <label class="small">Statusi</label>
        <div id="kasaStatus" class="red" style="padding:10px 0">Kasa e mbyllur</div>
      </div>

      <div class="col">
        <label class="small">Thyerja aktive</label>
        <div style="padding:10px 0"><b><span id="activeFloat">0.00</span> ALL</b></div>
      </div>
    </div>

    <button style="margin-top:10px" onclick="openKasa()">Hap Kasa</button>
  </div>

  <div class="card">
    <h3>Bilanci i Arkës</h3>

    <div class="stats">
      <div class="stat"><div class="stat-label">Cash ALL Neto</div><div class="stat-value"><span id="cashBalanceALL">0.00</span> ALL</div></div>
      <div class="stat"><div class="stat-label">Kartë</div><div class="stat-value"><span id="cardBalanceALL">0.00</span> ALL</div></div>
      <div class="stat"><div class="stat-label">Cash EUR</div><div class="stat-value"><span id="cashBalanceEUR">0.00</span> EUR</div></div>
      <div class="stat"><div class="stat-label">Thyerja</div><div class="stat-value"><span id="activeFloatCard">0.00</span> ALL</div></div>
    </div>

    <p>Cash ALL Neto: <b><span id="daily">0.00</span> ALL</b></p>
    <p>Kartë: <b><span id="dailyCard">0.00</span> ALL</b></p>
    <p>Cash EUR: <b><span id="dailyEUR">0.00</span> EUR</b></p>

    <hr>

    <p>Arka reale Cash ALL:
      <input id="cashRealALL" type="number" min="0" step=".01" style="width:170px">
    </p>

    <p>Arka reale Cash EUR:
      <input id="cashRealEUR" type="number" min="0" step=".01" style="width:170px">
    </p>

    <p class="small">
      Në pagesat EUR, eurot futen në Cash EUR dhe kusuri në ALL
      zbritet nga Cash ALL.
    </p>

    <p>
      Kursi:
      <input id="exchangeRateInput" type="number" min=".0001" step=".01" style="width:130px">
      ALL për 1 EUR
      <button onclick="saveExchangeRate()">Ruaj</button>
    </p>

    <button onclick="closeDay()">Mbyll Ditën</button>
    <button class="secondary" onclick="exportDailyClosuresExcel()">📊 Eksporto Bilancet Ditore</button>
  </div>

  <div class="card">
    <h3>Fitimi dhe Grafiku i Shitjeve</h3>

    <div class="stats">
      <div class="stat">
        <div class="stat-label">Shitje Totale</div>
        <div class="stat-value"><span id="totalSalesProfit">0.00</span> ALL</div>
      </div>
      <div class="stat">
        <div class="stat-label">Kosto Malli</div>
        <div class="stat-value"><span id="costGoodsSold">0.00</span> ALL</div>
      </div>
      <div class="stat">
        <div class="stat-label">Fitim Bruto</div>
        <div class="stat-value"><span id="dailyGrossProfit">0.00</span> ALL</div>
      </div>
    </div>

    <canvas id="salesChart" width="900" height="260" style="width:100%;max-width:900px;height:260px;border:1px solid #ddd;border-radius:12px;background:#fff"></canvas>
  </div>
</section>

<section id="hist">
  <div class="card">
    <h3>Historiku i Shitjeve</h3>
    <button onclick="exportCSV()">⬇️ Eksporto CSV</button>
    <button class="secondary" onclick="clearOld()">🧹 Fshi Historikun</button>
    <table id="histTable"></table>
  </div>
</section>

<section id="clients">
  <div class="card">
    <h3>Klientët Loyal</h3>

    <div class="row">
      <input id="clientSearch" class="col" placeholder="Kërko me emër ose telefon">
      <button onclick="renderLoyaltyTable()">Kërko</button>
      <button class="secondary" onclick="resetClientFilter()">Pastro</button>
    </div>

    <div style="margin-top:12px">
      <button onclick="exportLoyaltyData()">⬇️ Eksporto Klientët</button>
      <button class="secondary" onclick="backupData()">💾 Backup</button>
      <button class="secondary" onclick="restoreData()">📥 Restore</button>
    </div>

    <table id="loyaltyTable"></table>
  </div>
</section>

<section id="suppliers">
  <div class="card admin">
    <h3>Furnitorët & Marrja e Mallit</h3>

    <div class="row">
      <input id="supplierName" class="col" placeholder="Emri i furnitorit">
      <input id="supplierPhone" class="col" placeholder="Telefoni">
      <input id="supplierInvoice" class="col" placeholder="Numri i faturës">
    </div>

    <hr>

    <h3>Produkti i furnizimit</h3>

    <div class="row">
      <input id="purchaseScan" class="col" placeholder="Barkod / emër produkti" autocomplete="off">
      <input id="purchaseQty" class="col" type="number" min=".001" step=".001" placeholder="Sasia">
      <input id="purchaseCost" class="col" type="number" min="0" step=".01" placeholder="Çmimi i blerjes">
    </div>

    <div class="row" style="margin-top:8px">
      <input id="purchaseProductName" class="col" placeholder="Emri i produktit të ri">
      <input id="purchaseBarcode" class="col" placeholder="Barkodi i produktit të ri">
    </div>

    <div class="row" style="margin-top:8px">
      <select id="purchaseUnit" class="col">
        <option value="piece">Copë</option>
        <option value="kg">Kilogram</option>
      </select>

      <input id="purchaseSalePrice" class="col" type="number" min="0" step=".01" placeholder="Çmimi i shitjes">

      <select id="purchaseCategory" class="col">
        <option value="ushqim">Ushqim</option>
        <option value="pije">Pije</option>
        <option value="higjienike">Higjienike</option>
      </select>
    </div>

    <div class="row" style="margin-top:8px">
      <input id="purchaseExpiry" class="col" type="date">
      <input id="purchaseMinStock" class="col" type="number" min="0" step=".001" placeholder="Min Stock">
    </div>

    <p class="small">
      Nëse barkodi ekziston, produkti gjendet automatikisht.
      Nëse nuk ekziston, plotëso emrin, barkodin dhe çmimin e shitjes
      për të krijuar produkt të ri.
    </p>

    <div class="row" style="margin-top:10px">
      <button onclick="addPurchaseItem()">➕ Shto në furnizim</button>
      <button class="secondary" onclick="cancelPurchaseCart()">Anulo</button>
      <button class="secondary" onclick="exportPurchaseCSV()">⬇️ Eksporto CSV</button>
    </div>

    <table id="purchaseTable"></table>

    <h3>Total Furnizimi: <span id="purchaseTotal">0.00</span> ALL</h3>

    <div class="row" style="margin-top:10px">
      <input id="purchasePaid" type="number" min="0" step=".01" placeholder="Shuma e paguar te furnitori" style="flex:1;min-width:180px">
      <select id="purchasePaymentMethod" style="width:180px">
        <option value="cash_all">Cash (ALL)</option>
        <option value="card">Kartë</option>
      </select>
      <button onclick="completePurchase()">✅ Kryej Furnizim</button>
    </div>

    <div id="purchaseSummary" class="small"></div>
  </div>

  <div class="card">
    <h3>Historiku i Furnizimeve</h3>
    <table id="purchaseHistoryTable"></table>
  </div>
</section>

<section id="settings">
  <div class="card admin">
    <h3>Cilësimet</h3>

    <div class="row">
      <input id="cfg_leadDays" class="col" type="number" min="1" value="3">
      <input id="cfg_reviewDays" class="col" type="number" min="1" value="7">
      <input id="cfg_safety" class="col" type="number" min=".1" step=".1" value="1.5">
    </div>

    <button style="margin-top:10px" onclick="saveSettings()">Ruaj Cilësimet</button>
  </div>
</section>

<div id="alertsModal" class="modal">
  <div class="modal-content">
    <h3>Alarmet</h3>
    <div id="alertsBody"></div>
    <button class="secondary" onclick="closeAlertsModal()">Mbyll</button>
  </div>
</div>

<div id="viewModal" class="modal">
  <div class="modal-content">
    <h3>Detajet e Shitjes</h3>
    <div id="viewBody"></div>
    <input id="settleAmount" type="number" min="0" step=".01" placeholder="Shlyerje ALL">
    <button onclick="settleDebt()">Shlyej Borxh</button>
    <button class="secondary" onclick="closeView()">Mbyll</button>
  </div>
</div>

<div id="txnModal" class="modal">
  <div class="modal-content">
    <h3 id="txnTitle"></h3>
    <div id="txnMsg"></div>
    <button class="secondary" onclick="closeTxn()">Mbyll</button>
  </div>
</div>

<div id="printArea" style="display:none"></div>

<script>
'use strict';

/* ================= HELPERS ================= */

const $ = id => document.getElementById(id);

function parse(value,fallback){
  try{return JSON.parse(value) ?? fallback}
  catch(error){return fallback}
}

function num(value,fallback=0){
  const n=Number(value);
  return Number.isFinite(n)?n:fallback;
}

function money(value){
  return num(value).toFixed(2);
}

function clean(value){
  return String(value??'').trim();
}

function normalized(value){
  return clean(value).toLowerCase().replace(/\s+/g,' ');
}

function esc(value){
  return String(value??'').replace(/[&<>"']/g,c=>({
    '&':'&amp;','<':'&lt;','>':'&gt;',
    '"':'&quot;',"'":'&#39;'
  }[c]));
}

function csvCell(value){
  return `"${String(value??'').replace(/"/g,'""')}"`
}

function localDate(value){
  const date=new Date(value);
  if(Number.isNaN(date.getTime()))return '';
  return `${date.getFullYear()}-${String(date.getMonth()+1).padStart(2,'0')}-${String(date.getDate()).padStart(2,'0')}`;
}

function dateTime(value){
  const date=new Date(value);
  return Number.isNaN(date.getTime())
    ? '--'
    : date.toLocaleString('sq-AL');
}

function signedMoney(value){
  const n=num(value);
  return n>0 ? `+${money(n)}` : n<0 ? `-${money(Math.abs(n))}` : '0.00';
}

function downloadFile(filename,content,type){
  const blob=new Blob([content],{type});
  const url=URL.createObjectURL(blob);
  const link=document.createElement('a');
  link.href=url;
  link.download=filename;
  document.body.appendChild(link);
  link.click();
  link.remove();
  setTimeout(()=>URL.revokeObjectURL(url),500);
}

/* ================= STATE ================= */

const users=[
  {u:'admin',p:'admin',r:'admin'},
  {u:'kasier',p:'kasier',r:'kasier'}
];

const POINTS_PER_ALL=100;
const ALL_PER_POINT=1;

let role='guest';
let products=parse(localStorage.getItem('p'),[]);
let cart=[];
let salesHistory=parse(localStorage.getItem('salesHistory'),[]);
let loyaltyCustomers=parse(localStorage.getItem('loyaltyCustomers'),{});
let suppliers=parse(localStorage.getItem('suppliers'),[]);
let purchaseHistory=parse(localStorage.getItem('purchaseHistory'),[]);
let supplierCart=[];

let cashALL=num(localStorage.getItem('cashALL'),num(localStorage.getItem('daily'),0));
let cardALL=num(localStorage.getItem('cardALL'),num(localStorage.getItem('cardBalanceALL'),0));
let cashEUR=num(localStorage.getItem('cashEUR'),num(localStorage.getItem('eurInRegister'),0));

let openingFloatALL=num(localStorage.getItem('openingFloatALL'),0);
let kasaOpenedAt=localStorage.getItem('kasaOpenedAt')||'';
let exchangeRate=Math.max(.0001,num(localStorage.getItem('exchangeRate'),100));

let reorderConfig=parse(localStorage.getItem('reorderCfg'),{
  leadDays:3,reviewPeriodDays:7,safetyStockFactor:1.5,minOrderQty:1
});

let currentSaleIndex=null;

/* ================= STORAGE ================= */

function save(){
  localStorage.setItem('p',JSON.stringify(products));
  localStorage.setItem('salesHistory',JSON.stringify(salesHistory));
  localStorage.setItem('loyaltyCustomers',JSON.stringify(loyaltyCustomers));
  localStorage.setItem('suppliers',JSON.stringify(suppliers));
  localStorage.setItem('purchaseHistory',JSON.stringify(purchaseHistory));

  localStorage.setItem('cashALL',String(cashALL));
  localStorage.setItem('cardALL',String(cardALL));
  localStorage.setItem('cashEUR',String(cashEUR));

  localStorage.setItem('daily',String(cashALL));
  localStorage.setItem('cardBalanceALL',String(cardALL));
  localStorage.setItem('eurInRegister',String(cashEUR));

  localStorage.setItem('openingFloatALL',String(openingFloatALL));
  localStorage.setItem('kasaOpenedAt',kasaOpenedAt);
  localStorage.setItem('exchangeRate',String(exchangeRate));
  localStorage.setItem('reorderCfg',JSON.stringify(reorderConfig));
}

/* ================= NORMALIZATION ================= */

function productData(product){
  return {
    n:clean(product.n||'Pa emër'),
    b:clean(product.b||''),
    unit:product.unit==='kg'?'kg':'piece',
    p:Math.max(0,num(product.p)),
    c:Math.max(0,num(product.c ?? product.cost ?? 0)),
    s:Math.max(0,num(product.s)),
    category:['ushqim','pije','higjienike'].includes(product.category)
      ? product.category
      : 'ushqim',
    expiry:/^\d{4}-\d{2}-\d{2}$/.test(product.expiry||'')
      ? product.expiry
      : '',
    minStock:Math.max(0,num(product.minStock??product.min))
  };
}

products=Array.isArray(products)?products.map(productData):[];

/* ================= AUTH ================= */

function doLogin(){
  const user=users.find(item=>
    item.u===clean($('u').value)&&
    item.p===clean($('p').value)
  );

  if(!user){
    $('msg').textContent='Gabim login.';
    return;
  }

  role=user.r;
  $('loginSec').style.display='none';
  $('menu').style.display='flex';

  document.querySelectorAll('.admin').forEach(element=>{
    element.style.display=role==='admin'
      ? element.tagName==='SECTION'?'block':'inline-block'
      :'none';
  });

  openSec('sale');
  renderAll();
}

function logout(){
  location.reload();
}

function openSec(id){
  document.querySelectorAll('section').forEach(section=>{
    section.classList.remove('active');
  });

  $(id)?.classList.add('active');
}

/* ================= PRODUCTS ================= */

function addProduct(){
  const product=productData({
    n:$('pn').value,
    b:$('pb').value,
    unit:$('punit').value,
    p:$('pp').value,
    c:$('pc').value,
    s:$('ps').value,
    category:$('pcat').value,
    expiry:$('pexp').value,
    minStock:$('pmin').value
  });

  if(!product.n||!product.b){
    alert('Emri dhe barkodi janë të detyrueshëm.');
    return;
  }

  if(products.some(item=>item.b===product.b)){
    alert('Ky barkod ekziston.');
    return;
  }

  products.push(product);
  save();

  ['pn','pb','pp','pc','ps','pexp','pmin']
    .forEach(id=>$(id).value='');

  $('punit').value='piece';
  $('pcat').value='ushqim';
  renderAll();
}

function updateProduct(index,field,value){
  const product=products[index];
  if(!product)return;

  if(['n','b','expiry'].includes(field)){
    product[field]=clean(value);
  }

  if(field==='unit'){
    product.unit=value==='kg'?'kg':'piece';
  }

  if(['p','c','s','minStock'].includes(field)){
    product[field]=Math.max(0,num(value));
  }

  if(field==='category'){
    product.category=value;
  }

  if(field==='b'&&products.some((item,itemIndex)=>
    itemIndex!==index&&item.b===product.b
  )){
    alert('Ky barkod ekziston te një produkt tjetër.');
    renderProducts();
    return;
  }

  save();
  renderAll();
}

function deleteProduct(index){
  if(!products[index])return;

  if(!confirm(`Fshi produktin "${products[index].n}"?`)){
    return;
  }

  products.splice(index,1);
  save();
  renderAll();
}

function renderProducts(){
  $('prodTable').innerHTML=`
    <tr>
      <th>Emër</th><th>Barkod</th><th>Njësia</th>
      <th>Çmimi</th><th>Kosto</th><th>Stok</th><th>Min</th>
      <th>Kategori</th><th>Skadenca</th><th>Alarm</th><th>Fshi</th>
    </tr>
  `;

  const today=new Date();

  products.forEach((product,index)=>{
    let rowClass='';
    let alarm='';

    if(product.expiry){
      const expiry=new Date(product.expiry+'T23:59:59');

      if(expiry<today){
        rowClass='expired';
        alarm='<span class="red">Skaduar</span>';
      }else{
        const days=Math.ceil((expiry.getTime()-today.getTime())/86400000);

        if(days<=7){
          rowClass='expiring';
          alarm=`<span class="warn">Skadon ${days}d</span>`;
        }
      }
    }

    if(product.s<=product.minStock){
      rowClass=rowClass||'lowstock';
      alarm+=(alarm?' • ':'')+'<span class="red">Stok i ulët</span>';
    }

    $('prodTable').insertAdjacentHTML('beforeend',`
      <tr class="${rowClass}">
        <td><input value="${esc(product.n)}" onchange="updateProduct(${index},'n',this.value)"></td>
        <td><input value="${esc(product.b)}" onchange="updateProduct(${index},'b',this.value)"></td>
        <td>
          <select onchange="updateProduct(${index},'unit',this.value)">
            <option value="piece" ${product.unit==='piece'?'selected':''}>Copë</option>
            <option value="kg" ${product.unit==='kg'?'selected':''}>Kg</option>
          </select>
        </td>
        <td><input type="number" min="0" step=".01" value="${product.p}" onchange="updateProduct(${index},'p',this.value)"></td>
        <td><input type="number" min="0" step=".01" value="${product.c}" onchange="updateProduct(${index},'c',this.value)"></td>
        <td><input type="number" min="0" step=".001" value="${product.s}" onchange="updateProduct(${index},'s',this.value)"></td>
        <td><input type="number" min="0" step=".001" value="${product.minStock}" onchange="updateProduct(${index},'minStock',this.value)"></td>
        <td>
          <select onchange="updateProduct(${index},'category',this.value)">
            <option value="ushqim" ${product.category==='ushqim'?'selected':''}>Ushqim</option>
            <option value="pije" ${product.category==='pije'?'selected':''}>Pije</option>
            <option value="higjienike" ${product.category==='higjienike'?'selected':''}>Higjienike</option>
          </select>
        </td>
        <td><input type="date" value="${product.expiry}" onchange="updateProduct(${index},'expiry',this.value)"></td>
        <td>${alarm||'—'}</td>
        <td><button class="danger" onclick="deleteProduct(${index})">🗑️</button></td>
      </tr>
    `);
  });
}

/* ================= DASHBOARD ================= */

function renderStats(){
  const today=localDate(new Date());

  const records=salesHistory.filter(record=>
    localDate(record.timestamp)===today
  );

  const total=records.reduce((sum,record)=>sum+num(record.totalAll),0);

  const low=products.filter(product=>product.s<=product.minStock).length;
  const expired=products.filter(product=>
    product.expiry &&
    new Date(product.expiry+'T23:59:59')<new Date()
  ).length;

  $('statsGrid').innerHTML=[
    ['Shitje sot',`${money(total)} ALL`],
    ['Produkte',products.length],
    ['Stok i ulët',low],
    ['Skaduar',expired]
  ].map(item=>`
    <div class="stat">
      <div class="stat-label">${item[0]}</div>
      <div class="stat-value">${item[1]}</div>
    </div>
  `).join('');
}

/* ================= ALERTS ================= */

function getAlerts(){
  const result=[];
  const now=new Date();

  products.forEach(product=>{
    if(product.s<=product.minStock){
      result.push(`Stok i ulët: ${product.n}`);
    }

    if(product.expiry){
      const expiry=new Date(product.expiry+'T23:59:59');
      const days=Math.ceil((expiry.getTime()-now.getTime())/86400000);

      if(expiry<now){
        result.push(`Skaduar: ${product.n}`);
      }else if(days<=7){
        result.push(`Skadon së shpejti: ${product.n} (${days} ditë)`);
      }
    }
  });

  return result;
}

function checkAlerts(){
  $('alertCount').textContent=getAlerts().length;
}

function openAlertsModal(){
  const alerts=getAlerts();

  $('alertsBody').innerHTML=alerts.length
    ? `<ul>${alerts.map(item=>`<li>${esc(item)}</li>`).join('')}</ul>`
    : '<p>Nuk ka alarme.</p>';

  $('alertsModal').style.display='block';
}

function closeAlertsModal(){
  $('alertsModal').style.display='none';
}

/* ================= LOYALTY ================= */

function customerKey(){
  const name=normalized($('client').value);
  const phone=normalized($('clientPhone').value);

  if(!name&&!phone)return '';
  return `${name}|${phone}`;
}

function getCustomer(create=true){
  const key=customerKey();

  if(!key)return null;

  if(!loyaltyCustomers[key]&&create){
    loyaltyCustomers[key]={
      key,
      name:clean($('client').value),
      phone:clean($('clientPhone').value),
      points:0,
      totalEarned:0,
      totalUsed:0,
      totalSpentALL:0,
      transactions:0,
      createdAt:new Date().toISOString(),
      updatedAt:new Date().toISOString()
    };
  }

  return loyaltyCustomers[key]||null;
}

function calculateEarnedPoints(amount){
  return Math.floor(
    Math.max(0,num(amount))/POINTS_PER_ALL
  );
}

function loyaltyDiscount(total){
  if(!$('useLoyaltyPoints').checked){
    return {amount:0,used:0};
  }

  const customer=getCustomer();

  if(!customer||customer.points<=0){
    return {amount:0,used:0};
  }

  const amount=Math.min(
    customer.points*ALL_PER_POINT,
    total
  );

  return {
    amount:Math.round(amount*100)/100,
    used:Math.ceil(amount/ALL_PER_POINT)
  };
}

function refreshLoyaltyUI(){
  const customer=getCustomer();

  if(!customer){
    $('loyaltyInfo').textContent='Vendos emrin ose telefonin e klientit për të parë pikët.';
    $('useLoyaltyPoints').checked=false;
    $('useLoyaltyPoints').disabled=true;
    $('loyaltyDiscount').textContent='';
    renderCustomerResults();
    recalc();
    return;
  }

  $('loyaltyInfo').innerHTML=`
    Klienti: <b>${esc(customer.name||'--')}</b><br>
    Pikë aktuale: <span class="green">${customer.points}</span><br>
    Pikë totale të mbledhura: <b>${customer.totalEarned}</b><br>
    Pikë të përdorura: <b>${customer.totalUsed}</b><br>
    Shpenzuar: <b>${money(customer.totalSpentALL)} ALL</b>
  `;

  $('useLoyaltyPoints').disabled=customer.points<=0;

  if(customer.points<=0){
    $('useLoyaltyPoints').checked=false;
    $('loyaltyDiscount').textContent='Klienti nuk ka pikë për përdorim.';
  }else{
    $('loyaltyDiscount').textContent=`Mund të përdorë deri në ${money(customer.points*ALL_PER_POINT)} ALL zbritje.`;
  }

  renderCustomerResults();
  recalc();
}

function getCustomers(){
  return Object.values(loyaltyCustomers).sort(
    (a,b)=>num(b.points)-num(a.points)
  );
}

function renderCustomerResults(){
  const query=normalized(`${$('client').value} ${$('clientPhone').value}`);

  const box=$('customerResults');

  if(!query){
    box.style.display='none';
    box.innerHTML='';
    return;
  }

  const matches=getCustomers()
    .filter(customer=>normalized(`${customer.name} ${customer.phone}`).includes(query))
    .slice(0,8);

  if(!matches.length){
    box.style.display='none';
    box.innerHTML='';
    return;
  }

  box.innerHTML=matches.map(customer=>`
    <div class="result-row">
      <div>
        <b>${esc(customer.name||'--')}</b><br>
        <span class="small">
          ${esc(customer.phone||'--')}
          · ${customer.points} pikë
          · ${customer.totalEarned} totale
        </span>
      </div>

      <button onclick="selectCustomer('${encodeURIComponent(customer.key)}')">
        Zgjidh
      </button>
    </div>
  `).join('');

  box.style.display='block';
}

function selectCustomer(encodedKey){
  const customer=loyaltyCustomers[decodeURIComponent(encodedKey)];

  if(!customer)return;

  $('client').value=customer.name||'';
  $('clientPhone').value=customer.phone||'';
  $('customerResults').style.display='none';
  refreshLoyaltyUI();
}

function renderLoyaltyTable(){
  const query=normalized($('clientSearch').value);

  const customers=getCustomers().filter(customer=>
    !query || normalized(`${customer.name} ${customer.phone}`).includes(query)
  );

  $('loyaltyTable').innerHTML=`
    <tr>
      <th>Emri</th><th>Telefon</th><th>Pikë aktuale</th>
      <th>Pikë totale</th><th>Pikë përdorur</th>
      <th>Shpenzuar</th><th>Transaksione</th><th>Veprim</th>
    </tr>
  `;

  customers.forEach(customer=>{
    $('loyaltyTable').insertAdjacentHTML('beforeend',`
      <tr>
        <td>${esc(customer.name||'--')}</td>
        <td>${esc(customer.phone||'--')}</td>
        <td>${num(customer.points)}</td>
        <td>${num(customer.totalEarned)}</td>
        <td>${num(customer.totalUsed)}</td>
        <td>${money(customer.totalSpentALL)} ALL</td>
        <td>${num(customer.transactions)}</td>
        <td>
          <button onclick="selectCustomer('${encodeURIComponent(customer.key)}');openSec('sale')">
            Zgjidh
          </button>
        </td>
      </tr>
    `);
  });

  if(!customers.length){
    $('loyaltyTable').insertAdjacentHTML('beforeend',`
      <tr>
        <td colspan="8" class="muted">Nuk u gjet asnjë klient.</td>
      </tr>
    `);
  }
}

function resetClientFilter(){
  $('clientSearch').value='';
  renderLoyaltyTable();
}

/* ================= CART AND WEIGHT ================= */

function findProduct(value){
  const query = normalized(value || '');

  if(!query) return null;

  const exactBarcode = products.find(product =>
    normalized(product.b) === query
  );

  if(exactBarcode) return exactBarcode;

  return products.find(product =>
    normalized(product.n).includes(query)
  );
}

function getQuantityForProduct(product){
  if(product.unit==='kg'){
    const weight=num($('saleWeight').value);

    if(weight<=0){
      alert('Vendos peshën në kg.');
      $('saleWeight').focus();
      return 0;
    }

    return weight;
  }

  return 1;
}

function addToCart(product){
  if(!product)return;

  const quantity=getQuantityForProduct(product);
  if(quantity<=0)return;

  if(quantity>product.s){
    alert('Sasia/pesha tejkalon stokun.');
    return;
  }

  const item=cart.find(cartItem=>cartItem.b===product.b);

  if(item){
    if(item.q + quantity > product.s){
      alert('Sasia/pesha tejkalon stokun.');
      return;
    }

    item.q += quantity;
  }else{
    cart.push({
      b:product.b,
      n:product.n,
      p:product.p,
      c:product.c,
      q:quantity,
      unit:product.unit
    });
  }

  if(product.unit==='kg'){
    $('saleWeight').value='';
  }

  renderCart();
}

function manualAdd(){
  const value=$('saleScan').value;

  if(!clean(value))return;

  const product=findProduct(value);

  if(!product){
    alert('Produkti nuk u gjet.');
    $('saleScan').select();
    return;
  }

  addToCart(product);
  $('saleScan').value='';
  $('saleScan').focus();
}

function renderCart(){
  $('saleTable').innerHTML=`
    <tr>
      <th>Produkt</th>
      <th>Sasi/Peshë</th>
      <th>Çmim</th>
      <th>Total</th>
      <th>Fshi</th>
    </tr>
  `;

  cart.forEach((item,index)=>{
    const quantityText=item.unit==='kg'
      ? `${num(item.q).toFixed(3)} kg`
      : `${num(item.q)} copë`;

    const priceText=item.unit==='kg'
      ? `${money(item.p)} ALL/kg`
      : `${money(item.p)} ALL/copë`;

    $('saleTable').insertAdjacentHTML('beforeend',`
      <tr>
        <td>${esc(item.n)}</td>

        <td>
          <button onclick="changeQty(${index},-1)">➖</button>
          ${quantityText}
          <button onclick="changeQty(${index},1)">➕</button>
        </td>

        <td>${priceText}</td>
        <td>${money(item.q*item.p)} ALL</td>

        <td>
          <button class="danger" onclick="removeCartItem(${index})">🗑️</button>
        </td>
      </tr>
    `);
  });

  recalc();
}

function removeCartItem(index){
  cart.splice(index,1);
  renderCart();
}

function changeQty(index,delta){
  const item=cart[index];
  if(!item)return;

  const product=products.find(productItem=>productItem.b===item.b);

  const amount=item.unit==='kg' ? .001 : 1;
  item.q += delta*amount;

  if(item.q<=0){
    cart.splice(index,1);
  }else if(product && item.q>product.s){
    item.q=product.s;
    alert('Sasia/pesha tejkalon stokun.');
  }

  renderCart();
}

function calculateTotals(){
  const subtotal=Math.round(
    cart.reduce((sum,item)=>sum + item.q*item.p,0) * 100
  ) / 100;

  const discountPct=Math.min(
    100,
    Math.max(0, num($('discountPct')?.value,0))
  );

  const fixedDiscount=Math.max(
    0,
    num($('discountALL')?.value,0)
  );

  const percentageDiscount=Math.round(
    subtotal * discountPct / 100 * 100
  ) / 100;

  const totalDiscount=Math.min(
    subtotal,
    Math.round((percentageDiscount + fixedDiscount) * 100) / 100
  );

  const beforeLoyalty=Math.max(
    0,
    Math.round((subtotal-totalDiscount) * 100) / 100
  );

  const loyalty=loyaltyDiscount(beforeLoyalty);

  const finalTotal=Math.max(
    0,
    Math.round((beforeLoyalty-loyalty.amount) * 100) / 100
  );

  return {
    subtotal,
    discountPct,
    percentageDiscount,
    fixedDiscount,
    discountAmount:totalDiscount,
    before:beforeLoyalty,
    loyalty,
    total:finalTotal
  };
}

function paymentChanged(){
  if($('paymentMethod').value==='cash_eur'){
    $('saleCurrency').value='EUR';
  }else{
    $('saleCurrency').value='ALL';
  }

  recalc();
}

function recalc(){
  const totals=calculateTotals();

  $('tot').textContent=money(totals.total);

  const discountText=totals.discountAmount > 0
    ? `Ulje: -${money(totals.discountAmount)} ALL`
    : '';

  $('totInEur').innerHTML=
    $('saleCurrency').value==='EUR'
      ? `Total EUR:
         <b>${money(totals.total/exchangeRate)} EUR</b>
         ${discountText ? `<br><span class="green">${discountText}</span>` : ''}`
      : discountText
        ? `<span class="green">${discountText}</span>`
        : '';

  $('loyaltyDiscount').innerHTML=
    totals.loyalty.amount
      ? `<span class="green">
          Zbritje Loyal:
          -${money(totals.loyalty.amount)} ALL
        </span>`
      : '';

  const paid=num($('paid').value);
  const paidALL=$('paymentMethod').value==='cash_eur' ? paid*exchangeRate : paid;
  const difference=paidALL-totals.total;

  $('change').textContent=
    difference<0
      ? `Mungojnë ${money(Math.abs(difference))} ALL`
      : `Kusur ${money(difference)} ALL`;

  $('change').style.color=difference<0?'red':'green';
}

/* ================= CASH REGISTER ================= */

function getDailyProfitData(date=new Date()){
  const day=localDate(date);
  const records=salesHistory.filter(record => localDate(record.timestamp)===day);

  const salesTotal=records.reduce((sum,record)=>sum + num(record.totalAll),0);

  const costTotal=records.reduce((sum,record)=>{
    if(record.costAll !== undefined){
      return sum + num(record.costAll);
    }

    const fallbackCost=(record.items || []).reduce((itemSum,item)=>{
      const product = products.find(p => p.b === item.b);
      const unitCost = num(product?.c ?? item.c ?? 0);
      return itemSum + (num(item.q) * unitCost);
    },0);

    return sum + fallbackCost;
  },0);

  const grossProfit=Math.round((salesTotal - costTotal) * 100) / 100;

  return {
    salesTotal,
    costTotal,
    grossProfit,
    records
  };
}

function buildSalesChartData(){
  const map=new Map();

  salesHistory.forEach(record=>{
    (record.items || []).forEach(item=>{
      const key=item.n;
      const current=map.get(key) || { name:key, qty:0 };

      current.qty += num(item.q);
      map.set(key,current);
    });
  });

  return [...map.values()].sort((a,b)=>b.qty-a.qty).slice(0,8);
}

function renderSalesChart(){
  const canvas=$('salesChart');
  if(!canvas) return;

  const ctx=canvas.getContext('2d');
  const data=buildSalesChartData();

  const w=canvas.width;
  const h=canvas.height;
  const padding={top:20,right:20,bottom:70,left:40};
  const chartW=w-padding.left-padding.right;
  const chartH=h-padding.top-padding.bottom;

  ctx.clearRect(0,0,w,h);

  if(!data.length){
    ctx.fillStyle='#666';
    ctx.font='16px Segoe UI';
    ctx.fillText('Nuk ka shitje për këtë ditë.', 30, 60);
    return;
  }

  const maxQty=Math.max(...data.map(d=>d.qty),1);

  const barW=chartW / data.length * 0.7;
  const gap=chartW / data.length * 0.3;

  ctx.fillStyle='#334155';
  ctx.font='12px Segoe UI';
  ctx.textAlign='left';

  data.forEach((item,index)=>{
    const x=padding.left + index*(barW+gap) + 8;
    const ratio=item.qty / maxQty;
    const barH=ratio * chartH;
    const y=padding.top + chartH - barH;

    ctx.fillStyle='#2563eb';
    ctx.fillRect(x,y,barW,barH);

    ctx.fillStyle='#111827';
    ctx.font='11px Segoe UI';
    ctx.fillText(`${item.qty}`, x + barW/2 - 5, y - 6);

    ctx.fillStyle='#475569';
    ctx.font='10px Segoe UI';
    ctx.save();
    ctx.translate(x + barW/2, h - 20);
    ctx.rotate(-Math.PI / 4);
    ctx.fillText(item.name.substring(0,12), 0, 0);
    ctx.restore();
  });

  ctx.fillStyle='#334155';
  ctx.font='12px Segoe UI';
  ctx.fillText('Njësi të shitura', 10, 14);
}

function openKasa(){
  const amount=num($('openingFloatInput').value,0);

  if(amount<0){
    alert('Thyerja nuk mund të jetë negative.');
    return;
  }

  if(kasaOpenedAt && !confirm('Kasa është e hapur. Dëshiron të ndryshosh thyerjen?')){
    return;
  }

  openingFloatALL=amount;
  kasaOpenedAt=new Date().toISOString();

  save();
  updateBalance();

  showTxn(
    'Hapja e Kasës',
    `<div class="green">Kasa u hap me thyerje ${money(amount)} ALL.</div>`
  );
}

function updateBalance(){
  const profit=getDailyProfitData();

  $('daily').textContent=money(cashALL);
  $('dailyCard').textContent=money(cardALL);
  $('dailyEUR').textContent=money(cashEUR);

  $('cashBalanceALL').textContent=money(cashALL);
  $('cardBalanceALL').textContent=money(cardALL);
  $('cashBalanceEUR').textContent=money(cashEUR);

  $('activeFloat').textContent=money(openingFloatALL);
  $('activeFloatCard').textContent=money(openingFloatALL);
  $('exchangeRateInput').value=exchangeRate;

  $('kasaStatus').textContent=kasaOpenedAt
    ? `Hapur më ${dateTime(kasaOpenedAt)}`
    : 'Kasa e mbyllur';

  $('kasaStatus').className=kasaOpenedAt ? 'green' : 'red';

  $('totalSalesProfit').textContent=money(profit.salesTotal);
  $('costGoodsSold').textContent=money(profit.costTotal);
  $('dailyGrossProfit').textContent=money(profit.grossProfit);

  renderSalesChart();
}

function saveExchangeRate(){
  const value=num($('exchangeRateInput').value,0);

  if(value<=0){
    alert('Kurs i pavlefshëm.');
    return;
  }

  exchangeRate=value;
  save();
  recalc();

  showTxn(
    'Kursi',
    `<div class="green">1 EUR = ${money(exchangeRate)} ALL</div>`
  );
}

/* ================= DAILY BALANCE / EXCEL ================= */

function exportDailyClosuresExcel(){
  const closures=parse(localStorage.getItem('dayClosures'),[]);

  if(!closures.length){
    alert('Nuk ka bilance ditore të ruajtura.');
    return;
  }

  const rows=[[
    'Data',
    'Thyerja ALL',
    'Cash ALL sistem',
    'Kartë ALL',
    'Cash EUR sistem',
    'Arka reale ALL',
    'Arka reale EUR',
    'Cash ALL i pritur',
    'Diferenca ALL',
    'Diferenca EUR',
    'Kursi',
    'Shitje totale',
    'Kosto malli',
    'Fitim bruto'
  ]];

  closures.forEach(item=>{
    rows.push([
      item.date||item.timestamp||'',
      num(item.openingFloatALL),
      num(item.cashALLSystem??item.cashSalesALL),
      num(item.cardALLSystem??item.cardALL),
      num(item.cashEURSystem??item.cashEUR),
      num(item.realCashALL??item.realALL),
      num(item.realCashEUR??item.realEUR),
      num(item.expectedCashALL),
      signedMoney(item.diffCashALL??item.differenceALL),
      signedMoney(item.diffCashEUR??item.differenceEUR),
      num(item.exchangeRate),
      num(item.salesTotal),
      num(item.costTotal),
      num(item.grossProfit)
    ]);
  });

  const csv='\uFEFF'+rows.map(row=>row.map(csvCell).join(',')).join('\n');

  downloadFile('day_closures.csv',csv,'text/csv;charset=utf-8');
}

function closeDay(){
  if(!kasaOpenedAt){
    alert('Kasa nuk është hapur.');
    return;
  }

  const realCashALL=num($('cashRealALL').value,0);
  const realCashEUR=num($('cashRealEUR').value,0);

  const expectedCashALL=openingFloatALL + cashALL;
  const diffCashALL=realCashALL - expectedCashALL;
  const diffCashEUR=realCashEUR - cashEUR;

  const profitData=getDailyProfitData();

  const closures=parse(localStorage.getItem('dayClosures'),[]);

  closures.push({
    date:new Date().toISOString(),
    openingFloatALL,
    cashALLSystem:cashALL,
    cardALLSystem:cardALL,
    cashEURSystem:cashEUR,
    realCashALL,
    realCashEUR,
    expectedCashALL,
    diffCashALL,
    diffCashEUR,
    exchangeRate,
    salesTotal:profitData.salesTotal,
    costTotal:profitData.costTotal,
    grossProfit:profitData.grossProfit
  });

  localStorage.setItem('dayClosures',JSON.stringify(closures));

  const report=`
    <div class="green">Mbyllja e ditës u krye.</div>

    <p>Thyerja:
      <b>${money(openingFloatALL)} ALL</b>
    </p>

    <p>Cash ALL sistem:
      <b>${money(cashALL)} ALL</b>
    </p>

    <p>Kartë:
      <b>${money(cardALL)} ALL</b>
    </p>

    <p>Cash EUR:
      <b>${money(cashEUR)} EUR</b>
    </p>

    <hr>

    <p>Arka reale ALL:
      <b>${money(realCashALL)} ALL</b>
    </p>

    <p>Arka reale EUR:
      <b>${money(realCashEUR)} EUR</b>
    </p>

    <p>Cash ALL i pritur:
      <b>${money(expectedCashALL)} ALL</b>
    </p>

    <p>Diferenca ALL:
      <b class="${diffCashALL>=0?'green':'red'}">
        ${signedMoney(diffCashALL)} ALL
      </b>
    </p>

    <p>Diferenca EUR:
      <b class="${diffCashEUR>=0?'green':'red'}">
        ${signedMoney(diffCashEUR)} EUR
      </b>
    </p>

    <hr>

    <p>Shitje totale:
      <b>${money(profitData.salesTotal)} ALL</b>
    </p>

    <p>Kosto e mallit:
      <b>${money(profitData.costTotal)} ALL</b>
    </p>

    <p>Fitim bruto:
      <b class="${profitData.grossProfit>=0?'green':'red'}">
        ${money(profitData.grossProfit)} ALL
      </b>
    </p>

    <p class="small">
      Pozitive = tepricë. Negative = mungesë.
    </p>
  `;

  openingFloatALL=0;
  kasaOpenedAt='';
  cashALL=0;
  cardALL=0;
  cashEUR=0;

  $('cashRealALL').value='';
  $('cashRealEUR').value='';
  $('openingFloatInput').value='';

  save();
  updateBalance();

  showTxn('Mbyllje Dite',report);
}

/* ================= PAYMENTS ================= */

function updateBalancesAfterPayment(record){
  const method = record.paymentMethod || 'cash_all';
  const amount = num(record.amountPaid, 0);

  if(method === 'cash_all'){
    cashALL += amount;
  }else if(method === 'card'){
    cardALL += amount;
  }else if(method === 'cash_eur'){
    cashEUR += num(record.cashGivenRaw, 0);
    cashALL -= Math.max(0, num(record.changeALL, 0));
  }

  cashALL = Math.round(cashALL * 100) / 100;
  cardALL = Math.round(cardALL * 100) / 100;
  cashEUR = Math.round(cashEUR * 100) / 100;
}

function pay(){
  if(!kasaOpenedAt){
    alert('Kasa nuk është hapur. Vendos thyerjen te Bilanci dhe hap kasën.');
    openSec('bil');
    return;
  }

  if(!cart.length){
    alert('Shporta është bosh.');
    return;
  }

  const totals=calculateTotals();
  const method=$('paymentMethod').value;
  const rawPaid=num($('paid').value);

  if(!Number.isFinite(rawPaid)||rawPaid<0){
    alert('Shuma e paguar është e pavlefshme.');
    return;
  }

  const paidALL=method==='cash_eur' ? rawPaid*exchangeRate : rawPaid;
  const amountPaid=Math.min(Math.max(0,paidALL), totals.total);
  const changeALL=Math.max(0,paidALL-totals.total);
  const due=Math.max(0, totals.total-paidALL);
  const finalChangeALL=method==='card' ? 0 : changeALL;

  const customer=getCustomer();

  const saleCostAll=cart.reduce((sum,item)=>{
    const product = products.find(productItem => productItem.b === item.b);
    return sum + num(item.q) * num(product?.c ?? item.c ?? 0);
  },0);

  const record={
    id:`${Date.now()}_${Math.random().toString(36).slice(2,8)}`,
    timestamp:new Date().toISOString(),
    client:customer?.name || clean($('client').value) || null,
    clientPhone:customer?.phone || clean($('clientPhone').value) || null,
    items:cart.map(item=>{
      const product = products.find(productItem => productItem.b === item.b);
      return {
        ...item,
        c:num(product?.c ?? item.c ?? 0),
        salePrice:num(item.p)
      };
    }),
    subtotalAll:totals.subtotal,
    discountPct:totals.discountPct,
    discountPercentageALL:totals.percentageDiscount,
    discountFixedALL:totals.fixedDiscount,
    discountALL:totals.discountAmount,
    beforeLoyaltyAll:totals.before,
    loyaltyDiscountALL:totals.loyalty.amount,
    loyaltyPointsUsed:totals.loyalty.used,
    totalAll:totals.total,
    costAll:saleCostAll,
    grossProfitAll:Math.round((totals.total - saleCostAll) * 100) / 100,
    paymentMethod:method,
    paymentCurrency:method==='cash_eur' ? 'EUR' : 'ALL',
    cashGivenRaw:rawPaid,
    cashGivenALL:paidALL,
    amountPaid,
    changeALL:finalChangeALL,
    due,
    status:due<=0 ? 'paid' : 'owed',
    exchangeRateAtSale:exchangeRate,
    loyaltyPointsEarned:0,
    loyaltyBalanceAfter:0,
    customerTotalEarned:0,
    customerTotalUsed:0
  };

  if(customer){
    const earned=calculateEarnedPoints(record.amountPaid);

    customer.points=Math.max(
      0,
      num(customer.points) -
      record.loyaltyPointsUsed +
      earned
    );

    customer.totalEarned = num(customer.totalEarned) + earned;
    customer.totalUsed = num(customer.totalUsed) + record.loyaltyPointsUsed;
    customer.totalSpentALL = num(customer.totalSpentALL) + record.amountPaid;
    customer.transactions = num(customer.transactions) + 1;
    customer.updatedAt = new Date().toISOString();

    record.loyaltyPointsEarned=earned;
    record.loyaltyBalanceAfter=customer.points;
    record.customerTotalEarned=customer.totalEarned;
    record.customerTotalUsed=customer.totalUsed;
  }

  cart.forEach(item=>{
    const product=products.find(productItem=>productItem.b===item.b);

    if(product){
      product.s=Math.max(0, num(product.s) - num(item.q));
    }
  });

  salesHistory.unshift(record);
  updateBalancesAfterPayment(record);
  save();

  const methodLabel={
    cash_all:'Cash (ALL)',
    card:'Kartë',
    cash_eur:'Cash (EUR)'
  }[record.paymentMethod] || record.paymentMethod;

  const clientGivenText=
    record.paymentMethod==='cash_eur'
      ? `${money(record.cashGivenRaw)} EUR`
      : `${money(record.cashGivenRaw)} ALL`;

  let report=record.status==='paid'
    ? '<div class="green">Transaksioni u mbyll me sukses.</div>'
    : '<div class="warn">Shitja u regjistrua si borxh.</div>';

  report+=`
    <p><b>Mënyra:</b> ${esc(methodLabel)}</p>
    <p><b>Total:</b> ${money(record.totalAll)} ALL</p>
    <p><b>Klienti dha:</b> ${clientGivenText}</p>
    <p><b>Paguar:</b> ${money(record.amountPaid)} ALL</p>
    <p><b>Kusur:</b> ${money(record.changeALL)} ALL</p>
    <p><b>Mbetje/Borxh:</b> ${money(record.due)} ALL</p>
  `;

  if(record.discountALL > 0){
    report+=`
      <p><b>Ulje:</b>
        <span class="green">-${money(record.discountALL)} ALL</span>
      </p>
    `;
  }

  report+=`
    <p><b>Kosto e mallit:</b> ${money(record.costAll)} ALL</p>
    <p><b>Fitim bruto:</b> <span class="${record.grossProfitAll >= 0 ? 'green' : 'red'}">${money(record.grossProfitAll)} ALL</span></p>
  `;

  if(record.paymentMethod==='cash_eur'){
    report+=`
      <hr>
      <p class="small">
        Klienti dha:
        <b>${money(record.cashGivenRaw)} EUR</b>
      </p>
      <p class="small">
        Vlera në ALL:
        <b>${money(record.cashGivenALL)} ALL</b>
      </p>
      <p class="small">
        Kusuri i kthyer:
        <b>${money(record.changeALL)} ALL</b>
      </p>
      <p class="small">
        Kursi:
        <b>1 EUR = ${money(record.exchangeRateAtSale)} ALL</b>
      </p>
    `;
  }

  if(record.paymentMethod==='card'){
    report+=`
      <p class="small">
        Pagesa u regjistrua me kartë:
        <b>${money(record.amountPaid)} ALL</b>
      </p>
    `;
  }

  report+=`
    <hr>
    <b>Produktet:</b>
    <ul>
      ${record.items.map(item=>`
        <li>
          ${esc(item.n)}
          × ${item.q}
          ${item.unit==='kg'?'kg':'copë'}
          = ${money(item.q*item.salePrice)} ALL
        </li>
      `).join('')}
    </ul>
  `;

  if(record.client){
    report+=`
      <hr>
      <p><b>Klienti:</b> ${esc(record.client)}</p>
      <p><b>Pikë të fituara:</b> ${record.loyaltyPointsEarned}</p>
      <p><b>Pikë totale:</b> ${record.customerTotalEarned}</p>
      <p><b>Pikë të përdorura:</b> ${record.loyaltyPointsUsed}</p>
      <p><b>Pikë të disponueshme:</b> ${record.loyaltyBalanceAfter}</p>
    `;
  }

  cancelSale();
  renderAll();

  showTxn(record.status==='paid' ? 'Shitje e plotë' : 'Shitje me borxh', report);
  printInvoice(record);
}

function cancelSale(){
  cart=[];
  $('saleScan').value='';
  $('saleWeight').value='';
  $('client').value='';
  $('clientPhone').value='';
  $('paid').value='';
  $('discountPct').value='0';
  $('discountALL').value='0';
  $('useLoyaltyPoints').checked=false;
  $('useLoyaltyPoints').disabled=true;
  $('customerResults').style.display='none';
  $('customerResults').innerHTML='';
  renderCart();
  refreshLoyaltyUI();
}

/* ================= PRINTING ================= */

function printInvoice(record){
  const items=(record.items||[]).map(item=>`
    <tr>
      <td>${esc(item.n)}</td>
      <td>
        ${item.q}
        ${item.unit==='kg'?'kg':'copë'}
      </td>
      <td>${money(item.salePrice)} ALL</td>
      <td>${money(item.q*item.salePrice)} ALL</td>
    </tr>
  `).join('');

  const paymentLabel={
    cash_all:'Cash (ALL)',
    card:'Kartë',
    cash_eur:'Cash (EUR)'
  }[record.paymentMethod] || record.paymentMethod || '--';

  const clientGiven=
    record.paymentMethod==='cash_eur'
      ? `${money(record.cashGivenRaw)} EUR`
      : `${money(record.cashGivenRaw)} ALL`;

  const clientGivenALL=
    record.paymentMethod==='cash_eur'
      ? `${money(record.cashGivenALL)} ALL`
      : `${money(record.cashGivenRaw)} ALL`;

  $('printArea').innerHTML=`
    <div style="
      font-family:Arial,sans-serif;
      max-width:420px;
      margin:auto;
      color:#111
    ">

      <h2 style="text-align:center;margin:0">
        POS Market
      </h2>

      <p style="
        text-align:center;
        font-size:12px;
        margin:5px 0 12px
      ">
        Faturë shitjeje
      </p>

      <hr>

      <p>
        <b>Data:</b>
        ${esc(dateTime(record.timestamp))}<br>

        <b>Klient:</b>
        ${esc(record.client||'--')}<br>

        <b>Mënyra e pagesës:</b>
        ${esc(paymentLabel)}
      </p>

      <table style="
        width:100%;
        border-collapse:collapse;
        font-size:13px
      ">
        <thead>
          <tr>
            <th style="text-align:left">Produkt</th>
            <th>Sasi</th>
            <th>Çmim</th>
            <th>Total</th>
          </tr>
        </thead>

        <tbody>
          ${items}
        </tbody>
      </table>

      <hr>

      <div style="font-size:14px;line-height:1.8">
        <div style="
          display:flex;
          justify-content:space-between
        ">
          <span>Subtotal:</span>
          <b>${money(record.subtotalAll)} ALL</b>
        </div>

        ${
          record.discountALL > 0
            ? `<div style="
                display:flex;
                justify-content:space-between
              ">
                <span>Ulje:</span>
                <b>-${money(record.discountALL)} ALL</b>
              </div>`
            : ''
        }

        <div style="
          display:flex;
          justify-content:space-between
        ">
          <span>Zbritje Loyal:</span>
          <b>-${money(record.loyaltyDiscountALL)} ALL</b>
        </div>

        <div style="
          display:flex;
          justify-content:space-between;
          font-size:18px;
          border-top:2px solid #111;
          margin-top:5px;
          padding-top:5px
        ">
          <span><b>TOTAL:</b></span>
          <b>${money(record.totalAll)} ALL</b>
        </div>

        <br>

        <div style="
          display:flex;
          justify-content:space-between;
          color:#1d4ed8
        ">
          <span><b>Klienti dha:</b></span>
          <b>${clientGiven}</b>
        </div>

        ${
          record.paymentMethod==='cash_eur'
            ? `
              <div style="
                display:flex;
                justify-content:space-between;
                font-size:12px;
                color:#555
              ">
                <span>Vlera e pagesës në ALL:</span>
                <b>${clientGivenALL}</b>
              </div>

              <div style="
                display:flex;
                justify-content:space-between;
                font-size:12px;
                color:#555
              ">
                <span>Kursi:</span>
                <b>1 EUR = ${money(record.exchangeRateAtSale)} ALL</b>
              </div>
            `
            : ''
        }

        <div style="
          display:flex;
          justify-content:space-between;
          color:#15803d
        ">
          <span><b>Paguar:</b></span>
          <b>${money(record.amountPaid)} ALL</b>
        </div>

        <div style="
          display:flex;
          justify-content:space-between;
          color:#b45309
        ">
          <span><b>Kusur:</b></span>
          <b>${money(record.changeALL)} ALL</b>
        </div>

        <div style="
          display:flex;
          justify-content:space-between;
          color:#dc2626
        ">
          <span><b>Borxh/Mbetje:</b></span>
          <b>${money(record.due)} ALL</b>
        </div>

      </div>

      ${
        record.client
          ? `
            <hr>
            <p style="font-size:13px">
              <b>Programi Loyal</b><br>
              Pikë të fituara:
              ${num(record.loyaltyPointsEarned)}<br>
              Pikë totale:
              ${num(record.customerTotalEarned)}<br>
              Pikë të përdorshme:
              ${num(record.loyaltyBalanceAfter)}
            </p>
          `
          : ''
      }

      <hr>

      <p style="
        text-align:center;
        font-size:12px
      ">
        Faleminderit për blerjen!
      </p>

    </div>
  `;

  const printWindow=window.open('', '_blank', 'width=500,height=700');

  if(!printWindow){
    alert('Lejo popup-et në browser për të printuar faturën.');
    return;
  }

  printWindow.document.write(`
    <!DOCTYPE html>
    <html lang="sq">
    <head>
      <meta charset="UTF-8">
      <title>Faturë POS Market</title>

      <style>
        *{box-sizing:border-box}
        body{
          margin:10px;
          background:#fff;
          color:#111;
          font-family:Arial,sans-serif;
        }
        table{
          width:100%;
          border-collapse:collapse;
        }
        th,td{
          border:1px solid #ddd;
          padding:5px;
          text-align:center;
        }
        th:first-child,td:first-child{
          text-align:left;
        }
        @media print{
          body{margin:0}
          button{display:none!important}
        }
      </style>
    </head>

    <body>
      ${$('printArea').innerHTML}

      <script>
        window.onload=function(){
          window.print();

          window.onafterprint=function(){
            window.close();
          };
        };
      <\/script>
    </body>
    </html>
  `);

  printWindow.document.close();
}

/* ================= HISTORY / DEBT ================= */

function renderHistory(){
  $('histTable').innerHTML=`
    <tr>
      <th>Data</th><th>Klient</th><th>Total</th>
      <th>Kosto</th><th>Fitim</th><th>Paguar</th><th>Mbetje</th><th>Mënyra</th><th>Veprime</th>
    </tr>
  `;

  salesHistory.forEach((record,index)=>{
    $('histTable').insertAdjacentHTML('beforeend',`
      <tr>
        <td>${esc(dateTime(record.timestamp))}</td>
        <td>${esc(record.client||'--')}</td>
        <td>${money(record.totalAll)} ALL</td>
        <td>${money(record.costAll||0)} ALL</td>
        <td class="${num(record.grossProfitAll)>=0?'green':'red'}">${money(record.grossProfitAll||0)} ALL</td>
        <td>${money(record.amountPaid)} ALL</td>
        <td>${money(record.due)} ALL</td>
        <td>${esc(record.paymentMethod)}</td>
        <td>
          <button onclick="viewSale(${index})">Shiko</button>
          <button class="danger" onclick="deleteSale(${index})">🗑️</button>
        </td>
      </tr>
    `);
  });
}

function viewSale(index){
  const record=salesHistory[index];
  if(!record)return;

  currentSaleIndex=index;
  $('settleAmount').value=record.due||'';

  $('viewBody').innerHTML=`
    <p><b>Data:</b> ${esc(dateTime(record.timestamp))}</p>
    <p><b>Klient:</b> ${esc(record.client||'--')}</p>
    <p><b>Total:</b> ${money(record.totalAll)} ALL</p>
    <p><b>Kosto:</b> ${money(record.costAll||0)} ALL</p>
    <p><b>Fitim bruto:</b> <span class="${num(record.grossProfitAll)>=0?'green':'red'}">${money(record.grossProfitAll||0)} ALL</span></p>
    <p><b>Paguar:</b> ${money(record.amountPaid)} ALL</p>
    <p><b>Mbetje:</b> ${money(record.due)} ALL</p>
    <p><b>Mënyra:</b> ${esc(record.paymentMethod)}</p>
    <p><b>Pikë të fituara:</b> ${record.loyaltyPointsEarned||0}</p>
    <p><b>Pikë totale:</b> ${record.customerTotalEarned||0}</p>
    <p><b>Pikë të disponueshme:</b> ${record.loyaltyBalanceAfter||0}</p>
    <hr>
    <ul>
      ${(record.items||[]).map(item=>`
        <li>
          ${esc(item.n)} × ${item.q}
          ${item.unit==='kg'?'kg':'copë'}
          = ${money(item.q*item.salePrice)} ALL
        </li>
      `).join('')}
    </ul>
  `;

  $('viewModal').style.display='block';
}

function closeView(){
  $('viewModal').style.display='none';
  currentSaleIndex=null;
}

function deleteSale(index){
  if(!salesHistory[index])return;

  if(!confirm('Fshi këtë shitje? Bilanci dhe stoku nuk rikthehen.')){
    return;
  }

  salesHistory.splice(index,1);
  save();
  renderAll();
}

function settleDebt(){
  const record=salesHistory[currentSaleIndex];
  if(!record){
    alert('Nuk u gjet shitja.');
    return;
  }

  if(record.due<=0){
    alert('Kjo shitje nuk ka borxh.');
    return;
  }

  const amount=Math.min(num($('settleAmount').value), record.due);

  if(amount<=0){
    alert('Vendos një shumë të vlefshme.');
    return;
  }

  record.amountPaid += amount;
  record.due = Math.max(0, record.due - amount);
  record.status = record.due<=0 ? 'paid' : 'owed';

  if(record.paymentMethod==='cash_all') cashALL += amount;
  if(record.paymentMethod==='card') cardALL += amount;
  if(record.paymentMethod==='cash_eur') cashEUR += amount/exchangeRate;

  save();
  renderAll();
  viewSale(currentSaleIndex);

  showTxn('Shlyerje borxhi', `<div class="green">U shlyen ${money(amount)} ALL.</div>`);
}

/* ================= EXPORT ================= */

function exportCSV(){
  if(!salesHistory.length){
    alert('Nuk ka të dhëna.');
    return;
  }

  const rows=[[
    'id','timestamp','client','clientPhone',
    'totalAll','costAll','grossProfitAll','amountPaid','due',
    'paymentMethod','cashGivenRaw','changeALL',
    'pointsEarned','customerTotalEarned','items'
  ]];

  salesHistory.slice().reverse().forEach(record=>{
    rows.push([
      record.id,
      record.timestamp,
      record.client||'',
      record.clientPhone||'',
      record.totalAll,
      record.costAll||0,
      record.grossProfitAll||0,
      record.amountPaid,
      record.due,
      record.paymentMethod,
      record.cashGivenRaw,
      record.changeALL,
      record.loyaltyPointsEarned||0,
      record.customerTotalEarned||0,
      (record.items||[]).map(item=>`${item.n} x${item.q} ${item.unit}`).join(' | ')
    ]);
  });

  downloadFile('sales_history.csv','\uFEFF'+rows.map(row=>row.map(csvCell).join(',')).join('\n'),'text/csv;charset=utf-8');
}

function exportLoyaltyData(){
  const rows=[['name','phone','points','totalEarned','totalUsed','totalSpentALL','transactions']];

  getCustomers().forEach(customer=>{
    rows.push([
      customer.name||'',
      customer.phone||'',
      customer.points||0,
      customer.totalEarned||0,
      customer.totalUsed||0,
      customer.totalSpentALL||0,
      customer.transactions||0
    ]);
  });

  downloadFile('loyalty_customers.csv','\uFEFF'+rows.map(row=>row.map(csvCell).join(',')).join('\n'),'text/csv;charset=utf-8');
}

function backupData(){
  downloadFile(
    'pos_market_backup.json',
    JSON.stringify({
      version:9,
      createdAt:new Date().toISOString(),
      products,
      salesHistory,
      loyaltyCustomers,
      suppliers,
      purchaseHistory,
      cashALL,
      cardALL,
      cashEUR,
      openingFloatALL,
      kasaOpenedAt,
      exchangeRate,
      reorderConfig
    },null,2),
    'application/json'
  );
}

function restoreData(){
  const input=document.createElement('input');

  input.type='file';
  input.accept='application/json';

  input.onchange=event=>{
    const file=event.target.files[0];
    if(!file)return;

    const reader=new FileReader();

    reader.onload=loadEvent=>{
      try{
        const data=JSON.parse(loadEvent.target.result);

        if(Array.isArray(data.products)){
          products=data.products.map(productData);
        }

        if(Array.isArray(data.salesHistory)){
          salesHistory=data.salesHistory;
        }

        if(data.loyaltyCustomers && typeof data.loyaltyCustomers==='object'){
          loyaltyCustomers=data.loyaltyCustomers;
        }

        if(Array.isArray(data.suppliers)){
          suppliers=data.suppliers;
        }

        if(Array.isArray(data.purchaseHistory)){
          purchaseHistory=data.purchaseHistory;
        }

        cashALL=num(data.cashALL,cashALL);
        cardALL=num(data.cardALL,cardALL);
        cashEUR=num(data.cashEUR,cashEUR);
        openingFloatALL=num(data.openingFloatALL,openingFloatALL);
        kasaOpenedAt=String(data.kasaOpenedAt||kasaOpenedAt);
        exchangeRate=Math.max(.0001,num(data.exchangeRate,exchangeRate));

        if(data.reorderConfig){
          reorderConfig={...reorderConfig,...data.reorderConfig};
        }

        save();
        renderAll();

        alert('Backup u restaurua me sukses.');
      }catch(error){
        console.error(error);
        alert('Backup i pavlefshëm.');
      }
    };

    reader.readAsText(file);
  };

  input.click();
}

function clearOld(){
  if(!confirm('Je i sigurt? Do të fshihet i gjithë historiku.')){
    return;
  }

  salesHistory=[];
  save();
  renderAll();
}

/* ================= SUPPLIERS / PURCHASES ================= */

function ensureSupplier(){
  const name=clean($('supplierName').value);
  const phone=clean($('supplierPhone').value);
  const invoice=clean($('supplierInvoice').value);

  if(!name) return null;

  const key=`${normalized(name)}|${normalized(phone)}`;
  let supplier=suppliers.find(item=>item.key===key);

  if(!supplier){
    supplier={key,name,phone,invoice,createdAt:new Date().toISOString()};
    suppliers.push(supplier);
  }else{
    supplier.name=name;
    supplier.phone=phone;
    supplier.invoice=invoice;
  }

  save();
  return supplier;
}

function calculatePurchaseTotals(){
  const total=supplierCart.reduce((sum,item)=>sum + num(item.q)*num(item.cost),0);
  const qtyTotal=supplierCart.reduce((sum,item)=>sum + num(item.q),0);

  $('purchaseTotal').textContent=money(total);
  $('purchaseSummary').innerHTML=supplierCart.length
    ? `Artikuj: <b>${supplierCart.length}</b> • Sasi totale: <b>${money(qtyTotal)}</b> • Totali: <b>${money(total)} ALL</b>`
    : 'Asnjë artikull i shtuar.';

  return { total, qtyTotal };
}

function clearPurchaseInputs(){
  $('purchaseScan').value='';
  $('purchaseQty').value='';
  $('purchaseCost').value='';
  $('purchaseProductName').value='';
  $('purchaseBarcode').value='';
  $('purchaseSalePrice').value='';
  $('purchaseExpiry').value='';
  $('purchaseMinStock').value='';
  $('purchaseUnit').value='piece';
  $('purchaseCategory').value='ushqim';
  $('purchaseScan').focus();
}

function addPurchaseItem(){
  const scan=clean($('purchaseScan').value);
  const qty=num($('purchaseQty').value,0);
  const cost=num($('purchaseCost').value,0);

  if(!(qty>0)){
    alert('Sasia duhet të jetë më e madhe se 0.');
    return;
  }

  if(cost<0){
    alert('Çmimi i blerjes nuk mund të jetë negativ.');
    return;
  }

  let product=findProduct(scan);

  if(product){
    const existing=supplierCart.find(item=>item.b===product.b);

    if(existing){
      existing.q += qty;
      existing.cost = cost > 0 ? cost : existing.cost;
    }else{
      supplierCart.push({
        b:product.b,
        n:product.n,
        unit:product.unit,
        q:qty,
        cost:cost > 0 ? cost : num(product.c,0),
        salePrice:num(product.p,0),
        category:product.category,
        expiry:product.expiry,
        minStock:num(product.minStock,0),
        isNew:false
      });
    }
  }else{
    const name=clean($('purchaseProductName').value);
    const barcode=clean($('purchaseBarcode').value) || scan;
    const salePrice=num($('purchaseSalePrice').value,0);

    if(!name){
      alert('Për produkt të ri vendos emrin.');
      $('purchaseProductName').focus();
      return;
    }

    if(!barcode){
      alert('Për produkt të ri vendos barkodin.');
      $('purchaseBarcode').focus();
      return;
    }

    if(salePrice<=0){
      alert('Vendos çmimin e shitjes për produktin e ri.');
      $('purchaseSalePrice').focus();
      return;
    }

    if(products.some(item=>item.b===barcode) || supplierCart.some(item=>item.b===barcode)){
      alert('Ky barkod ekziston.');
      return;
    }

    supplierCart.push({
      b:barcode,
      n:name,
      unit:$('purchaseUnit').value==='kg'?'kg':'piece',
      q:qty,
      cost:cost > 0 ? cost : 0,
      salePrice:salePrice,
      category:$('purchaseCategory').value,
      expiry:$('purchaseExpiry').value,
      minStock:num($('purchaseMinStock').value,0),
      isNew:true
    });
  }

  clearPurchaseInputs();
  renderPurchaseCart();
}

function renderPurchaseCart(){
  $('purchaseTable').innerHTML=`
    <tr>
      <th>Produkt</th>
      <th>Sasi</th>
      <th>Çmimi blerjes</th>
      <th>Çmimi shitje</th>
      <th>Total</th>
      <th>Fshi</th>
    </tr>
  `;

  if(!supplierCart.length){
    $('purchaseTable').insertAdjacentHTML('beforeend',`
      <tr>
        <td colspan="6" class="muted">Nuk ka produkte në furnizim.</td>
      </tr>
    `);
    calculatePurchaseTotals();
    return;
  }

  supplierCart.forEach((item,index)=>{
    const qtyText=item.unit==='kg' ? `${money(item.q)} kg` : `${money(item.q)} copë`;
    const total=item.q * item.cost;
    const label=item.isNew ? `${esc(item.n)} <span class="green">(Produkt i ri)</span>` : esc(item.n);

    $('purchaseTable').insertAdjacentHTML('beforeend',`
      <tr>
        <td>${label}</td>
        <td>${qtyText}</td>
        <td>${money(item.cost)} ALL</td>
        <td>${money(item.salePrice ?? item.cost)} ALL</td>
        <td>${money(total)} ALL</td>
        <td><button class="danger" onclick="removePurchaseItem(${index})">🗑️</button></td>
      </tr>
    `);
  });

  calculatePurchaseTotals();
}

function removePurchaseItem(index){
  supplierCart.splice(index,1);
  renderPurchaseCart();
}

function cancelPurchaseCart(){
  supplierCart=[];
  $('supplierName').value='';
  $('supplierPhone').value='';
  $('supplierInvoice').value='';
  clearPurchaseInputs();
  renderPurchaseCart();
}

function completePurchase(){
  if(!supplierCart.length){
    alert('Shporta e furnizimit është bosh.');
    return;
  }

  const totals=calculatePurchaseTotals();
  const paid=num($('purchasePaid').value,0);

  if(!Number.isFinite(paid)||paid<0){
    alert('Shuma e paguar te furnitori është e pavlefshme.');
    return;
  }

  const supplier=ensureSupplier();
  if(!supplier){
    alert('Duhet të vendosni emrin e furnitorit.');
    $('supplierName').focus();
    return;
  }

  const record={
    id:`${Date.now()}_${Math.random().toString(36).slice(2,8)}`,
    timestamp:new Date().toISOString(),
    supplierName:supplier.name,
    supplierPhone:supplier.phone,
    supplierInvoice:supplier.invoice,
    items:JSON.parse(JSON.stringify(supplierCart)),
    totalAll:totals.total,
    amountPaid:paid,
    due:Math.max(0, totals.total - paid),
    paymentMethod:$('purchasePaymentMethod').value,
    totalItems:supplierCart.length,
    totalQty:totals.qtyTotal,
    status:paid >= totals.total ? 'paid' : 'owed'
  };

  supplierCart.forEach(item=>{
    let product=products.find(p=>p.b===item.b);

    if(!product){
      product=productData({
        n:item.n,
        b:item.b,
        unit:item.unit,
        p:item.salePrice ?? item.cost,
        c:item.cost,
        s:item.q,
        category:item.category || 'ushqim',
        expiry:item.expiry || '',
        minStock:item.minStock || 0
      });

      products.push(product);
    }else{
      product.s = Math.max(0, num(product.s) + num(item.q));

      if(item.cost > 0){
        product.c = item.cost;
      }

      if((item.salePrice ?? 0) > 0 && item.isNew){
        product.p = item.salePrice;
      }
    }
  });

  purchaseHistory.unshift(record);
  save();

  const methodLabel={
    cash_all:'Cash (ALL)',
    card:'Kartë'
  }[record.paymentMethod] || record.paymentMethod;

  const invoiceHtml=`
    <div class="green">Furnizimi u krye me sukses.</div>
    <p><b>Furnitori:</b> ${esc(record.supplierName)}</p>
    <p><b>Telefoni:</b> ${esc(record.supplierPhone||'--')}</p>
    <p><b>Fatura:</b> ${esc(record.supplierInvoice||'--')}</p>
    <p><b>Totali:</b> ${money(record.totalAll)} ALL</p>
    <p><b>Paguar:</b> ${money(record.amountPaid)} ALL</b>
    <p><b>Mbetje:</b> ${money(record.due)} ALL</p>
    <p><b>Mënyra:</b> ${esc(methodLabel)}</p>
    <p><b>Artikuj:</b> ${record.totalItems}</p>
    <p><b>Sasi totale:</b> ${money(record.totalQty)}</p>
    <hr>
    <ul>
      ${record.items.map(item=>`
        <li>
          ${esc(item.n)} × ${money(item.q)}
          ${item.unit==='kg'?'kg':'copë'}
          @ ${money(item.cost)} ALL
          = ${money(item.q*item.cost)} ALL
        </li>
      `).join('')}
    </ul>
  `;

  cancelPurchaseCart();
  renderAll();

  showTxn('Furnizim i kryer', invoiceHtml);
  printPurchaseInvoice(record);
}

function renderPurchaseHistory(){
  $('purchaseHistoryTable').innerHTML=`
    <tr>
      <th>Data</th>
      <th>Furnitori</th>
      <th>Artikuj</th>
      <th>Sasi</th>
      <th>Total</th>
      <th>Paguar</th>
      <th>Veprim</th>
    </tr>
  `;

  if(!purchaseHistory.length){
    $('purchaseHistoryTable').insertAdjacentHTML('beforeend',`
      <tr>
        <td colspan="7" class="muted">Nuk ka furnizime.</td>
      </tr>
    `);
    return;
  }

  purchaseHistory.forEach((record,index)=>{
    $('purchaseHistoryTable').insertAdjacentHTML('beforeend',`
      <tr>
        <td>${esc(dateTime(record.timestamp))}</td>
        <td>${esc(record.supplierName||'--')}</td>
        <td>${num(record.totalItems)}</td>
        <td>${money(record.totalQty)}</td>
        <td>${money(record.totalAll)} ALL</td>
        <td>${money(record.amountPaid)} ALL</td>
        <td><button onclick="viewPurchaseRecord(${index})">Shiko</button></td>
      </tr>
    `);
  });
}

function viewPurchaseRecord(index){
  const record=purchaseHistory[index];
  if(!record) return;

  const html=`
    <p><b>Data:</b> ${esc(dateTime(record.timestamp))}</p>
    <p><b>Furnitori:</b> ${esc(record.supplierName||'--')}</p>
    <p><b>Telefoni:</b> ${esc(record.supplierPhone||'--')}</p>
    <p><b>Fatura:</b> ${esc(record.supplierInvoice||'--')}</p>
    <p><b>Total:</b> ${money(record.totalAll)} ALL</p>
    <p><b>Paguar:</b> ${money(record.amountPaid)} ALL</p>
    <p><b>Mbetje:</b> ${money(record.due)} ALL</p>
    <p><b>Mënyra:</b> ${esc(record.paymentMethod)}</p>
    <hr>
    <ul>
      ${(record.items||[]).map(item=>`
        <li>
          ${esc(item.n)} × ${money(item.q)}
          ${item.unit==='kg'?'kg':'copë'}
          @ ${money(item.cost)} ALL
          = ${money(item.q*item.cost)} ALL
        </li>
      `).join('')}
    </ul>
  `;

  showTxn('Detajet e Furnizimit', html);
}

function exportPurchaseCSV(){
  if(!purchaseHistory.length){
    alert('Nuk ka të dhëna për eksport.');
    return;
  }

  const rows=[[
    'id','timestamp','supplierName','supplierPhone','supplierInvoice',
    'totalItems','totalQty','totalAll','amountPaid','due','paymentMethod','items'
  ]];

  purchaseHistory.forEach(record=>{
    rows.push([
      record.id,
      record.timestamp,
      record.supplierName||'',
      record.supplierPhone||'',
      record.supplierInvoice||'',
      record.totalItems||0,
      record.totalQty||0,
      record.totalAll||0,
      record.amountPaid||0,
      record.due||0,
      record.paymentMethod||'',
      (record.items||[]).map(item=>`${item.n} x${item.q} ${item.unit}`).join(' | ')
    ]);
  });

  downloadFile('purchase_history.csv','\uFEFF'+rows.map(row=>row.map(csvCell).join(',')).join('\n'),'text/csv;charset=utf-8');
}

function printPurchaseInvoice(record){
  const items=(record.items||[]).map(item=>`
    <tr>
      <td>${esc(item.n)}</td>
      <td>${money(item.q)} ${item.unit==='kg'?'kg':'copë'}</td>
      <td>${money(item.cost)} ALL</td>
      <td>${money(item.q*item.cost)} ALL</td>
    </tr>
  `).join('');

  const paymentLabel={
    cash_all:'Cash (ALL)',
    card:'Kartë'
  }[record.paymentMethod] || record.paymentMethod || '--';

  $('printArea').innerHTML=`
    <div style="
      font-family:Arial,sans-serif;
      max-width:440px;
      margin:auto;
      color:#111
    ">
      <h2 style="text-align:center;margin:0">POS Market</h2>
      <p style="text-align:center;font-size:12px;margin:5px 0 12px">Faturë Furnizimi</p>
      <hr>
      <p>
        <b>Data:</b> ${esc(dateTime(record.timestamp))}<br>
        <b>Furnitori:</b> ${esc(record.supplierName||'--')}<br>
        <b>Fatura:</b> ${esc(record.supplierInvoice||'--')}<br>
        <b>Mënyra:</b> ${esc(paymentLabel)}
      </p>
      <table style="width:100%;border-collapse:collapse;font-size:13px">
        <thead>
          <tr>
            <th style="text-align:left">Produkt</th>
            <th>Sasi</th>
            <th>Çmim</th>
            <th>Total</th>
          </tr>
        </thead>
        <tbody>
          ${items}
        </tbody>
      </table>

      <hr>

      <div style="font-size:14px;line-height:1.8">
        <div style="display:flex;justify-content:space-between">
          <span>Artikuj:</span>
          <b>${num(record.totalItems)}</b>
        </div>

        <div style="display:flex;justify-content:space-between">
          <span>Sasi totale:</span>
          <b>${money(record.totalQty)}</b>
        </div>

        <div style="display:flex;justify-content:space-between;font-size:18px;border-top:2px solid #111;margin-top:5px;padding-top:5px">
          <span><b>TOTAL:</b></span>
          <b>${money(record.totalAll)} ALL</b>
        </div>

        <div style="display:flex;justify-content:space-between;color:#1d4ed8">
          <span><b>Paguar:</b></span>
          <b>${money(record.amountPaid)} ALL</b>
        </div>

        <div style="display:flex;justify-content:space-between;color:#dc2626">
          <span><b>Mbetje:</b></span>
          <b>${money(record.due)} ALL</b>
        </div>
      </div>

      <hr>
      <p style="text-align:center;font-size:12px">Faleminderit për bashkëpunimin!</p>
    </div>
  `;

  const printWindow=window.open('', '_blank', 'width=500,height=700');

  if(!printWindow){
    alert('Lejo popup-et për të printuar faturën e furnizimit.');
    return;
  }

  printWindow.document.write(`
    <!DOCTYPE html>
    <html lang="sq">
    <head>
      <meta charset="UTF-8">
      <title>Faturë Furnizimi</title>
      <style>
        *{box-sizing:border-box}
        body{
          margin:10px;
          background:#fff;
          color:#111;
          font-family:Arial,sans-serif;
        }
        table{
          width:100%;
          border-collapse:collapse;
        }
        th,td{
          border:1px solid #ddd;
          padding:5px;
          text-align:center;
        }
        th:first-child,td:first-child{
          text-align:left;
        }
        @media print{
          body{margin:0}
          button{display:none!important}
        }
      </style>
    </head>
    <body>
      ${$('printArea').innerHTML}
      <script>
        window.onload=function(){
          window.print();
          window.onafterprint=function(){
            window.close();
          };
        };
      <\/script>
    </body>
    </html>
  `);

  printWindow.document.close();
}

/* ================= SETTINGS ================= */

function loadSettings(){
  $('cfg_leadDays').value = reorderConfig.leadDays || 3;
  $('cfg_reviewDays').value = reorderConfig.reviewPeriodDays || 7;
  $('cfg_safety').value = reorderConfig.safetyStockFactor || 1.5;
  $('exchangeRateInput').value = exchangeRate;
}

function saveSettings(){
  reorderConfig.leadDays=Math.max(1, num($('cfg_leadDays').value,3));
  reorderConfig.reviewPeriodDays=Math.max(1, num($('cfg_reviewDays').value,7));
  reorderConfig.safetyStockFactor=Math.max(.1, num($('cfg_safety').value,1.5));
  save();

  showTxn('Cilësimet', '<div class="green">Cilësimet u ruajtën.</div>');
}

/* ================= MODALS ================= */

function showTxn(title,html){
  $('txnTitle').textContent=title;
  $('txnMsg').innerHTML=html;
  $('txnModal').style.display='block';
}

function closeTxn(){
  $('txnModal').style.display='none';
  $('txnMsg').innerHTML='';
}

/* ================= RENDER ================= */

function renderAll(){
  renderProducts();
  renderCart();
  renderHistory();
  renderLoyaltyTable();
  renderStats();
  updateBalance();
  refreshLoyaltyUI();
  checkAlerts();
  renderPurchaseCart();
  renderPurchaseHistory();
  loadSettings();
}

/* ================= EVENTS ================= */

$('saleScan').addEventListener('keydown',event=>{
  if(event.key==='Enter'){
    event.preventDefault();
    manualAdd();
  }
});

$('purchaseScan').addEventListener('keydown',event=>{
  if(event.key==='Enter'){
    event.preventDefault();
    addPurchaseItem();
  }
});

$('pb').addEventListener('keydown',event=>{
  if(event.key==='Enter'){
    event.preventDefault();
    $('pn').focus();
  }
});

$('paid').addEventListener('input',recalc);
$('client').addEventListener('input',refreshLoyaltyUI);
$('clientPhone').addEventListener('input',refreshLoyaltyUI);
$('clientSearch').addEventListener('input',renderLoyaltyTable);

document.addEventListener('keydown',event=>{
  if(event.key==='Escape'){
    document.querySelectorAll('.modal').forEach(modal=>modal.style.display='none');
  }
});

['alertsModal','viewModal','txnModal'].forEach(id=>{
  $(id).addEventListener('click',event=>{
    if(event.target===$(id)){
      $(id).style.display='none';
    }
  });
});

window.addEventListener('storage',()=>{
  products=parse(localStorage.getItem('p'),[]);
  salesHistory=parse(localStorage.getItem('salesHistory'),[]);
  loyaltyCustomers=parse(localStorage.getItem('loyaltyCustomers'),{});
  suppliers=parse(localStorage.getItem('suppliers'),[]);
  purchaseHistory=parse(localStorage.getItem('purchaseHistory'),[]);

  cashALL=num(localStorage.getItem('cashALL'), num(localStorage.getItem('daily'),0));
  cardALL=num(localStorage.getItem('cardALL'), num(localStorage.getItem('cardBalanceALL'),0));
  cashEUR=num(localStorage.getItem('cashEUR'), num(localStorage.getItem('eurInRegister'),0));

  openingFloatALL=num(localStorage.getItem('openingFloatALL'),0);
  kasaOpenedAt=localStorage.getItem('kasaOpenedAt')||'';
  exchangeRate=num(localStorage.getItem('exchangeRate'),100);

  renderAll();
});

/* ================= INITIALIZATION ================= */

renderAll();

/* ================= GLOBAL FUNCTIONS ================= */

window.doLogin=doLogin;
window.logout=logout;
window.openSec=openSec;

window.addProduct=addProduct;
window.updateProduct=updateProduct;
window.deleteProduct=deleteProduct;

window.openAlertsModal=openAlertsModal;
window.closeAlertsModal=closeAlertsModal;

window.manualAdd=manualAdd;
window.addToCart=addToCart;
window.changeQty=changeQty;
window.removeCartItem=removeCartItem;
window.recalc=recalc;
window.paymentChanged=paymentChanged;
window.pay=pay;
window.cancelSale=cancelSale;

window.openKasa=openKasa;
window.updateBalance=updateBalance;
window.saveExchangeRate=saveExchangeRate;
window.closeDay=closeDay;
window.exportDailyClosuresExcel=exportDailyClosuresExcel;

window.viewSale=viewSale;
window.closeView=closeView;
window.deleteSale=deleteSale;
window.settleDebt=settleDebt;

window.printInvoice=printInvoice;
window.exportCSV=exportCSV;
window.exportLoyaltyData=exportLoyaltyData;
window.backupData=backupData;
window.restoreData=restoreData;
window.clearOld=clearOld;

window.selectCustomer=selectCustomer;
window.renderLoyaltyTable=renderLoyaltyTable;
window.resetClientFilter=resetClientFilter;
window.saveSettings=saveSettings;
window.closeTxn=closeTxn;
window.renderAll=renderAll;

window.addPurchaseItem=addPurchaseItem;
window.completePurchase=completePurchase;
window.cancelPurchaseCart=cancelPurchaseCart;
window.renderPurchaseHistory=renderPurchaseHistory;
window.viewPurchaseRecord=viewPurchaseRecord;
window.exportPurchaseCSV=exportPurchaseCSV;
window.printPurchaseInvoice=printPurchaseInvoice;
window.removePurchaseItem=removePurchaseItem;
</script>

</body>
</html>
