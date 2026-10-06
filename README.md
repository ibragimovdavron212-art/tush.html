# tush.html```html
<!DOCTYPE html>
<html lang="uz">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EduSRM — O'quv markazi boshqaruv tizimi</title>
<style>
  * { margin:0; padding:0; box-sizing:border-box; font-family:'Segoe UI',system-ui,sans-serif; }
  :root {
    --primary:#4f46e5; --primary-dark:#4338ca; --success:#10b981;
    --danger:#ef4444; --warning:#f59e0b; --bg:#f3f4f6;
    --card:#fff; --text:#1f2937; --muted:#6b7280; --border:#e5e7eb;
  }
  body { background:var(--bg); color:var(--text); display:flex; min-height:100vh; }

  /* LOGIN */
  #loginScreen {
    position:fixed; inset:0; background:linear-gradient(135deg,#4f46e5,#7c3aed);
    display:flex; align-items:center; justify-content:center; z-index:999;
  }
  .login-box {
    background:#fff; padding:40px; border-radius:16px; width:380px;
    box-shadow:0 20px 60px rgba(0,0,0,.3);
  }
  .login-box h1 { color:var(--primary); margin-bottom:8px; font-size:26px; }
  .login-box p { color:var(--muted); margin-bottom:24px; font-size:14px; }
  .login-box input {
    width:100%; padding:12px; margin-bottom:12px; border:1px solid var(--border);
    border-radius:8px; font-size:14px;
  }
  .login-box button {
    width:100%; padding:12px; background:var(--primary); color:#fff; border:none;
    border-radius:8px; font-size:15px; cursor:pointer; font-weight:600;
  }
  .login-box button:hover { background:var(--primary-dark); }
  .hint { font-size:12px; color:var(--muted); margin-top:10px; text-align:center; }

  /* SIDEBAR */
  .sidebar {
    width:250px; background:#1e1b4b; color:#fff; padding:20px 0;
    display:flex; flex-direction:column; position:fixed; top:0; bottom:0; overflow-y:auto;
  }
  .sidebar h2 { padding:0 20px 20px; font-size:18px; border-bottom:1px solid #312e81; }
  .sidebar nav a {
    display:flex; align-items:center; gap:10px; padding:12px 20px; color:#c7d2fe;
    text-decoration:none; font-size:14px; cursor:pointer; transition:.2s;
    border-left:3px solid transparent;
  }
  .sidebar nav a:hover { background:#312e81; color:#fff; }
  .sidebar nav a.active { background:#312e81; color:#fff; border-left-color:#818cf8; }
  .sidebar .user {
    margin-top:auto; padding:15px 20px; border-top:1px solid #312e81; font-size:13px;
  }
  .sidebar .user small { color:#a5b4fc; display:block; margin-top:4px; }
  /* MAIN */
  .main { margin-left:250px; flex:1; padding:24px; }
  .header {
    display:flex; justify-content:space-between; align-items:center; margin-bottom:20px;
  }
  .header h1 { font-size:24px; }
  .btn {
    padding:10px 18px; background:var(--primary); color:#fff; border:none;
    border-radius:8px; cursor:pointer; font-size:14px; font-weight:600;
  }
  .btn:hover { background:var(--primary-dark); }
  .btn-sm { padding:6px 12px; font-size:12px; }
  .btn-danger { background:var(--danger); }
  .btn-danger:hover { background:#dc2626; }
  .btn-success { background:var(--success); }
  .btn-warning { background:var(--warning); }

  /* CARDS */
  .stats { display:grid; grid-template-columns:repeat(auto-fit,minmax(200px,1fr)); gap:16px; margin-bottom:24px; }
  .stat-card {
    background:#fff; padding:20px; border-radius:12px;
      /* TABLE */
  .card { background:#fff; border-radius:12px; padding:20px; box-shadow:0 1px 3px rgba(0,0,0,.08); margin-bottom:20px; }
  table { width:100%; border-collapse:collapse; font-size:14px; }
  th, td { padding:12px; text-align:left; border-bottom:1px solid var(--border); }
  th { background:#f9fafb; font-weight:600; color:var(--muted); font-size:12px; text-transform:uppercase; }
  tr:hover td { background:#f9fafb; }
  .badge {
    display:inline-block; padding:3px 10px; border-radius:20px; font-size:11px; font-weight:600;
  }
  .badge-active { background:#d1fae5; color:#065f46; }
  .badge-inactive { background:#fee2e2; color:#991b1b; }
  .badge-pending { background:#fef3c7; color:#92400e; }
  .stars { color:#f59e0b; }

  /* MODAL */
  .modal-bg {
    display:none; position:fixed; inset:0; background:rgba(0,0,0,.5);
    z-index:1000; align-items:center; justify-content:center;
  }
  .modal-bg.show { display:flex; }
  .modal {
    background:#fff; padding:24px; border-radius:12px; width:480px; max-width:90%;
    max-height:90vh; overflow-y:auto;
  }
  .modal h3 { margin-bottom:18px; }
  .modal label { display:block; font-size:13px; margin-bottom:6px; color:var(--muted); }
  .modal input, .modal select, .modal textarea {
    width:100%; padding:10px; border:1px solid var(--border);
    border-radius:8px; margin-bottom:14px; font-size:14px;
  }
  .modal-actions { display:flex; gap:10px; justify-content:flex-end; }
  .btn-secondary { background:#e5e7eb; color:var(--text); }

  /* PAGE */
  .page { display:none; }
  .page.active { display:block; }

  .empty { text-align:center; padding:40px; color:var(--muted); }
  .toolbar { display:flex; gap:10px; margin-bottom:16px; }
  .toolbar input { flex:1; padding:10px; border:1px solid var(--border); border-radius:8px; }
    /* Toast */
  .toast {
    position:fixed; bottom:20px; right:20px; background:#1f2937; color:#fff;
    padding:14px 20px; border-radius:8px; z-index:2000; font-size:14px;
    animation:slideIn .3s;
  }
  @keyframes slideIn { from{transform:translateX(100%);opacity:0;} to{transform:translateX(0);opacity:1;} }
</style>
</head>
<body>

<!-- ================= LOGIN ================= -->
<div id="loginScreen">
  <div class="login-box">
    <h1>EduSRM</h1>
    <p>O'quv markazi boshqaruv tizimi</p>
    <input id="loginUser" placeholder="Login" value="admin">
    <input id="loginPass" type="password" placeholder="Parol" value="1234">
    <button onclick="login()">Kirish</button>
    <div class="hint">Demo: admin / 1234</div>
  </div>
</div>

<!-- ================= SIDEBAR ================= -->
<div class="sidebar">
  <h2>EduSRM</h2>
  <nav id="nav">
    <a data-page="dashboard" class="active">📊 Dashboard</a>
    <a data-page="partners">🤝 Hamkorlar</a>
    <a data-page="contracts">📄 Shartnomalar</a>
    <a data-page="requests">📝 Xarid talabnomasi</a>
    <a data-page="teachers">👨‍🏫 O'qituvchilar</a>
    <a data-page="kpi">⭐ Baholash (KPI)</a>
    <a data-page="finance">💰 Moliya</a>
    <a data-page="reports">📈 Hisobotlar</a>
    <a data-page="notifications">🔔 Bildirishnomalar</a>
    <a data-page="integrations">🔌 Integratsiyalar</a>
    <a data-page="settings">⚙️ Sozlamalar</a>
    <a data-page="security">🔒 Xavfsizlik</a>
  </nav>
  <div class="user">
    👤 <b id="userName">admin</b>
    <small>Administrator</small>
    <button class="btn btn-sm btn-danger" style="margin-top:10px;width:100%" onclick="logout()">Chiqish</button>
  </div>
</div>

<!-- ================= MAIN ================= -->
<div class="main">

  <!-- DASHBOARD -->
  <div class="page active" id="page-dashboard">
    <div class="header"><h1>Dashboard</h1></div>
    <div class="stats">
      <div class="stat-card"><div class="label">Hamkorlar</div><div class="value" id="stPartners">0</div></div>
      <div class="stat-card"><div class="label">Shartnomalar</div><div class="value" id="stContracts">0</div></div>
      <div class="stat-card"><div class="label">O'qituvchilar</div><div class="value" id="stTeachers">0</div></div>
      <div class="stat-card"><div class="label">Umumiy xarajat (so'm)</div><div class="value" id="stFinance">0</div></div>
    </div>
    <div class="card">
      <h3>Oxirgi talabnomalar</h3>
      <table><thead><tr><th>ID</th><th>Nomi</th><th>Miqdor</th><th>Holat</th></tr></thead>
      <tbody id="dashRequests"></tbody></table>
    </div>
  </div>
  
    box-shadow:0 1px 3px rgba(0,0,0,.08);
  }
  .stat-card .label { color:var(--muted); font-size:13px; margin-bottom:8px; }
  .stat-card .value { font-size:28px; font-weight:700; color:var(--primary); }
    <!-- PARTNERS -->
  <div class="page" id="page-partners">
    <div class="header">
      <h1>Hamkorlar</h1>
      <button class="btn" onclick="openPartnerModal()">+ Yangi hamkor</button>
    </div>
    <div class="card">
      <div class="toolbar"><input id="partnerSearch" placeholder="🔍 Qidirish..." oninput="renderPartners()"></div>
      <table>
        <thead><tr><th>Nomi</th><th>Turi</th><th>Telefon</th><th>Holat</th><th>Amal</th></tr></thead>
        <tbody id="partnersBody"></tbody>
      </table>
    </div>
  </div>

  <!-- CONTRACTS -->
  <div class="page" id="page-contracts">
    <div class="header">
      <h1>Shartnomalar</h1>
      <button class="btn" onclick="openContractModal()">+ Yangi shartnoma</button>
    </div>
    <div class="card">
      <table>
        <thead><tr><th>Raqam</th><th>Hamkor</th><th>Summa</th><th>Boshlanish</th><th>Tugash</th><th>Holat</th><th>Amal</th></tr></thead>
        <tbody id="contractsBody"></tbody>
      </table>
    </div>
  </div>

  <!-- REQUESTS -->
  <div class="page" id="page-requests">
    <div class="header">
      <h1>Xarid talabnomalari</h1>
      <button class="btn" onclick="openRequestModal()">+ Yangi talabnoma</button>
    </div>
    <div class="card">
      <table>
        <thead><tr><th>ID</th><th>Nomi</th><th>Miqdor</th><th>Holat</th><th>Amal</th></tr></thead>
        <tbody id="requestsBody"></tbody>
      </table>
    </div>
  </div>
    <!-- TEACHERS -->
  <div class="page" id="page-teachers">
    <div class="header">
      <h1>O'qituvchilar</h1>
      <button class="btn" onclick="openTeacherModal()">+ Yangi o'qituvchi</button>
    </div>
    <div class="card">
      <table>
        <thead><tr><th>FISH</th><th>Fan</th><th>Yuklama (soat)</th><th>Reyting</th><th>Holat</th><th>Amal</th></tr></thead>
        <tbody id="teachersBody"></tbody>
      </table>
    </div>
  </div>

  <!-- KPI -->
  <div class="page" id="page-kpi">
    <div class="header"><h1>Baholash va KPI</h1></div>
    <div class="card">
      <table>
        <thead><tr><th>O'qituvchi</th><th>Davomat %</th><th>O'quvchi NPS</th><th>Natija %</th><th>Umumiy reyting</th></tr></thead>
        <tbody id="kpiBody"></tbody>
      </table>
    </div>
  </div>

  <!-- FINANCE -->
  <div class="page" id="page-finance">
    <div class="header">
      <h1>Moliya</h1>
      <button class="btn" onclick="openFinanceModal()">+ To'lov qo'shish</button>
    </div>
    <div class="card">
      <table>
        <thead><tr><th>Hamkor/O'qituvchi</th><th>Summa</th><th>Sana</th><th>Turi</th><th>Holat</th></tr></thead>
        <tbody id="financeBody"></tbody>
      </table>
    </div>
  </div>

  <!-- REPORTS -->
  <div class="page" id="page-reports">
    <div class="header">
      <h1>Hisobotlar</h1>
      <button class="btn" onclick="exportCSV()">⬇ CSV yuklab olish</button>
    </div>
    <div class="stats">
      <div class="stat-card"><div class="label">Faol shartnomalar</div><div class="value" id="rpActive">0</div></div>
      <div class="stat-card"><div class="label">To'langan summa</div><div class="value" id="rpPaid">0</div></div>
      <div class="stat-card"><div class="label">Kutilayotgan to'lov</div><div class="value" id="rpPending">0</div></div>
      <div class="stat-card"><div class="label">O'rtacha reyting</div><div class="value" id="rpRating">0</div></div>
    </div>
  </div>
    <!-- NOTIFICATIONS -->
  <div class="page" id="page-notifications">
    <div class="header">
      <h1>Bildirishnomalar</h1>
      <button class="btn" onclick="openNotifModal()">+ Xabar yuborish</button>
    </div>
    <div class="card"><div id="notifList"></div></div>
  </div>

  <!-- INTEGRATIONS -->
  <div class="page" id="page-integrations">
    <div class="header"><h1>Integratsiyalar</h1></div>
    <div class="stats" id="integrationsList"></div>
  </div>

  <!-- SETTINGS -->
  <div class="page" id="page-settings">
    <div class="header"><h1>Sozlamalar</h1></div>
    <div class="card">
      <label>Kompaniya nomi</label>
      <input id="setCompany" style="width:100%;padding:10px;border:1px solid var(--border);border-radius:8px;margin-bottom:14px">
      <label>Valyuta</label>
      <select id="setCurrency" style="width:100%;padding:10px;border:1px solid var(--border);border-radius:8px;margin-bottom:14px">
        <option>UZS</option><option>USD</option><option>EUR</option>
      </select>
      <label>Til</label>
      <select id="setLang" style="width:100%;padding:10px;border:1px solid var(--border);border-radius:8px;margin-bottom:14px">
        <option>O'zbek</option><option>Русский</option><option>English</option>
      </select>
      <button class="btn" onclick="saveSettings()">Saqlash</button>
      <button class="btn btn-danger" style="margin-left:10px" onclick="resetData()">Barcha ma'lumotni o'chirish</button>
    </div>
  </div>

  <!-- SECURITY -->
  <div class="page" id="page-security">
    <div class="header"><h1>Xavfsizlik</h1></div>
    <div class="card">
      <h3>Audit jurnali</h3>
      <div id="auditLog" style="margin-top:14px;font-size:13px;color:var(--muted)"></div>
    </div>
  </div>

</div>
<!-- ================= MODAL ================= -->
<div class="modal-bg" id="modalBg">
  <div class="modal" id="modalContent"></div>
</div>

<script>
/* ============================================================
   DATA LAYER (localStorage)
============================================================ */
const DB = {
  get(k, def=[]) { try { return JSON.parse(localStorage.getItem('srm_'+k)) ?? def; } catch { return def; } },
  set(k, v) { localStorage.setItem('srm_'+k, JSON.stringify(v)); },
  push(k, item) { const a = this.get(k); item.id = Date.now(); a.push(item); this.set(k, a); return item; },
  remove(k, id) { this.set(k, this.get(k).filter(x => x.id != id)); },
  update(k, id, patch) {
    const a = this.get(k); const i = a.findIndex(x => x.id == id);
    if (i > -1) { a[i] = {...a[i], ...patch}; this.set(k, a); }
  }
};

/* Demo data */
if (!DB.get('seeded')) {
  DB.set('partners', [
    {id:1, name:"IT Academy MChJ", type:"O'qituvchi", phone:"+998901112233", status:"Faol"},
    {id:2, name:"Ustoz Nodira Karimova", type:"O'qituvchi", phone:"+998902223344", status:"Faol"},
    {id:3, name:"ContentPro Studio", type:"Kontent", phone:"+998903334455", status:"Faol"},
    {id:4, name:"Zoom Inc.", type:"Texnik", phone:"+1-888-799", status:"Faol"},
  ]);
  DB.set('contracts', [
    {id:1, num:"SH-001", partner:"IT Academy MChJ", amount:15000000, start:"2024-01-01", end:"2024-12-31", status:"Faol"},
    {id:2, num:"SH-002", partner:"Ustoz Nodira Karimova", amount:8000000, start:"2024-03-01", end:"2024-09-01", status:"Faol"},
  ]);
  DB.set('requests', [
    {id:1, name:"Yangi Python kursi uchun o'qituvchi", qty:2, status:"Tasdiqlangan"},
    {id:2, name:"Kamera jihozlari", qty:1, status:"Kutilmoqda"},
  ]);
  DB.set('teachers', [
    {id:1, name:"Nodira Karimova", subject:"Ingliz tili", hours:120, rating:4.8, status:"Faol"},
    {id:2, name:"Jasur Toshmatov", subject:"Python", hours:90, rating:4.6, status:"Faol"},
    {id:3, name:"Malika Yusupova", subject:"Matematika", hours:60, rating:4.9, status:"Faol"},
  ]);
  DB.set('finance', [
    {id:1, who:"Nodira Karimova", amount:5000000, date:"2024-05-01", type:"Oylik", status:"To'langan"},
    {id:2, who:"IT Academy MChJ", amount:12000000, date:"2024-05-05", type:"Xizmat", status:"Kutilmoqda"},
  ]);
  DB.set('notifs', [
    {id:1, text:"SH-002 shartnoma muddati 30 kun ichida tugaydi", date:new Date().toISOString()},
  ]);
  DB.set('settings', {company:"EduMarkaz", currency:"UZS", lang:"O'zbek"});
  DB.set('audit', [{id:1, action:"Tizim ishga tushdi", date:new Date().toISOString()}]);
  DB.set('seeded', true);
}

/* ============================================================
   AUTH
============================================================ */
function login() {
  const u = document.getElementById('loginUser').value;
  const p = document.getElementById('loginPass').value;
  if (u === 'admin' && p === '1234') {
    document.getElementById('loginScreen').style.display = 'none';
    document.getElementById('userName').textContent = u;
    audit('Tizimga kirdi: ' + u);
    renderAll();
  } else alert("Login yoki parol noto'g'ri!");
}
function logout() { location.reload(); }

/* ============================================================
   NAVIGATION
============================================================ */
document.querySelectorAll('#nav a').forEach(a => {
  a.onclick = () => {
    document.querySelectorAll('#nav a').forEach(x => x.classList.remove('active'));
    a.classList.add('active');
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById('page-' + a.dataset.page).classList.add('active');
    renderAll();
  };
});
  /* ============================================================
   UTILS
============================================================ */
function toast(msg, color='#1f2937') {
  const t = document.createElement('div');
  t.className = 'toast'; t.style.background = color; t.textContent = msg;
  document.body.appendChild(t);
  setTimeout(() => t.remove(), 2500);
}
function stars(r) { return '★'.repeat(Math.round(r)) + '☆'.repeat(5 - Math.round(r)); }
function fmt(n) { return Number(n).toLocaleString('uz-UZ'); }
function audit(action) {
  const a = DB.get('audit');
  a.push({id:Date.now(), action, date:new Date().toISOString()});
  DB.set('audit', a.slice(-50));
}
function badge(s) {
  const map = {'Faol':'active','Nofaol':'inactive','Tasdiqlangan':'active',
    'Kutilmoqda':'pending','Rad etilgan':'inactive','To\'langan':'active'};
  return `<span class="badge badge-${map[s]||'pending'}">${s}</span>`;
}
function closeModal() { document.getElementById('modalBg').classList.remove('show'); }
function showModal(html) {
  document.getElementById('modalContent').innerHTML = html;
  document.getElementById('modalBg').classList.add('show');
}

/* ============================================================
   RENDER
============================================================ */
function renderAll() {
  renderDashboard();
  renderPartners();
  renderContracts();
  renderRequests();
  renderTeachers();
  renderKPI();
  renderFinance();
  renderReports();
  renderNotifications();
  renderIntegrations();
  renderSettings();
  renderSecurity();
}

/* ---- DASHBOARD ---- */
function renderDashboard() {
  const p = DB.get('partners'), c = DB.get('contracts'), t = DB.get('teachers'), f = DB.get('finance');
  document.getElementById('stPartners').textContent = p.length;
  document.getElementById('stContracts').textContent = c.length;
  document.getElementById('stTeachers').textContent = t.length;
  document.getElementById('stFinance').textContent = fmt(f.reduce((s,x)=>s+Number(x.amount),0));
  document.getElementById('dashRequests').innerHTML = DB.get('requests').slice(-5).map(r =>
    `<tr><td>#${r.id}</td><td>${r.name}</td><td>${r.qty}</td><td>${badge(r.status)}</td></tr>`).join('')
    || '<tr><td colspan="4" class="empty">Ma\'lumot yo\'q</td></tr>';
}

/* ---- PARTNERS ---- */
function renderPartners() {
  const q = (document.getElementById('partnerSearch')?.value || '').toLowerCase();
  const list = DB.get('partners').filter(p => p.name.toLowerCase().includes(q));
  document.getElementById('partnersBody').innerHTML = list.map(p => `
    <tr>
      <td><b>${p.name}</b></td><td>${p.type}</td><td>${p.phone}</td>
      <td>${badge(p.status)}</td>
      <td>
        <button class="btn btn-sm btn-warning" onclick="editPartner(${p.id})">✏️</button>
        <button class="btn btn-sm btn-danger" onclick="delItem('partners',${p.id})">🗑</button>
      </td>
    </tr>`).join('') || '<tr><td colspan="5" class="empty">Bo\'sh</td></tr>';
}
function openPartnerModal(p = {}) {
  showModal(`
    <h3>${p.id ? 'Tahrirlash' : 'Yangi'} hamkor</h3>
    <label>Nomi</label><input id="m_name" value="${p.name||''}">
    <label>Turi</label>
    <select id="m_type">
      ${["O'qituvchi","Kontent","Texnik","Marketing","Material"].map(x =>
        `<option ${p.type===x?'selected':''}>${x}</option>`).join('')}
    </select>
    <label>Telefon</label><input id="m_phone" value="${p.phone||''}">
    <label>Holat</label>
    <select id="m_status">
      ${["Faol","Nofaol"].map(x => `<option ${p.status===x?'selected':''}>${x}</option>`).join('')}
    </select>
    <div class="modal-actions">
      <button class="btn btn-secondary" onclick="closeModal()">Bekor</button>
      <button class="btn" onclick="savePartner(${p.id||0})">Saqlash</button>
    </div>`);
}
function editPartner(id) { openPartnerModal(DB.get('partners').find(x => x.id === id)); }
function savePartner(id) {
  const data = {
    name: m_name.value, type: m_type.value,
    phone: m_phone.value, status: m_status.value
  };
  if (id) DB.update('partners', id, data); else DB.push('partners', data);
  audit((id?'Tahrirlandi':'Qo\'shildi') + ': hamkor ' + data.name);
  closeModal(); renderAll(); toast("✅ Saqlandi", "#10b981");
  }
  /* ---- CONTRACTS ---- */
function renderContracts() {
  document.getElementById('contractsBody').innerHTML = DB.get('contracts').map(c => `
    <tr>
      <td>${c.num}</td><td>${c.partner}</td><td>${fmt(c.amount)}</td>
      <td>${c.start}</td><td>${c.end}</td><td>${badge(c.status)}</td>
      <td>
        <button class="btn btn-sm btn-warning" onclick="editContract(${c.id})">✏️</button>
        <button class="btn btn-sm btn-danger" onclick="delItem('contracts',${c.id})">🗑</button>
      </td>
    </tr>`).join('') || '<tr><td colspan="7" class="empty">Bo\'sh</td></tr>';
}
function openContractModal(c = {}) {
  showModal(`
    <h3>${c.id ? 'Tahrirlash' : 'Yangi'} shartnoma</h3>
    <label>Raqam</label><input id="c_num" value="${c.num||''}">
    <label>Hamkor</label>
    <select id="c_partner">
      ${DB.get('partners').map(p => `<option ${c.partner===p.name?'selected':''}>${p.name}</option>`).join('')}
    </select>
    <label>Summa</label><input id="c_amount" type="number" value="${c.amount||''}">
    <label>Boshlanish</label><input id="c_start" type="date" value="${c.start||''}">
    <label>Tugash</label><input id="c_end" type="date" value="${c.end||''}">
    <label>Holat</label>
    <select id="c_status">
      ${["Faol","Nofaol"].map(x => `<option ${c.status===x?'selected':''}>${x}</option>`).join('')}
    </select>
    <div class="modal-actions">
      <button class="btn btn-secondary" onclick="closeModal()">Bekor</button>
      <button class="btn" onclick="saveContract(${c.id||0})">Saqlash</button>
    </div>`);
}
function editContract(id) { openContractModal(DB.get('contracts').find(x => x.id === id)); }
function saveContract(id) {
  const data = { num:c_num.value, partner:c_partner.value, amount:c_amount.value,
    start:c_start.value, end:c_end.value, status:c_status.value };
  if (id) DB.update('contracts', id, data); else DB.push('contracts', data);
  audit('Shartnoma saqlandi: ' + data.num);
  closeModal(); renderAll(); toast("✅ Saqlandi", "#10b981");
}

/* ---- REQUESTS ---- */
function renderRequests() {
  document.getElementById('requestsBody').innerHTML = DB.get('requests').map(r => `
    <tr>
      <td>#${r.id}</td><td>${r.name}</td><td>${r.qty}</td>
      <td>${badge(r.status)}</td>
      <td>
        <button class="btn btn-sm btn-success" onclick="setReqStatus(${r.id},'Tasdiqlangan')">✓</button>
        <button class="btn btn-sm btn-danger" onclick="setReqStatus(${r.id},'Rad etilgan')">✗</button>
        <button class="btn btn-sm btn-danger" onclick="delItem('requests',${r.id})">🗑</button>
      </td>
    </tr>`).join('') || '<tr><td colspan="5" class="empty">Bo\'sh</td></tr>';
}
function openRequestModal() {
  showModal(`
    <h3>Yangi talabnoma</h3>
    <label>Nomi</label><input id="r_name">
    <label>Miqdor</label><input id="r_qty" type="number" value="1">
    <div class="modal-actions">
      <button class="btn btn-secondary" onclick="closeModal()">Bekor</button>
      <button class="btn" onclick="saveRequest()">Saqlash</button>
    </div>`);
}
function saveRequest() {
  DB.push('requests', {name:r_name.value, qty:r_qty.value, status:'Kutilmoqda'});
  audit('Talabnoma: ' + r_name.value);
  closeModal(); renderAll(); toast("✅ Yuborildi", "#10b981");
}
function setReqStatus(id, s) { DB.update('requests', id, {status:s}); renderAll(); toast("Holat: "+s); }
  /* ---- TEACHERS ---- */
function renderTeachers() {
  document.getElementById('teachersBody').innerHTML = DB.get('teachers').map(t => `
    <tr>
      <td><b>${t.name}</b></td><td>${t.subject}</td><td>${t.hours}</td>
      <td class="stars">${stars(t.rating)} ${t.rating}</td>
      <td>${badge(t.status)}</td>
      <td>
        <button class="btn btn-sm btn-warning" onclick="editTeacher(${t.id})">✏️</button>
        <button class="btn btn-sm btn-danger" onclick="delItem('teachers',${t.id})">🗑</button>
      </td>
    </tr>`).join('') || '<tr><td colspan="6" class="empty">Bo\'sh</td></tr>';
}
function openTeacherModal(t = {}) {
  showModal(`
    <h3>${t.id ? 'Tahrirlash' : 'Yangi'} o'qituvchi</h3>
    <label>FISH</label><input id="t_name" value="${t.name||''}">
    <label>Fan</label><input id="t_subject" value="${t.subject||''}">
    <label>Yuklama (soat)</label><input id="t_hours" type="number" value="${t.hours||''}">
    <label>Reyting (0-5)</label><input id="t_rating" type="number" step="0.1" max="5" value="${t.rating||5}">
    <label>Holat</label>
    <select id="t_status">
      ${["Faol","Nofaol"].map(x => `<option ${t.status===x?'selected':''}>${x}</option>`).join('')}
    </select>
    <div class="modal-actions">
      <button class="btn btn-secondary" onclick="closeModal()">Bekor</button>
      <button class="btn" onclick="saveTeacher(${t.id||0})">Saqlash</button>
    </div>`);
}
function editTeacher(id) { openTeacherModal(DB.get('teachers').find(x => x.id === id)); }
function saveTeacher(id) {
  const data = { name:t_name.value, subject:t_subject.value, hours:t_hours.value,
    rating:parseFloat(t_rating.value), status:t_status.value };
  if (id) DB.update('teachers', id, data); else DB.push('teachers', data);
  audit('O\'qituvchi: ' + data.name);
  closeModal(); renderAll(); toast("✅ Saqlandi", "#10b981");
}

/* ---- KPI ---- */
function renderKPI() {
  document.getElementById('kpiBody').innerHTML = DB.get('teachers').map(t => {
    const att = Math.min(100, 80 + t.rating * 4).toFixed(0);
    const nps = (t.rating * 20).toFixed(0);
    const res = (t.rating * 18).toFixed(0);
    return `<tr><td><b>${t.name}</b></td><td>${att}%</td><td>${nps}</td><td>${res}%</td>
      <td class="stars">${stars(t.rating)} ${t.rating}</td></tr>`;
  }).join('') || '<tr><td colspan="5" class="empty">Bo\'sh</td></tr>';
}

/* ---- FINANCE ---- */
function renderFinance() {
  document.getElementById('financeBody').innerHTML = DB.get('finance').map(f => `
    <tr><td>${f.who}</td><td>${fmt(f.amount)}</td><td>${f.date}</td><td>${f.type}</td>
    <td>${badge(f.status)}</td>
    <td><button class="btn btn-sm btn-danger" onclick="delItem('finance',${f.id})">🗑</button></td>
    </tr>`).join('') || '<tr><td colspan="6" class="empty">Bo\'sh</td></tr>';
}
function openFinanceModal() {
  showModal(`
    <h3>Yangi to'lov</h3>
    <label>Kimga</label><input id="f_who">
    <label>Summa</label><input id="f_amount" type="number">
    <label>Sana</label><input id="f_date" type="date" value="${new Date().toISOString().slice(0,10)}">
    <label>Turi</label>
    <select id="f_type"><option>Oylik</option><option>Xizmat</option><option>Bonus</option></select>
    <label>Holat</label>
    <select id="f_status"><option>To'langan</option><option>Kutilmoqda</option></select>
    <div class="modal-actions">
      <button class="btn btn-secondary" onclick="closeModal()">Bekor</button>
      <button class="btn" onclick="saveFinance()">Saqlash</button>
    </div>`);
}
function saveFinance() {
  DB.push('finance', {who:f_who.value, amount:f_amount.value, date:f_date.value,
    type:f_type.value, status:f_status.value});
  audit('To\'lov: ' + f_who.value);
  closeModal(); renderAll(); toast("✅ Saqlandi", "#10b981");
    }
  /* ---- REPORTS ---- */
function renderReports() {
  const c = DB.get('contracts'), f = DB.get('finance'), t = DB.get('teachers');
  document.getElementById('rpActive').textContent = c.filter(x=>x.status==='Faol').length;
  document.getElementById('rpPaid').textContent = fmt(f.filter(x=>x.status==="To'langan").reduce((s,x)=>s+Number(x.amount),0));
  document.getElementById('rpPending').textContent = fmt(f.filter(x=>x.status==="Kutilmoqda").reduce((s,x)=>s+Number(x.amount),0));
  const avg = t.length ? (t.reduce((s,x)=>s+x.rating,0)/t.length).toFixed(2) : 0;
  document.getElementById('rpRating').textContent = avg;
}
function exportCSV() {
  const rows = [["Bo'lim","Ma'lumot"]];
  DB.get('partners').forEach(p => rows.push(['Hamkor', p.name + ' | ' + p.type]));
  DB.get('contracts').forEach(c => rows.push(['Shartnoma', c.num + ' | ' + c.amount]));
  DB.get('teachers').forEach(t => rows.push(['O\'qituvchi', t.name + ' | ' + t.subject]));
  const csv = rows.map(r => r.map(x => `"${x}"`).join(',')).join('\n');
  const blob = new Blob([csv], {type:'text/csv'});
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob); a.download = 'srm_report.csv'; a.click();
  toast("📥 Yuklandi", "#10b981");
}

/* ---- NOTIFICATIONS ---- */
function renderNotifications() {
  document.getElementById('notifList').innerHTML = DB.get('notifs').map(n => `
    <div style="padding:12px;border-bottom:1px solid var(--border)">
      🔔 ${n.text} <small style="color:var(--muted);float:right">${new Date(n.date).toLocaleString()}</small>
    </div>`).join('') || '<div class="empty">Xabarlar yo\'q</div>';
}
function openNotifModal() {
  showModal(`
    <h3>Xabar yuborish</h3>
    <label>Matn</label><textarea id="n_text" rows="3"></textarea>
    <div class="modal-actions">
      <button class="btn btn-secondary" onclick="closeModal()">Bekor</button>
      <button class="btn" onclick="saveNotif()">Yuborish</button>
    </div>`);
}
function saveNotif() {
  DB.push('notifs', {text:n_text.value, date:new Date().toISOString()});
  closeModal(); renderAll(); toast("🔔 Yuborildi", "#10b981");
}

/* ---- INTEGRATIONS ---- */
const INTEGRATIONS = [
  {name:"Telegram Bot", icon:"✈️", status:"Ulandi"},
  {name:"Zoom", icon:"📹", status:"Ulandi"},
  {name:"Google Classroom", icon:"🎓", status:"Ulanmagan"},
  {name:"Payme", icon:"💳", status:"Ulandi"},
  {name:"Click", icon:"💳", status:"Ulanmagan"},
  {name:"1C Buxgalteriya", icon:"📚", status:"Ulanmagan"},
];
function renderIntegrations() {
  document.getElementById('integrationsList').innerHTML = INTEGRATIONS.map(i => `
    <div class="stat-card">
      <div style="font-size:32px">${i.icon}</div>
      <div class="label" style="margin-top:8px">${i.name}</div>
      <div>${i.status==='Ulandi'?'<span class="badge badge-active">Ulandi</span>':'<span class="badge badge-inactive">Ulanmagan</span>'}</div>
      <button class="btn btn-sm" style="margin-top:10px" onclick="toggleIntegration('${i.name}')">
        ${i.status==='Ulandi'?'Uzish':'Ulash'}
      </button>
    </div>`).join('');
}
function toggleIntegration(name) {
  const i = INTEGRATIONS.find(x => x.name === name);
  i.status = i.status === 'Ulandi' ? 'Ulanmagan' : 'Ulandi';
  audit('Integratsiya: ' + name + ' → ' + i.status);
  renderIntegrations(); toast("🔌 " + name + ": " + i.status);
}

/* ---- SETTINGS ---- */
function renderSettings() {
  const s = DB.get('settings', {company:"", currency:"UZS", lang:"O'zbek"});
  document.getElementById('setCompany').value = s.company;
  document.getElementById('setCurrency').value = s.currency;
  document.getElementById('setLang').value = s.lang;
}
function saveSettings() {
  DB.set('settings', {company:setCompany.value, currency:setCurrency.value, lang:setLang.value});
  audit('Sozlamalar saqlandi');
  toast("✅ Saqlandi", "#10b981");
}
function resetData() {
  if (!confirm("Hamma ma'lumot o'chirilsinmi?")) return;
  localStorage.clear(); location.reload();
    }
  /* ---- SECURITY ---- */
function renderSecurity() {
  document.getElementById('auditLog').innerHTML = DB.get('audit').slice().reverse().slice(0,30).map(a =>
    `<div style="padding:6px 0;border-bottom:1px solid #f3f4f6">
      <b>${new Date(a.date).toLocaleString()}</b> — ${a.action}
    </div>`).join('');
}

/* ---- DELETE ---- */
function delItem(store, id) {
  if (!confirm("O'chirilsinmi?")) return;
  DB.remove(store, id); audit('O\'chirildi: ' + store + ' #' + id);
  renderAll(); toast("🗑 O'chirildi", "#ef4444");
}

/* Modal yopish */
document.getElementById('modalBg').onclick = e => {
  if (e.target.id === 'modalBg') closeModal();
};

/* Init */
window.addEventListener('DOMContentLoaded', () => {
  if (document.getElementById('loginScreen').style.display === 'none') renderAll();
});
</script>
</body>
</html>
```
