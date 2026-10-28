<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>EDUNEXUS School Manager</title>
<style>
:root{
  --bg:#F2F5F9;--surface:#FFFFFF;--ink:#16233A;--muted:#58677D;--line:#DCE3EC;
  --side:#14213D;--side-ink:#E6ECF7;--side-muted:#9FB0CC;
  --accent:#F5B700;--accent-ink:#2A2000;--focus:#2457D6;
  --ok:#1B7F52;--bad:#C0322B;--late:#A15F00;--hover:#EEF3FA;
  --rule:#D3E2F4;--margin:#F0A39C;
  --shadow:0 1px 2px rgba(20,33,61,.06),0 8px 24px rgba(20,33,61,.07);
  --head:'Bricolage Grotesque','Segoe UI',system-ui,sans-serif;
  --body:'Public Sans','Segoe UI',system-ui,sans-serif;
  box-sizing:border-box;
  padding-top:env(safe-area-inset-top,0px);
  padding-bottom:env(safe-area-inset-bottom,0px);
}
@media (prefers-color-scheme:dark){
  :root:not([data-theme="light"]){
    --bg:#0E1626;--surface:#16233A;--ink:#E8EDF5;--muted:#9AA8BD;--line:#26354F;
    --side:#0A111E;--hover:#1C2C47;--rule:#26405F;--margin:#8A4A4A;--focus:#7AA2FF;
    --ok:#4CC38A;--bad:#FF8076;--late:#F0B24A;
    --shadow:0 1px 2px rgba(0,0,0,.3),0 8px 24px rgba(0,0,0,.3);
  }
}
:root[data-theme="dark"]{
  --bg:#0E1626;--surface:#16233A;--ink:#E8EDF5;--muted:#9AA8BD;--line:#26354F;
  --side:#0A111E;--hover:#1C2C47;--rule:#26405F;--margin:#8A4A4A;--focus:#7AA2FF;
  --ok:#4CC38A;--bad:#FF8076;--late:#F0B24A;
  --shadow:0 1px 2px rgba(0,0,0,.3),0 8px 24px rgba(0,0,0,.3);
}
*,*::before,*::after{box-sizing:inherit}
html{scroll-padding-top:env(safe-area-inset-top,0px);-webkit-text-size-adjust:100%}
body{margin:0;background:var(--bg);color:var(--ink);font:400 16px/1.5 var(--body)}
h1,h2,h3{font-family:var(--head);margin:0;line-height:1.15;letter-spacing:-.01em}
h1{font-size:clamp(1.7rem,3vw,2.2rem);font-weight:800}
h2{font-size:1.2rem;font-weight:600}
h3{font-size:1rem;font-weight:600;margin:1.4rem 0 .5rem}
p{margin:0}
button,input,select,textarea{font:inherit;color:inherit}
:focus-visible{outline:3px solid var(--focus);outline-offset:2px}
.mut{color:var(--muted)}
.bad{color:var(--bad);font-weight:600}
.r{text-align:right}
small{font-size:.82rem}

/* shell */
.app{display:grid;grid-template-columns:240px minmax(0,1fr);
  min-height:calc(100vh - env(safe-area-inset-top,0px) - env(safe-area-inset-bottom,0px))}
.side{background:var(--side);color:var(--side-ink)}
.side-in{position:sticky;top:env(safe-area-inset-top,0px);display:flex;flex-direction:column;gap:1.25rem;padding:1.25rem .9rem}
.brand{display:flex;align-items:center;gap:.7rem;padding:0 .35rem}
.brand .mark{flex:none;width:40px;height:40px;border-radius:10px;background:var(--accent);color:var(--accent-ink);display:grid;place-items:center}
.brand strong{display:block;font:800 1.05rem/1.15 var(--head)}
.brand small{color:var(--side-muted)}
#nav{display:flex;flex-direction:column;gap:2px}
#nav button{display:flex;align-items:center;gap:.7rem;width:100%;padding:.6rem .7rem;border:0;border-radius:8px;background:transparent;color:var(--side-muted);font-weight:500;cursor:pointer;text-align:left;border-left:3px solid transparent}
#nav button:hover{background:rgba(255,255,255,.07);color:var(--side-ink)}
#nav button[aria-current="page"]{background:rgba(255,255,255,.1);color:#fff;border-left-color:var(--accent)}
#nav svg{width:20px;height:20px;flex:none;fill:none;stroke:currentColor;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round}
.side-foot{font-size:.8rem;color:var(--side-muted);padding:0 .35rem;display:grid;gap:.35rem}
.side-foot b{color:var(--side-ink);font-weight:600}
main{padding:1.75rem clamp(1rem,3vw,2.5rem) 4rem;max-width:1200px;width:100%}
main:focus{outline:none}

/* page header */
.ph{display:flex;flex-wrap:wrap;gap:1rem;align-items:flex-end;justify-content:space-between;margin-bottom:1.25rem}
.ph .sub{color:var(--muted);margin-top:.35rem}
.ph-act{display:flex;flex-wrap:wrap;gap:.5rem;align-items:center}

