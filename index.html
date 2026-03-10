<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0"/>
<title>Urology Ward — Sion Hospital</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;600;700;800&display=swap" rel="stylesheet"/>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-database-compat.js"></script>
<style>
*{box-sizing:border-box;margin:0;padding:0;}
body{background:#0d1421;color:#e2e8f0;font-family:'DM Sans',sans-serif;max-width:480px;margin:0 auto;min-height:100vh;}
input,select,textarea{width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px;font-family:'DM Sans',sans-serif;outline:none;}
button{cursor:pointer;font-family:'DM Sans',sans-serif;}
.topbar{background:#141c2e;padding:14px 16px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:10;border-bottom:1px solid #1e2d40;}
.bottomnav{position:fixed;bottom:0;left:50%;transform:translateX(-50%);width:100%;max-width:480px;background:#141c2e;border-top:1px solid #1e2d40;display:flex;justify-content:space-around;padding:10px 0 16px;z-index:10;}
.navbtn{background:none;border:none;display:flex;flex-direction:column;align-items:center;gap:3px;padding:0 16px;position:relative;}
.card{background:#1a2235;border-radius:12px;padding:12px 14px;margin-bottom:10px;}
.sec{background:#1a2235;border-radius:12px;padding:12px 14px;margin-bottom:12px;}
.sec-title{font-size:11px;font-weight:800;text-transform:uppercase;letter-spacing:1.2px;cursor:pointer;display:flex;justify-content:space-between;align-items:center;}
.tag{font-size:11px;padding:2px 8px;border-radius:20px;font-weight:600;white-space:nowrap;display:inline-block;}
.btn-primary{padding:13px;background:#4A9EFF;border:none;border-radius:12px;color:#fff;font-weight:800;font-size:15px;width:100%;}
.btn-danger{padding:13px 18px;background:#1a2235;border:1px solid #ef4444;border-radius:12px;color:#ef4444;font-weight:700;font-size:18px;}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:8px;}
.grid4{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-bottom:14px;}
.stat-card{background:#1a2235;border-radius:10px;padding:10px 6px;text-align:center;}
.label{font-size:11px;color:#64748b;margin-bottom:4px;text-transform:uppercase;letter-spacing:0.8px;}
.spinner{display:inline-block;width:14px;height:14px;border:2px solid #4A9EFF44;border-top:2px solid #4A9EFF;border-radius:50%;animation:spin 0.8s linear infinite;}
@keyframes spin{to{transform:rotate(360deg)}}
.sync-dot{width:8px;height:8px;border-radius:50%;display:inline-block;margin-left:6px;}
</style>
</head>
<body>

<div id="app"></div>

<script>
// ─── FIREBASE CONFIG ──────────────────────────────────────────────
const firebaseConfig = {
  databaseURL: "https://sion-urology-default-rtdb.firebaseio.com"
};
firebase.initializeApp(firebaseConfig);
const db = firebase.database();
const patientsRef = db.ref('patients');

// ─── CONSTANTS ────────────────────────────────────────────────────
const INVESTIGATIONS = ["CBC","RFT","LFT","Urine C/S","Urine R/M","Blood Group","HBsAg","HIV","HCV","CXR","ECG","RBS"];
const WORKFLOW_STAGES = ["Admission","Workup Sent","References Sent","Fitness Cleared","PAC Done","Consent Done","OT Posted","Post-Op","Discharge Ready"];
const OT_LISTS = ["Supra Major","PCNL / RIRS","URSL / CLT"];
const OT_PRIORITY = ["Emergency","Urgent","Semi-urgent","Elective"];
const DEVICE_TYPES = ["Urethral Catheter","DJ Stent","Nephrostomy","PCN Tube","Suprapubic Catheter","Ureteric Stent"];
const COMMON_DIAGNOSES = ["BPH / AUR","Ureteric Calculus","Renal Calculus","Bladder Calculus","Ca Bladder","Ca Kidney","Ca Prostate","Hydronephrosis","PUJ Obstruction","Urethral Stricture","VUR","Post PCNL","Post URSL","Pyonephrosis","Renal Abscess","Testicular Torsion","Epididymo-orchitis","Phimosis","Hypospadias","Urinary Fistula"];
const COMMON_DEPTS = ["Medicine","Anaesthesia (PAC)","Cardiology","Nephrology","Endocrinology","Chest Medicine","Neurology","Haematology"];

const STAGE_COLOR = {
  "Admission":"#4A9EFF","Workup Sent":"#F59E0B","References Sent":"#8B5CF6",
  "Fitness Cleared":"#06B6D4","PAC Done":"#10B981","Consent Done":"#84CC16",
  "OT Posted":"#F97316","Post-Op":"#EC4899","Discharge Ready":"#22C55E"
};
const PRIORITY_COLOR = {"Emergency":"#ef4444","Urgent":"#F97316","Semi-urgent":"#F59E0B","Elective":"#10B981"};

// ─── STATE ────────────────────────────────────────────────────────
let state = {
  patients: {},
  view: 'ward',
  activePatient: null,
  scanning: false,
  scanError: '',
  syncStatus: 'connecting', // connecting | live | error
  openSections: {}
};

function newPatient() {
  return {
    id: 'p_' + Date.now(),
    bed:"", name:"", age:"", diagnosis:"", admitDate: new Date().toISOString().split("T")[0],
    stage:"Admission", nextAction:"", comorbidities:"",
    investigations: Object.fromEntries(INVESTIGATIONS.map(i=>[i,"pending"])),
    references:[], devices:[], otList:"", otPriority:"Elective",
    facultyInstructions:[], caseSummary:"", notes:""
  };
}

// ─── FIREBASE SYNC ────────────────────────────────────────────────
patientsRef.on('value', snap => {
  state.patients = snap.val() || {};
  state.syncStatus = 'live';
  render();
}, err => {
  state.syncStatus = 'error';
  render();
});

function savePatient(p) {
  patientsRef.child(p.id).set(p);
}
function deletePatient(id) {
  patientsRef.child(id).remove();
}

// ─── HELPERS ──────────────────────────────────────────────────────
const daysSince = d => d ? Math.floor((Date.now()-new Date(d).getTime())/86400000) : 0;
const pendingInv = p => Object.values(p.investigations||{}).filter(v=>v==="pending").length;
const pendingRefs = p => (p.references||[]).filter(r=>!r.cleared).length;
const pList = () => Object.values(state.patients);

function tag(text, color) {
  return `<span class="tag" style="background:${color}22;color:${color}">${text}</span>`;
}

// ─── AI SCAN ──────────────────────────────────────────────────────
async function handleScan(files) {
  if (!files.length) return;
  state.scanning = true; state.scanError = '';
  render();
  try {
    const images = await Promise.all(Array.from(files).map(file => new Promise((res,rej) => {
      const r = new FileReader();
      r.onload = () => res({data: r.result.split(",")[1], type: file.type||"image/jpeg"});
      r.onerror = () => rej(new Error("Read failed"));
      r.readAsDataURL(file);
    })));

    const content = [
      ...images.map(img => ({type:"image", source:{type:"base64", media_type:img.type, data:img.data}})),
      {type:"text", text:`You are reading ${images.length} pages of a handwritten hospital case paper from a urology ward in India (Sion Hospital, Mumbai).
Read ALL pages and extract a complete patient record.
Return ONLY a JSON object, no explanation, no markdown:
{
  "name": "patient full name",
  "age": "age as number",
  "bed": "bed number",
  "admitDate": "YYYY-MM-DD",
  "diagnosis": "primary diagnosis",
  "comorbidities": "comma separated e.g. DM, HTN, CKD",
  "stage": "one of: Admission, Workup Sent, References Sent, Fitness Cleared, PAC Done, Consent Done, OT Posted, Post-Op, Discharge Ready",
  "nextAction": "what needs to be done next",
  "investigations": ["only investigations ordered from: CBC, RFT, LFT, Urine C/S, Urine R/M, Blood Group, HBsAg, HIV, HCV, CXR, ECG, RBS"],
  "devices": [{"type": "device name", "days": "days in situ"}],
  "caseSummary": "detailed summary: history, diagnosis, operation done, post-op status, imaging"
}
Use empty string or empty array if not found.`}
    ];

    const resp = await fetch("https://api.anthropic.com/v1/messages", {
      method:"POST",
      headers:{"Content-Type":"application/json"},
      body: JSON.stringify({model:"claude-sonnet-4-20250514", max_tokens:1500, messages:[{role:"user", content}]})
    });
    const data = await resp.json();
    const text = data.content.map(c=>c.text||"").join("");
    const extracted = JSON.parse(text.replace(/```json|```/g,"").trim());

    const p = newPatient();
    if (extracted.name) p.name = extracted.name;
    if (extracted.age) p.age = String(extracted.age);
    if (extracted.bed) p.bed = String(extracted.bed);
    if (extracted.admitDate) p.admitDate = extracted.admitDate;
    if (extracted.diagnosis) p.diagnosis = extracted.diagnosis;
    if (extracted.comorbidities) p.comorbidities = extracted.comorbidities;
    if (extracted.caseSummary) p.caseSummary = extracted.caseSummary;
    if (extracted.nextAction) p.nextAction = extracted.nextAction;
    if (extracted.stage && WORKFLOW_STAGES.includes(extracted.stage)) p.stage = extracted.stage;
    if (extracted.investigations?.length > 0) {
      INVESTIGATIONS.forEach(inv => { p.investigations[inv] = extracted.investigations.includes(inv) ? "pending" : "not-ordered"; });
    }
    if (extracted.devices?.length > 0) {
      p.devices = extracted.devices.map(d => ({type: typeof d==="string"?d:(d.type||d), days: typeof d==="object"?String(d.days||"0"):"0"}));
    }
    const refs = [];
    if (extracted.comorbidities) {
      const c = extracted.comorbidities.toLowerCase();
      if (c.includes("dm")||c.includes("diabet")) refs.push({dept:"Endocrinology", cleared:false});
      if (c.includes("htn")||c.includes("hypert")||c.includes("ihd")) refs.push({dept:"Cardiology", cleared:false});
      if (c.includes("ckd")||c.includes("renal")) refs.push({dept:"Nephrology", cleared:false});
      if (c.includes("copd")||c.includes("asthma")) refs.push({dept:"Chest Medicine", cleared:false});
    }
    refs.push({dept:"Medicine", cleared:false});
    refs.push({dept:"Anaesthesia (PAC)", cleared:false});
    p.references = refs;

    state.activePatient = p;
    state.view = 'patient';
  } catch(err) {
    state.scanError = "Could not read papers. Try better lighting or retake photos.";
  } finally {
    state.scanning = false;
    render();
  }
}

// ─── RENDER ───────────────────────────────────────────────────────
function render() {
  document.getElementById('app').innerHTML = buildApp();
  attachEvents();
}

function buildApp() {
  const v = state.view;
  if (v === 'ward') return buildShell(buildWard());
  if (v === 'ot') return buildShell(buildOT());
  if (v === 'pending') return buildShell(buildPending());
  if (v === 'patient') return buildPatient();
  return '';
}

function buildShell(content) {
  const pts = pList();
  const flagCount = pts.filter(p=>pendingInv(p)>0||pendingRefs(p)>0||p.stage==="Discharge Ready").length;
  const syncColor = state.syncStatus==='live'?'#10B981':state.syncStatus==='error'?'#ef4444':'#F59E0B';
  return `
  <div class="topbar">
    <div>
      <div style="font-weight:800;font-size:15px">Urology Ward <span class="sync-dot" style="background:${syncColor}" title="${state.syncStatus}"></span></div>
      <div style="font-size:11px;color:#475569">Sion Hospital · Dr. Ajit Sawant · ${pts.length}/36 beds</div>
    </div>
    <div style="font-size:11px;color:#475569">${new Date().toLocaleDateString('en-IN',{day:'2-digit',month:'short'})}</div>
  </div>
  <div style="padding-bottom:80px">${content}</div>
  <div class="bottomnav">
    ${['ward','ot','pending'].map(tab => `
      <button class="navbtn" onclick="nav('${tab}')">
        <span style="font-size:22px">${tab==='ward'?'🏥':tab==='ot'?'🔪':'⚠️'}</span>
        <span style="font-size:11px;font-weight:700;color:${state.view===tab?'#4A9EFF':'#475569'}">${tab==='ward'?'Ward':tab==='ot'?'OT List':'Pending'}</span>
        ${tab==='pending'&&flagCount>0?`<span style="position:absolute;top:-2px;right:8px;background:#ef4444;color:#fff;border-radius:50%;width:16px;height:16px;font-size:10px;display:flex;align-items:center;justify-content:center;font-weight:800">${flagCount}</span>`:''}
      </button>`).join('')}
  </div>`;
}

function buildWard() {
  const pts = pList();
  const otReady = pts.filter(p=>["Consent Done","OT Posted"].includes(p.stage)).length;
  const pendingLabs = pts.filter(p=>pendingInv(p)>0).length;
  const dcReady = pts.filter(p=>p.stage==="Discharge Ready").length;

  return `
  <div style="padding:12px">
    <div class="grid4">
      ${[['Beds',pts.length,'#4A9EFF'],['OT Ready',otReady,'#10B981'],['Pending',pendingLabs,'#F59E0B'],['D/C',dcReady,'#22C55E']].map(([l,v,c])=>`
        <div class="stat-card" style="border-top:3px solid ${c}">
          <div style="font-size:22px;font-weight:800;color:${c}">${v}</div>
          <div style="font-size:10px;color:#64748b;margin-top:2px">${l}</div>
        </div>`).join('')}
    </div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:14px">
      <button onclick="addManual()" style="padding:14px;background:#1a2235;border:1px solid #2a3448;border-radius:12px;color:#e2e8f0;font-weight:700;font-size:13px;display:flex;align-items:center;justify-content:center;gap:8px">
        <span style="font-size:18px">✏️</span> Manual Entry
      </button>
      <button onclick="document.getElementById('scanInput').click()" ${state.scanning?'disabled':''} style="padding:14px;background:${state.scanning?'#1a2235':'#4A9EFF22'};border:1px solid ${state.scanning?'#2a3448':'#4A9EFF'};border-radius:12px;color:${state.scanning?'#475569':'#4A9EFF'};font-weight:700;font-size:13px;display:flex;align-items:center;justify-content:center;gap:8px">
        ${state.scanning?`<span class="spinner"></span> Reading...`:`<span style="font-size:18px">📷</span> Scan Papers`}
      </button>
    </div>
    <input id="scanInput" type="file" accept="image/*" multiple style="display:none" onchange="handleScanInput(this)"/>
    ${state.scanError?`<div style="background:#ef444422;border:1px solid #ef4444;border-radius:10px;padding:10px 14px;font-size:13px;color:#ef4444;margin-bottom:12px">${state.scanError}</div>`:''}
    ${pts.length===0?`<div style="text-align:center;color:#475569;margin-top:40px"><div style="font-size:40px;margin-bottom:12px">🏥</div><div style="font-size:15px;font-weight:600">No patients yet</div><div style="font-size:13px;margin-top:6px">Add manually or scan case papers</div></div>`:''}
    ${pts.map(p => `
      <div class="card" style="border-left:4px solid ${STAGE_COLOR[p.stage]||'#4A9EFF'};cursor:pointer" onclick="openPatient('${p.id}')">
        <div style="display:flex;justify-content:space-between;align-items:flex-start;gap:8px">
          <div><span style="font-weight:700;font-size:15px">${p.name||'—'}</span> <span style="font-size:12px;color:#64748b">Bed ${p.bed} · ${p.age}y</span></div>
          <span class="tag" style="background:${STAGE_COLOR[p.stage]}22;color:${STAGE_COLOR[p.stage]};flex-shrink:0">${p.stage}</span>
        </div>
        <div style="font-size:13px;color:#94a3b8;margin-top:4px">${p.diagnosis||'No diagnosis'}</div>
        ${p.nextAction?`<div style="font-size:12px;color:#EC4899;margin-top:4px">→ ${p.nextAction}</div>`:''}
        <div style="display:flex;gap:6px;margin-top:8px;flex-wrap:wrap">
          ${pendingInv(p)>0?tag(pendingInv(p)+' labs','#F59E0B'):''}
          ${pendingRefs(p)>0?tag(pendingRefs(p)+' refs','#8B5CF6'):''}
          ${(p.devices||[]).map(d=>`${tag(d.type.split(' ')[0]+' '+d.days+'d','#06B6D4')}`).join('')}
          ${p.otList?tag(p.otList,'#F97316'):''}
        </div>
        <div style="font-size:11px;color:#334155;margin-top:6px">Admitted ${daysSince(p.admitDate)} days ago</div>
      </div>`).join('')}
  </div>`;
}

function buildOT() {
  const pts = pList().filter(p=>p.otList);
  return `<div style="padding:12px">
    ${OT_LISTS.map(list => {
      const listPts = pts.filter(p=>p.otList===list).sort((a,b)=>OT_PRIORITY.indexOf(a.otPriority)-OT_PRIORITY.indexOf(b.otPriority)||daysSince(b.admitDate)-daysSince(a.admitDate));
      return `
      <div style="margin-bottom:20px">
        <div style="font-size:12px;font-weight:800;color:#F97316;text-transform:uppercase;letter-spacing:1.5px;margin-bottom:10px;padding-bottom:6px;border-bottom:1px solid #1e2d40">
          ${list} <span style="color:#475569;font-weight:400">(${listPts.length})</span>
        </div>
        ${listPts.length===0?'<div style="color:#334155;font-size:13px;font-style:italic;padding-left:4px">No patients</div>':
          listPts.map((p,i)=>`
          <div class="card" style="display:flex;gap:10px;align-items:center;cursor:pointer" onclick="openPatient('${p.id}')">
            <div style="width:30px;height:30px;border-radius:50%;background:#0f172a;display:flex;align-items:center;justify-content:center;font-weight:800;color:#F97316;font-size:14px;flex-shrink:0">${i+1}</div>
            <div style="flex:1;min-width:0">
              <div style="font-weight:700;font-size:14px">${p.name} <span style="color:#475569;font-weight:400;font-size:12px">Bed ${p.bed}</span></div>
              <div style="font-size:12px;color:#94a3b8;margin-top:2px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${p.diagnosis}</div>
              <div style="display:flex;gap:6px;margin-top:6px;flex-wrap:wrap">
                ${tag(p.otPriority, PRIORITY_COLOR[p.otPriority])}
                ${tag('Wait '+daysSince(p.admitDate)+'d','#4A9EFF')}
                ${tag(p.stage, STAGE_COLOR[p.stage])}
              </div>
            </div>
          </div>`).join('')}
      </div>`;
    }).join('')}
  </div>`;
}

function buildPending() {
  const pts = pList();
  const sections = [
    {title:"Pending Investigations",color:"#F59E0B",items:pts.filter(p=>pendingInv(p)>0),sub:p=>`${pendingInv(p)} tests: `+Object.entries(p.investigations).filter(([,v])=>v==="pending").map(([k])=>k).join(", ")},
    {title:"References Not Cleared",color:"#8B5CF6",items:pts.filter(p=>pendingRefs(p)>0),sub:p=>(p.references||[]).filter(r=>!r.cleared).map(r=>r.dept).join(", ")},
    {title:"Discharge Ready",color:"#22C55E",items:pts.filter(p=>p.stage==="Discharge Ready"),sub:()=>"Ready for discharge"},
    {title:"Long Stay >7 days",color:"#EC4899",items:pts.filter(p=>daysSince(p.admitDate)>7&&p.stage!=="Discharge Ready"),sub:p=>`Day ${daysSince(p.admitDate)} · ${p.stage}`},
  ];
  return `<div style="padding:12px">
    ${sections.map(s=>`
      <div style="margin-bottom:20px">
        <div style="display:flex;align-items:center;gap:8px;margin-bottom:10px;padding-bottom:6px;border-bottom:1px solid #1e2d40">
          <span style="width:8px;height:8px;border-radius:50%;background:${s.color};display:inline-block;flex-shrink:0"></span>
          <span style="font-size:12px;font-weight:800;color:${s.color};text-transform:uppercase;letter-spacing:1px">${s.title}</span>
          <span style="margin-left:auto;font-size:12px;color:#475569;font-weight:700">${s.items.length}</span>
        </div>
        ${s.items.length===0?`<div style="color:#22C55E;font-size:13px;padding-left:4px">✓ All clear</div>`:
          s.items.map(p=>`
          <div class="card" style="cursor:pointer" onclick="openPatient('${p.id}')">
            <div style="font-weight:700;font-size:14px">${p.name} <span style="color:#64748b;font-weight:400;font-size:12px">· Bed ${p.bed}</span></div>
            <div style="font-size:12px;color:${s.color};margin-top:4px;line-height:1.5">${s.sub(p)}</div>
          </div>`).join('')}
      </div>`).join('')}
  </div>`;
}

function buildPatient() {
  const p = state.activePatient;
  if (!p) return '';
  const isNew = !state.patients[p.id];

  const field = (label, key, type='text', opts=null) => `
    <div style="margin-bottom:10px">
      <div class="label">${label}</div>
      ${opts
        ? `<select onchange="setField('${key}',this.value)" style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px">
            ${opts.map(o=>`<option value="${o}" ${p[key]===o?'selected':''}>${o||'Select...'}</option>`).join('')}
           </select>`
        : `<input type="${type}" value="${(p[key]||'').replace(/"/g,'&quot;')}" onchange="setField('${key}',this.value)" style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px"/>`
      }
    </div>`;

  const sec = (id, title, color, content) => {
    const open = state.openSections[id] !== false;
    return `
    <div class="sec">
      <div class="sec-title" style="color:${color};margin-bottom:${open?'12px':'0'}" onclick="toggleSec('${id}')">
        ${title} <span style="color:#334155">${open?'▲':'▼'}</span>
      </div>
      ${open?`<div>${content}</div>`:''}
    </div>`;
  };

  // Investigations
  const invHtml = `<div class="grid2">${INVESTIGATIONS.map(inv=>{
    const s = p.investigations[inv]||'pending';
    return `<div style="background:#0f172a;border-radius:8px;padding:8px 10px">
      <div style="font-size:12px;color:#cbd5e1;margin-bottom:6px;font-weight:700">${inv}</div>
      <div style="display:flex;gap:3px">
        ${[['pending','⏳','#F59E0B'],['done','✓','#10B981'],['abnormal','⚠️','#ef4444'],['not-ordered','—','#334155']].map(([st,ic,col])=>
          `<button onclick="setInv('${inv}','${st}')" style="flex:1;padding:5px 2px;font-size:12px;border-radius:6px;border:none;font-weight:700;background:${s===st?col:'#1a2235'};color:${s===st?'#fff':'#475569'}">${ic}</button>`
        ).join('')}
      </div>
    </div>`;
  }).join('')}</div>
  <div style="display:flex;gap:10px;margin-top:10px;font-size:11px;color:#475569"><span>⏳ Pending</span><span>✓ Done</span><span>⚠️ Abnormal</span><span>— Not ordered</span></div>`;

  // References
  const refsHtml = `
    ${(p.references||[]).map((r,i)=>`
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:8px;background:#0f172a;border-radius:8px;padding:8px 10px">
        <span style="flex:1;font-size:14px;font-weight:600">${r.dept}</span>
        <button onclick="toggleRef(${i})" style="padding:5px 12px;border-radius:6px;border:none;font-weight:700;font-size:11px;background:${r.cleared?'#10B981':'#F59E0B'};color:#fff">${r.cleared?'Cleared':'Pending'}</button>
        <button onclick="removeRef(${i})" style="background:none;border:none;color:#ef4444;font-size:18px;padding:0">×</button>
      </div>`).join('')}
    <div class="label" style="margin-top:8px">Quick Add</div>
    <div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:8px">
      ${COMMON_DEPTS.filter(d=>!(p.references||[]).find(r=>r.dept===d)).map(d=>
        `<button onclick="addRef('${d}')" style="padding:7px 12px;border-radius:20px;background:#8B5CF622;border:1px solid #8B5CF6;color:#8B5CF6;font-size:11px;font-weight:700">+ ${d}</button>`
      ).join('')}
    </div>
    <div style="display:flex;gap:8px">
      <input id="newRefInput" placeholder="Other department..." style="flex:1;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px"/>
      <button onclick="addRefCustom()" style="padding:10px 14px;background:#8B5CF6;border:none;border-radius:10px;color:#fff;font-weight:700">Add</button>
    </div>`;

  // Devices
  const devicesHtml = `
    ${(p.devices||[]).map((d,i)=>`
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:8px;background:#0f172a;border-radius:8px;padding:8px 10px">
        <span style="font-size:13px;color:#06B6D4;font-weight:700;flex:1">${d.type}</span>
        <span style="font-size:12px;color:#94a3b8">Day ${d.days}</span>
        <button onclick="removeDevice(${i})" style="background:none;border:none;color:#ef4444;font-size:18px;padding:0">×</button>
      </div>`).join('')}
    <div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:8px">
      ${DEVICE_TYPES.map(d=>`<button onclick="selectDevice('${d}')" id="devbtn_${d.replace(/ /g,'_')}" style="padding:7px 12px;border-radius:20px;background:#06B6D422;border:1px solid #06B6D4;color:#06B6D4;font-size:11px;font-weight:700">${d}</button>`).join('')}
    </div>
    <div style="display:flex;gap:8px">
      <input id="devDays" type="number" placeholder="Days in situ" style="flex:1;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px"/>
      <button onclick="addDevice()" style="padding:10px 14px;background:#06B6D4;border:none;border-radius:10px;color:#fff;font-weight:700">Add</button>
    </div>`;

  // Faculty instructions
  const instrHtml = `
    ${(p.facultyInstructions||[]).map((fi,i)=>`
      <div style="background:#0f172a;border-radius:8px;padding:8px 10px;margin-bottom:8px">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <span style="font-size:11px;color:#EC4899;font-weight:600">${fi.time}</span>
          <button onclick="removeInstr(${i})" style="background:none;border:none;color:#475569;font-size:16px;padding:0">×</button>
        </div>
        <div style="font-size:13px;margin-top:4px;line-height:1.5">${fi.text}</div>
      </div>`).join('')}
    <div style="display:flex;gap:8px;margin-top:4px">
      <input id="newInstrInput" placeholder="Type faculty instruction..." style="flex:1;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px"/>
      <button onclick="addInstr()" style="padding:10px 14px;background:#EC4899;border:none;border-radius:10px;color:#fff;font-weight:700">Add</button>
    </div>`;

  return `
  <div style="min-height:100vh;background:#0d1421">
    <div class="topbar">
      <button onclick="nav('ward')" style="background:none;border:none;color:#94a3b8;font-size:22px;padding:0">←</button>
      <div style="flex:1;margin-left:12px">
        <div style="font-weight:800;font-size:15px">${p.name||'New Patient'}</div>
        <div style="font-size:11px;color:#475569">Bed ${p.bed} · ${isNew?'New patient':'Editing'}</div>
      </div>
      <button onclick="saveAndBack()" style="padding:8px 18px;background:#4A9EFF;border:none;border-radius:10px;color:#fff;font-weight:700;font-size:14px">Save</button>
    </div>
    <div style="padding:12px 12px 80px">
      ${sec('basic','Basic Info','#4A9EFF',`
        <div style="display:grid;grid-template-columns:1fr 2fr 1fr;gap:8px;margin-bottom:10px">
          <div><div class="label">Bed</div><input value="${p.bed||''}" onchange="setField('bed',this.value)" placeholder="1A" style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px"/></div>
          <div><div class="label">Name</div><input value="${(p.name||'').replace(/"/g,'&quot;')}" onchange="setField('name',this.value)" placeholder="Patient name" style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px"/></div>
          <div><div class="label">Age</div><input type="number" value="${p.age||''}" onchange="setField('age',this.value)" placeholder="45" style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px"/></div>
        </div>
        <div style="margin-bottom:10px">
          <div class="label">Diagnosis</div>
          <select onchange="setField('diagnosis',this.value)" style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px;margin-bottom:6px">
            <option value="">Select diagnosis...</option>
            ${COMMON_DIAGNOSES.map(d=>`<option value="${d}" ${p.diagnosis===d?'selected':''}>${d}</option>`).join('')}
            <option value="__custom__">Other (type below)</option>
          </select>
          <input value="${(p.diagnosis||'').replace(/"/g,'&quot;')}" onchange="setField('diagnosis',this.value)" placeholder="Or type custom diagnosis..." style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px"/>
        </div>
        <div style="margin-bottom:10px"><div class="label">Comorbidities</div><input value="${(p.comorbidities||'').replace(/"/g,'&quot;')}" onchange="setField('comorbidities',this.value)" placeholder="DM, HTN, CKD..." style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px"/></div>
        <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:10px">
          <div><div class="label">Admit Date</div><input type="date" value="${p.admitDate||''}" onchange="setField('admitDate',this.value)" style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px"/></div>
          <div><div class="label">OT Priority</div><select onchange="setField('otPriority',this.value)" style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px">${OT_PRIORITY.map(o=>`<option value="${o}" ${p.otPriority===o?'selected':''}>${o}</option>`).join('')}</select></div>
        </div>
        <div><div class="label">OT List</div><div style="display:flex;gap:8px;flex-wrap:wrap">${['', ...OT_LISTS].map(l=>`<button onclick="setField('otList','${l}')" style="padding:8px 14px;border-radius:20px;border:none;font-weight:700;font-size:12px;background:${p.otList===l?'#F97316':'#0f172a'};color:${p.otList===l?'#fff':'#475569'}">${l||'None'}</button>`).join('')}</div></div>
      `)}
      ${sec('workflow','Workflow Stage','#4A9EFF',`
        <div style="display:flex;gap:6px;flex-wrap:wrap;margin-bottom:10px">
          ${WORKFLOW_STAGES.map(s=>`<button onclick="setField('stage','${s}')" style="padding:7px 12px;border-radius:20px;border:none;font-weight:700;font-size:11px;background:${p.stage===s?STAGE_COLOR[s]:'#0f172a'};color:${p.stage===s?'#fff':'#475569'}">${s}</button>`).join('')}
        </div>
        <div class="label">Next Action</div>
        <input value="${(p.nextAction||'').replace(/"/g,'&quot;')}" onchange="setField('nextAction',this.value)" placeholder="e.g. Await RFT, Send medicine ref..." style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px"/>
      `)}
      ${sec('inv','Investigations','#F59E0B', invHtml)}
      ${sec('refs','References','#8B5CF6', refsHtml)}
      ${sec('devices','Devices / Tubes','#06B6D4', devicesHtml)}
      ${sec('instr','Faculty Instructions','#EC4899', instrHtml)}
      ${sec('summary','Case Summary','#22C55E',`<textarea onchange="setField('caseSummary',this.value)" placeholder="Clinical summary for faculty briefing..." rows="5" style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px;resize:vertical;font-family:'DM Sans',sans-serif;line-height:1.6">${p.caseSummary||''}</textarea>`)}
      ${sec('notes','Notes','#64748b',`<textarea onchange="setField('notes',this.value)" placeholder="Any other notes..." rows="3" style="width:100%;padding:10px 12px;border-radius:10px;border:1px solid #2a3448;background:#0f172a;color:#e2e8f0;font-size:14px;resize:vertical;font-family:'DM Sans',sans-serif">${p.notes||''}</textarea>`)}
      <div style="display:flex;gap:10px;margin-top:8px">
        <button onclick="saveAndBack()" class="btn-primary">Save Patient</button>
        ${!isNew?`<button onclick="confirmDelete()" class="btn-danger">🗑</button>`:''}
      </div>
    </div>
  </div>`;
}

// ─── EVENTS ───────────────────────────────────────────────────────
function attachEvents() {}

window.nav = function(v) { state.view = v; render(); };
window.addManual = function() { state.activePatient = newPatient(); state.view = 'patient'; render(); };
window.openPatient = function(id) { state.activePatient = JSON.parse(JSON.stringify(state.patients[id])); state.view = 'patient'; render(); };
window.handleScanInput = function(el) { handleScan(el.files); el.value=''; };

window.setField = function(key, val) {
  if (!state.activePatient) return;
  state.activePatient[key] = val;
};
window.setInv = function(inv, status) {
  state.activePatient.investigations[inv] = status;
  render();
};
window.toggleRef = function(i) {
  state.activePatient.references[i].cleared = !state.activePatient.references[i].cleared;
  render();
};
window.removeRef = function(i) {
  state.activePatient.references.splice(i,1);
  render();
};
window.addRef = function(dept) {
  if (!state.activePatient.references) state.activePatient.references = [];
  state.activePatient.references.push({dept, cleared:false});
  render();
};
window.addRefCustom = function() {
  const val = document.getElementById('newRefInput')?.value?.trim();
  if (val) { addRef(val); }
};
window._selectedDevice = '';
window.selectDevice = function(d) { window._selectedDevice = d; render(); };
window.addDevice = function() {
  const days = document.getElementById('devDays')?.value || '0';
  if (!window._selectedDevice) return;
  if (!state.activePatient.devices) state.activePatient.devices = [];
  state.activePatient.devices.push({type: window._selectedDevice, days});
  window._selectedDevice = '';
  render();
};
window.removeDevice = function(i) {
  state.activePatient.devices.splice(i,1);
  render();
};
window.addInstr = function() {
  const val = document.getElementById('newInstrInput')?.value?.trim();
  if (!val) return;
  if (!state.activePatient.facultyInstructions) state.activePatient.facultyInstructions = [];
  state.activePatient.facultyInstructions.push({text:val, time:new Date().toLocaleString('en-IN',{day:'2-digit',month:'short',hour:'2-digit',minute:'2-digit'})});
  render();
};
window.removeInstr = function(i) {
  state.activePatient.facultyInstructions.splice(i,1);
  render();
};
window.toggleSec = function(id) {
  state.openSections[id] = state.openSections[id] === false ? true : false;
  render();
};
window.saveAndBack = function() {
  if (!state.activePatient) return;
  savePatient(state.activePatient);
  state.view = 'ward';
  render();
};
window.confirmDelete = function() {
  if (confirm('Delete this patient?')) {
    deletePatient(state.activePatient.id);
    state.activePatient = null;
    state.view = 'ward';
    render();
  }
};

// ─── INIT ─────────────────────────────────────────────────────────
render();
</script>
</body>
</html>
