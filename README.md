<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>VereinManager – VS Canucks & Mighty Ducks</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: 'Segoe UI', system-ui, sans-serif; background: #f4f5f7; color: #1a1a2e; min-height: 100vh; }

    /* ── Header ── */
    header { background: #1a1a2e; position: sticky; top: 0; z-index: 100; box-shadow: 0 2px 12px rgba(0,0,0,.25); }
    .header-inner { max-width: 1100px; margin: 0 auto; padding: 0 20px; display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 10px; min-height: 64px; }
    .logo { display: flex; align-items: center; gap: 12px; }
    .logo-icon { font-size: 32px; }
    .logo-title { font-size: 20px; font-weight: 800; color: #fff; letter-spacing: -.5px; }
    .logo-title span { color: #e85d04; }
    .logo-sub { font-size: 11px; color: #aaa; margin-top: -2px; }
    nav { display: flex; gap: 4px; flex-wrap: wrap; padding: 8px 0; }
    nav button { background: transparent; border: none; color: #bbb; padding: 8px 14px; border-radius: 8px; cursor: pointer; font-size: 14px; font-weight: 500; transition: all .15s; }
    nav button.active { background: #e85d04; color: #fff; }

    /* ── Main ── */
    main { max-width: 1100px; margin: 0 auto; padding: 28px 20px 80px; }
    .page-title { font-size: 26px; font-weight: 800; margin-bottom: 20px; }
    .page-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 20px; flex-wrap: wrap; gap: 10px; }
    .section-label { font-size: 12px; font-weight: 700; text-transform: uppercase; letter-spacing: 1px; color: #888; margin: 20px 0 8px; }
    .empty-page { text-align: center; color: #aaa; padding: 60px 20px; font-size: 16px; }
    .empty { color: #bbb; font-size: 14px; padding: 12px 0; }

    /* ── Buttons ── */
    .btn-primary { background: #e85d04; color: #fff; border: none; padding: 10px 20px; border-radius: 8px; cursor: pointer; font-weight: 700; font-size: 14px; }
    .btn-secondary { background: #f4f5f7; color: #333; border: none; padding: 7px 14px; border-radius: 8px; cursor: pointer; font-size: 13px; font-weight: 500; }
    .btn-danger { background: #f4f5f7; color: #c0392b; border: none; padding: 7px 14px; border-radius: 8px; cursor: pointer; font-size: 13px; font-weight: 500; }
    .pay-toggle { color: #fff; border: none; padding: 5px 14px; border-radius: 20px; cursor: pointer; font-weight: 700; font-size: 13px; }
    .pay-toggle.paid { background: #2d6a4f; }
    .pay-toggle.unpaid { background: #e85d04; }

    /* ── Cards ── */
    .card { background: #fff; border-radius: 12px; padding: 20px 22px; box-shadow: 0 1px 4px rgba(0,0,0,.07); margin-bottom: 16px; }
    .card-title { font-weight: 700; font-size: 15px; margin-bottom: 14px; }

    /* ── Stat Grid ── */
    .stat-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 16px; margin-bottom: 28px; }
    .stat-card { background: #fff; border-radius: 12px; padding: 20px 22px; display: flex; gap: 16px; align-items: center; box-shadow: 0 1px 4px rgba(0,0,0,.07); }
    .stat-icon { font-size: 28px; }
    .stat-value { font-size: 26px; font-weight: 800; }
    .stat-label { font-size: 13px; color: #888; margin-top: 2px; }
    .two-col { display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 20px; }

    /* ── List rows ── */
    .list-row { display: flex; align-items: center; gap: 12px; padding: 8px 0; border-bottom: 1px solid #f0f0f0; }
    .list-main { font-weight: 600; font-size: 14px; }
    .list-sub { font-size: 12px; color: #888; }
    .team-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; display: inline-block; }
    .badge { margin-left: auto; background: #eef2ff; color: #3730a3; padding: 3px 10px; border-radius: 20px; font-size: 12px; font-weight: 600; white-space: nowrap; }
    .badge-warn { background: #fff3e0; color: #e85d04; }

    /* ── Session Cards ── */
    .session-card { background: #fff; border-radius: 12px; display: flex; overflow: hidden; box-shadow: 0 1px 4px rgba(0,0,0,.07); margin-bottom: 12px; }
    .session-stripe { width: 6px; flex-shrink: 0; }
    .session-body { flex: 1; padding: 16px 18px; }
    .session-top { display: flex; justify-content: space-between; align-items: flex-start; flex-wrap: wrap; gap: 10px; }
    .session-team { font-weight: 700; font-size: 15px; }
    .session-date { font-size: 13px; color: #555; margin-top: 2px; }
    .session-note { font-size: 12px; color: #888; margin-top: 2px; }
    .session-meta { display: flex; gap: 8px; flex-wrap: wrap; align-items: center; }
    .session-actions { display: flex; gap: 10px; margin-top: 12px; }

    /* ── Members ── */
    .member-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 12px; }
    .member-card { background: #fff; border-radius: 10px; padding: 16px 14px; box-shadow: 0 1px 4px rgba(0,0,0,.07); position: relative; text-align: center; }
    .member-avatar { width: 46px; height: 46px; border-radius: 50%; color: #fff; font-weight: 800; font-size: 20px; display: flex; align-items: center; justify-content: center; margin: 0 auto 10px; }
    .member-name { font-weight: 600; font-size: 14px; }
    .member-sub { font-size: 12px; color: #888; margin-top: 2px; }
    .delete-btn { position: absolute; top: 8px; right: 8px; background: none; border: none; cursor: pointer; color: #ccc; font-size: 14px; padding: 2px; }

    /* ── Payments ── */
    .pay-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px; flex-wrap: wrap; gap: 8px; }
    .pay-total { font-weight: 700; color: #e85d04; }
    .pay-row { display: flex; align-items: center; gap: 10px; padding: 8px 0; border-bottom: 1px solid #f0f0f0; }
    .pay-name { font-weight: 600; font-size: 14px; flex: 1; }
    .pay-from { font-size: 12px; color: #888; }
    .guest-tag { font-size: 11px; background: #fff3e0; color: #e85d04; padding: 2px 8px; border-radius: 10px; font-weight: 700; }

    /* ── Modal ── */
    .overlay { position: fixed; inset: 0; background: rgba(0,0,0,.45); z-index: 200; display: flex; align-items: center; justify-content: center; padding: 20px; }
    .modal { background: #fff; border-radius: 16px; width: 100%; max-width: 480px; max-height: 90vh; overflow-y: auto; box-shadow: 0 20px 60px rgba(0,0,0,.25); }
    .modal-header { display: flex; justify-content: space-between; align-items: center; padding: 20px 24px 0; position: sticky; top: 0; background: #fff; z-index: 1; }
    .modal-title { font-weight: 800; font-size: 17px; }
    .modal-sub { font-size: 13px; color: #888; padding: 4px 24px 8px; }
    .close-btn { background: none; border: none; font-size: 18px; cursor: pointer; color: #888; padding: 4px; }
    .modal-body { padding: 16px 24px 24px; }
    label.field { display: block; font-size: 12px; font-weight: 700; color: #555; margin-bottom: 4px; margin-top: 12px; }
    input.field, select.field { width: 100%; padding: 10px 12px; border: 1.5px solid #e0e0e0; border-radius: 8px; font-size: 14px; margin-bottom: 4px; font-family: inherit; outline: none; }
    .attend-label { font-weight: 700; font-size: 13px; margin: 14px 0 8px; }
    .attend-row { display: flex; align-items: center; gap: 10px; padding: 8px 0; border-bottom: 1px solid #f0f0f0; }
    .attend-name { flex: 1; font-size: 14px; font-weight: 500; }
    .attend-cb { width: 18px; height: 18px; cursor: pointer; accent-color: #e85d04; }
    .time-row { display: flex; gap: 10px; }
    .time-row > div { flex: 1; }

    /* ── Loading ── */
    #loading { display: flex; align-items: center; justify-content: center; height: 100vh; font-size: 18px; color: #888; gap: 12px; }
    #setup-hint { display: none; background: #fff3e0; border: 2px solid #e85d04; border-radius: 12px; padding: 24px; max-width: 600px; margin: 40px auto; }
    #setup-hint h2 { color: #e85d04; margin-bottom: 12px; }
    #setup-hint code { background: #f0f0f0; padding: 2px 6px; border-radius: 4px; font-size: 13px; }
    #app { display: none; }
  </style>
</head>
<body>

<div id="loading">⏳ Verbinde mit Datenbank…</div>

<div id="setup-hint">
  <h2>⚙️ Firebase noch nicht konfiguriert</h2>
  <p>Bitte trage deine Firebase-Zugangsdaten in der Datei ein (Zeile mit <code>FIREBASE_CONFIG</code>).<br>
  Die vollständige Anleitung findest du in der <strong>ANLEITUNG.md</strong> Datei.</p>
</div>

<div id="app">
  <header>
    <div class="header-inner">
      <div class="logo">
        <span class="logo-icon">⚽</span>
        <div>
          <div class="logo-title">Vereins<span>Manager</span></div>
          <div class="logo-sub">VS Canucks &amp; Mighty Ducks</div>
        </div>
      </div>
      <nav>
        <button class="active" onclick="showTab('dashboard')">📊 Übersicht</button>
        <button onclick="showTab('sessions')">📅 Trainings</button>
        <button onclick="showTab('members')">👥 Mitglieder</button>
        <button onclick="showTab('payments')">💶 Zahlungen</button>
      </nav>
    </div>
  </header>
  <main id="main-content"></main>
</div>

<!-- Firebase SDKs -->
<script type="module">
// ══════════════════════════════════════════════════════════════
//  🔧 HIER DEINE FIREBASE-ZUGANGSDATEN EINTRAGEN
//  (Anleitung: siehe ANLEITUNG.md)
// ══════════════════════════════════════════════════════════════
const FIREBASE_CONFIG = {
  apiKey:  "AIzaSyBlBS0oQ73_Tm1K4QMIthgHwk5sLGeEZpQ",
  authDomain:  "vereinsmanager-canucks.firebaseapp.com",
  databaseURL: "https://vereinsmanager-canucks-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "vereinsmanager-canucks",
  storageBucket: "vereinsmanager-canucks.firebasestorage.app",
  messagingSenderId: "971472721142",
  appId: "1:971472721142:web:18e57be329ae485233c8d7"
};
// ══════════════════════════════════════════════════════════════

import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
import { getDatabase, ref, onValue, set, update, remove } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-database.js";

// Check if config is filled in
const isConfigured = FIREBASE_CONFIG.apiKey !== "DEIN_API_KEY";

if (!isConfigured) {
  document.getElementById('loading').style.display = 'none';
  document.getElementById('setup-hint').style.display = 'block';
} else {
  const app = initializeApp(FIREBASE_CONFIG);
  const db = getDatabase(app);

  // ── State ─────────────────────────────────────────────────
  const TEAMS = [
    { id: "t1", name: "VS Canucks",   color: "#e85d04" },
    { id: "t2", name: "Mighty Ducks", color: "#0077b6" },
  ];

  let state = { members: {}, sessions: {}, payments: {} };
  let currentTab = "dashboard";
  let activeSessionId = null;

  // ── Firebase helpers ──────────────────────────────────────
  const dbRef = (path) => ref(db, path);
  const uid = () => Math.random().toString(36).slice(2, 10);

  // ── Realtime listeners ────────────────────────────────────
  onValue(dbRef("members"),  snap => { state.members  = snap.val() || {}; render(); });
  onValue(dbRef("sessions"), snap => { state.sessions = snap.val() || {}; render(); });
  onValue(dbRef("payments"), snap => { state.payments = snap.val() || {}; render(); });

  document.getElementById('loading').style.display = 'none';
  document.getElementById('app').style.display = 'block';

  // ── Helpers ───────────────────────────────────────────────
  const fmt = d => new Date(d + "T12:00:00").toLocaleDateString("de-DE", { weekday:"short", day:"2-digit", month:"2-digit", year:"numeric" });
  const teamColor = id => TEAMS.find(t => t.id === id)?.color ?? "#888";
  const teamName  = id => TEAMS.find(t => t.id === id)?.name ?? "–";
  const members   = () => Object.values(state.members);
  const sessions  = () => Object.values(state.sessions);
  const needsPay  = (sess, mid) => state.members[mid] && state.members[mid].teamId !== sess.teamId;
  const isPaid    = (sessId, mid) => !!(state.payments[sessId] && state.payments[sessId][mid]);

  // ── Actions ───────────────────────────────────────────────
  window.showTab = (tab) => { currentTab = tab; activeSessionId = null; render(); };

  window.addMember = () => {
    const name   = document.getElementById('m-name').value.trim();
    const number = document.getElementById('m-number').value.trim();
    const teamId = document.getElementById('m-team').value;
    if (!name) return;
    const id = uid();
    set(dbRef(`members/${id}`), { id, name, number, teamId });
    closeModal();
  };

  window.deleteMember = (id) => { if (confirm("Mitglied wirklich löschen?")) remove(dbRef(`members/${id}`)); };

  window.addSession = () => {
    const teamId    = document.getElementById('s-team').value;
    const date      = document.getElementById('s-date').value;
    const startTime = document.getElementById('s-start').value;
    const endTime   = document.getElementById('s-end').value;
    const note      = document.getElementById('s-note').value.trim();
    if (!date || !startTime) return;
    const id = uid();
    set(dbRef(`sessions/${id}`), { id, teamId, date, startTime, endTime, note, attendees: {} });
    closeModal();
  };

  window.deleteSession = (id) => { if (confirm("Training wirklich löschen?")) remove(dbRef(`sessions/${id}`)); };

  window.openSession = (id) => { activeSessionId = id; renderAttendance(); };

  window.toggleAttend = (sessId, membId) => {
    const sess = state.sessions[sessId];
    if (!sess) return;
    const currently = sess.attendees && sess.attendees[membId];
    if (currently) {
      update(dbRef(`sessions/${sessId}/attendees`), { [membId]: null });
      // also clear payment
      if (state.payments[sessId]) update(dbRef(`payments/${sessId}`), { [membId]: null });
    } else {
      update(dbRef(`sessions/${sessId}/attendees`), { [membId]: true });
    }
  };

  window.togglePaid = (sessId, membId) => {
    const paid = isPaid(sessId, membId);
    update(dbRef(`payments/${sessId}`), { [membId]: !paid });
  };

  window.closeModal = () => {
    const m = document.getElementById('modal');
    if (m) m.remove();
  };

  window.showAddMember = () => {
    const opts = TEAMS.map(t => `<option value="${t.id}">${t.name}</option>`).join('');
    showModal("Mitglied hinzufügen", `
      <label class="field">Name *</label>
      <input class="field" id="m-name" placeholder="Vorname Nachname" />
      <label class="field">Trikotnummer</label>
      <input class="field" id="m-number" placeholder="z.B. 10" type="number" />
      <label class="field">Gemeldet bei</label>
      <select class="field" id="m-team">${opts}</select>
      <br><br>
      <button class="btn-primary" onclick="addMember()">Hinzufügen</button>
    `);
  };

  window.showAddSession = () => {
    const opts = TEAMS.map(t => `<option value="${t.id}">${t.name}</option>`).join('');
    const today = new Date().toISOString().slice(0,10);
    showModal("Training hinzufügen", `
      <label class="field">Mannschaft *</label>
      <select class="field" id="s-team">${opts}</select>
      <label class="field">Datum *</label>
      <input class="field" id="s-date" type="date" value="${today}" />
      <div class="time-row">
        <div><label class="field">Beginn *</label><input class="field" id="s-start" type="time" /></div>
        <div><label class="field">Ende</label><input class="field" id="s-end" type="time" /></div>
      </div>
      <label class="field">Notiz</label>
      <input class="field" id="s-note" placeholder="z.B. Halle B" />
      <br><br>
      <button class="btn-primary" onclick="addSession()">Hinzufügen</button>
    `);
  };

  // ── Modal ─────────────────────────────────────────────────
  function showModal(title, body) {
    const existing = document.getElementById('modal');
    if (existing) existing.remove();
    const el = document.createElement('div');
    el.id = 'modal';
    el.className = 'overlay';
    el.innerHTML = `
      <div class="modal">
        <div class="modal-header">
          <div class="modal-title">${title}</div>
          <button class="close-btn" onclick="closeModal()">✕</button>
        </div>
        <div class="modal-body">${body}</div>
      </div>`;
    el.addEventListener('click', e => { if (e.target === el) closeModal(); });
    document.body.appendChild(el);
  }

  // ── Render Attendance Modal ───────────────────────────────
  function renderAttendance() {
    const sess = state.sessions[activeSessionId];
    if (!sess) return;
    const ms = members().sort((a,b) => a.name.localeCompare(b.name));
    const attendees = sess.attendees || {};
    const openAmt = ms.filter(m => attendees[m.id] && needsPay(sess, m.id) && !isPaid(activeSessionId, m.id)).length * 5;
    const rows = ms.map(m => {
      const present = !!attendees[m.id];
      const guest   = needsPay(sess, m.id);
      const paid    = isPaid(activeSessionId, m.id);
      return `
        <div class="attend-row">
          <input class="attend-cb" type="checkbox" ${present ? 'checked' : ''} onchange="toggleAttend('${activeSessionId}','${m.id}')" />
          <span class="team-dot" style="background:${teamColor(m.teamId)}"></span>
          <span class="attend-name">${m.name}</span>
          ${guest ? '<span class="guest-tag">Gast</span>' : ''}
          ${present && guest ? `<button class="pay-toggle ${paid ? 'paid' : 'unpaid'}" onclick="togglePaid('${activeSessionId}','${m.id}')">${paid ? '✓ 5 € bezahlt' : '⏳ 5 € offen'}</button>` : ''}
        </div>`;
    }).join('');

    showModal(
      `Training: ${teamName(sess.teamId)} – ${fmt(sess.date)}`,
      `<div class="modal-sub">${sess.startTime}${sess.endTime ? ' – ' + sess.endTime : ''}${sess.note ? ' · ' + sess.note : ''}</div>
       <div class="attend-label">Anwesenheit eintragen:</div>
       ${rows}
       <div style="margin-top:12px;font-size:13px;color:#888;">
         ${Object.keys(attendees).filter(k=>attendees[k]).length} Anwesende · Gastgebühren offen: ${openAmt} €
       </div>`
    );
  }

  // ── Main Render ───────────────────────────────────────────
  function render() {
    // update active attendance modal if open
    if (activeSessionId) { renderAttendance(); }

    // update nav
    document.querySelectorAll('nav button').forEach((b,i) => {
      const tabs = ['dashboard','sessions','members','payments'];
      b.classList.toggle('active', tabs[i] === currentTab);
    });

    const el = document.getElementById('main-content');

    if (currentTab === 'dashboard')  el.innerHTML = renderDashboard();
    if (currentTab === 'sessions')   el.innerHTML = renderSessions();
    if (currentTab === 'members')    el.innerHTML = renderMembers();
    if (currentTab === 'payments')   el.innerHTML = renderPayments();
  }

  // ── Dashboard ─────────────────────────────────────────────
  function renderDashboard() {
    const ms = members(), ss = sessions();
    const openAmt = ss.reduce((sum, s) => sum + Object.keys(s.attendees||{}).filter(mid => s.attendees[mid] && needsPay(s,mid) && !isPaid(s.id,mid)).length * 5, 0);
    const paidAmt = ss.reduce((sum, s) => sum + Object.keys(s.attendees||{}).filter(mid => s.attendees[mid] && needsPay(s,mid) &&  isPaid(s.id,mid)).length * 5, 0);
    const today = new Date().toISOString().slice(0,10);
    const upcoming = ss.filter(s => s.date >= today).sort((a,b) => a.date.localeCompare(b.date)).slice(0,5);

    const upcomingHtml = upcoming.length ? upcoming.map(s => {
      const cnt = Object.values(s.attendees||{}).filter(Boolean).length;
      return `<div class="list-row">
        <span class="team-dot" style="background:${teamColor(s.teamId)}"></span>
        <div><div class="list-main">${teamName(s.teamId)}</div>
             <div class="list-sub">${fmt(s.date)} · ${s.startTime}${s.endTime?' – '+s.endTime:''}</div></div>
        <span class="badge">${cnt} anwesend</span>
      </div>`;
    }).join('') : '<div class="empty">Keine bevorstehenden Trainings</div>';

    const openList = ss.flatMap(s =>
      Object.keys(s.attendees||{}).filter(mid => s.attendees[mid] && needsPay(s,mid) && !isPaid(s.id,mid))
        .map(mid => ({ s, m: state.members[mid] }))
    ).slice(0,6);

    const openHtml = openList.length ? openList.map(({s,m}) => `
      <div class="list-row">
        <span class="team-dot" style="background:#e85d04"></span>
        <div><div class="list-main">${m?.name}</div>
             <div class="list-sub">${fmt(s.date)} bei ${teamName(s.teamId)}</div></div>
        <span class="badge badge-warn">5 €</span>
      </div>`) .join('') : '<div class="empty">Alle Zahlungen eingegangen ✅</div>';

    return `
      <h2 class="page-title">Übersicht</h2>
      <div class="stat-grid">
        ${statCard("👥","Mitglieder", ms.length, "#0077b6")}
        ${statCard("📅","Trainings gesamt", ss.length, "#7b2d8b")}
        ${statCard("✅","Eingegangen (€)", paidAmt+" €", "#2d6a4f")}
        ${statCard("⏳","Ausstehend (€)", openAmt+" €", "#e85d04")}
      </div>
      <div class="two-col">
        <div class="card"><div class="card-title">📅 Nächste Trainings</div>${upcomingHtml}</div>
        <div class="card"><div class="card-title">⚠️ Offene Zahlungen</div>${openHtml}</div>
      </div>`;
  }

  function statCard(icon, label, value, color) {
    return `<div class="stat-card" style="border-left:4px solid ${color}">
      <div class="stat-icon">${icon}</div>
      <div><div class="stat-value" style="color:${color}">${value}</div>
           <div class="stat-label">${label}</div></div>
    </div>`;
  }

  // ── Sessions ──────────────────────────────────────────────
  function renderSessions() {
    const today = new Date().toISOString().slice(0,10);
    const ss = sessions();
    const upcoming = ss.filter(s => s.date >= today).sort((a,b) => a.date.localeCompare(b.date));
    const past     = ss.filter(s => s.date <  today).sort((a,b) => b.date.localeCompare(a.date));

    const card = s => {
      const cnt    = Object.values(s.attendees||{}).filter(Boolean).length;
      const guests = Object.keys(s.attendees||{}).filter(mid => s.attendees[mid] && needsPay(s,mid));
      const unpaid = guests.filter(mid => !isPaid(s.id, mid));
      return `<div class="session-card">
        <div class="session-stripe" style="background:${teamColor(s.teamId)}"></div>
        <div class="session-body">
          <div class="session-top">
            <div>
              <div class="session-team">${teamName(s.teamId)}</div>
              <div class="session-date">${fmt(s.date)} · ${s.startTime}${s.endTime?' – '+s.endTime:''}</div>
              ${s.note ? `<div class="session-note">${s.note}</div>` : ''}
            </div>
            <div class="session-meta">
              <span class="badge">${cnt} anwesend</span>
              ${unpaid.length ? `<span class="badge badge-warn">${unpaid.length*5} € offen</span>` : ''}
            </div>
          </div>
          <div class="session-actions">
            <button class="btn-secondary" onclick="openSession('${s.id}')">📋 Anwesenheit</button>
            <button class="btn-danger" onclick="deleteSession('${s.id}')">🗑 Löschen</button>
          </div>
        </div>
      </div>`;
    };

    return `
      <div class="page-header">
        <h2 class="page-title">Trainings</h2>
        <button class="btn-primary" onclick="showAddSession()">+ Training hinzufügen</button>
      </div>
      ${upcoming.length ? '<div class="section-label">Bevorstehend</div>' : ''}
      ${upcoming.map(card).join('')}
      ${past.length ? '<div class="section-label">Vergangen</div>' : ''}
      ${past.map(card).join('')}
      ${ss.length === 0 ? '<div class="empty-page">Noch keine Trainings. Klicke auf „+ Training hinzufügen".</div>' : ''}`;
  }

  // ── Members ───────────────────────────────────────────────
  function renderMembers() {
    return `
      <div class="page-header">
        <h2 class="page-title">Mitglieder</h2>
        <button class="btn-primary" onclick="showAddMember()">+ Mitglied hinzufügen</button>
      </div>
      ${TEAMS.map(team => {
        const tm = members().filter(m => m.teamId === team.id);
        return `
          <div style="margin-bottom:28px">
            <div class="section-label" style="color:${team.color}">● ${team.name} (${tm.length})</div>
            ${tm.length === 0 ? '<div class="empty">Keine Mitglieder</div>' : ''}
            <div class="member-grid">
              ${tm.map(m => `
                <div class="member-card" style="border-top:3px solid ${team.color}">
                  <div class="member-avatar" style="background:${team.color}">${m.name[0].toUpperCase()}</div>
                  <div class="member-name">${m.name}</div>
                  ${m.number ? `<div class="member-sub">#${m.number}</div>` : ''}
                  <button class="delete-btn" onclick="deleteMember('${m.id}')">✕</button>
                </div>`).join('')}
            </div>
          </div>`;
      }).join('')}`;
  }

  // ── Payments ──────────────────────────────────────────────
  function renderPayments() {
    const ss = sessions().filter(s => {
      const guests = Object.keys(s.attendees||{}).filter(mid => s.attendees[mid] && needsPay(s,mid));
      return guests.length > 0;
    }).sort((a,b) => b.date.localeCompare(a.date));

    if (ss.length === 0) return '<h2 class="page-title">Zahlungen</h2><div class="empty-page">Noch keine Gasttrainings eingetragen.</div>';

    return `<h2 class="page-title">Zahlungsübersicht (5 € / Gasttraining)</h2>` +
      ss.map(s => {
        const guests = Object.keys(s.attendees||{}).filter(mid => s.attendees[mid] && needsPay(s,mid));
        return `<div class="card">
          <div class="pay-header">
            <div><span class="team-dot" style="background:${teamColor(s.teamId)}"></span>
              <strong>${teamName(s.teamId)}</strong> · ${fmt(s.date)} ${s.startTime}
            </div>
            <div class="pay-total">Gesamt: ${guests.length*5} €</div>
          </div>
          ${guests.map(mid => {
            const m = state.members[mid];
            const paid = isPaid(s.id, mid);
            return `<div class="pay-row">
              <span class="team-dot" style="background:${teamColor(m?.teamId)}"></span>
              <div class="pay-name">${m?.name}</div>
              <div class="pay-from">aus ${teamName(m?.teamId)}</div>
              <button class="pay-toggle ${paid?'paid':'unpaid'}" onclick="togglePaid('${s.id}','${mid}')">
                ${paid ? '✓ Bezahlt' : '⏳ Offen'}
              </button>
            </div>`;
          }).join('')}
        </div>`;
      }).join('');
  }

  // initial render
  render();
}
</script>
</body>
</html>
