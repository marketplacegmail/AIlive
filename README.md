
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>AI Đọc Tiếng Việt – iBasic</title>
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
:root {
  --purple: #7F77DD; --purple-light: #EEEDFE; --purple-dark: #3C3489;
  --teal: #1D9E75; --teal-light: #E1F5EE;
  --coral: #D85A30; --coral-light: #FAECE7;
  --amber-light: #FAEEDA; --amber-dark: #854F0B;
  --gray-50: #F1EFE8; --gray-100: #D3D1C7; --gray-200: #B4B2A9;
  --gray-600: #5F5E5A; --gray-800: #444441;
  --bg: #ffffff; --bg2: #f8f7f5;
  --border: rgba(0,0,0,0.09);
  --text: #1a1a18; --text2: #5F5E5A;
  --radius: 10px; --shadow: 0 1px 4px rgba(0,0,0,0.07);
}
body {
  font-family: 'Segoe UI', -apple-system, system-ui, sans-serif;
  background: var(--gray-50); min-height: 100vh;
  padding: 24px 16px; color: var(--text); font-size: 14px; line-height: 1.5;
}
.app { max-width: 780px; margin: 0 auto; }
.header { text-align: center; margin-bottom: 24px; }
.header h1 { font-size: 22px; font-weight: 600; letter-spacing: -0.3px; }
.header p { color: var(--text2); font-size: 12px; margin-top: 4px; }