/* controls */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:.4rem;min-height:40px;padding:.5rem .95rem;border:1px solid var(--line);border-radius:8px;background:var(--surface);color:var(--ink);font-weight:600;cursor:pointer}
.btn:hover{background:var(--hover)}
.btn.pri{background:var(--accent);border-color:var(--accent);color:var(--accent-ink)}
.btn.pri:hover{filter:brightness(.95)}
.btn.dan{background:var(--bad);border-color:var(--bad);color:#fff}
.btn.sm{min-height:34px;padding:.3rem .7rem;font-size:.9rem}
.btn:disabled{opacity:.5;cursor:not-allowed}
.link{border:0;background:none;padding:0;font-weight:600;color:var(--ink);cursor:pointer;text-align:left;text-decoration:underline;text-decoration-color:var(--line);text-underline-offset:3px}
.link:hover{text-decoration-color:var(--ink)}
input,select,textarea{width:100%;min-height:40px;padding:.45rem .65rem;border:1px solid var(--line);border-radius:8px;background:var(--surface)}
textarea{resize:vertical}
select{width:auto;max-width:100%}
.tools{display:flex;flex-wrap:wrap;gap:.6rem;margin-bottom:1rem}
.tools input[type=search]{flex:1 1 260px;width:auto}
.check{display:inline-flex;align-items:center;gap:.5rem;min-height:40px}
.check input{width:18px;height:18px;min-height:0}
.row{display:flex;flex-wrap:wrap;gap:.5rem;align-items:center}

/* tables */
.tw{overflow-x:auto;background:var(--surface);border:1px solid var(--line);border-radius:12px}
.tbl{width:100%;border-collapse:collapse;min-width:560px}
.tbl th{padding:.7rem .9rem;text-align:left;font-size:.82rem;font-weight:600;color:var(--muted);border-bottom:1px solid var(--line);white-space:nowrap}
.tbl td{padding:.65rem .9rem;border-bottom:1px solid var(--line);vertical-align:middle}
.tbl tr:last-child td{border-bottom:0}
.tbl th.r,.tbl td.r{text-align:right}
.tbl tbody tr:hover{background:var(--hover)}
.tbl td,.tbl th{font-variant-numeric:tabular-nums}
.owe{color:var(--bad);font-weight:600}
.tag{display:inline-block;padding:.1rem .55rem;border-radius:99px;border:1px solid var(--line);font-size:.8rem;color:var(--muted)}

/* panels, empty, facts */
.panel{background:var(--surface);border:1px solid var(--line);border-radius:12px;padding:1.25rem;margin-bottom:1.25rem}
.panel>h2{margin-bottom:.9rem}
.empty,.start{background:var(--surface);border:1px dashed var(--line);border-radius:12px;padding:2rem 1.25rem;text-align:center;display:grid;gap:.6rem;justify-items:center}
.empty p,.start p{color:var(--muted);max-width:46ch}
.start{border-style:solid;box-shadow:var(--shadow);padding:2.5rem 1.25rem}
.facts{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:1px;background:var(--line);border:1px solid var(--line);border-radius:12px;overflow:hidden;margin-bottom:1.5rem}
.fact{background:var(--surface);padding:.9rem 1rem}
.fact span{display:block;font-size:.82rem;color:var(--muted)}
.fact b{display:block;font:800 1.55rem/1.2 var(--head);margin-top:.15rem;font-variant-numeric:tabular-nums}
.fact small{color:var(--muted)}
.cols{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:1.25rem;align-items:start}
.list{list-style:none;margin:0;padding:0}
.list li{display:flex;justify-content:space-between;gap:1rem;align-items:center;padding:.65rem 0;border-bottom:1px solid var(--line)}
.list li:last-child{border-bottom:0}
.list .t{font-weight:600}
.notice{padding:.7rem 0;border-bottom:1px solid var(--line)}
.notice:last-child{border-bottom:0}
.notice p{color:var(--muted);margin-top:.2rem;white-space:pre-wrap}

/* classes */
.cgrid{display:grid;grid-template-columns:repeat(auto-fill,minmax(270px,1fr));gap:1rem}
.ccard{background:var(--surface);border:1px solid var(--line);border-radius:12px;padding:1.1rem;display:grid;gap:.7rem;align-content:start}
.chips{display:flex;flex-wrap:wrap;gap:.35rem}
.chip{padding:.1rem .6rem;border-radius:6px;background:var(--hover);font-size:.85rem}

/* tabs */
.tabs{display:flex;gap:.25rem;border-bottom:1px solid var(--line);margin-bottom:1.1rem}
.tabs button{border:0;background:none;padding:.6rem .9rem;font-weight:600;color:var(--muted);cursor:pointer;border-bottom:3px solid transparent;margin-bottom:-1px}
.tabs button[aria-selected="true"]{color:var(--ink);border-bottom-color:var(--accent)}

/* register: the one memorable thing */
.regbar{display:flex;flex-wrap:wrap;gap:.6rem;align-items:center;justify-content:space-between;margin-bottom:.9rem}
.counts{display:flex;flex-wrap:wrap;gap:1rem;font-size:.92rem}
.counts b{font-variant-numeric:tabular-nums}
.register{position:relative;background:var(--surface);border:1px solid var(--line);border-radius:12px;overflow:hidden;box-shadow:var(--shadow)}
.register::before{content:"";position:absolute;top:0;bottom:0;left:3.4rem;width:2px;background:var(--margin);opacity:.85}
.reg-row{display:grid;grid-template-columns:3.4rem 1fr auto;align-items:center;min-height:3.4rem;border-bottom:1px solid var(--rule);padding-right:.75rem}
.reg-row:last-child{border-bottom:0}
.reg-row .no{text-align:center;color:var(--muted);font-size:.85rem;font-variant-numeric:tabular-nums}
.reg-row .nm{padding:.5rem .9rem;font-weight:500;min-width:0;overflow-wrap:anywhere}
.marks{display:flex;gap:.4rem}
.mk{width:2.6rem;height:2.6rem;border-radius:50%;border:2px solid var(--line);background:transparent;color:var(--muted);font:700 .95rem var(--head);cursor:pointer}
.mk:hover:not(:disabled){border-color:var(--muted)}
.mk:disabled{cursor:default}
.mk.p[aria-pressed="true"]{background:var(--ok);border-color:var(--ok);color:#fff}
.mk.a[aria-pressed="true"]{background:var(--bad);border-color:var(--bad);color:#fff}
.mk.l[aria-pressed="true"]{background:var(--late);border-color:var(--late);color:#fff}
:root[data-theme="dark"] .mk[aria-pressed="true"]{color:#0E1626}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]) .mk[aria-pressed="true"]{color:#0E1626}}
.legend{display:flex;gap:1rem;flex-wrap:wrap;font-size:.85rem;color:var(--muted);margin:.7rem 0 0}

/* grades */
.split{display:grid;grid-template-columns:260px minmax(0,1fr);gap:1.25rem;align-items:start}
.alist{display:grid;gap:.4rem}
.alist button{text-align:left;padding:.7rem .8rem;border:1px solid var(--line);border-radius:10px;background:var(--surface);cursor:pointer;display:grid;gap:.1rem}
.alist button[aria-current="true"]{border-color:var(--ink);box-shadow:inset 3px 0 0 var(--accent)}
.alist small{color:var(--muted)}
.score{width:6.5rem;text-align:right}
.bulk-grade-meta{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:.8rem}
.bulk-grade-grid{max-height:min(52vh,540px);overflow:auto;border:1px solid var(--line);border-radius:10px}
.bulk-grade-grid .tbl{min-width:max-content;margin:0}
.bulk-grade-grid .tbl th{position:sticky;top:0;z-index:1;background:var(--surface)}
.bulk-grade-grid .tbl td:first-child,.bulk-grade-grid .tbl th:first-child{position:sticky;left:0;background:var(--surface);z-index:2}
.bulk-grade-grid .tbl th:first-child{z-index:3}
.bulk-score{width:5.5rem;min-width:5.5rem;text-align:right}
dialog.wide{width:min(1120px,calc(100vw - 1.5rem))}
@media (max-width:700px){.bulk-grade-meta{grid-template-columns:1fr}.bulk-score{width:4.5rem;min-width:4.5rem}}

/* forms and dialog */
.fields{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:.9rem}
.fields.grid2{grid-template-columns:repeat(auto-fit,minmax(220px,1fr))}
.fld{display:grid;gap:.3rem;font-weight:600;font-size:.92rem;align-content:start}
.fld i{font-weight:400;color:var(--muted);font-style:normal}
.fld.wide{grid-column:1/-1}
dialog{border:0;border-radius:14px;padding:0;background:var(--surface);color:var(--ink);width:min(640px,calc(100vw - 1.5rem));max-height:calc(100vh - 2rem);box-shadow:0 20px 60px rgba(0,0,0,.35)}
dialog::backdrop{background:rgba(10,17,30,.55)}
#dlg-body{padding:1.4rem;display:grid;gap:1rem}
.dact{display:flex;justify-content:flex-end;gap:.5rem;flex-wrap:wrap;margin-top:.4rem}
.err{color:var(--bad);font-weight:600;min-height:1.2em}
.dhead{display:flex;gap:.9rem;align-items:center}
.avatar{width:52px;height:52px;border-radius:50%;background:var(--accent);color:var(--accent-ink);display:grid;place-items:center;font:800 1.1rem var(--head);flex:none}
.kv{display:grid;grid-template-columns:repeat(auto-fit,minmax(170px,1fr));gap:.7rem 1rem;margin:0}
.kv dt{font-size:.8rem;color:var(--muted)}
.kv dd{margin:0;font-weight:500}
.three{display:grid;grid-template-columns:repeat(3,1fr);gap:1px;background:var(--line);border:1px solid var(--line);border-radius:10px;overflow:hidden}
.three div{background:var(--surface);padding:.7rem .8rem}
.three span{display:block;font-size:.8rem;color:var(--muted)}
.three b{font:800 1.25rem var(--head)}

#toast{position:fixed;left:50%;bottom:calc(1.25rem + env(safe-area-inset-bottom,0px));transform:translate(-50%,20px);background:var(--ink);color:var(--bg);padding:.65rem 1rem;border-radius:10px;font-weight:600;opacity:0;pointer-events:none;transition:opacity .2s,transform .2s;z-index:50;max-width:calc(100vw - 2rem)}
#toast.show{opacity:1;transform:translate(-50%,0)}
#toast.err{background:var(--bad);color:#fff}
.banner{background:var(--hover);border:1px solid var(--line);border-radius:10px;padding:.6rem .9rem;margin-bottom:1rem;font-size:.92rem}
.skel{height:14px;border-radius:7px;background:var(--line);margin:.6rem 0}
.ro .w{display:none!important}
.staff .w:not(.sw){display:none!important}
#nav button[hidden]{display:none}
.fact[hidden],.panel[hidden]{display:none}
.app.gate{grid-template-columns:1fr}
.gate .side{display:none}
.gate main{max-width:none;margin:0 auto;display:grid;place-items:center;min-height:80vh}
.login{width:min(440px,100%);background:var(--surface);border:1px solid var(--line);border-radius:16px;box-shadow:var(--shadow);padding:1.75rem;display:grid;gap:1rem}
.login .lb{display:flex;align-items:center;gap:.7rem}
.login .lb .mark{width:44px;height:44px;border-radius:11px;background:var(--accent);color:var(--accent-ink);display:grid;place-items:center}
.pw{position:relative}
.pw input{padding-right:4.5rem}
.pw button{position:absolute;right:4px;top:4px;min-height:32px;padding:0 .7rem;border:0;background:none;font-weight:600;cursor:pointer;color:var(--muted)}

@media (max-width:900px){
  .app{grid-template-columns:1fr}
  .side-in{flex-direction:row;align-items:center;gap:.75rem;padding:.6rem .75rem;overflow-x:auto}
  .brand{flex:none}
  .brand small,.side-foot{display:none}
  #nav{flex-direction:row;gap:2px}
  #nav button{width:auto;white-space:nowrap;border-left:0;border-bottom:3px solid transparent;border-radius:8px 8px 0 0;padding:.5rem .7rem}
  #nav button[aria-current="page"]{border-bottom-color:var(--accent)}
  .split{grid-template-columns:1fr}
  .fields{grid-template-columns:1fr}
}
@media print{
  body{background:#fff!important;color:#111!important;font-size:11pt}
  .side,.ph-act,.tools,.w,button,.btn,#toast,.banner{display:none!important}
  .app{display:block!important}main{max-width:none!important;padding:0!important}
  .panel,.tw,.facts,.ccard{box-shadow:none!important;break-inside:avoid;border-color:#bbb!important}
  .tbl{min-width:0!important;font-size:9pt}.tbl th,.tbl td{padding:5px!important}
  .panel{margin-bottom:10px!important}
}
@media (prefers-reduced-motion:reduce){*{transition:none!important;animation:none!important}}
</style>
</head>
<body>
<div class="app" id="shell">
  <aside class="side">
    <div class="side-in">
      <div class="brand">
        <div class="mark" aria-hidden="true"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 6c-2-1.5-5-2-8-2v14c3 0 6 .5 8 2 2-1.5 5-2 8-2V4c-3 0-6 .5-8 2zM12 6v14"/></svg></div>
        <div><strong id="sname">School</strong><small id="sterm"></small></div>
      </div>
      <nav id="nav" aria-label="Main"></nav>
      <div class="side-foot" id="sfoot"></div>
    </div>
  </aside>
  <main id="main" tabindex="-1"><section style="max-width:760px;margin:48px auto;padding:24px;background:#fff;color:#16233A;border:1px solid #DCE3EC;border-radius:16px;font:16px/1.5 system-ui,sans-serif"><h1 style="margin-top:0">EDUNEXUS School Manager</h1><p>Starting the application…</p><p>If this message remains visible, JavaScript may be blocked or the application encountered a startup error. Refresh the page or open this file in a current version of Chrome or Edge.</p></section></main>
</div>
<dialog id="dlg"><div id="dlg-body"></div></dialog>
<div id="toast" role="status" aria-live="polite"></div>

<script src="./supabase-config.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<script>
window.addEventListener('error',function(ev){
  try{
    const m=document.getElementById('main');
    if(m){
      const msg=(ev&&ev.message)||'An unexpected startup error occurred.';
      m.innerHTML='<section style="max-width:820px;margin:32px auto;padding:24px;background:#fff;color:#16233A;border:1px solid #DCE3EC;border-radius:16px;font:16px/1.5 system-ui,sans-serif"><h1>EDUNEXUS could not start</h1><p>The page encountered a JavaScript error instead of loading the dashboard.</p><p><b>Error:</b> '+String(msg).replace(/[&<>"']/g,function(c){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]})+'</p><p>Try opening this file in an updated Chrome or Edge browser. Your saved school data has not been cleared by this diagnostic screen.</p><button onclick="location.reload()" style="padding:10px 16px;border:0;border-radius:8px;background:#2457D6;color:#fff;font-weight:600;cursor:pointer">Reload application</button></section>';
    }
  }catch(ignore){}
});
window.addEventListener('unhandledrejection',function(ev){
  try{const m=document.getElementById('main');if(m&&!m.textContent.trim())m.innerHTML='<section style="margin:32px auto;padding:24px;background:#fff;color:#16233A;border-radius:16px;font:16px/1.5 system-ui,sans-serif"><h1>EDUNEXUS could not finish loading</h1><p>A background operation failed. Reload the application and try again.</p></section>';}catch(ignore){}
});
(function(){
'use strict';

/* ---------- helpers ---------- */
const $=(s,r=document)=>r.querySelector(s);
const esc=s=>String(s==null?'':s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const pad=n=>String(n).padStart(2,'0');
const dstr=d=>d.getFullYear()+'-'+pad(d.getMonth()+1)+'-'+pad(d.getDate());
const todayStr=()=>dstr(new Date());
const fmtDate=s=>{if(!s)return '';const p=s.split('-').map(Number);return new Date(p[0],p[1]-1,p[2]).toLocaleDateString(undefined,{day:'numeric',month:'short',year:'numeric'})};
const byName=(a,b)=>(a.name||'').localeCompare(b.name||'');
const by=(arr,id)=>arr.find(x=>x.id===id);
const initials=n=>(n||'?').split(/\s+/).filter(Boolean).slice(0,2).map(w=>w[0].toUpperCase()).join('');
const plural=(n,w)=>n+' '+w+(n===1?'':'s');
const mean=a=>a.length?a.reduce((x,y)=>x+y,0)/a.length:null;
const genId=()=>Date.now().toString(36)+Math.random().toString(36).slice(2,8);
const letter=p=>p>=80?'A':p>=70?'B':p>=60?'C':p>=50?'D':p>=40?'E':'F';

/* ---------- state ---------- */
const COLS=['students','teachers','classes','attendance','grades','fees','notices','timetable','events','expenses'];
const S={students:[],teachers:[],classes:[],attendance:[],grades:[],fees:[],notices:[],timetable:[],events:[],expenses:[],
  settings:{schoolName:'My school',term:'Term 1',currency:'UGX',passMark:50},accounts:[]};
const ui={view:'overview',mode:'connecting',loaded:{},slow:false,canWrite:true,dl:null,busy:false,role:'admin',me:'',uid:null,access:[],profiles:{},share:'admin',acct:null,loginTab:'username',loginId:'',fails:0,lockUntil:0,gateDone:null,
  sq:'',sclass:'',attClass:'',attDate:todayStr(),attDraft:null,
  grClass:'',grTab:'assess',grAssess:'',grDraft:null,fq:'',fowing:false,
  authUser:null,schoolId:null,joinCode:'',authTab:'login',cloudReady:false,cloudStatus:'',authError:'',authGeneration:0};
const cls=id=>by(S.classes,id), stu=id=>by(S.students,id);
const className=id=>{const c=cls(id);return c?c.name:'No class'};
const money=n=>{const c=S.settings.currency||'';const v=Math.abs(Math.round(n*100)/100).toLocaleString();return (n<0?'\u2212':'')+c+(c.length>1&&!/\s$/.test(c)?' ':'')+v};

let _bm=null,_am=null;
function balMap(){if(_bm)return _bm;const m={};S.students.forEach(s=>m[s.id]={billed:0,paid:0,bal:0});
  for(const f of S.fees){const a=+f.amount||0;
    if(f.kind==='charge'){(f.studentIds||[]).forEach(id=>{if(m[id])m[id].billed+=a})}
    else if(f.kind==='payment'&&m[f.studentId])m[f.studentId].paid+=a}
  for(const k in m)m[k].bal=m[k].billed-m[k].paid;return _bm=m}
function attMap(){if(_am)return _am;const m={};
  for(const a of S.attendance)for(const k in (a.marks||{})){const v=a.marks[k];const r=m[k]||(m[k]={p:0,a:0,l:0});
    if(v==='P')r.p++;else if(v==='A')r.a++;else if(v==='L')r.l++}
  return _am=m}
const attPct=r=>{if(!r)return null;const t=r.p+r.a+r.l;return t?Math.round((r.p+r.l)/t*100):null};
function subjAvgs(sid){const acc={};
  for(const g of S.grades){const n=g.scores&&g.scores[sid];
    if(Number.isFinite(n)&&g.max>0)(acc[g.subject]=acc[g.subject]||[]).push(Math.min(100,n/g.max*100))}
  const out={};for(const k in acc)out[k]=mean(acc[k]);return out}

/* ---------- storage backends ---------- */
const LS_KEY='school-manager-v1';
function lsLoad(){try{const j=JSON.parse(localStorage.getItem(LS_KEY)||'null');
  if(j){COLS.forEach(c=>S[c]=j[c]||[]);S.accounts=j.accounts||[];if(j.settings)Object.assign(S.settings,j.settings)}}catch(e){}}
function lsSave(){try{localStorage.setItem(LS_KEY,JSON.stringify(S))}catch(e){}}
const localBackend={
  async put(col,obj){const id=obj.id||genId();const rec=Object.assign({},obj,{id});const i=S[col].findIndex(x=>x.id===id);
    if(i>=0)S[col][i]=rec;else S[col].push(rec);lsSave();scheduleRender();return id},
  async remove(col,id){S[col]=S[col].filter(x=>x.id!==id);lsSave();scheduleRender()},
  async saveSettings(v){Object.assign(S.settings,v);lsSave();scheduleRender()},
  async wipe(){COLS.forEach(c=>S[c]=[]);lsSave();scheduleRender()}
};
let supabaseClient=null;
let realtimeChannel=null;
let backend=localBackend;
let userNs=null;
const cloudCollections=new Set(COLS);
const defaultSchoolSettings={schoolName:'My school',term:'Term 1',currency:'UGX',passMark:50};
function unwrapSupabase(result){if(result&&result.error)throw result.error;return result?result.data:null}
function clearCloudData(){COLS.forEach(c=>{S[c]=[];ui.loaded[c]=true});S.accounts=[];ui.loaded.accounts=true;Object.assign(S.settings,defaultSchoolSettings);ui.schoolId=null;ui.joinCode='';ui.canWrite=false;}
function memberToAccount(m){return {id:m.user_id,name:m.display_name||m.email||'School user',username:m.username||'',email:m.email||'',role:m.role||'teacher',disabled:!!m.disabled,createdAt:m.created_at?Date.parse(m.created_at):Date.now()}}
function supabaseBackend(client){
  let schoolId=null;
  async function refreshCollection(col){
    if(!cloudCollections.has(col)||!schoolId)return;
    const {data,error}=await client.from('school_records').select('record_id,data').eq('school_id',schoolId).eq('collection',col).order('created_at',{ascending:true});
    if(error)throw error;
    S[col]=(data||[]).map(r=>Object.assign({},r.data||{},{id:r.record_id}));ui.loaded[col]=true;scheduleRender();
  }
  async function refreshMembers(){
    if(!schoolId)return;
    const {data,error}=await client.from('school_memberships').select('user_id,display_name,username,email,role,disabled,created_at').eq('school_id',schoolId).order('created_at',{ascending:true});
    if(error)throw error;
    S.accounts=(data||[]).map(memberToAccount);ui.loaded.accounts=true;
    const own=S.accounts.find(a=>ui.authUser&&a.id===ui.authUser.id);
    if(own){ui.acct=own;ui.role=own.role;ui.share=own.role;ui.canWrite=!own.disabled&&own.role!=='viewer';}
    scheduleRender();
  }
  async function refreshSettings(){
    if(!schoolId)return;
    const {data,error}=await client.from('school_settings').select('data').eq('school_id',schoolId).maybeSingle();
    if(error)throw error;
    if(data&&data.data)Object.assign(S.settings,defaultSchoolSettings,data.data);
    scheduleRender();
  }
  async function start(id){
    schoolId=id;ui.schoolId=id;ui.loaded={};COLS.forEach(c=>ui.loaded[c]=false);ui.loaded.accounts=false;
    if(realtimeChannel){try{await client.removeChannel(realtimeChannel)}catch(e){}realtimeChannel=null;}
    await Promise.all([...COLS.map(refreshCollection),refreshMembers(),refreshSettings()]);
    if(ui.role==='admin'){
      try{const {data,error}=await client.rpc('get_school_join_code');if(error)throw error;ui.joinCode=data||'';}catch(e){console.warn('Could not load school join code',e);ui.joinCode='';}
    } else ui.joinCode='';
    realtimeChannel=client.channel('edunexus-school-'+id)
      .on('postgres_changes',{event:'*',schema:'public',table:'school_records',filter:'school_id=eq.'+id},payload=>{
        const col=(payload.new&&payload.new.collection)||(payload.old&&payload.old.collection);
        if(cloudCollections.has(col))refreshCollection(col).catch(dbErr);
      })
      .on('postgres_changes',{event:'*',schema:'public',table:'school_settings',filter:'school_id=eq.'+id},()=>refreshSettings().catch(dbErr))
      .on('postgres_changes',{event:'*',schema:'public',table:'school_memberships',filter:'school_id=eq.'+id},()=>refreshMembers().catch(dbErr))
      .subscribe(status=>{ui.cloudStatus=status;if(status==='SUBSCRIBED')ui.cloudReady=true;scheduleRender();});
    ui.cloudReady=true;scheduleRender();
  }
  return {
    start,
    async put(col,obj){
      if(col==='accounts'){
        if(!obj.id)throw new Error('New accounts must register and join with the school code first.');
        const {data,error}=await client.rpc('admin_update_member',{p_user_id:obj.id,p_display_name:obj.name||null,p_username:obj.username||null,p_role:obj.role||'teacher',p_disabled:!!obj.disabled});
        if(error)throw error;await refreshMembers();return obj.id;
      }
      if(!cloudCollections.has(col))throw new Error('Unsupported data section: '+col);
      const id=obj.id||genId();const rec=Object.assign({},obj,{id});
      const {error}=await client.from('school_records').upsert({school_id:schoolId,collection:col,record_id:id,data:rec},{onConflict:'school_id,collection,record_id'});
      if(error)throw error;await refreshCollection(col);return id;
    },
    async remove(col,id){
      if(col==='accounts'){
        const {error}=await client.rpc('admin_remove_member',{p_user_id:id});if(error)throw error;await refreshMembers();return;
      }
      if(!cloudCollections.has(col))throw new Error('Unsupported data section: '+col);
      const {error}=await client.from('school_records').delete().eq('school_id',schoolId).eq('collection',col).eq('record_id',id);
      if(error)throw error;await refreshCollection(col);
    },
    async saveSettings(v){
      const merged=Object.assign({},S.settings,v);
      const {data,error}=await client.from('school_settings').update({data:merged,updated_at:new Date().toISOString()}).eq('school_id',schoolId).select('school_id').maybeSingle();
      if(error)throw error;if(!data)throw new Error('No settings row was updated. Check administrator access.');
      Object.assign(S.settings,merged);scheduleRender();
    },
    async wipe(){
      const {error}=await client.from('school_records').delete().eq('school_id',schoolId);
      if(error)throw error;await Promise.all(COLS.map(refreshCollection));
    },
    async refreshMembers(){return refreshMembers();},
    async stop(){if(realtimeChannel){try{await client.removeChannel(realtimeChannel)}catch(e){}realtimeChannel=null;}}
  };
}
async function loadProfiles(){
  if(!userNs)return;
  const ids=ui.access.map(a=>a.id).filter(i=>!(i in ui.profiles));
  if(!ids.length)return;
  try{const ps=await userNs.profiles(ids);ids.forEach(i=>{ui.profiles[i]=(ps&&ps[i]&&ps[i].name)||''});scheduleRender()}catch(e){}
}
function dbErr(e){if(e&&e.code==='revoked'){ui.canWrite=false;scheduleRender()}else if(window.console)console.warn('db',e)}
const errMsg=e=>e&&e.code==='quota_exceeded'?'Storage is full. Delete some records and try again.':
  e&&(e.code==='42501'||e.code==='PGRST301'||e.status===401||e.status===403)?'You do not have permission to change this data. Check your account role.':
  (e&&e.message?String(e.message):'Couldn’t save. Check your connection and try again.');
async function run(fn,okMsg){
  if(!ui.canWrite){toast('You have view-only access.',true);return false}
  try{await fn();if(okMsg)toast(okMsg);return true}
  catch(e){if(e&&e.code==='invalid_argument'&&ui.mode==='shared'){ui.canWrite=false;scheduleRender()}toast(errMsg(e),true);return false}
}

/* ---------- ui primitives ---------- */
let toastT=0;
function toast(msg,isErr){const t=$('#toast');t.textContent=msg;t.className='show'+(isErr?' err':'');clearTimeout(toastT);toastT=setTimeout(()=>{t.className=''},3600)}
function dlg(html){$('#dlg-body').innerHTML=html;const d=$('#dlg');if(!d.open)d.showModal()}
function closeDlg(){const d=$('#dlg');if(d.open)d.close();d.classList.remove('wide')}
let pend=null;
function confirmBox(title,msg,label){
  return new Promise(res=>{pend=res;
    dlg(`<h2>${esc(title)}</h2><p>${esc(msg)}</p><div class="dact"><button type="button" class="btn" data-act="c-no">Cancel</button><button type="button" class="btn dan" data-act="c-yes">${esc(label||'Delete')}</button></div>`);
    setTimeout(()=>{const b=$('[data-act="c-no"]');if(b)b.focus()},30)});
}
function fieldHtml(f,v){
  const id='f-'+f.name;const val=v!==undefined&&v!==null?v:(f.def!==undefined?f.def:'');let ctl;
  if(f.type==='select')ctl=`<select id="${id}">${f.options.map(o=>`<option value="${esc(o.v)}"${String(o.v)===String(val)?' selected':''}>${esc(o.l)}</option>`).join('')}</select>`;
  else if(f.type==='textarea')ctl=`<textarea id="${id}" rows="4">${esc(val)}</textarea>`;
  else ctl=`<input id="${id}" type="${f.type||'text'}" value="${esc(val)}"${f.min!==undefined?` min="${f.min}"`:''}${f.max!==undefined?` max="${f.max}"`:''}${f.type==='number'?' step="any" inputmode="decimal"':''}${f.placeholder?` placeholder="${esc(f.placeholder)}"`:''}>`;
  return `<label class="fld${f.wide?' wide':''}" for="${id}"><span>${esc(f.label)}${f.required?'':' <i>(optional)</i>'}</span>${ctl}</label>`;
}
function formDialog(o){
  const vals=o.values||{};
  dlg(`<form id="frm" novalidate style="display:grid;gap:1rem"><h2>${esc(o.title)}</h2>${o.note?`<p class="mut">${esc(o.note)}</p>`:''}<div class="fields">${o.fields.map(f=>fieldHtml(f,vals[f.name])).join('')}</div><p class="err" id="frm-err" role="alert"></p><div class="dact"><button type="button" class="btn" data-act="close">Cancel</button><button class="btn pri" type="submit" id="frm-ok">${esc(o.submit||'Save')}</button></div></form>`);
  $('#frm').onsubmit=async e=>{
    e.preventDefault();const out={};
    for(const f of o.fields){const el=$('#f-'+f.name);let v=el.value;if(typeof v==='string')v=v.trim();
      if(f.type==='number'){v=v===''?'':Number(v)}
      const blank=v===''||(f.type==='number'&&!Number.isFinite(v));
      if(f.required&&blank){$('#frm-err').textContent=f.label+' is required.';el.focus();return}
      if(f.type==='number'&&!blank&&f.min!==undefined&&v<f.min){$('#frm-err').textContent=f.label+' must be at least '+f.min+'.';el.focus();return}
      out[f.name]=v}
    const b=$('#frm-ok');b.disabled=true;const ok=await o.onSave(out);
    if(ok!==false)closeDlg();else if(b)b.disabled=false;
  };
  setTimeout(()=>{const f=$('#frm input,#frm select,#frm textarea');if(f)f.focus()},30);
}
const btn=(label,act,o)=>{o=o||{};return `<button type="button" class="btn${o.pri?' pri':''}${o.dan?' dan':''}${o.sm?' sm':''}${o.w?' w':''}${o.sw?' sw':''}" data-act="${act}"${o.id!==undefined?` data-id="${esc(o.id)}"`:''}${o.extra||''}${o.dis?' disabled':''}>${label}</button>`};
const head=(t,sub,actions)=>`<header class="ph"><div><h1>${esc(t)}</h1>${sub?`<p class="sub">${esc(sub)}</p>`:''}</div><div class="ph-act">${actions||''}</div></header>`;
const note=(t,sub,actions)=>`<div class="empty"><h2>${esc(t)}</h2>${sub?`<p>${esc(sub)}</p>`:''}${actions?`<div class="row">${actions}</div>`:''}</div>`;
const needClass=()=>note('Add a class first','Attendance, grades and student records are organised by class.',btn('Add a class','class-new',{pri:1,w:1}));
const classOptions=(sel,blank)=>(blank?`<option value="">${esc(blank)}</option>`:'')+S.classes.slice().sort(byName).map(c=>`<option value="${esc(c.id)}"${c.id===sel?' selected':''}>${esc(c.name)}</option>`).join('');
const nextAdm=()=>{const n=S.students.map(s=>parseInt(String(s.admNo||'').replace(/\D/g,''),10)).filter(Number.isFinite);return pad(Math.max(0,...n)+1).padStart(3,'0')};

/* ---------- views ---------- */
function vOverview(){
  const t=todayStr(),st=S.settings;
  const sub=(st.term?st.term+', ':'')+new Date().toLocaleDateString(undefined,{weekday:'long',day:'numeric',month:'long'});
  if(!S.students.length&&!S.classes.length&&!S.teachers.length){
    return head(st.schoolName,sub)+`<section class="start"><h2>Set up your school</h2><p>Create your classes first, then enrol students and teachers. Or load sample data to look around; you can clear it from Settings.</p><div class="row">${btn('Add a class','class-new',{pri:1,w:1})}${btn('Load sample data','sample',{w:1})}</div>${ui.canWrite?'':'<p>No records yet. The school administrator can set things up.</p>'}</section>`;
  }
  let present=0,total=0;
  S.attendance.filter(a=>a.date===t).forEach(r=>Object.values(r.marks||{}).forEach(v=>{total++;if(v==='P'||v==='L')present++}));
  const bm=balMap();let billed=0,paid=0,owed=0;
  S.students.forEach(s=>{const b=bm[s.id];billed+=b.billed;paid+=b.paid;if(b.bal>0)owed+=b.bal});
  const facts=`<div class="facts">
    <div class="fact"><span>Students</span><b>${S.students.length}</b></div>
    <div class="fact"><span>Teachers</span><b>${S.teachers.length}</b></div>
    <div class="fact"><span>Classes</span><b>${S.classes.length}</b></div>
    <div class="fact"><span>Present today</span><b>${total?present+' of '+total:'None taken'}</b></div>
    <div class="fact"${ui.role!=='admin'?' hidden':''}><span>Fees collected</span><b>${money(paid)}</b>${billed?`<small>of ${money(billed)} billed</small>`:''}</div>
    <div class="fact"${ui.role!=='admin'?' hidden':''}><span>Fees outstanding</span><b>${money(owed)}</b></div></div>`;
  const regs=S.classes.slice().sort(byName).map(c=>{
    const r=S.attendance.find(a=>a.id===c.id+'_'+t);
    let status;
    if(r){const v=Object.values(r.marks||{});const p=v.filter(x=>x==='P'||x==='L').length;status=`<span>${p} of ${v.length} present</span>`}
    else status=`<span class="mut">Not taken</span>`;
    return `<li><span class="t">${esc(c.name)}</span><span class="row">${status}${btn(r?'View':'Take register','goto-att',{id:c.id,sm:1})}</span></li>`}).join('');
  const notices=S.notices.slice().sort((a,b)=>(b.date||'').localeCompare(a.date||'')).slice(0,3).map(n=>`<div class="notice"><b>${esc(n.title)}</b> <small class="mut">${fmtDate(n.date)}</small><p>${esc((n.body||'').slice(0,160))}${(n.body||'').length>160?'…':''}</p></div>`).join('');
  const owing=S.students.filter(s=>bm[s.id].bal>0).sort((a,b)=>bm[b.id].bal-bm[a.id].bal).slice(0,5)
    .map(s=>`<li><span><button class="link" data-act="stu-open" data-id="${esc(s.id)}">${esc(s.name)}</button> <small class="mut">${esc(className(s.classId))}</small></span><span class="owe">${money(bm[s.id].bal)}</span></li>`).join('');
  return head(st.schoolName,sub)+facts+`<div class="cols">
    <section class="panel"><h2>Today\u2019s registers</h2>${regs?`<ul class="list">${regs}</ul>`:'<p class="mut">Add a class to start taking registers.</p>'}</section>
    <section class="panel"><h2>Notices</h2>${notices||'<p class="mut">No notices posted yet.</p>'}<div class="row" style="margin-top:.8rem">${btn('All notices','nav',{sm:1,extra:' data-view="notices"'})}</div></section>
    <section class="panel"${ui.role!=='admin'?' hidden':''}><h2>Largest fee balances</h2>${owing?`<ul class="list">${owing}</ul>`:'<p class="mut">No outstanding balances.</p>'}</section></div>`;
}

function vStudents(){
  const q=ui.sq.trim().toLowerCase(),am=attMap(),bm=balMap();
  const rows=S.students.filter(s=>(!ui.sclass||s.classId===ui.sclass)&&(!q||[s.name,s.admNo,s.guardian].join(' ').toLowerCase().includes(q))).sort(byName);
  const tools=`<div class="tools"><input id="sq" type="search" data-in="sq" placeholder="Search by name, admission no. or guardian" value="${esc(ui.sq)}" aria-label="Search students"><select data-in="sclass" aria-label="Filter by class">${classOptions(ui.sclass,'All classes')}</select></div>`;
  let table;
  if(!S.students.length)table=note('No students yet','Enrol your first student to start tracking attendance, grades and fees.',btn('Add student','stu-new',{pri:1,w:1}));
  else if(!rows.length)table=note('No matches','Try a different search or class.');
  else table=`<div class="tw"><table class="tbl"><thead><tr><th>Adm. no.</th><th>Student</th><th>Class</th><th>Guardian</th><th class="r">Attendance</th>${ui.role==='admin'?'<th class="r">Fee balance</th>':''}</tr></thead><tbody>${rows.map(s=>{
    const p=attPct(am[s.id]),b=bm[s.id];
    return `<tr><td>${esc(s.admNo)}</td><td><button class="link" data-act="stu-open" data-id="${esc(s.id)}">${esc(s.name)}</button></td><td>${esc(className(s.classId))}</td><td>${esc(s.guardian||'')}${s.phone?` <small class="mut">${esc(s.phone)}</small>`:''}</td><td class="r">${p===null?'<span class="mut">No data</span>':`<span class="${p<75?'bad':''}">${p}%</span>`}</td>${ui.role==='admin'?`<td class="r ${b.bal>0?'owe':''}">${b.billed===0?'<span class="mut">Not billed</span>':b.bal>0?money(b.bal):'Paid up'}</td>`:''}</tr>`}).join('')}</tbody></table></div>`;
  return head('Students',plural(S.students.length,'student')+' enrolled',btn('Add student','stu-new',{pri:1,w:1}))+tools+table;
}

function vTeachers(){
  const rows=S.teachers.slice().sort(byName);
  const table=!rows.length?note('No teachers yet','Add teachers so you can assign them to classes.',btn('Add teacher','tea-new',{pri:1,w:1})):
  `<div class="tw"><table class="tbl"><thead><tr><th>Name</th><th>Subject</th><th>Contact</th><th>Class teacher of</th><th></th></tr></thead><tbody>${rows.map(t=>{
    const cs=S.classes.filter(c=>c.teacherId===t.id).map(c=>c.name).join(', ');
    return `<tr><td><b>${esc(t.name)}</b></td><td>${esc(t.subject||'')}</td><td>${esc([t.phone,t.email].filter(Boolean).join(', '))}</td><td>${esc(cs)||'<span class="mut">None</span>'}</td><td class="r"><span class="row w" style="justify-content:flex-end">${btn('Edit','tea-edit',{id:t.id,sm:1})}${btn('Delete','tea-del',{id:t.id,sm:1})}</span></td></tr>`}).join('')}</tbody></table></div>`;
  return head('Teachers',plural(S.teachers.length,'teacher'),btn('Add teacher','tea-new',{pri:1,w:1}))+table;
}

function vClasses(){
  const cards=S.classes.slice().sort(byName).map(c=>{
    const n=S.students.filter(s=>s.classId===c.id).length,t=by(S.teachers,c.teacherId);
    return `<article class="ccard"><div><h2>${esc(c.name)}</h2><p class="mut">${t?'Class teacher: '+esc(t.name):'No class teacher assigned'}</p></div><p><b>${plural(n,'student')}</b></p><div class="chips">${(c.subjects||[]).map(s=>`<span class="chip">${esc(s)}</span>`).join('')}</div><div class="row">${btn('Open register','goto-att',{id:c.id,sm:1})}${btn('Edit','class-edit',{id:c.id,sm:1,w:1})}${btn('Delete','class-del',{id:c.id,sm:1,w:1})}</div></article>`}).join('');
  return head('Classes',plural(S.classes.length,'class'),btn('Add class','class-new',{pri:1,w:1}))+
    (cards?`<div class="cgrid">${cards}</div>`:note('No classes yet','Create a class, then enrol students into it.',btn('Add class','class-new',{pri:1,w:1})));
}

function vAttendance(){
  if(!S.classes.length)return head('Attendance')+needClass();
  if(!ui.attClass||!cls(ui.attClass))ui.attClass=S.classes.slice().sort(byName)[0].id;
  const c=cls(ui.attClass),studs=S.students.filter(s=>s.classId===c.id).sort(byName);
  const docId=c.id+'_'+ui.attDate,saved=S.attendance.find(a=>a.id===docId);
  if(!ui.attDraft||ui.attDraft.key!==docId||!ui.attDraft.dirty)ui.attDraft={key:docId,marks:Object.assign({},saved?saved.marks:{}),dirty:false};
  const d=ui.attDraft,ro=!ui.canWrite;
  const cnt={P:0,A:0,L:0};studs.forEach(s=>{if(cnt[d.marks[s.id]]!==undefined)cnt[d.marks[s.id]]++});
  const un=studs.length-cnt.P-cnt.A-cnt.L;
  const bar=`<div class="tools"><select data-in="attClass" aria-label="Class">${classOptions(c.id)}</select><input type="date" data-in="attDate" id="att-date" value="${esc(ui.attDate)}" aria-label="Date" style="width:auto"></div>`;
  let reg;
  if(!studs.length)reg=note('No students in '+c.name,'Enrol students into this class to take a register.',btn('Add student','stu-new',{pri:1,w:1}));
  else reg=`<div class="regbar"><div class="counts"><span><b>${cnt.P}</b> present</span><span><b>${cnt.L}</b> late</span><span><b>${cnt.A}</b> absent</span><span class="mut"><b>${un}</b> not marked</span></div><div class="row w sw">${btn('Mark all present','att-all')}${btn('Save register','att-save',{pri:1,dis:!d.dirty,extra:' id="att-save"'})}</div></div>
  <div class="register">${studs.map((s,i)=>`<div class="reg-row"><span class="no">${i+1}</span><span class="nm">${esc(s.name)}</span><span class="marks">${[['P','p','Present'],['L','l','Late'],['A','a','Absent']].map(m=>`<button type="button" class="mk ${m[1]}" data-act="mark" data-id="${esc(s.id)}" data-v="${m[0]}" aria-pressed="${d.marks[s.id]===m[0]}" aria-label="${m[2]}: ${esc(s.name)}" title="${m[2]}"${ro?' disabled':''}>${m[0]}</button>`).join('')}</span></div>`).join('')}</div>
  <p class="legend"><span>P present</span><span>L late (counts as present)</span><span>A absent</span><span>Tap a mark again to clear it.</span></p>`;
  const recent=S.attendance.filter(a=>a.classId===c.id).sort((a,b)=>b.date.localeCompare(a.date)).slice(0,7).map(a=>{
    const v=Object.values(a.marks||{});const p=v.filter(x=>x==='P').length,l=v.filter(x=>x==='L').length,ab=v.filter(x=>x==='A').length;
    return `<li><button class="link" data-act="att-date" data-date="${esc(a.date)}">${fmtDate(a.date)}</button><span class="mut">${p} present, ${l} late, ${ab} absent</span></li>`}).join('');
  return head('Attendance','Take the register for a class and day.')+bar+reg+(recent?`<section class="panel" style="margin-top:1.25rem"><h2>Recent registers for ${esc(c.name)}</h2><ul class="list">${recent}</ul></section>`:'');
}

const pctCell=(n,max)=>{if(n>max)return `<span class="bad">Over ${max}</span>`;const p=n/max*100;return Math.round(p)+'% <b>'+letter(p)+'</b>'};
function vGrades(){
  if(!S.classes.length)return head('Grades')+needClass();
  if(!ui.grClass||!cls(ui.grClass))ui.grClass=S.classes.slice().sort(byName)[0].id;
  const c=cls(ui.grClass);
  const tabs=`<div class="tabs" role="tablist"><button role="tab" data-act="g-tab" data-tab="assess" aria-selected="${ui.grTab==='assess'}">Assessments</button><button role="tab" data-act="g-tab" data-tab="results" aria-selected="${ui.grTab==='results'}">Class results</button></div>`;
  const top=head('Grades','Enter one subject at a time, or record all class subjects in a single grid.',`<select data-in="grClass" aria-label="Class">${classOptions(c.id)}</select>${btn('Enter marks for all subjects','g-bulk',{pri:1,w:1,sw:1,dis:!ui.canWrite})}${btn('New assessment','g-new',{w:1,sw:1,dis:!ui.canWrite})}`);
  return top+tabs+(ui.grTab==='results'?resultsTable(c):assessPane(c));
}
function assessPane(c){
  const list=S.grades.filter(g=>g.classId===c.id).sort((a,b)=>(b.date||'').localeCompare(a.date||''));
  if(ui.grAssess&&!list.some(g=>g.id===ui.grAssess))ui.grAssess='';
  if(!ui.grAssess&&list.length)ui.grAssess=list[0].id;
  const cur=list.find(g=>g.id===ui.grAssess);
  if(!cur)return note('No assessments for '+c.name,'Create an assessment, such as a test or assignment, then enter each student\u2019s score.',btn('New assessment','g-new',{pri:1,w:1,sw:1}));
  const studs=S.students.filter(s=>s.classId===c.id).sort(byName);
  if(!ui.grDraft||ui.grDraft.id!==cur.id||!ui.grDraft.dirty)ui.grDraft={id:cur.id,scores:Object.assign({},cur.scores||{}),dirty:false};
  const d=ui.grDraft,ro=!ui.canWrite;
  const vals=studs.map(s=>d.scores[s.id]).filter(Number.isFinite),avg=mean(vals.map(v=>Math.min(100,v/cur.max*100)));
  const side=`<div class="alist">${list.map(g=>{const n=Object.keys(g.scores||{}).length;return `<button type="button" data-act="g-pick" data-id="${esc(g.id)}" aria-current="${g.id===cur.id}"><b>${esc(g.subject)}: ${esc(g.title)}</b><small>${fmtDate(g.date)}, out of ${g.max}, ${n} scored</small></button>`}).join('')}</div>`;
  const main=!studs.length?note('No students in '+c.name,'Enrol students into this class to record scores.'):
  `<div class="regbar"><div><h2>${esc(cur.subject)}: ${esc(cur.title)}</h2><p class="mut">Out of ${cur.max}${avg===null?'':', class average '+Math.round(avg)+'%'}</p></div><div class="row w sw">${btn('Edit details','g-edit',{id:cur.id})}${btn('Delete','g-del',{id:cur.id})}${btn('Save scores','g-save',{pri:1,dis:!d.dirty,extra:' id="g-save"'})}</div></div>
  <div class="tw"><table class="tbl"><thead><tr><th>Student</th><th class="r">Score</th><th>Result</th></tr></thead><tbody>${studs.map(s=>{const n=d.scores[s.id];return `<tr><td>${esc(s.name)}</td><td class="r"><input class="score" type="number" step="any" min="0" max="${cur.max}" inputmode="decimal" id="sc-${esc(s.id)}" data-in="score" data-id="${esc(s.id)}" value="${Number.isFinite(n)?n:''}" aria-label="Score for ${esc(s.name)}"${ro?' disabled':''}></td><td id="pc-${esc(s.id)}">${Number.isFinite(n)?pctCell(n,cur.max):''}</td></tr>`}).join('')}</tbody></table></div>`;
  return `<div class="split"><div>${side}</div><div>${main}</div></div>`;
}
function resultsTable(c){
  const studs=S.students.filter(s=>s.classId===c.id);
  if(!studs.length)return note('No students in '+c.name,'Enrol students into this class to see results.');
  if(!S.grades.some(g=>g.classId===c.id))return note('No scores yet','Create an assessment and enter scores to see class results.');
  const subs=[...new Set([...(c.subjects||[]),...S.grades.filter(g=>g.classId===c.id).map(g=>g.subject)])];
  const rows=studs.map(s=>{const a=subjAvgs(s.id);return{s,a,ov:mean(Object.values(a))}});
  const ranked=rows.filter(r=>r.ov!==null).sort((x,y)=>y.ov-x.ov);
  ranked.forEach((r,i)=>{r.pos=i>0&&Math.abs(ranked[i-1].ov-r.ov)<1e-9?ranked[i-1].pos:i+1});
  rows.sort((x,y)=>(x.pos||999)-(y.pos||999)||byName(x.s,y.s));
  const pm=S.settings.passMark;
  const cell=v=>v===undefined||v===null?'<span class="mut">\u2013</span>':`<span class="${v<pm?'bad':''}">${Math.round(v)}%</span>`;
  return `<div class="row" style="margin-bottom:.8rem">${ui.dl?btn('Download all report cards for this class','rc-class',{id:c.id}):''}</div><div class="tw"><table class="tbl"><thead><tr><th>Position</th><th>Student</th>${subs.map(x=>`<th class="r">${esc(x)}</th>`).join('')}<th class="r">Overall</th><th>Grade</th></tr></thead><tbody>${rows.map(r=>`<tr><td>${r.pos||'\u2013'}</td><td><button class="link" data-act="stu-open" data-id="${esc(r.s.id)}">${esc(r.s.name)}</button></td>${subs.map(x=>`<td class="r">${cell(r.a[x])}</td>`).join('')}<td class="r"><b>${cell(r.ov)}</b></td><td>${r.ov===null?'':'<b>'+letter(r.ov)+'</b>'}</td></tr>`).join('')}</tbody></table></div><p class="legend"><span>Each figure is the mean of that subject\u2019s assessment percentages. Marks below ${pm}% are shown in red.</span></p>`;
}

function vFees(){
  const bm=balMap(),q=ui.fq.trim().toLowerCase();
  let tb=0,tp=0,owed=0;S.students.forEach(s=>{const b=bm[s.id];tb+=b.billed;tp+=b.paid;if(b.bal>0)owed+=b.bal});
  const rows=S.students.filter(s=>(!q||(s.name+' '+(s.admNo||'')).toLowerCase().includes(q))&&(!ui.fowing||bm[s.id].bal>0)).sort(byName);
  const facts=`<div class="facts"><div class="fact"><span>Billed</span><b>${money(tb)}</b></div><div class="fact"><span>Collected</span><b>${money(tp)}</b></div><div class="fact"><span>Outstanding</span><b>${money(owed)}</b></div></div>`;
  const tools=`<div class="tools"><input id="fq" type="search" data-in="fq" placeholder="Search students" value="${esc(ui.fq)}" aria-label="Search students"><label class="check"><input type="checkbox" data-in="fowing"${ui.fowing?' checked':''}> Owing only</label></div>`;
  let table;
  if(!S.students.length)table=note('No students yet','Fees are tracked per student. Add students first.');
  else if(!rows.length)table=note('No matches','Try a different search, or turn off \u201cOwing only\u201d.');
  else table=`<div class="tw"><table class="tbl"><thead><tr><th>Student</th><th>Class</th><th class="r">Billed</th><th class="r">Paid</th><th class="r">Balance</th><th></th></tr></thead><tbody>${rows.map(s=>{const b=bm[s.id];return `<tr><td><button class="link" data-act="ledger" data-id="${esc(s.id)}">${esc(s.name)}</button></td><td>${esc(className(s.classId))}</td><td class="r">${money(b.billed)}</td><td class="r">${money(b.paid)}</td><td class="r ${b.bal>0?'owe':''}">${money(b.bal)}</td><td class="r"><span class="row w" style="justify-content:flex-end">${btn('Record payment','pay',{id:s.id,sm:1})}</span></td></tr>`}).join('')}</tbody></table></div>`;
  const hist=S.fees.filter(f=>f.kind==='charge'&&f.scope==='class').sort((a,b)=>(b.date||'').localeCompare(a.date||''));
  const histHtml=hist.length?`<section class="panel" style="margin-top:1.25rem"><h2>Class billing history</h2><div class="tw" style="border:0"><table class="tbl"><thead><tr><th>Date</th><th>Class</th><th>Description</th><th class="r">Per student</th><th class="r">Students</th><th></th></tr></thead><tbody>${hist.map(f=>`<tr><td>${fmtDate(f.date)}</td><td>${esc(className(f.classId))}</td><td>${esc(f.note)}</td><td class="r">${money(+f.amount||0)}</td><td class="r">${(f.studentIds||[]).length}</td><td class="r"><span class="w">${btn('Remove','bill-del',{id:f.id,sm:1})}</span></td></tr>`).join('')}</tbody></table></div></section>`:'';
  return head('Fees','Bill classes, record payments and follow up balances.',`${btn('Bill a class','bill',{w:1})}${btn('Record payment','pay',{pri:1,w:1})}`)+facts+tools+table+histHtml;
}

function vNotices(){
  const rows=S.notices.slice().sort((a,b)=>(b.date||'').localeCompare(a.date||''));
  return head('Notices','Announcements for parents, teachers and students.',btn('Post notice','notice-new',{pri:1,w:1}))+
  (rows.length?rows.map(n=>`<section class="panel"><div class="regbar" style="margin:0 0 .4rem"><div><h2>${esc(n.title)}</h2><small class="mut">${fmtDate(n.date)}, for ${esc((n.audience||'Everyone').toLowerCase())}</small></div><span class="w">${btn('Delete','notice-del',{id:n.id,sm:1})}</span></div><p style="white-space:pre-wrap">${esc(n.body)}</p></section>`).join(''):note('No notices yet','Post a notice and it will show on the overview.',btn('Post notice','notice-new',{pri:1,w:1})));
}


function vTimetable(){
  const days=['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'];
  const entries=S.timetable.slice().sort((a,b)=>days.indexOf(a.day)-days.indexOf(b.day)||(a.start||'').localeCompare(b.start||''));
  const rows=entries.length?`<div class="tw"><table class="tbl"><thead><tr><th>Day</th><th>Time</th><th>Class</th><th>Subject</th><th>Teacher</th><th>Room</th><th></th></tr></thead><tbody>${entries.map(t=>`<tr><td>${esc(t.day)}</td><td>${esc(t.start)}–${esc(t.end)}</td><td>${esc(className(t.classId))}</td><td>${esc(t.subject)}</td><td>${esc((by(S.teachers,t.teacherId)||{}).name||'—')}</td><td>${esc(t.room||'—')}</td><td class="r"><span class="row w">${btn('Edit','tt-edit',{id:t.id,sm:1})}${btn('Delete','tt-del',{id:t.id,sm:1})}</span></td></tr>`).join('')}</tbody></table></div>`:note('No lessons scheduled','Add lessons to create a weekly timetable.',btn('Add lesson','tt-new',{pri:1,w:1}));
  return head('Timetable','Manage weekly lessons, teachers, classes and rooms.',btn('Add lesson','tt-new',{pri:1,w:1}))+rows;
}
function vCalendar(){
 const rows=S.events.slice().sort((a,b)=>(a.date||'').localeCompare(b.date||''));
 return head('School calendar','Track school events, deadlines, meetings and holidays.',btn('Add event','event-new',{pri:1,w:1}))+
 (rows.length?rows.map(e=>`<section class="panel"><div class="regbar"><div><h2>${esc(e.title)}</h2><p class="mut">${fmtDate(e.date)} · ${esc(e.category||'Event')}${e.location?' · '+esc(e.location):''}</p></div><span class="row w">${btn('Edit','event-edit',{id:e.id,sm:1})}${btn('Delete','event-del',{id:e.id,sm:1})}</span></div><p style="white-space:pre-wrap">${esc(e.description||'')}</p></section>`).join(''):note('No events yet','Add the next school activity or important date.',btn('Add event','event-new',{pri:1,w:1})));
}
function vExpenses(){
 const total=S.expenses.reduce((n,x)=>n+(Number(x.amount)||0),0);
 const rows=S.expenses.slice().sort((a,b)=>(b.date||'').localeCompare(a.date||''));
 return head('Expenses','Record operational spending and keep a simple expense register.',btn('Record expense','expense-new',{pri:1,w:1}))+
 `<div class="facts"><div class="fact"><span>Total recorded expenses</span><b>${money(total)}</b></div><div class="fact"><span>Entries</span><b>${rows.length}</b></div></div>`+
 (rows.length?`<div class="tw"><table class="tbl"><thead><tr><th>Date</th><th>Category</th><th>Description</th><th>Paid to</th><th class="r">Amount</th><th></th></tr></thead><tbody>${rows.map(x=>`<tr><td>${fmtDate(x.date)}</td><td>${esc(x.category)}</td><td>${esc(x.description)}</td><td>${esc(x.payee||'—')}</td><td class="r">${money(+x.amount||0)}</td><td class="r"><span class="row w">${btn('Edit','expense-edit',{id:x.id,sm:1})}${btn('Delete','expense-del',{id:x.id,sm:1})}</span></td></tr>`).join('')}</tbody></table></div>`:note('No expenses recorded','Record school running costs to start tracking spending.',btn('Record expense','expense-new',{pri:1,w:1})));
}

function vSettings(){
  const s=S.settings,shared=ui.mode==='shared',canExport=!!ui.dl&&S.students.length>0;
  return head('Settings','School details, data portability and backup.',btn('Print current page','print-page',{w:1}))+
  `<section class="panel"><h2>School details</h2><div class="fields grid2"><label class="fld"><span>School name</span><input id="set-name" value="${esc(s.schoolName)}"></label><label class="fld"><span>Current term</span><input id="set-term" value="${esc(s.term)}"></label><label class="fld"><span>Currency symbol or code</span><input id="set-cur" value="${esc(s.currency)}" placeholder="For example $ or EUR"></label><label class="fld"><span>Pass mark (%)</span><input id="set-pass" type="number" min="0" max="100" value="${esc(s.passMark)}"></label></div><div class="row" style="margin-top:1rem">${btn('Save settings','set-save',{pri:1,w:1})}</div></section>
  <section class="panel"><h2>Data</h2><p class="mut" style="margin-bottom:1rem">${shared?'Records are stored in this page\u2019s shared database. People you share the page with as contributors can edit them; viewers can only read.':'Shared storage isn\u2019t available in this view, so records are saved in this browser only.'}</p><div class="row">${btn('Export students (CSV)','exp-students',{dis:!S.students.length})}${btn('Export fee ledger (CSV)','exp-fees',{dis:!S.fees.length})}${btn('Load sample data','sample',{w:1,dis:!!(S.students.length||S.classes.length)})}${btn('Download full backup','backup',{w:1})}${btn('Restore backup','restore',{w:1})}${btn('Clear all records','wipe',{w:1,dan:1})}</div>${(S.students.length||S.classes.length)?'<p class="mut" style="margin-top:.7rem"><small>Sample data can only be loaded into an empty school.</small></p>':''}</section>`+accessPanel();
}
function accessPanel(){
  if(ui.mode!=='shared')return `<section class="panel"><h2>Cloud sync</h2><p class="mut">Cloud sync is not configured in this copy. Add your Supabase project URL and publishable key to <code>supabase-config.js</code>, then redeploy to Vercel.</p></section>`;
  const roleName=r=>r==='admin'?'Administrator':r==='teacher'?'Teacher':'Viewer';
  const rows=ui.access.slice().map(a=>`<tr><td>${esc(ui.profiles[a.id]||'School member')}${a.id===ui.uid?' <small class="mut">(you)</small>':''}</td><td>${roleName(a.role)}</td><td>${a.at?new Date(a.at).toLocaleString():''}</td></tr>`).join('');
  const join=ui.role==='admin'?`<div class="panel" style="margin-top:1rem"><h3>Invite staff to EDUNEXUS</h3><p class="mut">Share this school code only with people who should join this school. They must create their own account, sign in, and use the code to join. New members start with Teacher access; you can change their role in Users.</p><div class="row"><code style="padding:.6rem .8rem;border:1px solid var(--line);border-radius:8px;font-weight:800;letter-spacing:.12em">${esc(ui.joinCode||'Loading…')}</code>${ui.joinCode?btn('Copy school code','copy-join-code',{pri:1}):''}</div></div>`:'';
  return `<section class="panel"><h2>Cloud storage and access</h2><p class="mut">School records are stored in Supabase PostgreSQL. Signed-in school members see the same records across devices. Database policies enforce tenant and role access; the page alone is not the security boundary.</p><p class="mut">Connection status: <b>${esc(ui.cloudStatus||'Connecting')}</b></p>${join}<h3>School members</h3>${rows?`<div class="tw"><table class="tbl"><thead><tr><th>Person</th><th>Role</th><th>Last activity</th></tr></thead><tbody>${rows}</tbody></table></div>`:'<p class="mut">Member activity is not available yet.</p>'}</section>`;
}
const views={overview:vOverview,students:vStudents,teachers:vTeachers,classes:vClasses,attendance:vAttendance,grades:vGrades,fees:vFees,notices:vNotices,timetable:vTimetable,calendar:vCalendar,expenses:vExpenses,users:vUsers,settings:vSettings};

/* ---------- nav + render ---------- */
const NAV=[['overview','Overview','M3 11l9-8 9 8M5 10v10h14V10'],
 ['students','Students','M16 8a4 4 0 1 0-8 0 4 4 0 0 0 8 0zM4 21c0-4 3.6-6 8-6s8 2 8 6'],
 ['teachers','Teachers','M3 7l9-4 9 4-9 4-9-4zM7 10v5c0 1.5 2.2 3 5 3s5-1.5 5-3v-5'],
 ['classes','Classes','M4 4h7v7H4zM13 4h7v7h-7zM4 13h7v7H4zM13 13h7v7h-7z'],
 ['attendance','Attendance','M4 4h16v16H4zM8 12l3 3 5-6'],
 ['grades','Grades','M5 20V10M12 20V4M19 20v-7'],
 ['fees','Fees','M3 6h18v12H3zM3 10h18M7 15h3'],
 ['notices','Notices','M4 5h16v11H9l-5 4V5z'],
 ['timetable','Timetable','M4 5h16v15H4zM8 3v4M16 3v4M4 10h16'],
 ['calendar','Calendar','M4 5h16v15H4zM8 3v4M16 3v4M4 10h16'],
 ['expenses','Expenses','M3 6h18v12H3zM3 10h18M7 15h3'],
 ['users','Users','M16 8a4 4 0 1 0-8 0 4 4 0 0 0 8 0zM4 21c0-4 3.6-6 8-6s8 2 8 6M19 8v6M22 11h-6'],
 ['settings','Settings','M12 9a3 3 0 1 0 0 6 3 3 0 0 0 0-6zM12 2v3M12 19v3M2 12h3M19 12h3M5 5l2 2M17 17l2 2M19 5l-2 2M7 17l-2 2']];
$('#nav').innerHTML=NAV.map(n=>`<button type="button" data-act="nav" data-view="${n[0]}"><svg viewBox="0 0 24 24" aria-hidden="true"><path d="${n[2]}"/></svg><span>${n[1]}</span></button>`).join('')+`<button type="button" data-act="logout" id="nav-out"><svg viewBox="0 0 24 24" aria-hidden="true"><path d="M9 4H5v16h4M16 8l4 4-4 4M20 12H9"/></svg><span>Sign out</span></button>`;

const ROLE_VIEWS={admin:null,teacher:['overview','students','teachers','classes','attendance','grades','notices','timetable','calendar'],viewer:['notices','calendar']};
const allowed=v=>!ROLE_VIEWS[ui.role]||ROLE_VIEWS[ui.role].includes(v);
const loading=()=>ui.mode==='connecting'||(ui.mode==='shared'&&!!ui.authUser&&!!ui.schoolId&&!ui.slow&&(COLS.some(c=>!ui.loaded[c])||!ui.loaded.accounts));
let raf=0;
function scheduleRender(){if(raf)return;raf=requestAnimationFrame(()=>{raf=0;render()})}
function render(){
  _bm=null;_am=null;
  const a=document.activeElement,main=$('#main');
  const aid=a&&a.id&&main.contains(a)?a.id:null;
  const sel=aid&&typeof a.selectionStart==='number'?[a.selectionStart,a.selectionEnd]:null;
  if(ui.acct){const cur=by(S.accounts,ui.acct.id);if(!cur||cur.disabled){ui.acct=null;ui.role=ui.share;try{sessionStorage.removeItem(SESSION_KEY)}catch(e){}}else ui.acct=cur}
  if(!allowed(ui.view))ui.view=ui.role==='viewer'?'notices':'overview';
  const st=S.settings;
  $('#sname').textContent=st.schoolName||'School';$('#sterm').textContent=st.term||'';
  document.title=(st.schoolName||'School')+' management';
  document.querySelectorAll('#nav button').forEach(b=>{b.hidden=b.dataset.view?!allowed(b.dataset.view):!ui.acct;if(b.dataset.view===ui.view)b.setAttribute('aria-current','page');else b.removeAttribute('aria-current')});
  $('#shell').classList.toggle('ro',!ui.canWrite);$('#shell').classList.toggle('staff',ui.role==='teacher');
  const profileStatus=ui.mode==='shared'?(ui.role==='admin'?'Administrator':ui.role==='teacher'?'Teacher':'Viewer'):ui.mode==='local'?(ui.acct?(ui.role==='admin'?'Administrator · Local account':ui.role==='teacher'?'Teacher · Local account':'Viewer · Local account'):'Not signed in'): 'Connecting';
  $('#sfoot').innerHTML=`<span><b>${ui.acct?esc(ui.acct.name):ui.me?esc(ui.me):(ui.mode==='shared'?'Signed in':ui.mode==='local'?'This device only':'Connecting')}</b></span><span>${esc(profileStatus)}</span>`;
  let html;
  const gh=loading()?null:gateHtml();$('#shell').classList.toggle('gate',!!gh);
  if(gh)html=gh;
  else if(loading())html='<div class="skel" style="width:40%;height:28px"></div><div class="skel"></div><div class="skel" style="width:80%"></div><div class="skel" style="width:60%"></div>';
  else{
    html=(ui.authError?'<div class="banner">'+esc(ui.authError)+'</div>':'')+(ui.role==='viewer'&&ui.mode!=='connecting'?'<div class="banner">You are signed in with view-only access. You can read notices. Ask the school administrator for teacher access to see records.</div>':(!ui.canWrite&&ui.mode!=='connecting'?'<div class="banner">You have view-only access, so editing is turned off.</div>':''))+
      (ui.mode==='local'?'<div class="banner">Shared storage isn\u2019t available here. Records are saved in this browser only.</div>':'')+
      views[ui.view]();
  }
  if(gh&&ui.gateDone===gh)return;
  ui.gateDone=gh||null;
  main.innerHTML=html;
  if(aid){const n=document.getElementById(aid);if(n){n.focus({preventScroll:true});if(sel&&n.setSelectionRange){try{n.setSelectionRange(sel[0],sel[1])}catch(e){}}}}
}
function go(v){ui.view=v;render();window.scrollTo(0,0)}

/* ---------- accounts and sign-in ---------- */
const b64=buf=>{let s='';new Uint8Array(buf).forEach(x=>{s+=String.fromCharCode(x)});return btoa(s)};
const unb64=s=>Uint8Array.from(atob(s),c=>c.charCodeAt(0));
const newSalt=()=>b64(crypto.getRandomValues(new Uint8Array(16)));
async function hashPw(pw,salt){
  const k=await crypto.subtle.importKey('raw',new TextEncoder().encode(pw),'PBKDF2',false,['deriveBits']);
  return b64(await crypto.subtle.deriveBits({name:'PBKDF2',salt:unb64(salt),iterations:100000,hash:'SHA-256'},k,256));
}
const roleLabel=r=>r==='admin'?'Administrator':r==='teacher'?'Teacher':'Viewer';
const SESSION_KEY='sm-session';
const USER_RE=/^[a-z0-9._-]{3,30}$/i,MAIL_RE=/^[^@\s]+@[^@\s]+\.[^@\s]+$/;
const adminCount=ex=>S.accounts.filter(a=>a.role==='admin'&&!a.disabled&&a.id!==ex).length;
function applyLogin(a){
  ui.acct=a;ui.role=ui.share==='viewer'?'viewer':(ui.share==='admin'&&a.role==='admin'?'admin':'teacher');
  ui.loginId='';if(!allowed(ui.view))ui.view='overview';
  try{sessionStorage.setItem(SESSION_KEY,a.id)}catch(e){}
  scheduleRender();
}
function restoreSession(){
  if(ui.acct)return;let id=null;try{id=sessionStorage.getItem(SESSION_KEY)}catch(e){}
  const a=id&&by(S.accounts,id);if(a&&!a.disabled&&!a.mustChange)applyLogin(a);
}
async function logout(){
  if(ui.mode==='shared'&&supabaseClient){await supabaseClient.auth.signOut();return;}
  ui.acct=null;ui.role=ui.share;ui.view='overview';ui.loginId='';ui.attDraft=null;ui.grDraft=null;
  try{sessionStorage.removeItem(SESSION_KEY)}catch(e){}
  closeDlg();render();window.scrollTo(0,0);
}
const lbrand=()=>`<div class="lb"><div class="mark" aria-hidden="true"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 6c-2-1.5-5-2-8-2v14c3 0 6 .5 8 2 2-1.5 5-2 8-2V4c-3 0-6 .5-8 2zM12 6v14"/></svg></div><div><strong style="font:800 1.1rem var(--head)">${esc(S.settings.schoolName)}</strong><br><small class="mut">${esc(S.settings.term)}</small></div></div>`;
function cloudLoginHtml(){
  const authNotice=ui.authError?`<div class="banner" role="alert" style="margin:.75rem 0">${esc(ui.authError)}</div>`:'';
  if(ui.authTab==='signup')return `<section class="login">${lbrand()}${authNotice}<h1 style="font-size:1.6rem">Create your EDUNEXUS account</h1><p class="mut">Create the first school administrator account, or join an existing school with its join code. Sign in with your email and password. No verification code is needed when Supabase “Confirm email” is turned off.</p>
  <form id="sf" novalidate style="display:grid;gap:1rem">
  <label class="fld" for="su-name"><span>Full name</span><input id="su-name" autocomplete="name" required value=""></label>
  <label class="fld" for="su-mail"><span>Email address</span><input id="su-mail" type="email" autocomplete="email" autocapitalize="none" required value=""></label>
  <label class="fld" for="su-pw"><span>Password (at least 8 characters)</span><input id="su-pw" type="password" autocomplete="new-password" required></label>
  <label class="fld" for="su-pw2"><span>Confirm password</span><input id="su-pw2" type="password" autocomplete="new-password" required></label>
  <label class="fld" for="su-school"><span>School name (for the first administrator)</span><input id="su-school" placeholder="e.g. EDUNEXUS Secondary School"></label>
  <label class="fld" for="su-code"><span>School join code (for existing school members)</span><input id="su-code" autocapitalize="characters" placeholder="Leave blank when creating a new school"></label>
  <p class="mut"><small>Enter either a school name or a join code, not both. For password-only setup without a verification code, turn off “Confirm email” in your Supabase project's Email provider settings before creating the account.</small></p>
  <p class="err" id="gx-err" role="alert"></p><button class="btn pri" type="submit" id="gx-go">Create account</button></form>
  <p class="mut">Already registered? <button class="link" type="button" data-act="auth-tab" data-tab="login">Sign in</button></p></section>`;
  return `<section class="login">${lbrand()}${authNotice}<h1 style="font-size:1.6rem">Sign in to EDUNEXUS</h1><p class="mut">Use your administrator email and password. EDUNEXUS uses password-based sign-in; it should not ask you for a verification code when Supabase “Confirm email” is turned off.</p>
  <form id="lf" novalidate style="display:grid;gap:1rem">
  <label class="fld" for="lg-id"><span>Email address</span><input id="lg-id" data-in="lgid" type="email" autocomplete="username" autocapitalize="none" spellcheck="false" value="${esc(ui.loginId)}" required></label>
  <label class="fld" for="lg-pw"><span>Password</span><div class="pw"><input id="lg-pw" type="password" autocomplete="current-password" required><button type="button" data-act="pw-toggle" aria-label="Show or hide password">Show</button></div></label>
  <p class="err" id="lg-err" role="alert"></p><button class="btn pri" type="submit" id="lg-go">Sign in</button>
  <button class="btn" type="button" data-act="forgot-password">Forgot password?</button></form>
  <p class="mut"><small>First-time setup? Create your administrator account with your email and password. Email confirmation must be disabled in Supabase to skip verification codes.</small></p>
  <p class="mut">New to EDUNEXUS? <button class="link" type="button" data-act="auth-tab" data-tab="signup">Create an account or set up a school</button></p></section>`;
}
function cloudMembershipSetupHtml(){
  const authNotice=ui.authError?`<div class="banner" role="alert" style="margin:.75rem 0">${esc(ui.authError)}</div>`:'';
  const nm=(ui.authUser&&ui.authUser.user_metadata&&ui.authUser.user_metadata.full_name)||'';
  return `<section class="login">${lbrand()}${authNotice}<h1 style="font-size:1.6rem">Connect your account to a school</h1><p class="mut">Your account is signed in, but it is not linked to a school yet. Create the first school, or join one using the school code from its administrator.</p>
  <form id="mf" novalidate style="display:grid;gap:1rem">
  <label class="fld" for="ms-name"><span>Your full name</span><input id="ms-name" autocomplete="name" value="${esc(nm)}" required></label>
  <label class="fld" for="ms-school"><span>School name (to create a new school)</span><input id="ms-school" placeholder="Enter only if you are setting up a new school"></label>
  <label class="fld" for="ms-code"><span>School join code (to join an existing school)</span><input id="ms-code" autocapitalize="characters" placeholder="Enter only if joining a school"></label>
  <p class="err" id="mf-err" role="alert"></p><button class="btn pri" type="submit" id="mf-go">Continue</button>
  <button class="btn" type="button" data-act="logout">Sign out</button></form></section>`;
}
function gateHtml(){
  if(ui.mode==='shared'){
    if(!ui.authUser)return cloudLoginHtml();
    if(!ui.acct)return cloudMembershipSetupHtml();
    return null;
  }
  if(ui.share==='viewer')return null;
  if(!ui.acct){if(!S.accounts.length)return ui.share==='admin'?setupHtml():`<section class="login">${lbrand()}<h1 style="font-size:1.6rem">Setup pending</h1><p class="mut">The school administrator hasn’t created the first account yet. Please check back soon.</p></section>`;return loginHtml();}
  return ui.acct.mustChange?changeHtml():null;
}
function loginHtml(){
  const em=ui.loginTab==='email';
  return `<section class="login">${lbrand()}<h1 style="font-size:1.6rem">Sign in</h1>
  <div class="tabs" role="tablist" style="margin:0"><button type="button" role="tab" data-act="login-tab" data-tab="username" aria-selected="${!em}">Username</button><button type="button" role="tab" data-act="login-tab" data-tab="email" aria-selected="${em}">Email</button></div>
  <form id="lf" novalidate style="display:grid;gap:1rem"><label class="fld" for="lg-id"><span>${em?'Email address':'Username'}</span><input id="lg-id" data-in="lgid" type="${em?'email':'text'}" autocomplete="${em?'email':'username'}" autocapitalize="none" spellcheck="false" value="${esc(ui.loginId)}"></label>
  <label class="fld" for="lg-pw"><span>Password</span><div class="pw"><input id="lg-pw" type="password" autocomplete="current-password"><button type="button" data-act="pw-toggle" aria-label="Show or hide password">Show</button></div></label><p class="err" id="lg-err" role="alert"></p><button class="btn pri" type="submit" id="lg-go">Sign in</button></form><p class="mut"><small>Forgot your password? Ask your school administrator to reset it.</small></p></section>`;
}
function setupHtml(){
  return `<section class="login">${lbrand()}<h1 style="font-size:1.6rem">Create the administrator account</h1><p class="mut">First-time setup for local browser storage only. For cloud sync, configure Supabase in supabase-config.js.</p>
  <form id="sf" novalidate style="display:grid;gap:1rem"><label class="fld" for="su-name"><span>Full name</span><input id="su-name" value=""></label><label class="fld" for="su-user"><span>Username</span><input id="su-user" value="josam" autocapitalize="none"></label><label class="fld" for="su-mail"><span>Email address</span><input id="su-mail" type="email" value=""></label><label class="fld" for="su-pw"><span>Password</span><input id="su-pw" type="password" autocomplete="new-password"></label><label class="fld" for="su-pw2"><span>Confirm password</span><input id="su-pw2" type="password" autocomplete="new-password"></label><p class="err" id="gx-err" role="alert"></p><button class="btn pri" type="submit" id="gx-go">Create account and sign in</button></form></section>`;
}
function changeHtml(){
  return `<section class="login">${lbrand()}<h1 style="font-size:1.6rem">Choose a new password</h1><p class="mut">Pick a password with at least 6 characters.</p><form id="cf" novalidate style="display:grid;gap:1rem"><label class="fld" for="cf-pw"><span>New password</span><input id="cf-pw" type="password" autocomplete="new-password"></label><label class="fld" for="cf-pw2"><span>Confirm new password</span><input id="cf-pw2" type="password" autocomplete="new-password"></label><p class="err" id="gx-err" role="alert"></p><div class="dact"><button type="button" class="btn" data-act="logout">Sign out</button><button class="btn pri" type="submit" id="gx-go">Save password</button></div></form></section>`;
}
const cryptoOk=()=>!!(window.crypto&&crypto.subtle);
async function completePendingMembership(){
  if(!supabaseClient||!ui.authUser)return false;
  let pending=null;try{pending=JSON.parse(localStorage.getItem('edunexus-pending-membership')||'null')}catch(e){}
  if(!pending)return false;
  const name=pending.name||ui.authUser.user_metadata?.full_name||ui.authUser.email||'School user';
  let result;
  if(pending.schoolName){result=await supabaseClient.rpc('create_school',{p_school_name:pending.schoolName,p_display_name:name,p_email:ui.authUser.email||'',p_username:(ui.authUser.email||'').split('@')[0]});}
  else if(pending.joinCode){result=await supabaseClient.rpc('join_school',{p_join_code:pending.joinCode,p_display_name:name,p_email:ui.authUser.email||'',p_username:(ui.authUser.email||'').split('@')[0]});}
  else return false;
  if(result.error)throw result.error;
  try{localStorage.removeItem('edunexus-pending-membership')}catch(e){}
  await syncAuthSession(ui.authUser);
  return true;
}
async function syncAuthSession(user){
  const gen=++ui.authGeneration;
  ui.authUser=user||null;ui.acct=null;ui.schoolId=null;ui.canWrite=false;
  if(!user){if(backend&&backend.stop)await backend.stop();clearCloudData();ui.role='viewer';ui.share='viewer';ui.cloudReady=false;ui.cloudStatus='SIGNED_OUT';ui.authTab='login';render();return;}
  ui.uid=user.id;ui.me=(user.user_metadata&&user.user_metadata.full_name)||user.email||'';
  const {data:member,error}=await supabaseClient.from('school_memberships').select('school_id,user_id,display_name,username,email,role,disabled,created_at').eq('user_id',user.id).maybeSingle();
  if(gen!==ui.authGeneration)return;
  if(error)throw error;
  if(!member){if(backend&&backend.stop)await backend.stop();clearCloudData();ui.authUser=user;ui.canWrite=false;ui.role='viewer';ui.share='viewer';ui.loaded.accounts=true;COLS.forEach(c=>ui.loaded[c]=true);ui.cloudReady=true;render();return;}
  const acct=memberToAccount(member);ui.schoolId=member.school_id;ui.acct=acct;ui.role=acct.role;ui.share=acct.role;ui.canWrite=!acct.disabled&&acct.role!=='viewer';ui.cloudReady=false;
  if(acct.disabled){ui.authError='This account has been disabled by the school administrator.';ui.acct=null;clearCloudData();ui.authUser=user;render();return;}
  backend=supabaseBackend(supabaseClient);await backend.start(member.school_id);
  if(gen!==ui.authGeneration)return;
  ui.acct=by(S.accounts,user.id)||acct;ui.role=ui.acct.role;ui.share=ui.acct.role;ui.canWrite=ui.acct.role!=='viewer'&&!ui.acct.disabled;render();
}
async function doLogin(){
  if(ui.mode==='shared'&&supabaseClient){
    const err=m=>{const p=$('#lg-err');if(p)p.textContent=m;};
    const email=$('#lg-id').value.trim().toLowerCase(),password=$('#lg-pw').value;
    if(!email||!password){err('Enter your email and password.');return;}
    const b=$('#lg-go');b.disabled=true;
    const {data,error}=await supabaseClient.auth.signInWithPassword({email,password});b.disabled=false;
    if(error){
      const detail=String(error.message||'');
      if(/email not confirmed|email.*confirm/i.test(detail)) err('Email confirmation is still enabled in Supabase. Turn off Confirm email under Authentication → Sign In / Providers → Email. An already-created unconfirmed account may need to be confirmed or recreated from Supabase Authentication → Users.');
      else err(detail==='Invalid login credentials'?'Email or password is incorrect.':detail);
      return;
    }
    try{await syncAuthSession(data.user);await completePendingMembership();toast('Signed in successfully.');}catch(e){err(e.message||'Signed in, but could not load your school.');}
    return;
  }
  const err=m=>{const p=$('#lg-err');if(p)p.textContent=m};const now=Date.now();
  if(now<ui.lockUntil){err('Too many attempts. Try again in '+Math.ceil((ui.lockUntil-now)/1000)+' seconds.');return;}
  const em=ui.loginTab==='email',idv=$('#lg-id').value.trim().toLowerCase(),pw=$('#lg-pw').value;
  if(!idv||!pw){err('Enter your '+(em?'email address':'username')+' and password.');return;}if(!cryptoOk()){err('This browser can’t verify passwords securely.');return;}
  const b=$('#lg-go');b.disabled=true;const a=S.accounts.find(x=>em?(x.email||'').toLowerCase()===idv:(x.username||'').toLowerCase()===idv);let ok=false;
  try{ok=a?(await hashPw(pw,a.salt))===a.hash:(await hashPw(pw,newSalt()),false)}catch(e){}b.disabled=false;
  if(!ok){ui.fails++;if(ui.fails>=5){ui.fails=0;ui.lockUntil=Date.now()+30000;err('Too many attempts. Try again in 30 seconds.')}else err('Incorrect '+(em?'email':'username')+' or password.');$('#lg-pw').value='';return;}
  if(a.disabled){err('This account is disabled. Ask your school administrator.');return;}ui.fails=0;applyLogin(a);
}
async function doSetup(){
  if(ui.mode==='shared'&&supabaseClient){
    const err=m=>{const p=$('#gx-err');if(p)p.textContent=m;};
    const name=$('#su-name').value.trim(),email=$('#su-mail').value.trim().toLowerCase(),password=$('#su-pw').value,password2=$('#su-pw2').value,schoolName=$('#su-school').value.trim(),joinCode=$('#su-code').value.trim().toUpperCase();
    if(!name||!email||!password){err('Enter your name, email, and password.');return;}if(password.length<8){err('Use a password with at least 8 characters.');return;}if(password!==password2){err('The two passwords do not match.');return;}if(!!schoolName===!!joinCode){err('Enter either a school name or a school join code, but not both.');return;}
    const b=$('#gx-go');b.disabled=true;
    let signupResult;
    try {
      signupResult=await supabaseClient.auth.signUp({
        email,password,
        options:{data:{full_name:name},emailRedirectTo:window.location.origin+window.location.pathname}
      });
    } catch(e) {
      b.disabled=false;err(e&&e.message?e.message:'Could not contact the authentication service. Check your connection and try again.');return;
    }
    const {data,error}=signupResult;b.disabled=false;
    if(error){err(error.message);return;}
    try{localStorage.setItem('edunexus-pending-membership',JSON.stringify({name,schoolName,joinCode}));}catch(e){}
    if(data.session&&data.user){try{await syncAuthSession(data.user);await completePendingMembership();toast('Your account and school access are ready.');}catch(e){err(e.message||'Account created but school setup could not finish. Sign in and retry.');}}
    else{ui.authTab='login';render();toast('Account created, but Supabase still requires email confirmation. Turn off Confirm email in Supabase before creating a new account to use password-only setup.');}
    return;
  }
  const err=m=>{$('#gx-err').textContent=m},g=id=>$('#'+id).value.trim();const name=g('su-name'),username=g('su-user'),email=g('su-mail'),pw=$('#su-pw').value,pw2=$('#su-pw2').value;
  if(!name||!username||!email||!pw){err('Fill in every field.');return;}if(!USER_RE.test(username)){err('Username must be 3 to 30 letters, numbers, dots, dashes or underscores.');return;}if(!MAIL_RE.test(email)){err('Enter a valid email address.');return;}if(pw!==pw2){err('The two passwords don’t match.');return;}if(!cryptoOk()){err('This browser can’t store passwords securely.');return;}
  const b=$('#gx-go');b.disabled=true;const salt=newSalt(),hash=await hashPw(pw,salt);const rec={name,username,email,role:'admin',hash,salt,disabled:false,mustChange:pw.length<6,createdAt:Date.now()};let nid;
  const ok=await run(async()=>{nid=await backend.put('accounts',rec)});if(ok)applyLogin(by(S.accounts,nid)||Object.assign({id:nid},rec));else b.disabled=false;
}
async function doMembershipSetup(){
  const err=m=>{const p=$('#mf-err');if(p)p.textContent=m;};if(!supabaseClient||!ui.authUser){err('Please sign in again.');return;}
  const name=$('#ms-name').value.trim(),schoolName=$('#ms-school').value.trim(),joinCode=$('#ms-code').value.trim().toUpperCase();
  if(!name){err('Enter your full name.');return;}if(!!schoolName===!!joinCode){err('Enter either a school name or a join code, not both.');return;}
  const b=$('#mf-go');b.disabled=true;
  try{const result=schoolName?await supabaseClient.rpc('create_school',{p_school_name:schoolName,p_display_name:name,p_email:ui.authUser.email||'',p_username:(ui.authUser.email||'').split('@')[0]}):await supabaseClient.rpc('join_school',{p_join_code:joinCode,p_display_name:name,p_email:ui.authUser.email||'',p_username:(ui.authUser.email||'').split('@')[0]});if(result.error)throw result.error;await syncAuthSession(ui.authUser);toast(schoolName?'School created.':'Joined school successfully.');}
  catch(e){err(e.message||'Could not connect to that school. Check the code and try again.');}finally{if($('#mf-go'))$('#mf-go').disabled=false;}
}
async function resendConfirmationEmail(email){
  if(!supabaseClient){toast('Cloud authentication is not connected. Refresh the page and try again.',true);return;}
  const address=String(email||'').trim().toLowerCase();
  if(!MAIL_RE.test(address)){toast('Enter the email address you used to register.',true);return;}
  try{
    const {error}=await supabaseClient.auth.resend({
      type:'signup',email:address,
      options:{emailRedirectTo:window.location.origin+window.location.pathname}
    });
    if(error)throw error;
    toast('If the account needs confirmation, a new confirmation email has been requested for '+address+'.');
  }catch(e){toast(e&&e.message?e.message:'Could not request a new confirmation email. Check the Supabase Auth settings.',true);}
}
async function sendPasswordReset(email){
  if(!supabaseClient||!email){toast('An email address is required for password reset.',true);return;}
  const {error}=await supabaseClient.auth.resetPasswordForEmail(email,{redirectTo:window.location.origin+window.location.pathname});
  if(error)toast(error.message||'Could not send password reset email.',true);else toast('Password reset instructions were sent to '+email+'.');
}
async function doChange(){
  const err=m=>{$('#gx-err').textContent=m},pw=$('#cf-pw').value,pw2=$('#cf-pw2').value;
  if(pw.length<6){err('Use at least 6 characters.');return}
  if(pw!==pw2){err('The two passwords don’t match.');return}
  const b=$('#gx-go');b.disabled=true;
  const salt=newSalt(),hash=await hashPw(pw,salt),rec=Object.assign({},ui.acct,{salt,hash,mustChange:false});
  const ok=await run(()=>backend.put('accounts',rec),'Password saved');
  if(ok){ui.acct=rec;scheduleRender()}else b.disabled=false;
}
function vUsers(){
  const me=ui.acct&&ui.acct.id,rows=S.accounts.slice().sort((a,b)=>(a.name||'').localeCompare(b.name||''));
  const table=rows.length?`<div class="tw"><table class="tbl"><thead><tr><th>Name</th><th>Username</th><th>Email</th><th>Role</th><th>Status</th><th></th></tr></thead><tbody>${rows.map(a=>`<tr><td><b>${esc(a.name)}</b>${a.id===me?' <small class="mut">(you)</small>':''}</td><td>${esc(a.username)}</td><td>${esc(a.email)}</td><td>${roleLabel(a.role)}</td><td>${a.disabled?'<span class="bad">Disabled</span>':'Active'}</td><td class="r"><span class="row w" style="justify-content:flex-end">${btn('Edit role','user-edit',{id:a.id,sm:1})}${btn('Reset password','user-pw',{id:a.id,sm:1})}${a.id===me?'':btn(a.disabled?'Enable':'Disable','user-toggle',{id:a.id,sm:1})}${a.id===me?'':btn('Remove access','user-del',{id:a.id,sm:1})}</span></td></tr>`).join('')}</tbody></table></div>`:note('No school members yet','Share the school code with a teacher so they can create an account and join.',btn('Show school join code','user-new',{pri:1,w:1}));
  return head('Users','Manage who can access this school and what they can do.',btn('Invite / add user','user-new',{pri:1,w:1}))+`<div class="banner">To protect accounts, users create their own password through Supabase Auth. Share the school join code with trusted staff; new members start as teachers. Change their role here after they join.</div>`+table;
}
function userForm(a){
  if(!a&&ui.mode==='shared'){
    dlg(`<h2>Invite a school member</h2><p>Ask the person to open EDUNEXUS, choose <b>Create an account or set up a school</b>, register with their own email, and enter this school join code. They will begin with Teacher access. You can change their role after they join.</p><div class="panel"><p class="mut">School join code</p><p style="font-size:1.5rem;font-weight:800;letter-spacing:.16em">${esc(ui.joinCode||'Loading…')}</p></div><div class="dact"><button type="button" class="btn" data-act="close">Close</button>${ui.joinCode?btn('Copy school code','copy-join-code',{pri:1}):''}</div>`);return;
  }
  const f=[{name:'name',label:'Full name',required:true,wide:true},{name:'username',label:'Username'},{name:'role',label:'Role',type:'select',options:[{v:'teacher',l:'Teacher'},{v:'admin',l:'Administrator'},{v:'viewer',l:'Viewer'}]},{name:'email',label:'Email address',type:'email',required:true,wide:true}];
  if(!a)f.push({name:'password',label:'Temporary password',required:true,wide:true,placeholder:'At least 4 characters'});
  formDialog({title:a?'Edit user':'Add user',note:a?'':'Local-only account creation. For cloud accounts, use the school join code.',fields:f,values:a||{role:'teacher'},submit:a?'Save':'Add user',
    onSave:async v=>{
      const err=m=>{$('#frm-err').textContent=m;return false},lu=(v.username||'').toLowerCase(),le=v.email.toLowerCase(),oid=a&&a.id;
      if(v.username&&!USER_RE.test(v.username))return err('Username must be 3 to 30 letters, numbers, dots, dashes or underscores.');
      if(!MAIL_RE.test(v.email))return err('Enter a valid email address.');
      if(S.accounts.some(x=>x.id!==oid&&(x.username||'').toLowerCase()===lu&&lu))return err('That username is already taken.');
      if(S.accounts.some(x=>x.id!==oid&&(x.email||'').toLowerCase()===le))return err('That email is already used by another user.');
      if(a&&a.role==='admin'&&v.role!=='admin'&&adminCount(a.id)===0)return err('There must be at least one administrator.');
      const rec=Object.assign({},a||{},{name:v.name,username:v.username,email:v.email,role:v.role});
      if(!a){if(ui.mode==='shared')return err('For cloud accounts, use Invite / add user and share the school join code.');if(v.password.length<4)return err('Password must be at least 4 characters.');if(!cryptoOk())return err('This browser can’t store passwords securely.');rec.salt=newSalt();rec.hash=await hashPw(v.password,rec.salt);rec.disabled=false;rec.mustChange=false;rec.createdAt=Date.now();}
      return run(()=>backend.put('accounts',rec),a?'User updated':'User added');
    }});
}
async function resetPwForm(a){
  if(!a)return;
  if(ui.mode==='shared'){await sendPasswordReset(a.email);return;}
  formDialog({title:'Reset password for '+a.name,submit:'Set password',note:'Share the new password with them directly.',fields:[{name:'password',label:'New password',required:true,wide:true,placeholder:'At least 4 characters'}],
    onSave:async v=>{if(v.password.length<4){$('#frm-err').textContent='Password must be at least 4 characters.';return false;}if(!cryptoOk()){$('#frm-err').textContent='This browser can’t store passwords securely.';return false;}const salt=newSalt(),hash=await hashPw(v.password,salt);return run(()=>backend.put('accounts',Object.assign({},a,{salt,hash,mustChange:false})),'Password updated');}});
}
function reportHtml(sid){
  const s=stu(sid);if(!s)return '';
  const c=cls(s.classId),st=S.settings,a=subjAvgs(sid),ov=mean(Object.values(a));
  const mates=S.students.filter(x=>x.classId===s.classId).map(x=>({id:x.id,ov:mean(Object.values(subjAvgs(x.id)))})).filter(x=>x.ov!==null).sort((p,q)=>q.ov-p.ov);
  const me=mates.find(m=>m.id===sid),pos=me?1+mates.findIndex(z=>Math.abs(z.ov-me.ov)<1e-9):null;
  const subs=[...new Set([...((c&&c.subjects)||[]),...Object.keys(a)])];
  const rows=subs.map(sub=>{
    const det=S.grades.filter(g=>g.subject===sub&&g.classId===s.classId&&Number.isFinite(g.scores&&g.scores[sid])).sort((x,y)=>(x.date||'').localeCompare(y.date||'')).map(g=>g.title+' '+g.scores[sid]+'/'+g.max).join(', ');
    return `<tr><td>${esc(sub)}</td><td>${esc(det)||'No scores yet'}</td><td class="n">${a[sub]===undefined?'-':Math.round(a[sub])+'%'}</td><td>${a[sub]===undefined?'':letter(a[sub])}</td></tr>`}).join('');
  const ap=attPct(attMap()[sid]);
  return `<div class="rc"><div class="hd"><div><h1>${esc(st.schoolName)}</h1><div class="sub">Student report card${st.term?', '+esc(st.term):''}</div></div><div style="text-align:right"><b>${esc(s.name)}</b><br>${esc(c?c.name:'')}<br>Admission no. ${esc(s.admNo||'')}</div></div><table><thead><tr><th>Subject</th><th>Assessments</th><th class="n">Average</th><th>Grade</th></tr></thead><tbody>${rows||'<tr><td colspan="4">No subjects set for this class.</td></tr>'}</tbody></table><div class="sum"><div>Overall average<b>${ov===null?'No data':Math.round(ov)+'% ('+letter(ov)+')'}</b></div><div>Class position<b>${pos?pos+' of '+mates.length:'-'}</b></div><div>Attendance<b>${ap===null?'No data':ap+'%'}</b></div></div><p><b>Comment:</b> ${esc(remark(ov))}</p><div class="sig"><div>Class teacher</div><div>Head teacher</div><div>Parent or guardian</div></div></div>`;
}
function reportDoc(ids){
  return `<!doctype html><html lang="en"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>Report cards</title><style>body{margin:0;background:#eef1f5;padding:16px}.rc{max-width:760px;margin:0 auto 16px}.np{max-width:760px;margin:0 auto 12px}${RC_CSS}@media print{body{background:#fff;padding:0}.np{display:none}.rc{border:0;margin:0;max-width:none;page-break-after:always}}</style></head><body><div class="np"><button onclick="print()" style="padding:8px 14px;font-weight:600">Print or save as PDF</button></div>${ids.map(i=>reportHtml(i)).join('')}</body></html>`;
}
function reportDialog(sid){
  if(!stu(sid))return;
  dlg(`<style>${RC_CSS}</style>${reportHtml(sid)}<p class="mut"><small>${ui.dl?'Download the card, open it in your browser, then choose Print or Save as PDF.':'Downloads aren’t available in this view.'}</small></p><div class="dact">${btn('Close','close')}${ui.dl?btn('Download report card','rc-dl',{id:sid,pri:1}):''}</div>`);
}
async function rcDownload(ids,label){
  if(!ui.dl)return;const s=stu(ids[0]);
  const nm=String(label||(s&&s.name)||'report').toLowerCase().replace(/[^a-z0-9]+/g,'-').replace(/^-|-$/g,'');
  try{await ui.dl.save({filename:'report-card'+(ids.length>1?'s':'')+'-'+nm+'.html',data:reportDoc(ids)})}
  catch(e){if(!e||e.code!=='declined')toast('Couldn’t save the file.',true)}
}

/* ---------- entity forms ---------- */
function studentForm(s){
  if(!S.classes.length){toast('Add a class before enrolling students.',true);return}
  formDialog({title:s?'Edit student':'Add student',
    fields:[{name:'name',label:'Full name',required:true,wide:true},
      {name:'classId',label:'Class',type:'select',required:true,options:S.classes.slice().sort(byName).map(c=>({v:c.id,l:c.name}))},
      {name:'admNo',label:'Admission no.'},
      {name:'gender',label:'Gender',type:'select',options:[{v:'',l:'Not stated'},{v:'F',l:'Female'},{v:'M',l:'Male'}]},
      {name:'dob',label:'Date of birth',type:'date'},
      {name:'guardian',label:'Parent or guardian',wide:true},
      {name:'phone',label:'Guardian phone'}],
    values:s||{classId:ui.sclass||ui.attClass||S.classes[0].id,admNo:nextAdm()},
    onSave:v=>run(()=>backend.put('students',Object.assign({},s||{},v)),s?'Student updated':'Student added')});
}
function teacherForm(t){
  formDialog({title:t?'Edit teacher':'Add teacher',
    fields:[{name:'name',label:'Full name',required:true,wide:true},{name:'subject',label:'Main subject'},{name:'phone',label:'Phone'},{name:'email',label:'Email',type:'email',wide:true}],
    values:t||{},onSave:v=>run(()=>backend.put('teachers',Object.assign({},t||{},v)),t?'Teacher updated':'Teacher added')});
}
function classForm(c){
  formDialog({title:c?'Edit class':'Add class',
    fields:[{name:'name',label:'Class name',required:true,wide:true,placeholder:'For example Class 5A'},
      {name:'teacherId',label:'Class teacher',type:'select',wide:true,options:[{v:'',l:'No class teacher'}].concat(S.teachers.slice().sort(byName).map(t=>({v:t.id,l:t.name})))},
      {name:'subjects',label:'Subjects, separated by commas',required:true,wide:true}],
    values:c?Object.assign({},c,{subjects:(c.subjects||[]).join(', ')}):{subjects:'English, Mathematics, Science, Social Studies'},
    onSave:v=>run(()=>backend.put('classes',Object.assign({},c||{},{name:v.name,teacherId:v.teacherId,subjects:v.subjects.split(',').map(x=>x.trim()).filter(Boolean)})),c?'Class updated':'Class added')});
}
function payForm(sid){
  if(!S.students.length){toast('Add a student first.',true);return}
  formDialog({title:'Record payment',submit:'Record payment',
    fields:[{name:'studentId',label:'Student',type:'select',required:true,wide:true,options:S.students.slice().sort(byName).map(s=>({v:s.id,l:s.name+' ('+className(s.classId)+')'}))},
      {name:'amount',label:'Amount',type:'number',required:true,min:0.01},{name:'date',label:'Date received',type:'date',required:true},
      {name:'method',label:'Method',type:'select',options:['Cash','Mobile money','Bank transfer','Cheque','Other'].map(x=>({v:x,l:x}))},
      {name:'note',label:'Reference'}],
    values:{studentId:sid||S.students.slice().sort(byName)[0].id,date:todayStr(),method:'Cash'},
    onSave:v=>run(()=>backend.put('fees',{kind:'payment',studentId:v.studentId,amount:v.amount,date:v.date,method:v.method,note:v.note}),'Payment recorded')});
}
function billForm(){
  if(!S.classes.length){toast('Add a class first.',true);return}
  formDialog({title:'Bill a class',submit:'Bill class',note:'Charges every student currently in the class. Students who join later are not billed automatically.',
    fields:[{name:'classId',label:'Class',type:'select',required:true,wide:true,options:S.classes.slice().sort(byName).map(c=>({v:c.id,l:c.name}))},
      {name:'note',label:'Description',required:true,wide:true,placeholder:'For example Tuition, Term 1'},
      {name:'amount',label:'Amount per student',type:'number',required:true,min:0.01},{name:'date',label:'Date',type:'date',required:true}],
    values:{date:todayStr(),classId:ui.sclass||S.classes[0].id,note:'Tuition, '+(S.settings.term||'')},
    onSave:v=>{const ids=S.students.filter(s=>s.classId===v.classId).map(s=>s.id);
      if(!ids.length){$('#frm-err').textContent='That class has no students to bill.';return false}
      return run(()=>backend.put('fees',{kind:'charge',scope:'class',classId:v.classId,studentIds:ids,note:v.note,amount:v.amount,date:v.date,term:S.settings.term}),'Billed '+plural(ids.length,'student'))}});
}
function chargeForm(sid){
  formDialog({title:'Add a charge for '+(stu(sid)?stu(sid).name:'student'),submit:'Add charge',
    fields:[{name:'note',label:'Description',required:true,wide:true,placeholder:'For example School uniform'},
      {name:'amount',label:'Amount',type:'number',required:true,min:0.01},{name:'date',label:'Date',type:'date',required:true}],
    values:{date:todayStr()},
    onSave:v=>run(()=>backend.put('fees',{kind:'charge',scope:'student',studentIds:[sid],note:v.note,amount:v.amount,date:v.date,term:S.settings.term}),'Charge added').then(ok=>{if(ok)setTimeout(()=>ledger(sid),80);return ok})});
}
function bulkMarksForm(){
  const c=cls(ui.grClass);
  if(!c){toast('Choose a class first.',true);return;}
  if(!ui.canWrite){toast('You have view-only access.',true);return;}
  const subjects=[...new Set((c.subjects||[]).map(x=>String(x||'').trim()).filter(Boolean))];
  const studs=S.students.filter(s=>s.classId===c.id).sort(byName);
  if(!subjects.length){toast('Add subjects to this class in Classes → Edit class first.',true);return;}
  if(!studs.length){toast('Add students to '+c.name+' before entering marks.',true);return;}
  const rows=studs.map((st,i)=>`<tr><td>${i+1}</td><td><b>${esc(st.name)}</b><br><small class="mut">${esc(st.admNo||'No admission number')}</small></td>${subjects.map(sub=>`<td><input class="bulk-score" type="number" min="0" max="100" step="any" inputmode="decimal" data-bulk-score data-student-id="${esc(st.id)}" data-subject="${esc(sub)}" aria-label="${esc(sub)} mark for ${esc(st.name)}" placeholder="—"></td>`).join('')}</tr>`).join('');
  const html=`<form id="bulk-grades-form" novalidate>
    <div><h2>Enter marks for all subjects</h2><p class="mut" style="margin-top:.35rem">${esc(c.name)} · ${studs.length} student${studs.length===1?'':'s'} · ${subjects.length} subject${subjects.length===1?'':'s'}</p></div>
    <div class="bulk-grade-meta">
      <label class="fld" for="bulk-title"><span>Assessment title</span><input id="bulk-title" required maxlength="120" value="End of term" placeholder="e.g. Midterm test"></label>
      <label class="fld" for="bulk-date"><span>Assessment date</span><input id="bulk-date" type="date" required value="${todayStr()}"></label>
      <label class="fld" for="bulk-max"><span>Maximum mark per subject</span><input id="bulk-max" type="number" min="1" max="10000" step="any" required value="100"></label>
    </div>
    <p class="mut">Enter marks in the subject columns, then save once. Blank cells are skipped; if you are updating an assessment with the same title and date, existing marks in blank cells are kept. The maximum applies to every subject in this grid.</p>
    <div class="bulk-grade-grid"><table class="tbl"><thead><tr><th>#</th><th>Student</th>${subjects.map(sub=>`<th class="r">${esc(sub)}</th>`).join('')}</tr></thead><tbody>${rows}</tbody></table></div>
    <p class="err" id="bulk-grades-error" role="alert" aria-live="polite"></p>
    <div class="dact"><button type="button" class="btn" data-act="close">Cancel</button><button type="submit" class="btn pri" id="bulk-grades-save">Save all subject marks</button></div>
  </form>`;
  const dialog=$('#dlg');dialog.classList.add('wide');dlg(html);
  $('#bulk-grades-form').addEventListener('submit',async e=>{
    e.preventDefault();
    const form=e.currentTarget,err=$('#bulk-grades-error'),save=$('#bulk-grades-save');
    const title=$('#bulk-title').value.trim(),date=$('#bulk-date').value,max=Number($('#bulk-max').value);
    err.textContent='';
    if(!title||!date){err.textContent='Enter an assessment title and date.';return;}
    if(!Number.isFinite(max)||max<=0){err.textContent='The maximum mark must be greater than zero.';return;}
    const incoming=Object.fromEntries(subjects.map(sub=>[sub,{}]));
    let count=0,invalid=null;
    form.querySelectorAll('[data-bulk-score]').forEach(input=>{
      const raw=input.value.trim();if(raw==='')return;
      const score=Number(raw);
      if(!Number.isFinite(score)||score<0||score>max){invalid=input;return;}
      incoming[input.dataset.subject][input.dataset.studentId]=score;count++;
    });
    if(invalid){err.textContent='Every mark must be between 0 and '+max+'. Please correct the highlighted subject mark.';invalid.focus();return;}
    if(!count){err.textContent='Enter at least one mark before saving.';return;}
    if(!ui.canWrite){err.textContent='Your account has view-only access.';return;}
    save.disabled=true;save.textContent='Saving marks…';
    const assessmentIds=[];
    const ok=await run(async()=>{
      for(const subject of subjects){
        const existing=S.grades.find(g=>g.classId===c.id&&g.subject===subject&&g.title===title&&g.date===date);
        const scores=Object.assign({},existing&&existing.scores||{},incoming[subject]);
        const record={id:existing?existing.id:genId(),classId:c.id,subject,title,date,max,scores};
        await backend.put('grades',record);
        assessmentIds.push(record.id);
      }
    },'Saved marks for all '+subjects.length+' subjects');
    if(ok){ui.grAssess=assessmentIds[0]||'';ui.grDraft=null;ui.grTab='assess';closeDlg();render();}
    else{
      err.textContent='Saving did not finish. Some subject assessments may already have been saved; check Grades before retrying. Reusing the same title and date will update matching assessments.';
      save.disabled=false;save.textContent='Save all subject marks';
    }
  });
}

function assessForm(g){
  const c=cls(ui.grClass);if(!c)return;
  const subs=(c.subjects||[]).slice();if(g&&!subs.includes(g.subject))subs.push(g.subject);
  formDialog({title:g?'Edit assessment':'New assessment for '+c.name,
    fields:[subs.length?{name:'subject',label:'Subject',type:'select',required:true,options:subs.map(x=>({v:x,l:x}))}:{name:'subject',label:'Subject',required:true},
      {name:'title',label:'Title',required:true,placeholder:'For example Midterm test'},
      {name:'date',label:'Date',type:'date',required:true},{name:'max',label:'Maximum score',type:'number',required:true,min:1}],
    values:g||{date:todayStr(),max:100},
    onSave:async v=>{let nid;const ok=await run(async()=>{nid=await backend.put('grades',Object.assign({scores:{}},g||{},{classId:c.id,subject:v.subject,title:v.title,date:v.date,max:v.max}))},g?'Assessment updated':'Assessment created');
      if(ok){ui.grAssess=nid;ui.grDraft=null;ui.grTab='assess';render()}return ok}});
}
function noticeForm(){
  formDialog({title:'Post a notice',submit:'Post notice',
    fields:[{name:'title',label:'Title',required:true,wide:true},
      {name:'audience',label:'For',type:'select',options:['Everyone','Parents','Teachers','Students'].map(x=>({v:x,l:x}))},
      {name:'body',label:'Message',type:'textarea',required:true,wide:true}],
    onSave:v=>run(()=>backend.put('notices',{title:v.title,audience:v.audience,body:v.body,date:todayStr()}),'Notice posted')});
}

/* ---------- detail dialogs ---------- */
function stuDetail(id){
  const s=stu(id);if(!s)return;
  const ap=attPct(attMap()[id]),b=balMap()[id],avgs=subjAvgs(id),ov=mean(Object.values(avgs));
  const res=S.grades.filter(g=>g.classId===s.classId&&Number.isFinite(g.scores&&g.scores[id])).sort((a,b)=>(b.date||'').localeCompare(a.date||'')).slice(0,6);
  dlg(`<div class="dhead"><div class="avatar" aria-hidden="true">${esc(initials(s.name))}</div><div><h2>${esc(s.name)}</h2><p class="mut">${esc(className(s.classId))}, admission no. ${esc(s.admNo||'not set')}</p></div></div>
  <dl class="kv"><div><dt>Parent or guardian</dt><dd>${esc(s.guardian||'Not set')}</dd></div><div><dt>Guardian phone</dt><dd>${esc(s.phone||'Not set')}</dd></div><div><dt>Date of birth</dt><dd>${s.dob?fmtDate(s.dob):'Not set'}</dd></div><div><dt>Gender</dt><dd>${s.gender==='F'?'Female':s.gender==='M'?'Male':'Not stated'}</dd></div></dl>
  <div class="three"><div><span>Attendance</span><b>${ap===null?'No data':ap+'%'}</b></div><div><span>Average mark</span><b>${ov===null?'No data':Math.round(ov)+'% '+letter(ov)}</b></div><div${ui.role!=='admin'?' hidden':''}><span>Fee balance</span><b class="${b.bal>0?'owe':''}">${b.billed===0?'Not billed':money(b.bal)}</b></div></div>
  <div><h3 style="margin-top:0">Recent results</h3>${res.length?`<ul class="list">${res.map(g=>`<li><span>${esc(g.subject)}: ${esc(g.title)}</span><span>${g.scores[id]} / ${g.max} <b>${letter(Math.min(100,g.scores[id]/g.max*100))}</b></span></li>`).join('')}</ul>`:'<p class="mut">No scores recorded yet.</p>'}</div>
  <div class="dact" style="justify-content:space-between"><span class="row w">${btn('Edit','stu-edit',{id})}${btn('Delete','stu-del',{id})}</span><span class="row">${btn('Report card','rc',{id})}${ui.role==='admin'?btn('Fee ledger','ledger',{id}):''}${btn('Close','close',{pri:1})}</span></div>`);
}
function ledger(sid){
  const s=stu(sid);if(!s)return;const rows=[];
  S.fees.forEach(f=>{
    if(f.kind==='charge'&&(f.studentIds||[]).includes(sid))rows.push({d:f.date||'',t:f.note||'Charge',a:+f.amount||0,c:true,id:f.id,shared:(f.studentIds||[]).length>1});
    else if(f.kind==='payment'&&f.studentId===sid)rows.push({d:f.date||'',t:[f.method||'Payment',f.note].filter(Boolean).join(', '),a:+f.amount||0,c:false,id:f.id})});
  rows.sort((a,b)=>a.d.localeCompare(b.d));let r=0;rows.forEach(x=>{r+=x.c?x.a:-x.a;x.run=r});
  dlg(`<div><h2>${esc(s.name)}</h2><p class="mut">${esc(className(s.classId))}, balance <b class="${r>0?'owe':''}">${money(r)}</b></p></div>
  ${rows.length?`<div class="tw"><table class="tbl" style="min-width:480px"><thead><tr><th>Date</th><th>Description</th><th class="r">Charge</th><th class="r">Payment</th><th class="r">Balance</th><th></th></tr></thead><tbody>${rows.map(x=>`<tr><td>${fmtDate(x.d)}</td><td>${esc(x.t)}</td><td class="r">${x.c?money(x.a):''}</td><td class="r">${x.c?'':money(x.a)}</td><td class="r">${money(x.run)}</td><td class="r"><span class="w">${x.shared?'<small class="mut">Class charge</small>':btn('Remove','fee-del',{id:x.id,sm:1,extra:` data-sid="${esc(sid)}"`})}</span></td></tr>`).join('')}</tbody></table></div>`:'<p class="mut">No charges or payments yet.</p>'}
  <div class="dact" style="justify-content:space-between"><span class="row w">${btn('Add charge','charge',{id:sid})}${btn('Record payment','pay',{id:sid,pri:1})}</span>${btn('Close','close')}</div>`);
}

/* ---------- timetable editor ---------- */
function timetableForm(t){
 formDialog({title:t?'Edit lesson':'Add timetable lesson',values:t||{day:'Monday',start:'08:00',end:'08:40'},fields:[
 {name:'day',label:'Day',type:'select',required:true,options:['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday'].map(x=>({v:x,l:x}))},
 {name:'start',label:'Start time',type:'time',required:true},{name:'end',label:'End time',type:'time',required:true},
 {name:'classId',label:'Class',type:'select',required:true,options:S.classes.map(c=>({v:c.id,l:c.name}))},
 {name:'subject',label:'Subject',required:true},{name:'teacherId',label:'Teacher',type:'select',options:[{v:'',l:'Unassigned'},...S.teachers.map(x=>({v:x.id,l:x.name}))]},
 {name:'room',label:'Room / venue'}],onSave:async v=>{
 if(v.end<=v.start)return ($('#frm-err').textContent='End time must be after start time.',false);
 const conflict=S.timetable.find(x=>x.id!==(t&&t.id)&&x.day===v.day&&x.classId===v.classId&&v.start<x.end&&v.end>x.start);
 if(conflict)return ($('#frm-err').textContent='This class already has a lesson during that time.',false);
 return run(()=>backend.put('timetable',Object.assign({},t||{},v)),'Timetable saved');
 }});
}
function eventForm(ev){
 formDialog({title:ev?'Edit event':'Add school event',values:ev||{date:todayStr(),category:'School activity'},fields:[
 {name:'title',label:'Event title',required:true,wide:true},{name:'date',label:'Date',type:'date',required:true},
 {name:'category',label:'Category',type:'select',options:['School activity','Examination','Meeting','Holiday','Deadline','Other'].map(x=>({v:x,l:x}))},
 {name:'location',label:'Location'},{name:'description',label:'Details',type:'textarea',wide:true}],onSave:v=>run(()=>backend.put('events',Object.assign({},ev||{},v)),'Event saved')});
}
function expenseForm(x){
 formDialog({title:x?'Edit expense':'Record expense',values:x||{date:todayStr(),category:'Utilities'},fields:[
 {name:'date',label:'Date',type:'date',required:true},{name:'category',label:'Category',type:'select',required:true,options:['Utilities','Supplies','Repairs','Transport','Salaries','Food','Other'].map(v=>({v,l:v}))},
 {name:'description',label:'Description',required:true,wide:true},{name:'payee',label:'Paid to'},{name:'amount',label:'Amount',type:'number',min:0,required:true}],onSave:v=>run(()=>backend.put('expenses',Object.assign({},x||{},v,{amount:Number(v.amount)})),'Expense saved')});
}
function browserDownload(filename,content,type){
 const blob=new Blob([content],{type:type||'text/plain;charset=utf-8'}),url=URL.createObjectURL(blob),a=document.createElement('a');
 a.href=url;a.download=filename;a.style.display='none';document.body.appendChild(a);a.click();a.remove();
 setTimeout(()=>URL.revokeObjectURL(url),1500);
}
function downloadBackup(){
 try{
   const payload={app:'School Management',version:2,exportedAt:new Date().toISOString(),data:S};
   browserDownload('school-backup-'+todayStr()+'.json',JSON.stringify(payload,null,2),'application/json');
   toast('Backup downloaded. Store it somewhere safe.');
 }catch(e){toast('Could not create backup in this browser.',true)}
}
function importBackup(){
 const input=document.createElement('input');input.type='file';input.accept='.json,application/json';
 input.onchange=async()=>{const file=input.files&&input.files[0];if(!file)return;
 try{const data=JSON.parse(await file.text()),d=data.data||data;
 if(!d||typeof d!=='object'||!Array.isArray(d.students)||!Array.isArray(d.teachers)||!Array.isArray(d.classes))throw Error('This file does not look like a school backup.');
 const allowedCols=['students','teachers','classes','attendance','grades','fees','notices','timetable','events','expenses'];
 for(const col of allowedCols){if(d[col]!==undefined&&!Array.isArray(d[col]))throw Error('Invalid backup section: '+col)}
 if(d.settings!==undefined&&(typeof d.settings!=='object'||Array.isArray(d.settings)))throw Error('Invalid school settings in backup.');
 for(const col of allowedCols){for(const rec of (d[col]||[])){if(!rec||typeof rec!=='object'||Array.isArray(rec)||!rec.id)throw Error('Invalid record in '+col+'.')}}
 if(!await confirmBox('Restore backup?','This replaces the current school records with the selected backup. Download a backup first if you need to keep the current data.','Restore backup'))return;
 const ok=await run(async()=>{for(const c of COLS){const arr=Array.isArray(d[c])?d[c]:[];for(const old of S[c].slice())await backend.remove(c,old.id);for(const rec of arr)await backend.put(c,rec)}
 if(Array.isArray(d.accounts)){for(const old of S.accounts.slice())await backend.remove('accounts',old.id);for(const rec of d.accounts)await backend.put('accounts',rec)}if(d.settings)await backend.saveSettings(d.settings);},'Backup restored');
 if(ok){if(backend===localBackend){lsSave()}render()}
 }catch(e){toast('Could not restore backup: '+(e.message||'invalid file'),true)}};
 input.click();
}

async function sampleData(){
  if(ui.busy)return;ui.busy=true;toast('Loading sample data, this takes a few seconds\u2026');
  let seed=7;const rnd=()=>{seed=(seed*1103515245+12345)&0x7fffffff;return seed/0x7fffffff};
  try{
    const put=(c,o)=>backend.put(c,o);
    const subjects=['English','Mathematics','Science','Social Studies'];
    const T=[['Ms. Namukasa','English'],['Mr. Okumu','Mathematics'],['Mrs. Tendo','Science'],['Mr. Ssebugwawo','Social Studies']];
    const tIds=[];for(const t of T)tIds.push(await put('teachers',{name:t[0],subject:t[1],phone:'',email:''}));
    const cDefs=[['Class 5A',tIds[0]],['Class 5B',tIds[1]],['Class 6A',tIds[2]]];
    const cIds=[];for(const c of cDefs)cIds.push(await put('classes',{name:c[0],teacherId:c[1],subjects}));
    const names=['Amina Okello','Brian Mugisha','Chloe Nakato','David Kato','Esther Achieng','Felix Ssemakula','Grace Auma','Hassan Mukasa','Irene Namutebi','Joel Opio','Kevin Byaruhanga','Lydia Nabirye','Moses Tumusiime','Naomi Akello','Oscar Lubega','Patience Atim','Ruth Nansubuga','Samuel Waiswa'];
    const sIds=[[],[],[]];
    for(let i=0;i<names.length;i++){const ci=i%3,sn=names[i].split(' ')[1];
      const id=await put('students',{name:names[i],classId:cIds[ci],admNo:pad(i+1).padStart(3,'0'),gender:i%2?'M':'F',dob:'2015-'+pad(1+i%12)+'-'+pad(3+i),guardian:(i%2?'Mr. ':'Mrs. ')+sn,phone:'0700 000 0'+pad(10+i)});
      sIds[ci].push(id)}
    const days=[];for(let k=0;days.length<4&&k<14;k++){const d=new Date();d.setDate(d.getDate()-k);if(d.getDay()!==0&&d.getDay()!==6)days.push(dstr(d))}
    for(let ci=0;ci<3;ci++)for(let di=0;di<days.length;di++){
      if(ci===2&&di===0)continue;
      const marks={};sIds[ci].forEach(id=>{const r=rnd();marks[id]=r<.08?'A':r<.16?'L':'P'});
      await put('attendance',{id:cIds[ci]+'_'+days[di],classId:cIds[ci],date:days[di],marks})}
    for(let ci=0;ci<3;ci++){
      for(const g of [['Mathematics','Midterm test',50],['English','Essay',20]]){
        const scores={};sIds[ci].forEach(id=>{scores[id]=Math.round(g[2]*(.4+rnd()*.55)*2)/2});
        await put('grades',{classId:cIds[ci],subject:g[0],title:g[1],date:days[days.length-1],max:g[2],scores})}}
    const now=todayStr();
    for(let ci=0;ci<3;ci++)await put('fees',{kind:'charge',scope:'class',classId:cIds[ci],studentIds:sIds[ci],note:'Tuition, Term 1',amount:400,date:now,term:'Term 1'});
    for(let i=0;i<12;i++){const ci=i%3;await put('fees',{kind:'payment',studentId:sIds[ci][Math.floor(i/3)],amount:i%3===0?400:200,date:now,method:i%2?'Mobile money':'Cash',note:''})}
    await put('notices',{title:'Welcome to the new term',audience:'Everyone',body:'Classes start at 8:00. Please make sure school fees for the term are cleared by the end of the month.',date:now});
    toast('Sample data loaded');
  }catch(e){toast(errMsg(e),true)}
  ui.busy=false;scheduleRender();
}

/* ---------- csv export ---------- */
const csvCell=c=>{let s=String(c==null?'':c);if(/^[=+\-@]/.test(s))s="'"+s;return /[",\n]/.test(s)?'"'+s.replace(/"/g,'""')+'"':s};
const toCsv=rows=>rows.map(r=>r.map(csvCell).join(',')).join('\n');
async function exportCsv(kind){
  const bm=balMap();let rows,name;
  if(kind==='students'){name='students.csv';rows=[['Admission no.','Name','Class','Gender','Date of birth','Guardian','Phone','Fee balance']].concat(S.students.slice().sort(byName).map(s=>[s.admNo,s.name,className(s.classId),s.gender,s.dob,s.guardian,s.phone,bm[s.id].bal]))}
  else{name='fee-ledger.csv';const ent=[];
    S.fees.forEach(f=>{if(f.kind==='payment'){const s=stu(f.studentId);if(s)ent.push([f.date,s.name,className(s.classId),'Payment',f.method||'',f.note||'',f.amount])}
      else(f.studentIds||[]).forEach(id=>{const s=stu(id);if(s)ent.push([f.date,s.name,className(s.classId),'Charge','',f.note||'',f.amount])})});
    ent.sort((a,b)=>String(a[0]).localeCompare(String(b[0])));rows=[['Date','Student','Class','Type','Method','Description','Amount']].concat(ent)}
  try{await ui.dl.save({filename:name,data:toCsv(rows)})}catch(e){if(!e||e.code!=='declined')toast('Couldn\u2019t export the file.',true)}
}

/* ---------- events ---------- */
async function unsaved(kind){
  const d=kind==='att'?ui.attDraft:ui.grDraft;if(!d||!d.dirty)return true;
  return confirmBox('Discard unsaved changes?','You have changes that haven\u2019t been saved yet.','Discard');
}
document.addEventListener('click',async e=>{
  const el=e.target.closest('[data-act]');if(!el)return;
  const a=el.dataset.act,id=el.dataset.id;
  switch(a){
    case 'nav':go(el.dataset.view);break;
    case 'login-tab':ui.loginTab=el.dataset.tab;render();break;
    case 'auth-tab':ui.authTab=el.dataset.tab;ui.authError='';render();break;
    case 'forgot-password':{const em=$('#lg-id')&&$('#lg-id').value.trim();if(!em){toast('Enter your email address first.',true);break}await sendPasswordReset(em);break}
    case 'resend-confirmation':{const em=$('#lg-id')&&$('#lg-id').value.trim();if(!em){toast('Enter the email address you used to register.',true);break}await resendConfirmationEmail(em);break}
    case 'copy-join-code':if(ui.joinCode){try{await navigator.clipboard.writeText(ui.joinCode);toast('School join code copied.')}catch(e){toast('Copy is unavailable; select and copy the code manually.',true)}}break;
    case 'pw-toggle':{const i=el.closest('.pw').querySelector('input');const sh=i.type==='password';i.type=sh?'text':'password';el.textContent=sh?'Hide':'Show';break}
    case 'logout':await logout();break;
    case 'rc':reportDialog(id);break;
    case 'rc-dl':rcDownload([id]);break;
    case 'rc-class':{const ids=S.students.filter(s=>s.classId===id).sort(byName).map(s=>s.id);if(!ids.length){toast('No students in this class.',true);break}rcDownload(ids,cls(id)&&cls(id).name);break}
    case 'user-new':userForm();break;
    case 'user-edit':userForm(by(S.accounts,id));break;
    case 'user-pw':await resetPwForm(by(S.accounts,id));break;
    case 'user-toggle':{const a=by(S.accounts,id);if(!a)break;
      if(ui.acct&&a.id===ui.acct.id){toast('You can’t disable your own account.',true);break}
      if(!a.disabled&&a.role==='admin'&&adminCount(a.id)===0){toast('There must be at least one active administrator.',true);break}
      await run(()=>backend.put('accounts',Object.assign({},a,{disabled:!a.disabled})),a.disabled?'User enabled':'User disabled');break}
    case 'user-del':{const a=by(S.accounts,id);if(!a)break;
      if(a.role==='admin'&&!a.disabled&&adminCount(a.id)===0){toast('There must be at least one active administrator.',true);break}
      if(await confirmBox('Delete '+a.name+'?','They will no longer be able to sign in. Records they entered are kept.','Delete user'))await run(()=>backend.remove('accounts',id),'User deleted');break}
    case 'close':closeDlg();break;
    case 'c-yes':case 'c-no':{const r=pend;pend=null;closeDlg();if(r)r(a==='c-yes');break}
    case 'sample':sampleData();break;
    case 'tt-new':timetableForm();break;
    case 'tt-edit':timetableForm(by(S.timetable,id));break;
    case 'tt-del':if(await confirmBox('Delete lesson?','This lesson will be removed from the timetable.','Delete'))await run(()=>backend.remove('timetable',id),'Lesson deleted');break;
    case 'event-new':eventForm();break;
    case 'event-edit':eventForm(by(S.events,id));break;
    case 'event-del':if(await confirmBox('Delete event?','This event will be removed from the school calendar.','Delete'))await run(()=>backend.remove('events',id),'Event deleted');break;
    case 'expense-new':expenseForm();break;
    case 'expense-edit':expenseForm(by(S.expenses,id));break;
    case 'expense-del':if(await confirmBox('Delete expense?','This expense record will be removed.','Delete'))await run(()=>backend.remove('expenses',id),'Expense deleted');break;
    case 'print-page':window.print();break;
    case 'backup':downloadBackup();break;
    case 'restore':importBackup();break;
    case 'goto-att':ui.attClass=id;ui.attDraft=null;ui.attDate=todayStr();go('attendance');break;
    // students
    case 'stu-new':studentForm();break;
    case 'stu-open':stuDetail(id);break;
    case 'stu-edit':studentForm(stu(id));break;
    case 'stu-del':{const s=stu(id);if(!s)break;
      if(await confirmBox('Delete '+s.name+'?','This removes the student and their payments. Attendance and grade history for the class stays in the totals already recorded.','Delete student')){
        const pays=S.fees.filter(f=>f.kind==='payment'&&f.studentId===id);
        const ok=await run(async()=>{for(const p of pays)await backend.remove('fees',p.id);await backend.remove('students',id)},'Student deleted');if(!ok)closeDlg()}
      else stuDetail(id);break}
    // teachers
    case 'tea-new':teacherForm();break;
    case 'tea-edit':teacherForm(by(S.teachers,id));break;
    case 'tea-del':{const t=by(S.teachers,id);if(!t)break;
      if(await confirmBox('Delete '+t.name+'?','They will be removed as class teacher from any class they lead.','Delete teacher'))
        await run(async()=>{for(const c of S.classes.filter(c=>c.teacherId===id))await backend.put('classes',Object.assign({},c,{teacherId:''}));await backend.remove('teachers',id)},'Teacher deleted');break}
    // classes
    case 'class-new':classForm();break;
    case 'class-edit':classForm(cls(id));break;
    case 'class-del':{const c=cls(id);if(!c)break;
      const n=S.students.filter(s=>s.classId===id).length;
      if(n){toast('Move or delete the '+plural(n,'student')+' in '+c.name+' first.',true);break}
      if(await confirmBox('Delete '+c.name+'?','Its registers and assessments will be deleted too.','Delete class'))
        await run(async()=>{for(const x of S.attendance.filter(x=>x.classId===id))await backend.remove('attendance',x.id);for(const g of S.grades.filter(g=>g.classId===id))await backend.remove('grades',g.id);await backend.remove('classes',id)},'Class deleted');break}
    // attendance
    case 'mark':{const d=ui.attDraft;if(!d||!ui.canWrite)break;const v=el.dataset.v;if(d.marks[id]===v)delete d.marks[id];else d.marks[id]=v;d.dirty=true;render();break}
    case 'att-all':{const d=ui.attDraft;if(!d)break;S.students.filter(s=>s.classId===ui.attClass).forEach(s=>d.marks[s.id]='P');d.dirty=true;render();break}
    case 'att-save':{const d=ui.attDraft,c=cls(ui.attClass);if(!d||!c)break;
      const ids=new Set(S.students.filter(s=>s.classId===c.id).map(s=>s.id)),marks={};
      Object.keys(d.marks).forEach(k=>{if(ids.has(k))marks[k]=d.marks[k]});
      const ok=await run(()=>backend.put('attendance',{id:c.id+'_'+ui.attDate,classId:c.id,date:ui.attDate,marks}),'Register saved');
      if(ok){d.dirty=false;render()}break}
    case 'att-date':if(await unsaved('att')){ui.attDate=el.dataset.date;ui.attDraft=null}render();break;
    // grades
    case 'g-tab':ui.grTab=el.dataset.tab;render();break;
    case 'g-pick':if(await unsaved('gr')){ui.grAssess=id;ui.grDraft=null}render();break;
    case 'g-new':assessForm();break;
    case 'g-bulk':bulkMarksForm();break;
    case 'g-edit':assessForm(by(S.grades,id));break;
    case 'g-del':{const g=by(S.grades,id);if(!g)break;
      if(await confirmBox('Delete this assessment?',g.subject+': '+g.title+' and all its scores will be removed.','Delete assessment')){
        if(await run(()=>backend.remove('grades',id),'Assessment deleted')){ui.grAssess='';ui.grDraft=null;render()}}break}
    case 'g-save':{const d=ui.grDraft,g=d&&by(S.grades,d.id);if(!g)break;const sc={};
      Object.keys(d.scores).forEach(k=>{const n=d.scores[k];if(Number.isFinite(n))sc[k]=Math.max(0,Math.min(g.max,n))});
      const ok=await run(()=>backend.put('grades',Object.assign({},g,{scores:sc})),'Scores saved');
      if(ok){d.dirty=false;d.scores=sc;render()}break}
    // fees
    case 'bill':billForm();break;
    case 'pay':payForm(id);break;
    case 'charge':chargeForm(id);break;
    case 'ledger':ledger(id);break;
    case 'fee-del':{const sid=el.dataset.sid;
      if(await confirmBox('Remove this entry?','The student\u2019s balance will be recalculated.','Remove')){await run(()=>backend.remove('fees',id),'Entry removed');setTimeout(()=>ledger(sid),80)}else ledger(sid);break}
    case 'bill-del':{const f=by(S.fees,id);if(!f)break;
      if(await confirmBox('Remove this class charge?','It will be taken off all '+(f.studentIds||[]).length+' students it was applied to.','Remove charge'))await run(()=>backend.remove('fees',id),'Charge removed');break}
    // notices
    case 'notice-new':noticeForm();break;
    case 'notice-del':if(await confirmBox('Delete this notice?','It will no longer show on the overview.','Delete notice'))await run(()=>backend.remove('notices',id),'Notice deleted');break;
    // settings
    case 'set-save':{const pass=Number($('#set-pass').value);
      if(!Number.isFinite(pass)||pass<0||pass>100){toast('Pass mark must be between 0 and 100.',true);break}
      await run(()=>backend.saveSettings({schoolName:$('#set-name').value.trim()||'My school',term:$('#set-term').value.trim(),currency:$('#set-cur').value,passMark:pass}),'Settings saved');break}
    case 'exp-students':exportCsv('students');break;
    case 'exp-fees':exportCsv('fees');break;
    case 'wipe':if(await confirmBox('Clear all records?','This permanently deletes every student, teacher, class, register, grade, fee and notice.','Clear everything')){
      toast('Clearing records\u2026');await run(()=>backend.wipe(),'All records cleared')}break;
  }
});
document.addEventListener('input',e=>{
  const el=e.target.closest('[data-in]');if(!el)return;const k=el.dataset.in;
  if(k==='sq'){ui.sq=el.value;render()}
  else if(k==='fq'){ui.fq=el.value;render()}
  else if(k==='lgid'){ui.loginId=el.value}
  else if(k==='score'){
    const d=ui.grDraft,g=d&&by(S.grades,d.id);if(!g)return;const sid=el.dataset.id,v=el.value.trim();
    if(v==='')delete d.scores[sid];else{const n=Number(v);if(Number.isFinite(n))d.scores[sid]=n}
    d.dirty=true;const p=document.getElementById('pc-'+sid);if(p){const n=d.scores[sid];p.innerHTML=Number.isFinite(n)?pctCell(n,g.max):''}
    const sv=$('#g-save');if(sv)sv.disabled=false}
});
document.addEventListener('change',async e=>{
  const el=e.target.closest('[data-in]');if(!el)return;const k=el.dataset.in;
  if(k==='sclass'){ui.sclass=el.value;render()}
  else if(k==='fowing'){ui.fowing=el.checked;render()}
  else if(k==='attClass'||k==='attDate'){if(el.value&&await unsaved('att')){ui[k]=el.value;ui.attDraft=null}render()}
  else if(k==='grClass'){if(await unsaved('gr')){ui.grClass=el.value;ui.grAssess='';ui.grDraft=null}render()}
});
document.addEventListener('submit',e=>{
  const id=e.target&&e.target.id;
  if(id==='lf'){e.preventDefault();doLogin()}
  else if(id==='sf'){e.preventDefault();doSetup()}
  else if(id==='mf'){e.preventDefault();doMembershipSetup()}
  else if(id==='cf'){e.preventDefault();doChange()}
});
$('#dlg').addEventListener('click',e=>{if(e.target===$('#dlg'))closeDlg()});
$('#dlg').addEventListener('close',()=>{if(pend){const r=pend;pend=null;r(false)}});

/* ---------- init ---------- */
async function init(){
  try {
    const callbackUrl=new URL(window.location.href);
    const callbackHash=new URLSearchParams(callbackUrl.hash.replace(/^#/,''));
    const callbackError=callbackUrl.searchParams.get('error_description')||callbackUrl.searchParams.get('error')||callbackHash.get('error_description')||callbackHash.get('error');
    const callbackErrorCode=callbackUrl.searchParams.get('error_code')||callbackHash.get('error_code')||'';
    if(callbackError){
      const decoded=String(callbackError).replace(/\+/g,' ');
      if(/otp_expired|expired|invalid/i.test(callbackErrorCode+' '+decoded))
        ui.authError='This confirmation link has expired or was already used. To use no-code password sign-in for future accounts, turn off Confirm email in Supabase Authentication settings. Existing unconfirmed accounts may need to be confirmed or recreated.';
      else ui.authError='Email confirmation could not finish: '+decoded+'. To skip verification codes for new accounts, turn off Confirm email in Supabase Authentication settings. For confirmation-based accounts, check the Supabase Site URL and Redirect URLs.';
      ['error','error_code','error_description'].forEach(k=>{callbackUrl.searchParams.delete(k);callbackHash.delete(k)});
      callbackUrl.hash=callbackHash.toString()?'#'+callbackHash.toString():'';
      history.replaceState({},document.title,callbackUrl.pathname+(callbackUrl.search?callbackUrl.search:'')+callbackUrl.hash);
    }
    render();
  } catch(e){console.error('EDUNEXUS startup render failed:',e);throw e;}
  const cfg=window.EDUNEXUS_CONFIG||{};
  const cloudConfigured=typeof cfg.SUPABASE_URL==='string'&&/^https:\/\//.test(cfg.SUPABASE_URL)&&typeof cfg.SUPABASE_ANON_KEY==='string'&&cfg.SUPABASE_ANON_KEY.length>20&&!/YOUR_|PASTE_|REPLACE_ME/i.test(cfg.SUPABASE_URL+cfg.SUPABASE_ANON_KEY);
  if(cloudConfigured&&window.supabase&&typeof window.supabase.createClient==='function'){
    try{
      supabaseClient=window.supabase.createClient(cfg.SUPABASE_URL,cfg.SUPABASE_ANON_KEY,{auth:{persistSession:true,autoRefreshToken:true,detectSessionInUrl:true}});
      backend=supabaseBackend(supabaseClient);ui.mode='shared';ui.share='viewer';ui.role='viewer';ui.canWrite=false;ui.cloudStatus='CONNECTING';ui.cloudReady=false;COLS.forEach(c=>ui.loaded[c]=true);ui.loaded.accounts=true;
      supabaseClient.auth.onAuthStateChange((_event,session)=>{setTimeout(()=>syncAuthSession(session&&session.user||null).catch(e=>{console.error('EDUNEXUS auth refresh failed',e);ui.authError=e.message||'Authentication could not be refreshed.';render();}),0)});
      const {data,error}=await supabaseClient.auth.getSession();if(error)throw error;
      await syncAuthSession(data.session&&data.session.user||null);
      if(ui.authUser)await completePendingMembership().catch(e=>{console.warn('Pending school setup not finished',e);ui.authError=e.message||'Pending school setup failed.';render();});
      render();return;
    }catch(e){console.error('Supabase initialization failed:',e);ui.authError=e.message||'Could not connect to Supabase.';}
  }
  backend=localBackend;ui.mode='local';ui.share='admin';ui.role='admin';ui.canWrite=true;lsLoad();restoreSession();render();
}

init();
})();
</script>
</body>
</html>