/* TABS */
.tabs { display:flex; background:var(--bg); border:1px solid var(--border); border-radius:var(--radius); padding:4px; margin-bottom:18px; gap:4px; }
.tab { flex:1; padding:9px 12px; border:none; background:transparent; border-radius:8px; font-size:13px; font-weight:500; color:var(--text2); cursor:pointer; transition:all .15s; }
.tab.active { background:var(--purple); color:#fff; }
.tab:not(.active):hover { background:var(--gray-50); }
.panel { display:none; }
.panel.active { display:block; }

/* CARD */
.card { background:var(--bg); border:1px solid var(--border); border-radius:var(--radius); padding:20px; margin-bottom:14px; box-shadow:var(--shadow); }
.card-title { font-size:11px; font-weight:600; color:var(--text2); text-transform:uppercase; letter-spacing:.6px; margin-bottom:12px; }

/* INPUTS */
input[type="text"], input[type="password"], select, textarea {
  width:100%; padding:10px 12px; border:1px solid var(--border); border-radius:8px;
  font-size:14px; font-family:inherit; color:var(--text); background:var(--bg); outline:none; transition:border-color .15s;
}
input:focus, textarea:focus, select:focus { border-color:var(--purple); box-shadow:0 0 0 3px rgba(127,119,221,.1); }
textarea { min-height:130px; resize:vertical; line-height:1.6; }
.row { display:flex; gap:8px; }
.row input, .row select { flex:1; }

/* BUTTONS */
.btn { padding:9px 16px; border-radius:8px; font-size:13px; font-weight:600; cursor:pointer; border:1px solid transparent; transition:all .15s; white-space:nowrap; display:inline-flex; align-items:center; gap:5px; }
.btn-p { background:var(--purple); color:#fff; }
.btn-p:hover { background:var(--purple-dark); }
.btn-p:disabled { opacity:.4; cursor:not-allowed; }
.btn-s { background:var(--bg); color:var(--text); border-color:var(--border); }
.btn-s:hover { background:var(--gray-50); }
.btn-d { background:var(--coral-light); color:var(--coral); border-color:rgba(216,90,48,.2); }
.btn-d:hover { background:#f5c4b3; }
.btn-xl { padding:13px 24px; font-size:15px; border-radius:10px; width:100%; justify-content:center; margin-top:4px; }

/* BADGE */
.badge { display:inline-flex; align-items:center; gap:4px; padding:3px 10px; border-radius:20px; font-size:12px; font-weight:500; }
.b-ok { background:var(--teal-light); color:var(--teal); }
.b-err { background:var(--coral-light); color:var(--coral); }
.b-warn { background:var(--amber-light); color:var(--amber-dark); }
.b-info { background:var(--purple-light); color:var(--purple-dark); }

/* SLIDERS */
.sl-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(165px,1fr)); gap:10px; margin-top:12px; }
.sl label { display:flex; justify-content:space-between; font-size:12px; color:var(--text2); margin-bottom:4px; }
.sl label b { color:var(--purple); }
input[type="range"] { width:100%; accent-color:var(--purple); height:4px; padding:0; border:none; box-shadow:none; outline:none; }
.sl-hint { font-size:11px; color:var(--gray-200); margin-top:2px; }

/* UPLOAD */
.uz { border:2px dashed var(--border); border-radius:8px; padding:20px; text-align:center; cursor:pointer; transition:all .15s; color:var(--text2); }
.uz:hover,.uz.over { border-color:var(--purple); background:var(--purple-light); }
.uz .ico { font-size:26px; margin-bottom:4px; }
.uz small { font-size:11px; color:var(--gray-200); display:block; margin-top:3px; }

/* AUDIO PREVIEW */
.aprv { display:none; background:var(--bg2); border:1px solid var(--border); border-radius:8px; padding:10px 12px; margin-top:10px; }
.aprv.show { display:block; }
.aprv .frow { display:flex; justify-content:space-between; align-items:center; margin-bottom:6px; font-size:12px; color:var(--text2); }
audio { width:100%; height:34px; }

/* CLONED */
.cbox { display:none; background:var(--teal-light); border:1px solid rgba(29,158,117,.25); border-radius:8px; padding:10px 14px; margin-top:10px; flex-direction:row; justify-content:space-between; align-items:center; font-size:13px; color:#085041; }
.cbox.show { display:flex; }

/* RECORDER */
.rec-row { display:flex; align-items:center; gap:8px; margin-top:8px; flex-wrap:wrap; }
.timer { font-family:monospace; font-size:13px; font-weight:700; padding:5px 10px; background:var(--bg2); border:1px solid var(--border); border-radius:6px; }
.timer.rec { color:#A32D2D; border-color:#F7C1C1; background:#FCEBEB; }

/* PROGRESS */
.prog { display:none; text-align:center; padding:14px; color:var(--text2); font-size:13px; gap:8px; align-items:center; justify-content:center; }
.prog.show { display:flex; }
.spin { width:16px; height:16px; border:2px solid var(--border); border-top-color:var(--purple); border-radius:50%; animation:spin .7s linear infinite; flex-shrink:0; }
@keyframes spin { to { transform:rotate(360deg); } }

/* OUTPUT */
.out-card { display:none; background:var(--bg); border:1px solid var(--border); border-radius:var(--radius); padding:18px; margin-top:10px; box-shadow:var(--shadow); }
.out-card.show { display:block; }
.out-label { font-size:13px; font-weight:600; margin-bottom:8px; }
.out-actions { display:flex; gap:8px; margin-top:10px; flex-wrap:wrap; }

/* ALERT */
.al { padding:10px 14px; border-radius:8px; font-size:13px; line-height:1.6; }
.al-info { background:var(--purple-light); color:var(--purple-dark); border:1px solid rgba(127,119,221,.2); }
.al-warn { background:var(--amber-light); color:var(--amber-dark); border:1px solid rgba(239,159,39,.3); }
.al-err  { background:var(--coral-light); color:#4A1B0C; border:1px solid rgba(216,90,48,.25); }
.al-ok   { background:var(--teal-light); color:#085041; border:1px solid rgba(29,158,117,.25); }
.mt8 { margin-top:8px; }
.mt12 { margin-top:12px; }

/* TOAST */
.toast { position:fixed; bottom:20px; right:20px; background:var(--gray-800); color:#fff; padding:10px 16px; border-radius:8px; font-size:13px; z-index:9999; opacity:0; transform:translateY(8px); transition:all .25s; max-width:320px; pointer-events:none; }
.toast.show { opacity:1; transform:none; }
.toast.ok { background:#0F6E56; }
.toast.err { background:#A32D2D; }

/* MISC */
.divider { display:flex; align-items:center; gap:8px; margin:12px 0; color:var(--gray-200); font-size:11px; text-transform:uppercase; }
.divider::before,.divider::after { content:''; flex:1; height:1px; background:var(--border); }
.char-stats { display:flex; justify-content:space-between; font-size:11px; color:var(--gray-200); margin-top:4px; }
details { border:1px solid var(--border); border-radius:8px; padding:8px 12px; margin-top:8px; }
details summary { font-size:12px; font-weight:600; cursor:pointer; color:var(--text2); user-select:none; }
details summary:hover { color:var(--purple); }
details .di { margin-top:8px; font-size:12px; color:var(--text2); line-height:1.7; }
details a { color:var(--purple); }
code { background:var(--gray-50); padding:1px 5px; border-radius:4px; font-family:monospace; font-size:12px; }
</style>
</head>
<body>
<div class="app">
  <div class="header">
    <h1>🎙️ AI Đọc Tiếng Việt</h1>
    <p>Web Speech (miễn phí, chạy ngay) · ElevenLabs Voice Clone (API key)</p>
  </div>

  <div class="tabs">
    <button class="tab active" onclick="switchTab(0)">🔊 Web Speech — Miễn phí</button>
    <button class="tab" onclick="switchTab(1)">✨ ElevenLabs — Clone giọng</button>
  </div>

  <!-- ======= TAB 1: WEB SPEECH ======= -->
  <div class="panel active" id="tab0">
    <div class="card">
      <div class="card-title">Chọn giọng đọc</div>
      <div id="wsStatus"><div class="al al-warn">⏳ Đang tải danh sách giọng...</div></div>
      <div class="mt12">
        <select id="voiceSel"></select>
        <div id="vInfo" style="font-size:12px;color:var(--text2);margin-top:6px;display:none;"></div>
      </div>
      <div class="sl-grid mt12">
        <div class="sl">
          <label>Tốc độ <b id="rV">1.0×</b></label>
          <input type="range" id="wsRate" min="0.5" max="2" step="0.1" value="1.0" />
          <div class="sl-hint">0.5× chậm → 2× nhanh</div>
        </div>
        <div class="sl">
          <label>Cao độ <b id="pV">1.0</b></label>
          <input type="range" id="wsPitch" min="0.5" max="2" step="0.1" value="1.0" />
          <div class="sl-hint">0.5 trầm → 2 cao</div>
        </div>
        <div class="sl">
          <label>Âm lượng <b id="vV">100%</b></label>
          <input type="range" id="wsVol" min="0" max="1" step="0.05" value="1" />
          <div class="sl-hint">0% → 100%</div>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-title">Văn bản</div>
      <textarea id="wsText">Xin chào, đây là iBasic Việt Nam – thương hiệu nội y và đồ mặc nhà hàng đầu dành cho cả gia đình. Chúng tôi mang đến sự thoải mái từ những điều nhỏ nhất để bạn lo được chuyện lớn hơn.</textarea>
      <div class="char-stats"><span id="wsCC">0 ký tự</span><span>Không giới hạn (Web Speech)</span></div>
    </div>

    <button class="btn btn-p btn-xl" id="wsBtn" onclick="wsSpeakStop()">▶ Đọc ngay</button>

    <div class="prog" id="wsProg">
      <div class="spin"></div><span id="wsProgTxt">Đang đọc...</span>
    </div>

    <div class="al al-info mt12">
      <b>Lưu ý:</b> Web Speech chạy ngay trên trình duyệt, không cần key, không upload audio lên server. Để tải file MP3 và clone giọng thật, dùng tab <b>ElevenLabs</b>.
    </div>

    <details class="mt8">
      <summary>🤔 Không thấy giọng tiếng Việt?</summary>
      <div class="di">
        <b>Windows (Chrome/Edge):</b> Settings → Time &amp; Language → Language → thêm "Tiếng Việt" → cài Text-to-Speech<br>
        <b>Mac (Chrome):</b> System Settings → Accessibility → Spoken Content → System Voice → Customize → tìm "Vietnamese"<br>
        <b>Android:</b> Cài <i>Google Text-to-Speech</i> từ Play Store<br>
        <b>iOS/Safari:</b> Settings → Accessibility → Spoken Content → Voices → Vietnamese<br>
        → Sau khi cài, <b>tải lại trang</b>.
      </div>
    </details>
  </div>

  <!-- ======= TAB 2: ELEVENLABS ======= -->
  <div class="panel" id="tab1">

    <!-- HƯỚNG DẪN CORS -->
    <div class="al al-warn mt8" id="corsGuide">
      ⚠️ <b>Quan trọng – Cách mở file đúng:</b><br>
      Trình duyệt block API call khi mở file trực tiếp (<code>file://</code>). Phải mở qua local server:<br><br>
      • <b>Cách dễ nhất (VS Code):</b> Cài extension <a href="https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer" target="_blank"><b>Live Server</b></a> → chuột phải file HTML → <i>"Open with Live Server"</i> → URL sẽ là <code>http://127.0.0.1:5500/...</code><br>
      • <b>Không có VS Code:</b> Mở Terminal tại thư mục chứa file → gõ <code>python3 -m http.server 8080</code> → mở <code>http://localhost:8080/vi-tts-app.html</code><br>
      • <b>Hoặc:</b> Tải file lên bất kỳ hosting nào (Netlify Drop, GitHub Pages...)<br><br>
      <span id="originNote" style="font-size:12px;color:var(--amber-dark);"></span>
    </div>

    <!-- API KEY -->
    <div class="card mt12">
      <div class="card-title">API Key · ElevenLabs</div>
      <div class="row">
        <input type="password" id="apiKey" placeholder="sk_... (Dán API key ElevenLabs)" />
        <button class="btn btn-p" onclick="saveKey()">Lưu</button>
        <button class="btn btn-s" id="togBtn" onclick="toggleKey()">Hiện</button>
        <button class="btn btn-d" onclick="clearKey()">Xóa</button>
      </div>
      <div id="kStatus" style="margin-top:8px;"><span class="badge b-err">⚠ Chưa có key</span></div>
      <details class="mt8">
        <summary>Lấy API key miễn phí ở đâu?</summary>
        <div class="di">
          1. Đăng ký tại <a href="https://elevenlabs.io" target="_blank">elevenlabs.io</a> (miễn phí)<br>
          2. Vào <b>Profile → API Keys → Create new key</b><br>
          3. Copy key dạng <code>sk_...</code> và dán vào ô trên<br>
          4. Gói Free: 10.000 ký tự/tháng + Voice Clone miễn phí<br>
          5. Key chỉ lưu trong localStorage trình duyệt của bạn
        </div>
      </details>
    </div>

    <!-- CLONE VOICE -->
    <div class="card">
      <div class="card-title">Mẫu giọng (để clone)</div>

      <label for="vFile">
        <div class="uz" id="uzEl">
          <div class="ico">🎵</div>
          <div><b>Click để upload</b> hoặc kéo thả file vào đây</div>
          <small>MP3, WAV, M4A · Tối đa 10MB · Khuyến nghị 30–60 giây</small>
        </div>
      </label>
      <input type="file" id="vFile" accept="audio/*" style="display:none;" />

      <div class="rec-row">
        <span style="font-size:12px;color:var(--text2);">Hoặc thu trực tiếp:</span>
        <button class="btn btn-s" id="rBtn" onclick="toggleRec()">🎤 Bắt đầu thu</button>
        <span class="timer" id="rTimer">00:00</span>
      </div>

      <div class="aprv" id="aPrv">
        <div class="frow">
          <span id="aLbl">—</span>
          <button class="btn btn-d" style="padding:3px 8px;font-size:11px;" onclick="clearSample()">✖ Xóa</button>
        </div>
        <audio id="aAud" controls></audio>
      </div>

      <div class="row mt12">
        <input type="text" id="vName" value="GiongToi" placeholder="Tên giọng (vd: GiongNhi)" />
        <button class="btn btn-p" id="clBtn" onclick="doClone()" disabled>✨ Clone</button>
      </div>

      <div class="cbox" id="cBox">
        <span>✅ Giọng: <b id="cName">—</b></span>
        <button class="btn btn-d" style="padding:4px 10px;font-size:11px;" onclick="deleteClone()">🗑 Xóa</button>
      </div>

      <div class="divider">hoặc chọn giọng có sẵn</div>
      <div class="row">
        <select id="elVSel"><option value="">— Tải danh sách —</option></select>
        <button class="btn btn-s" onclick="loadVoices()">🔄</button>
      </div>
    </div>

    <!-- TEXT -->
    <div class="card">
      <div class="card-title">Văn bản tiếng Việt</div>
      <textarea id="elText">Xin chào, đây là iBasic Việt Nam – thương hiệu nội y và đồ mặc nhà hàng đầu dành cho cả gia đình. Chúng tôi mang đến sự thoải mái từ những điều nhỏ nhất để bạn lo được chuyện lớn hơn.</textarea>
      <div class="char-stats"><span id="elCC">0 ký tự</span><span>Khuyến nghị ≤5000 ký tự/lần</span></div>
      <div class="sl-grid mt12">
        <div class="sl">
          <label>Độ ổn định <b id="stV">0.50</b></label>
          <input type="range" id="stab" min="0" max="1" step="0.05" value="0.5" />
          <div class="sl-hint">Thấp = cảm xúc · Cao = ổn định</div>
        </div>
        <div class="sl">
          <label>Giống giọng mẫu <b id="smV">0.75</b></label>
          <input type="range" id="sim" min="0" max="1" step="0.05" value="0.75" />
          <div class="sl-hint">Cao = bám sát giọng gốc</div>
        </div>
        <div class="sl">
          <label>Phong cách <b id="syV">0.00</b></label>
          <input type="range" id="sty" min="0" max="1" step="0.05" value="0" />
          <div class="sl-hint">Cao = giàu cảm xúc hơn</div>
        </div>
      </div>
    </div>

    <button class="btn btn-p btn-xl" id="genBtn" onclick="doGenerate()">🔊 Tạo giọng đọc</button>

    <div class="prog" id="elProg">
      <div class="spin"></div><span id="elPT">Đang xử lý...</span>
    </div>

    <div class="out-card" id="elOut">
      <div class="out-label">🎧 Kết quả</div>
      <audio id="outAud" controls></audio>
      <div class="out-actions">
        <button class="btn btn-p" onclick="dlAudio()">⬇ Tải MP3</button>
        <button class="btn btn-s" onclick="doGenerate()">🔄 Tạo lại</button>
      </div>
    </div>

  </div>
</div>

<div class="toast" id="toast"></div>

<script>
/* ── CONFIG ── */
const API = 'https://api.elevenlabs.io/v1';
const MODEL = 'eleven_multilingual_v2';
const SK_KEY = 'el_key_v3';
const SK_CV  = 'el_cv_v3';

/* ── STATE ── */
let sBlob = null, sFName = '';
let mRec = null, rChunks = [], rTimer = null, rStart = 0;
let lastBlob = null;
let isSpeaking = false;
let wsVoices = [];

/* ── DETECT ORIGIN ── */
// Nếu chạy từ file://, cảnh báo sớm
const isFileOrigin = location.protocol === 'file:';
window.addEventListener('DOMContentLoaded', () => {
  const note = document.getElementById('originNote');
  if (isFileOrigin) {
    note.innerHTML = '🔴 Hiện tại bạn đang mở từ <code>file://</code> — ElevenLabs API <b>sẽ bị block</b>. Vui lòng mở qua local server theo hướng dẫn trên.';
  } else {
    note.innerHTML = '🟢 Đang chạy trên <code>' + location.origin + '</code> — API có thể hoạt động.';
    document.getElementById('corsGuide').className = 'al al-ok mt8';
    document.getElementById('corsGuide').innerHTML =
      '✅ <b>Đang chạy trên HTTP server</b> — ElevenLabs API sẵn sàng. Nhập API key và bắt đầu.<br><span style="font-size:12px;">' + location.href + '</span>';
  }

  // Load key
  const k = localStorage.getItem(SK_KEY);
  if (k) { document.getElementById('apiKey').value = k; setKS(true); loadVoices(); }
  const cv = localStorage.getItem(SK_CV);
  if (cv) { const d = JSON.parse(cv); showClone(d.name, d.id); }

  // WS init
  initWS();

  // Sliders
  sl('wsRate','rV', v => v.toFixed(1)+'×');
  sl('wsPitch','pV', v => v.toFixed(1));
  sl('wsVol','vV', v => Math.round(v*100)+'%');
  sl('stab','stV', v => v.toFixed(2));
  sl('sim','smV', v => v.toFixed(2));
  sl('sty','syV', v => v.toFixed(2));

  // Counters
  cc('wsText','wsCC');
  cc('elText','elCC');

  // File upload
  document.getElementById('vFile').addEventListener('change', e => { if (e.target.files[0]) handleF(e.target.files[0]); });
  const uz = document.getElementById('uzEl');
  ['dragenter','dragover'].forEach(ev => uz.addEventListener(ev, e => { e.preventDefault(); uz.classList.add('over'); }));
  ['dragleave','drop'].forEach(ev => uz.addEventListener(ev, e => { e.preventDefault(); uz.classList.remove('over'); }));
  uz.addEventListener('drop', e => { if (e.dataTransfer.files[0]) handleF(e.dataTransfer.files[0]); });
});

/* ── TABS ── */
function switchTab(i) {
  document.querySelectorAll('.panel').forEach((p,j) => p.classList.toggle('active', i===j));
  document.querySelectorAll('.tab').forEach((t,j) => t.classList.toggle('active', i===j));
  if (isSpeaking) stopWS();
}

/* ── WEB SPEECH ── */
function initWS() {
  const stEl = document.getElementById('wsStatus');
  const sel  = document.getElementById('voiceSel');
  if (!('speechSynthesis' in window)) {
    stEl.innerHTML = '<div class="al al-err">❌ Trình duyệt không hỗ trợ. Dùng Chrome hoặc Edge.</div>';
    return;
  }
  function fill() {
    wsVoices = speechSynthesis.getVoices();
    if (!wsVoices.length) return;
    const vi = wsVoices.filter(v => v.lang.toLowerCase().startsWith('vi'));
    const ot = wsVoices.filter(v => !v.lang.toLowerCase().startsWith('vi'));
    sel.innerHTML = '';
    if (vi.length) {
      const g = document.createElement('optgroup'); g.label = '🇻🇳 Tiếng Việt';
      vi.forEach(v => { const o=document.createElement('option'); o.value=v.name; o.textContent=`${v.name} (${v.lang})`; g.appendChild(o); });
      sel.appendChild(g);
    }
    if (ot.length) {
      const g = document.createElement('optgroup'); g.label = '🌐 Ngôn ngữ khác';
      ot.slice(0,25).forEach(v => { const o=document.createElement('option'); o.value=v.name; o.textContent=`${v.name} (${v.lang})`; g.appendChild(o); });
      sel.appendChild(g);
    }
    stEl.innerHTML = vi.length
      ? `<span class="badge b-ok">✓ ${vi.length} giọng tiếng Việt</span>`
      : '<div class="al al-warn">⚠️ Không thấy giọng tiếng Việt. Xem hướng dẫn bên dưới hoặc dùng tab ElevenLabs.</div>';
    sel.addEventListener('change', showVI);
    showVI();
  }
  speechSynthesis.addEventListener('voiceschanged', fill);
  fill();
}
function showVI() {
  const sel = document.getElementById('voiceSel');
  const el = document.getElementById('vInfo');
  if (!sel.value) { el.style.display='none'; return; }
  const v = wsVoices.find(x => x.name === sel.value);
  if (!v) { el.style.display='none'; return; }
  el.style.display='block';
  el.textContent = `Ngôn ngữ: ${v.lang} · Loại: ${v.localService ? 'Offline (nhanh)' : 'Online'}`;
}
function wsSpeakStop() {
  if (isSpeaking) { stopWS(); return; }
  const text = document.getElementById('wsText').value.trim();
  if (!text) return toast('Vui lòng nhập văn bản','err');
  const sel = document.getElementById('voiceSel').value;
  const voice = wsVoices.find(v => v.name === sel) || wsVoices.find(v => v.lang.startsWith('vi')) || null;
  const u = new SpeechSynthesisUtterance(text);
  u.voice  = voice;
  u.rate   = parseFloat(document.getElementById('wsRate').value);
  u.pitch  = parseFloat(document.getElementById('wsPitch').value);
  u.volume = parseFloat(document.getElementById('wsVol').value);
  u.lang   = voice ? voice.lang : 'vi-VN';
  u.onstart = () => { isSpeaking=true; document.getElementById('wsBtn').textContent='⏹ Dừng'; document.getElementById('wsProg').classList.add('show'); };
  u.onend = u.onerror = () => { isSpeaking=false; document.getElementById('wsBtn').textContent='▶ Đọc ngay'; document.getElementById('wsProg').classList.remove('show'); };
  speechSynthesis.cancel();
  speechSynthesis.speak(u);
}
function stopWS() {
  speechSynthesis.cancel(); isSpeaking=false;
  document.getElementById('wsBtn').textContent='▶ Đọc ngay';
  document.getElementById('wsProg').classList.remove('show');
}

/* ── EL API KEY ── */
function getKey() { return localStorage.getItem(SK_KEY) || document.getElementById('apiKey').value.trim(); }
function saveKey() {
  const k = document.getElementById('apiKey').value.trim();
  if (!k) return toast('Nhập API key','err');
  if (!k.startsWith('sk_')) return toast('Key phải bắt đầu bằng sk_','err');
  localStorage.setItem(SK_KEY, k); setKS(true); toast('Đã lưu API key','ok'); loadVoices();
}
function clearKey() {
  if (!confirm('Xóa API key?')) return;
  localStorage.removeItem(SK_KEY); document.getElementById('apiKey').value=''; setKS(false);
}
function toggleKey() {
  const i = document.getElementById('apiKey');
  const b = document.getElementById('togBtn');
  i.type = i.type==='password' ? 'text' : 'password';
  b.textContent = i.type==='password' ? 'Hiện' : 'Ẩn';
}
function setKS(ok) {
  document.getElementById('kStatus').innerHTML = ok
    ? '<span class="badge b-ok">✓ Đã có API key</span>'
    : '<span class="badge b-err">⚠ Chưa có key</span>';
}

/* ── SAMPLE FILE ── */
function handleF(file) {
  const ok = file.type.startsWith('audio/') || /\.(mp3|wav|m4a|ogg|webm|flac)$/i.test(file.name);
  if (!ok) return toast('File không phải audio','err');
  if (file.size > 10*1024*1024) return toast('File quá lớn (>10MB)','err');
  sBlob = file; sFName = file.name;
  document.getElementById('aAud').src = URL.createObjectURL(file);
  document.getElementById('aLbl').textContent = `${file.name} (${(file.size/1024).toFixed(0)} KB)`;
  document.getElementById('aPrv').classList.add('show');
  document.getElementById('clBtn').disabled = false;
}
function clearSample() {
  sBlob=null; sFName='';
  document.getElementById('vFile').value='';
  document.getElementById('aPrv').classList.remove('show');
  document.getElementById('clBtn').disabled=true;
}
async function toggleRec() {
  const btn=document.getElementById('rBtn'), tEl=document.getElementById('rTimer');
  if (!mRec || mRec.state==='inactive') {
    try {
      const stream = await navigator.mediaDevices.getUserMedia({audio:true});
      const mime = MediaRecorder.isTypeSupported('audio/wav') ? 'audio/wav'
                 : MediaRecorder.isTypeSupported('audio/mp4') ? 'audio/mp4' : 'audio/webm';
      mRec = new MediaRecorder(stream, {mimeType:mime}); rChunks=[];
      mRec.ondataavailable = e => rChunks.push(e.data);
      mRec.onstop = () => {
        const ext = mime.includes('wav')?'wav':mime.includes('mp4')?'mp4':'webm';
        handleF(new File([new Blob(rChunks,{type:mime})], `rec.${ext}`, {type:mime}));
        stream.getTracks().forEach(t=>t.stop());
      };
      mRec.start(); rStart=Date.now();
      tEl.classList.add('rec'); btn.textContent='⏹ Dừng'; btn.className='btn btn-d';
      rTimer=setInterval(()=>{
        const s=Math.floor((Date.now()-rStart)/1000);
        tEl.textContent=`${String(Math.floor(s/60)).padStart(2,'0')}:${String(s%60).padStart(2,'0')}`;
        if(s>=90) toggleRec();
      },500);
    } catch(e) { toast('Không truy cập mic: '+e.message,'err'); }
  } else {
    mRec.stop(); clearInterval(rTimer);
    tEl.classList.remove('rec'); btn.textContent='🎤 Bắt đầu thu'; btn.className='btn btn-s';
  }
}

/* ── CLONE VOICE ── */
async function doClone() {
  if (isFileOrigin) return toast('Mở qua local server trước (xem hướng dẫn)','err');
  const key=getKey(); if(!key) return toast('Nhập API key trước','err');
  if(!sBlob) return toast('Upload mẫu giọng trước','err');
  const name=(document.getElementById('vName').value.trim()||'GiongToi')+'_'+Date.now().toString(36);
  showP('elProg','Đang clone giọng (15–30s)...');
  document.getElementById('clBtn').disabled=true;
  try {
    const form=new FormData();
    form.append('name',name);
    form.append('description','Vietnamese voice – iBasic');
    form.append('files',sBlob,sFName||'sample.mp3');
    const r=await fetch(`${API}/voices/add`,{method:'POST',headers:{'xi-api-key':key},body:form});
    if(!r.ok) throw new Error(elErr(await r.text(),r.status));
    const d=await r.json();
    localStorage.setItem(SK_CV,JSON.stringify({id:d.voice_id,name}));
    showClone(name,d.voice_id);
    toast('Clone giọng thành công!','ok'); loadVoices();
  } catch(e) { toast('Lỗi clone: '+e.message,'err'); }
  finally { hideP('elProg'); document.getElementById('clBtn').disabled=false; }
}
function showClone(name,id) {
  document.getElementById('cName').textContent=name;
  const b=document.getElementById('cBox'); b.classList.add('show'); b.dataset.vid=id;
}
async function deleteClone() {
  const cv=localStorage.getItem(SK_CV); if(!cv) return;
  if(!confirm('Xóa giọng clone khỏi ElevenLabs?')) return;
  const d=JSON.parse(cv);
  try { await fetch(`${API}/voices/${d.id}`,{method:'DELETE',headers:{'xi-api-key':getKey()}}); } catch(e){}
  localStorage.removeItem(SK_CV);
  document.getElementById('cBox').classList.remove('show');
  toast('Đã xóa giọng'); loadVoices();
}

/* ── LOAD VOICES ── */
async function loadVoices() {
  const key=getKey(); if(!key) return;
  if(isFileOrigin) return;
  const sel=document.getElementById('elVSel');
  sel.innerHTML='<option>Đang tải...</option>';
  try {
    const r=await fetch(`${API}/voices`,{headers:{'xi-api-key':key}});
    if(!r.ok) throw new Error(elErr(await r.text(),r.status));
    const d=await r.json();
    sel.innerHTML='<option value="">— Chọn giọng —</option>';
    const cl=d.voices.filter(v=>v.category==='cloned'||v.category==='generated');
    const pm=d.voices.filter(v=>v.category==='premade');
    if(cl.length){ const g=document.createElement('optgroup'); g.label='🎤 Giọng đã clone'; cl.forEach(v=>ao(g,v.voice_id,v.name)); sel.appendChild(g); }
    if(pm.length){ const g=document.createElement('optgroup'); g.label='🔊 Giọng mặc định'; pm.forEach(v=>ao(g,v.voice_id,`${v.name}${v.labels?.gender?' ('+v.labels.gender+')':''}`)); sel.appendChild(g); }
    const cv=localStorage.getItem(SK_CV);
    if(cv) sel.value=JSON.parse(cv).id;
  } catch(e) { sel.innerHTML=`<option value="">Lỗi: ${e.message}</option>`; }
}
function ao(p,v,t) { const o=document.createElement('option'); o.value=v; o.textContent=t; p.appendChild(o); }

/* ── GENERATE ── */
async function doGenerate() {
  if(isFileOrigin) return toast('Mở qua local server trước (xem hướng dẫn)','err');
  const key=getKey(); if(!key) return toast('Nhập API key trước','err');
  const text=document.getElementById('elText').value.trim(); if(!text) return toast('Nhập văn bản','err');
  let vid=document.getElementById('elVSel').value;
  if(!vid){ const cv=localStorage.getItem(SK_CV); if(cv) vid=JSON.parse(cv).id; }
  if(!vid) return toast('Chọn hoặc clone giọng trước','err');
  showP('elProg','Đang tạo giọng đọc...'); document.getElementById('genBtn').disabled=true;
  document.getElementById('elOut').classList.remove('show');
  try {
    const body=JSON.stringify({
      text, model_id:MODEL,
      voice_settings:{
        stability:parseFloat(document.getElementById('stab').value),
        similarity_boost:parseFloat(document.getElementById('sim').value),
        style:parseFloat(document.getElementById('sty').value),
        use_speaker_boost:true
      }
    });
    const r=await fetch(`${API}/text-to-speech/${vid}?output_format=mp3_44100_128`,{
      method:'POST',
      headers:{'xi-api-key':key,'Content-Type':'application/json','Accept':'audio/mpeg'},
      body
    });
    if(!r.ok) throw new Error(elErr(await r.text(),r.status));
    lastBlob=await r.blob();
    document.getElementById('outAud').src=URL.createObjectURL(lastBlob);
    document.getElementById('elOut').classList.add('show');
    toast('Tạo giọng thành công!','ok');
    document.getElementById('elOut').scrollIntoView({behavior:'smooth',block:'nearest'});
  } catch(e) { toast('Lỗi: '+e.message,'err'); }
  finally { hideP('elProg'); document.getElementById('genBtn').disabled=false; }
}
function dlAudio() {
  if(!lastBlob) return toast('Chưa có audio','err');
  const a=document.createElement('a');
  a.href=URL.createObjectURL(lastBlob);
  a.download=`ibasic_voice_${new Date().toISOString().slice(0,19).replace(/:/g,'-')}.mp3`;
  document.body.appendChild(a); a.click(); document.body.removeChild(a);
}

/* ── HELPERS ── */
function sl(id,out,fmt) {
  const el=document.getElementById(id), o=document.getElementById(out);
  const up=()=>o.textContent=fmt(parseFloat(el.value));
  el.addEventListener('input',up); up();
}
function cc(tid,cid) {
  const ta=document.getElementById(tid), o=document.getElementById(cid);
  const up=()=>o.textContent=ta.value.length.toLocaleString()+' ký tự';
  ta.addEventListener('input',up); up();
}
function showP(id,msg) { document.getElementById(id.replace('Prog','PT')||id+'T')&&(document.getElementById(id.replace('Prog','PT')||id+'T').textContent=msg); document.getElementById(id).classList.add('show'); }
function hideP(id) { document.getElementById(id).classList.remove('show'); }
// Fix showP
function showP(id,msg) {
  const pEl=document.getElementById(id);
  const tEl=pEl.querySelector('span');
  if(tEl) tEl.textContent=msg;
  pEl.classList.add('show');
}
function toast(msg,type='') {
  const t=document.getElementById('toast');
  t.textContent=msg; t.className='toast '+type;
  clearTimeout(t._t); void t.offsetWidth; t.classList.add('show');
  t._t=setTimeout(()=>t.classList.remove('show'),3500);
}
function elErr(raw,status) {
  try { const j=JSON.parse(raw); if(j.detail) return typeof j.detail==='string'?j.detail:(j.detail.status||'')+': '+(j.detail.message||''); } catch(e){}
  if(status===401) return 'API key sai hoặc hết hạn';
  if(status===422) return 'Tham số không hợp lệ (422)';
  if(status===429) return 'Hết quota hoặc quá nhiều request (429)';
  return 'Lỗi HTTP '+status;
}
</script>
</body>
</html>
