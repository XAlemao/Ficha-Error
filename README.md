# Ficha-Error
Ficha de RPG

<!doctype html>
<html lang="pt-BR">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Ficha RPG — Projeto Final (3 páginas)</title>
<style>
  /* Theme variables (default = Preto) */
  :root{
    --bg: #0b0b0b;
    --panel-bg: #111;
    --panel-fore: #fff;
    --accent: #a41f1f;
    --muted: #aaa;
    --panel-border: #000;
    --hp-good: #2ecc71;
    --hp-bad: #e74c3c;
    --culpa-good: #4caf50;
    --culpa-bad: #f44336;
    --card-bg: #fff;
    --card-fore: #000;
    --btn-shadow: 0 3px 8px rgba(0,0,0,0.4);
  }
  /* Purple theme */
  :root[data-theme="roxo"]{
    --bg:#0e0416; --panel-bg:#12061b; --panel-fore:#efe6ff;
    --accent:#8a3ab9; --muted:#cdbbed; --panel-border:#200529;
    --hp-good:#7ee0a6; --hp-bad:#ff6b9a;
    --culpa-good:#a3ff8a; --culpa-bad:#ff75a3;
    --card-bg:#12061b; --card-fore:#efe6ff;
  }
  /* Red theme */
  :root[data-theme="vermelho"]{
    --bg:#130000; --panel-bg:#2b0606; --panel-fore:#fff0f0;
    --accent:#c62828; --muted:#f0cfcf; --panel-border:#3b0000;
    --hp-good:#ff9f9f; --hp-bad:#8b0000;
    --culpa-good:#ffd7d7; --culpa-bad:#ff6b6b;
    --card-bg:#2b0606; --card-fore:#fff0f0;
  }
  /* Dark blue theme (replaces white) */
  :root[data-theme="azul"]{
    --bg:#071328; --panel-bg:#0b1730; --panel-fore:#e8f2ff;
    --accent:#1f6feb; --muted:#9eb9e6; --panel-border:#05213b;
    --hp-good:#6be6a1; --hp-bad:#ff6b6b;
    --culpa-good:#7fe1ff; --culpa-bad:#ff9fb3;
    --card-bg:#071a33; --card-fore:#e8f2ff;
  }

  html,body{height:100%;margin:0;font-family:Inter,system-ui,Segoe UI,Arial,Helvetica,sans-serif;background:var(--bg);color:var(--panel-fore)}
  .app{max-width:1400px;margin:12px auto;padding:12px;box-sizing:border-box}
  header{display:flex;align-items:center;gap:12px;margin-bottom:12px}
  header h1{margin:0;font-size:1.15rem}
  .top-controls{margin-left:auto;display:flex;gap:8px;align-items:center}

  /* buttons improved */
  button, select, input[type="button"]{
    background:var(--accent);
    color:var(--panel-fore);
    border:0;
    padding:8px 10px;
    border-radius:8px;
    cursor:pointer;
    box-shadow: var(--btn-shadow);
    transition: transform .12s ease, box-shadow .12s ease, opacity .12s ease;
  }
  button.secondary{
    background:transparent;
    border:1px solid rgba(255,255,255,0.08);
    box-shadow:none;
  }
  button:hover{ transform: translateY(-2px); opacity:0.98; }
  .muted{color:var(--muted);font-size:13px}

  /* Main area: left = saved list/actions, center = tabs/pages, right = quick info */
  .layout{display:grid;grid-template-columns:320px 1fr 260px;gap:12px}
  @media(max-width:1100px){ .layout{grid-template-columns:1fr; } }

  /* Saved panel */
  .panel{background:var(--panel-bg);color:var(--panel-fore);padding:10px;border-radius:8px;border:1px solid var(--panel-border);box-sizing:border-box}
  .saved-list{width:100%;padding:6px;border-radius:6px;background:transparent;border:1px solid rgba(255,255,255,0.06);color:var(--panel-fore)}
  .saved-actions{display:flex;gap:6px;margin-top:8px;flex-wrap:wrap}
  .small{font-size:13px}

  /* Tabs & pages */
  .tabs{display:flex;gap:6px;margin-bottom:8px}
  .tabs button{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:8px 10px;border-radius:6px}
  .tabs button.active{background:var(--accent);color:var(--panel-fore)}
  .pages{background:var(--card-bg);color:var(--card-fore);padding:12px;border-radius:8px;border:1px solid var(--panel-border)}
  .page{display:none}
  .page.active{display:block}

  /* 3-column page layout inside page for print */
  .three-cols{display:grid;grid-template-columns:320px 1fr 320px;gap:12px}
  @media(max-width:1100px){ .three-cols{grid-template-columns:1fr} }

  /* portrait image */
  .portrait{background:rgba(0,0,0,0.15);padding:8px;border-radius:6px;text-align:center}
  .portrait img{width:100%;height:auto;border-radius:6px;border:2px solid var(--panel-border)}

  /* bars */
  .bar{height:20px;background:#222;border-radius:10px;overflow:hidden;border:1px solid rgba(0,0,0,0.4)}
  .bar-fill{height:100%;width:0%;transition:width .18s linear}

  /* fields */
  .field{margin-top:8px}
  label{display:block;font-size:13px;margin-bottom:6px;font-weight:600}
  input[type="text"], input[type="number"], textarea, select{width:100%;padding:6px;border-radius:6px;border:1px solid rgba(0,0,0,0.12);box-sizing:border-box}
  textarea{min-height:80px;resize:vertical}

  /* page-specific styles: make areas visually similar to samples */
  .big-box{background:rgba(0,0,0,0.04);padding:8px;border-radius:6px;min-height:120px}
  .grid-abilities{display:grid;grid-template-columns:repeat(2,1fr);gap:8px}
  .ability{background:rgba(0,0,0,0.03);padding:8px;border-radius:6px}

  /* right side quick */
  .quick{display:flex;flex-direction:column;gap:8px}
  .meta-row{display:flex;gap:8px;align-items:center}

  /* inventory */
  .inventory-grid{display:grid;grid-template-columns:repeat(8,1fr);gap:8px}
  .inv-slot{background:rgba(0,0,0,0.05);border-radius:6px;padding:6px;text-align:center;border:1px dashed rgba(255,255,255,0.04)}
  .inv-slot img{width:64px;height:64px;object-fit:cover;border-radius:6px;border:1px solid var(--panel-border);background:rgba(0,0,0,0.06)}
  .equip-list{display:flex;flex-direction:column;gap:8px}
  .equip-slot{display:flex;gap:8px;align-items:center;padding:6px;border-radius:6px;background:rgba(0,0,0,0.03)}
  .equip-slot img{width:48px;height:48px;object-fit:cover;border-radius:6px;border:1px solid var(--panel-border);background:rgba(0,0,0,0.06)}

  /* footer */
  footer{margin-top:12px;color:var(--muted);font-size:13px;text-align:center}

  /* Print rules: print only specific content */
  @page { size:A4 landscape; margin:10mm; }
  @media print{
    body{background:white;color:black}
    header, .saved-list, .saved-actions, .top-controls, .right-col, .tabs, .theme-select { display:none !important; }
    .app{max-width:100%;padding:0}
    .pages, .page{display:block !important}
    .page{page-break-after:always}
  }
  /* helper small UI */
  .row{display:flex;gap:8px;align-items:center}
  .tiny{font-size:12px;color:var(--muted)}
  .controls-row{display:flex;gap:8px;align-items:center;margin-top:8px}
</style>
</head>
<body>
<div class="app" id="app">
  <header>
    <h1>Ficha RPG — Projeto Final</h1>
    <div class="muted">(3 páginas — salvar/carregar/export/import/print)</div>
    <div class="top-controls">
      <label class="tiny">Tema</label>
      <select id="themeSelect" class="theme-select">
        <option value="preto">Preto</option>
        <option value="roxo">Roxo</option>
        <option value="vermelho">Vermelho</option>
        <option value="azul">Azul escuro</option>
      </select>
      <button id="printPageBtn" title="Imprimir página atual">Imprimir página</button>
      <button id="printAllBtn" title="Imprimir todas as páginas">Imprimir todas</button>
    </div>
  </header>

  <div class="layout">
    <!-- LEFT: saved list & actions -->
    <div>
      <div class="panel">
        <div class="small">Fichas salvas (local)</div>
        <select id="savedList" class="saved-list" size="6" style="margin-top:8px"></select>
        <div class="saved-actions">
          <button id="newBtn">Novo</button>
          <button id="saveBtn">Salvar</button>
          <button id="saveAsBtn" class="secondary">Salvar como...</button>
          <button id="loadBtn" class="secondary">Carregar</button>
          <button id="deleteBtn" class="secondary">Excluir</button>
        </div>

        <div style="margin-top:10px" class="small">
          <label><input type="checkbox" id="autoSave"> Auto-save</label>
        </div>

        <div style="margin-top:12px">
          <button id="exportJson">Exportar JSON</button>
          <button id="importJson" class="secondary">Importar JSON</button>
          <input id="importFile" type="file" accept="application/json" style="display:none"/>
        </div>

        <div style="margin-top:12px" class="tiny muted">As fichas são salvas localmente no navegador. Para sincronizar entre dispositivos, peça sincronização em nuvem.</div>
      </div>
    </div>

    <!-- CENTER: tabs & pages -->
    <div>
      <div class="tabs">
        <button class="tab-btn active" data-page="p1">Página 1 — Story</button>
        <button class="tab-btn" data-page="p2">Página 2 — Battle</button>
        <button class="tab-btn" data-page="p3">Página 3 — Inventory</button>
      </div>

      <div class="pages panel">
        <!-- PAGE 1 -->
        <div class="page active" id="p1">
          <div class="three-cols">
            <!-- left col -->
            <div>
              <div class="portrait">
                <img id="portraitImg" src="" alt="Imagem do personagem" />
                <div style="margin-top:8px" class="row">
                  <input id="fileInput" type="file" accept="image/*"/>
                  <button id="clearImg" class="secondary">Limpar</button>
                </div>
              </div>

              <div class="field">
                <label>Nome / Raça / Level</label>
                <input id="p1_name" type="text" placeholder="Nome"/>
                <div class="row" style="margin-top:6px">
                  <input id="p1_archetype" type="text" placeholder="Raça"/>
                  <input id="p1_level" type="number" min="0" placeholder="Nível" style="width:90px"/>
                </div>
              </div>

              <div class="field" style="margin-top:8px">
                <label>Atributos</label>
                <div class="small">
                  <div class="row"><div style="width:86px">Might</div><input id="attr_might" type="number" min="0" style="width:80px"/></div>
                  <div class="row"><div style="width:86px">Vitality</div><input id="attr_vitality" type="number" min="0" style="width:80px"/></div>
                  <div class="row"><div style="width:86px">Agility</div><input id="attr_agility" type="number" min="0" style="width:80px"/></div>
                  <div class="row"><div style="width:86px">Instinct</div><input id="attr_instinct" type="number" min="0" style="width:80px"/></div>
                  <div class="row"><div style="width:86px">Persona</div><input id="attr_persona" type="number" min="0" style="width:80px"/></div>
                </div>
              </div>

            </div>

            <!-- center col (story removed per request) -->
            <div>
              <div class="field">
                <label>Observações</label>
                <textarea id="p1_notes" placeholder="Campo de observações (substitui story, removido conforme solicitado)"></textarea>
              </div>
            </div>

            <!-- right col -->
            <div>
              <div class="field">
                <label>Culpa</label>
                <div class="bar" style="margin-bottom:6px">
                  <div id="culpaFill" class="bar-fill" style="background:linear-gradient(90deg,var(--culpa-good),var(--culpa-bad));width:0%"></div>
                </div>
                <div class="row">
                  <input id="culpaRange" type="range" min="0" max="100" value="0" style="flex:1"/>
                  <div id="culpaValue" class="tiny" style="width:56px;text-align:right">0%</div>
                </div>
              </div>

              <div class="field" style="margin-top:8px">
                <label>Opções</label>
                <div><label><input id="opt_grey_skills" type="checkbox"/> Skills cinza</label></div>
                <div><label><input id="opt_grey_egos" type="checkbox"/> EGOs cinza</label></div>
              </div>
            </div>
          </div>
        </div>

        <!-- PAGE 2 -->
        <div class="page" id="p2">
          <div class="three-cols">
            <!-- left: small info + passive tiles -->
            <div>
              <div class="panel" style="padding:8px">
                <label>Battle Ability / Health</label>
                <div class="field">
                  <label>HP</label>
                  <div class="bar" style="margin-bottom:6px"><div id="hpFill" class="bar-fill" style="background:linear-gradient(90deg,var(--hp-good),var(--hp-bad));width:100%"></div></div>
                  <div class="row" style="align-items:center">
                    <input id="hpCurr" type="number" min="0" style="width:80px"/> /
                    <input id="hpMax" type="number" min="1" style="width:80px"/>
                    <div id="hpPercent" class="tiny" style="margin-left:8px">100%</div>
                  </div>
                  <input id="hpRange" type="range" min="0" max="100" value="100" style="margin-top:6px;width:100%"/>
                </div>

                <div class="field" style="margin-top:8px">
                  <label>Speed / E.R.</label>
                  <input id="p2_speed" type="text" placeholder="1d8 +0"/>
                  <label style="margin-top:6px">Stagger / Max</label>
                  <input id="p2_stagger" type="text"/>
                </div>
              </div>

              <div style="margin-top:8px" class="panel">
                <label>Passivas</label>
                <div class="small">
                  <div id="passivesContainer">
                    <input id="p2_pass1" placeholder="Passiva 1"/>
                    <input id="p2_pass2" placeholder="Passiva 2" style="margin-top:6px"/>
                    <!-- extras inserted here -->
                  </div>
                  <div class="controls-row">
                    <button id="addPassiveBtn" class="secondary">Adicionar Passiva</button>
                  </div>
                </div>
              </div>
            </div>

            <!-- center: abilities grid -->
            <div>
              <div class="field">
                <label>Battle Abilities (slots)</label>
                <div class="controls-row" style="margin-bottom:6px">
                  <button id="addAbilityBtn">Adicionar Battle Ability</button>
                </div>
                <div id="abilitiesContainer" class="grid-abilities">
                  <div class="ability">
                    <label>Ability 1</label>
                    <input id="p2_a1_name" placeholder="Nome"/>
                    <div class="row" style="margin-top:6px">
                      <input id="p2_a1_cost" placeholder="Custo" style="width:100px"/>
                      <input id="p2_a1_limit" placeholder="Limit" style="width:100px"/>
                    </div>
                    <textarea id="p2_a1_effect" placeholder="Efeitos / Dice results" style="margin-top:6px"></textarea>
                    <div class="tiny">Módulos usados (lista)</div>
                    <input id="p2_a1_modules" placeholder="module1, module2" />
                  </div>

                  <div class="ability">
                    <label>Ability 2</label>
                    <input id="p2_a2_name" placeholder="Nome"/>
                    <div class="row" style="margin-top:6px">
                      <input id="p2_a2_cost" placeholder="Custo" style="width:100px"/>
                      <input id="p2_a2_limit" placeholder="Limit" style="width:100px"/>
                    </div>
                    <textarea id="p2_a2_effect" placeholder="Efeitos / Dice results" style="margin-top:6px"></textarea>
                    <div class="tiny">Módulos usados</div>
                    <input id="p2_a2_modules" placeholder="module1, module2" />
                  </div>

                  <!-- extra dynamic abilities will be appended here as elements with class 'battle-ability extra' -->
                </div>
              </div>

              <div class="field" style="margin-top:8px">
                <label>Extras / Feats (lado direito grande)</label>
                <textarea id="p2_feats" placeholder="Feats / Extras" style="height:200px"></textarea>
              </div>
            </div>

            <!-- right col: removed ability 3/4, kept notes -->
            <div>
              <div class="panel" style="padding:8px">
                <label>Notas rápidas</label>
                <textarea id="p2_notes" placeholder="Notas" style="height:200px"></textarea>
              </div>
            </div>
          </div>
        </div>

        <!-- PAGE 3: Inventory -->
        <div class="page" id="p3">
          <div class="three-cols">
            <!-- left: inventory grid -->
            <div>
              <div class="panel">
                <label>Inventário do Player</label>
                <div id="inventoryGrid" class="inventory-grid" style="margin-top:8px">
                  <!-- slots rendered here -->
                </div>
                <div class="controls-row">
                  <button id="addInvSlotBtn">Adicionar slot de inventário</button>
                  <button id="clearInvBtn" class="secondary">Limpar inventário</button>
                </div>
              </div>
            </div>

            <!-- center: equipáveis -->
            <div>
              <div class="panel">
                <label>Equipáveis</label>
                <div id="equipList" class="equip-list" style="margin-top:8px">
                  <!-- equip slots rendered here -->
                </div>
                <div class="controls-row">
                  <button id="addEquipSlotBtn">Adicionar slot equipável</button>
                </div>
              </div>
            </div>

            <!-- right: extra info / legend -->
            <div>
              <div class="panel">
                <label>Legenda / Notas do Inventário</label>
                <textarea id="p3_extra" placeholder="Notas sobre itens e regras de inventário" style="height:320px"></textarea>
              </div>
            </div>
          </div>
        </div>
      </div>

    </div>

    <!-- RIGHT: quick info + save status -->
    <div>
      <div class="panel quick">
        <div><strong>Estado</strong></div>
        <div class="meta-row"><div class="tiny">Ficha atual:</div><div id="currentName" style="margin-left:auto">—</div></div>
        <div class="meta-row"><div class="tiny">Último salvamento:</div><div id="currentTime" style="margin-left:auto">—</div></div>
        <div style="margin-top:6px">
          <div class="tiny">Ações rápidas:</div>
          <div style="display:flex;gap:6px;margin-top:6px">
            <button id="quickSave">Salvar</button>
            <button id="quickExport" class="secondary">Exportar</button>
          </div>
        </div>

        <div style="margin-top:8px" class="tiny muted">Observação: imagens são armazenadas em base64 (compactadas). Se o localStorage ficar grande, exporte como JSON para backup.</div>
      </div>
    </div>
  </div>

  <footer>Pronto — arquivo único. Tem dúvidas sobre campos específicos? Me diga e eu ajusto.</footer>
</div>

<script>
/* ---------- Utilities ---------- */
const STORAGE_KEY = 'rpg_final_v1';
let currentId = null;
let isDirty = false;
const maxImageDim = 900; // compress max dimension

// inventory/equip state
let inventoryData = []; // array of {img, caption}
let equipData = []; // array of {img, caption}

function uid(){ return 's_' + Date.now() + '_' + Math.floor(Math.random()*10000); }
function nowStr(ts){ if(!ts) return '—'; return new Date(ts).toLocaleString(); }

/* ---------- Theme handling ---------- */
const themeSelect = document.getElementById('themeSelect');
function applyTheme(name){
  if(name==='preto') name = null;
  if(name) document.documentElement.setAttribute('data-theme', name);
  else document.documentElement.removeAttribute('data-theme');
}
themeSelect.addEventListener('change', ()=> applyTheme(themeSelect.value));
(function(){ /* init default */
  applyTheme(themeSelect.value);
})();

/* ---------- Page/tab handling ---------- */
document.querySelectorAll('.tab-btn').forEach(btn=>{
  btn.addEventListener('click', ()=>{
    document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
    btn.classList.add('active');
    const page = btn.dataset.page;
    document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
    document.getElementById(page).classList.add('active');
  });
});

/* ---------- Image upload + compression ---------- */
const fileInput = document.getElementById('fileInput');
const portraitImg = document.getElementById('portraitImg');
const clearImg = document.getElementById('clearImg');

function compressAndSetImage(file, cb){
  const reader = new FileReader();
  reader.onload = function(e){
    const img = new Image();
    img.onload = function(){
      const canvas = document.createElement('canvas');
      let w = img.width, h = img.height;
      if(Math.max(w,h) > maxImageDim){
        const ratio = maxImageDim / Math.max(w,h);
        w = Math.round(w*ratio); h = Math.round(h*ratio);
      }
      canvas.width = w; canvas.height = h;
      const ctx = canvas.getContext('2d');
      ctx.fillStyle = '#fff';
      ctx.fillRect(0,0,w,h);
      ctx.drawImage(img,0,0,w,h);
      // quality 0.85
      const dataUrl = canvas.toDataURL('image/jpeg', 0.85);
      cb(dataUrl);
    };
    img.src = e.target.result;
  };
  reader.readAsDataURL(file);
}

fileInput.addEventListener('change', (e)=>{
  const f = e.target.files[0];
  if(!f) return;
  compressAndSetImage(f, (dataUrl)=>{
    portraitImg.src = dataUrl;
    markDirty();
  });
});
clearImg.addEventListener('click', ()=>{
  portraitImg.src = '';
  fileInput.value = '';
  markDirty();
});

/* ---------- Bars: Culpa & HP ---------- */
const culpaRange = document.getElementById('culpaRange');
const culpaFill = document.getElementById('culpaFill');
const culpaValue = document.getElementById('culpaValue');

function updateCulpaUI(val){
  val = Number(val) || 0;
  culpaFill.style.width = Math.min(100, Math.max(0, val)) + '%';
  culpaValue.textContent = val + '%';
}
culpaRange.addEventListener('input', ()=>{
  updateCulpaUI(culpaRange.value);
  markDirty();
});
updateCulpaUI(culpaRange.value);

const hpCurr = document.getElementById('hpCurr');
const hpMax = document.getElementById('hpMax');
const hpRange = document.getElementById('hpRange');
const hpFill = document.getElementById('hpFill');
const hpPercent = document.getElementById('hpPercent');

function updateHPUI(){
  const curr = Math.max(0, Number(hpCurr.value) || 0);
  const max = Math.max(1, Number(hpMax.value) || 1);
  const pct = Math.round((curr/max)*100);
  hpFill.style.width = Math.min(100, Math.max(0, pct)) + '%';
  hpPercent.textContent = pct + '%';
  hpRange.value = pct;
}
hpCurr.addEventListener('input', ()=>{ updateHPUI(); markDirty(); });
hpMax.addEventListener('input', ()=>{ updateHPUI(); markDirty(); });
hpRange.addEventListener('input', ()=>{
  const pct = Number(hpRange.value) || 0;
  const max = Math.max(1, Number(hpMax.value) || 1);
  const newCurr = Math.round(max * pct / 100);
  hpCurr.value = newCurr;
  updateHPUI();
  markDirty();
});
updateHPUI();

/* ---------- Dynamic Passivas & Abilities ---------- */
const passivesContainer = document.getElementById('passivesContainer');
const addPassiveBtn = document.getElementById('addPassiveBtn');

function renderPassives(arr){
  // arr = array of strings (existing passives)
  const len = Math.max(2, arr.length);
  passivesContainer.innerHTML = '';
  for(let i=0;i<len;i++){
    const wrapper = document.createElement('div');
    wrapper.style.display = 'flex';
    wrapper.style.gap = '6px';
    if(i>0) wrapper.style.marginTop = '6px';
    const input = document.createElement('input');
    input.placeholder = 'Passiva ' + (i+1);
    input.value = arr[i] || '';
    input.dataset.index = i;
    input.style.flex = '1';
    input.addEventListener('input', markDirty);
    wrapper.appendChild(input);

    // show remove button only for extras that actually exist (i >= 2 and index < arr.length)
    if(i >= 2 && i < arr.length){
      const removeBtn = document.createElement('button');
      removeBtn.className = 'secondary';
      removeBtn.textContent = 'Remover';
      removeBtn.addEventListener('click', ()=>{
        const current = getPassivesFromDOM();
        // splice at i (remove the exact passive)
        current.splice(i,1);
        renderPassives(current);
        markDirty();
      });
      wrapper.appendChild(removeBtn);
    }

    passivesContainer.appendChild(wrapper);
  }
}

function getPassivesFromDOM(){
  // read only input values from passivesContainer (in order)
  const inputs = Array.from(passivesContainer.querySelectorAll('input'));
  return inputs.map(i=>i.value || '');
}

let addPassiveLock = false;
addPassiveBtn.addEventListener('click', ()=>{
  if(addPassiveLock) return;
  addPassiveLock = true;
  setTimeout(()=> addPassiveLock = false, 300);
  const current = getPassivesFromDOM();
  current.push(''); // add exactly one
  renderPassives(current);
  markDirty();
});

/* Abilities dynamic extras */
const abilitiesContainer = document.getElementById('abilitiesContainer');
const addAbilityBtn = document.getElementById('addAbilityBtn');

function createExtraAbilityElement(idx, data){
  const wrap = document.createElement('div');
  wrap.className = 'ability battle-ability extra';
  const label = document.createElement('label');
  label.textContent = 'Ability ' + (idx+1);
  wrap.appendChild(label);

  const name = document.createElement('input');
  name.placeholder = 'Nome';
  name.value = data?.name || '';
  wrap.appendChild(name);

  const row = document.createElement('div');
  row.className = 'row';
  row.style.marginTop = '6px';
  const cost = document.createElement('input'); cost.placeholder='Custo'; cost.style.width='100px'; cost.value=data?.cost||'';
  const limit = document.createElement('input'); limit.placeholder='Limit'; limit.style.width='100px'; limit.value=data?.limit||'';
  row.appendChild(cost); row.appendChild(limit);
  wrap.appendChild(row);

  const eff = document.createElement('textarea'); eff.style.marginTop='6px'; eff.placeholder='Efeitos'; eff.value = data?.effect||'';
  wrap.appendChild(eff);

  const modules = document.createElement('input'); modules.placeholder='Módulos usados'; modules.value = data?.modules||''; modules.style.marginTop='6px';
  wrap.appendChild(modules);

  const removeBtn = document.createElement('button'); removeBtn.textContent='Remover'; removeBtn.className='secondary'; removeBtn.style.marginTop='6px';
  removeBtn.addEventListener('click', ()=>{
    wrap.remove();
    // after removing DOM node, renumber labels
    renumberAbilities();
    markDirty();
  });
  wrap.appendChild(removeBtn);

  // mark dirty on changes
  [name, cost, limit, eff, modules].forEach(el=>el.addEventListener('input', markDirty));
  return wrap;
}

function renumberAbilities(){
  const extras = abilitiesContainer.querySelectorAll('.battle-ability.extra');
  extras.forEach((node, idx)=>{
    const label = node.querySelector('label');
    if(label) label.textContent = 'Ability ' + (2 + idx + 1); // base 2 static abilities -> extras start at 3
  });
}

function getAbilitiesFromDOM(){
  const arr = [];
  // read static a1,a2
  arr.push({
    name: document.getElementById('p2_a1_name').value || '',
    cost: document.getElementById('p2_a1_cost').value || '',
    limit: document.getElementById('p2_a1_limit').value || '',
    effect: document.getElementById('p2_a1_effect').value || '',
    modules: document.getElementById('p2_a1_modules').value || ''
  });
  arr.push({
    name: document.getElementById('p2_a2_name').value || '',
    cost: document.getElementById('p2_a2_cost').value || '',
    limit: document.getElementById('p2_a2_limit').value || '',
    effect: document.getElementById('p2_a2_effect').value || '',
    modules: document.getElementById('p2_a2_modules').value || ''
  });
  // extras
  const extras = abilitiesContainer.querySelectorAll('.battle-ability.extra');
  extras.forEach(node=>{
    const inputs = node.querySelectorAll('input, textarea');
    const name = inputs[0]?.value || '';
    // inputs[1] and inputs[2] are cost and limit in the row
    const cost = inputs[1]?.value || '';
    const limit = inputs[2]?.value || '';
    const effect = node.querySelector('textarea')?.value || '';
    // modules input is last input in the node
    const inputList = node.querySelectorAll('input');
    const modules = inputList[inputList.length-1]?.value || '';
    arr.push({name,cost,limit,effect,modules});
  });
  return arr;
}

addAbilityBtn.addEventListener('click', ()=>{
  const extras = abilitiesContainer.querySelectorAll('.battle-ability.extra');
  const idx = 2 + extras.length;
  const el = createExtraAbilityElement(idx, {});
  abilitiesContainer.appendChild(el);
  renumberAbilities();
  markDirty();
});

/* ---------- Inventory / Equip rendering ---------- */
const inventoryGrid = document.getElementById('inventoryGrid');
const addInvSlotBtn = document.getElementById('addInvSlotBtn');
const clearInvBtn = document.getElementById('clearInvBtn');
const equipList = document.getElementById('equipList');
const addEquipSlotBtn = document.getElementById('addEquipSlotBtn');

function renderInventory(){
  inventoryGrid.innerHTML = '';
  inventoryData.forEach((slot, i)=>{
    const div = document.createElement('div');
    div.className = 'inv-slot';
    const img = document.createElement('img');
    img.src = slot.img || '';
    img.alt = slot.caption || '';
    img.addEventListener('click', ()=> {
      fileInp.click();
    });
    const caption = document.createElement('input');
    caption.placeholder = 'Legenda';
    caption.value = slot.caption || '';
    caption.addEventListener('input', ()=>{
      inventoryData[i].caption = caption.value;
      markDirty();
    });
    const fileInp = document.createElement('input');
    fileInp.type = 'file';
    fileInp.accept = 'image/*';
    fileInp.style.display = 'none';
    fileInp.addEventListener('change', (e)=>{
      const f = e.target.files[0];
      if(!f) return;
      compressAndSetImage(f, (dataUrl)=>{
        inventoryData[i].img = dataUrl;
        renderInventory();
        markDirty();
      });
    });
    const removeBtn = document.createElement('button');
    removeBtn.textContent = 'Remover';
    removeBtn.className = 'secondary';
    removeBtn.style.marginTop = '6px';
    removeBtn.addEventListener('click', ()=>{
      inventoryData.splice(i,1);
      renderInventory();
      markDirty();
    });

    div.appendChild(img);
    div.appendChild(caption);
    div.appendChild(fileInp);
    div.appendChild(removeBtn);
    inventoryGrid.appendChild(div);
  });
}

function renderEquip(){
  equipList.innerHTML = '';
  equipData.forEach((slot, i)=>{
    const row = document.createElement('div');
    row.className = 'equip-slot';
    const img = document.createElement('img'); img.src = slot.img || ''; img.alt = slot.caption || '';
    const caption = document.createElement('input'); caption.placeholder='Legenda'; caption.value = slot.caption||''; caption.style.flex='1';
    caption.addEventListener('input', ()=>{ equipData[i].caption = caption.value; markDirty(); });

    const fileInp = document.createElement('input'); fileInp.type='file'; fileInp.accept='image/*'; fileInp.style.display='none';
    fileInp.addEventListener('change', (e)=>{ const f = e.target.files[0]; if(!f) return; compressAndSetImage(f, (dataUrl)=>{ equipData[i].img = dataUrl; renderEquip(); markDirty(); }); });

    const uploadBtn = document.createElement('button'); uploadBtn.textContent='Upload'; uploadBtn.className='secondary';
    uploadBtn.addEventListener('click', ()=> fileInp.click());

    const removeBtn = document.createElement('button'); removeBtn.textContent='Remover'; removeBtn.className='secondary';
    removeBtn.addEventListener('click', ()=>{ equipData.splice(i,1); renderEquip(); markDirty(); });

    row.appendChild(img);
    row.appendChild(caption);
    row.appendChild(fileInp);
    row.appendChild(uploadBtn);
    row.appendChild(removeBtn);
    equipList.appendChild(row);
  });
}

addInvSlotBtn.addEventListener('click', ()=>{ inventoryData.push({img:'', caption:''}); renderInventory(); markDirty(); });
clearInvBtn.addEventListener('click', ()=>{ if(confirm('Limpar todo o inventário?')){ inventoryData = []; renderInventory(); markDirty(); } });
addEquipSlotBtn.addEventListener('click', ()=>{ equipData.push({img:'', caption:''}); renderEquip(); markDirty(); });

/* ---------- Collect / Populate (all pages) ---------- */
function collectAll(){
  return {
    id: currentId,
    meta:{ name: document.getElementById('p1_name').value || 'Sem nome' },
    page1: {
      name: document.getElementById('p1_name').value,
      archetype: document.getElementById('p1_archetype').value,
      level: document.getElementById('p1_level').value,
      attrs:{
        might: Number(document.getElementById('attr_might').value)||0,
        vitality: Number(document.getElementById('attr_vitality').value)||0,
        agility: Number(document.getElementById('attr_agility').value)||0,
        instinct: Number(document.getElementById('attr_instinct').value)||0,
        persona: Number(document.getElementById('attr_persona').value)||0
      },
      notes: document.getElementById('p1_notes').value || '',
      culpa: Number(document.getElementById('culpaRange').value)||0,
      options:{
        skillsGrey: document.getElementById('opt_grey_skills').checked,
        egosGrey: document.getElementById('opt_grey_egos').checked
      }
    },
    page2: {
      hpCurr: Number(hpCurr.value)||0,
      hpMax: Number(hpMax.value)||1,
      speed: document.getElementById('p2_speed').value,
      stagger: document.getElementById('p2_stagger').value,
      passes: getPassivesFromDOM(),
      abilities: getAbilitiesFromDOM(),
      feats: document.getElementById('p2_feats').value,
      notes: document.getElementById('p2_notes').value
    },
    page3: {
      inventory: inventoryData.slice(),
      equip: equipData.slice(),
      extra: document.getElementById('p3_extra').value || ''
    },
    portrait: portraitImg.src || ''
  };
}

function populateAll(obj){
  if(!obj) return;
  currentId = obj.id || null;
  document.getElementById('p1_name').value = obj.page1?.name || '';
  document.getElementById('p1_archetype').value = obj.page1?.archetype || '';
  document.getElementById('p1_level').value = obj.page1?.level || '';
  document.getElementById('attr_might').value = obj.page1?.attrs?.might || '';
  document.getElementById('attr_vitality').value = obj.page1?.attrs?.vitality || '';
  document.getElementById('attr_agility').value = obj.page1?.attrs?.agility || '';
  document.getElementById('attr_instinct').value = obj.page1?.attrs?.instinct || '';
  document.getElementById('attr_persona').value = obj.page1?.attrs?.persona || '';
  document.getElementById('p1_notes').value = obj.page1?.notes || '';
  document.getElementById('culpaRange').value = obj.page1?.culpa || 0;
  updateCulpaUI(obj.page1?.culpa || 0);
  document.getElementById('opt_grey_skills').checked = !!obj.page1?.options?.skillsGrey;
  document.getElementById('opt_grey_egos').checked = !!obj.page1?.options?.egosGrey;

  // page2
  document.getElementById('hpCurr').value = obj.page2?.hpCurr ?? 0;
  document.getElementById('hpMax').value = obj.page2?.hpMax ?? 1;
  updateHPUI();
  document.getElementById('p2_speed').value = obj.page2?.speed || '';
  document.getElementById('p2_stagger').value = obj.page2?.stagger || '';
  // passives
  const passes = obj.page2?.passes || ['',''];
  renderPassives(passes);

  // abilities
  const ab = obj.page2?.abilities || [];
  if(ab[0]){ document.getElementById('p2_a1_name').value = ab[0].name || ''; document.getElementById('p2_a1_cost').value = ab[0].cost||''; document.getElementById('p2_a1_limit').value = ab[0].limit||''; document.getElementById('p2_a1_effect').value = ab[0].effect||''; document.getElementById('p2_a1_modules').value = ab[0].modules||''; } else { document.getElementById('p2_a1_name').value=''; document.getElementById('p2_a1_cost').value=''; document.getElementById('p2_a1_limit').value=''; document.getElementById('p2_a1_effect').value=''; document.getElementById('p2_a1_modules').value=''; }
  if(ab[1]){ document.getElementById('p2_a2_name').value = ab[1].name || ''; document.getElementById('p2_a2_cost').value = ab[1].cost||''; document.getElementById('p2_a2_limit').value = ab[1].limit||''; document.getElementById('p2_a2_effect').value = ab[1].effect||''; document.getElementById('p2_a2_modules').value = ab[1].modules||''; } else { document.getElementById('p2_a2_name').value=''; document.getElementById('p2_a2_cost').value=''; document.getElementById('p2_a2_limit').value=''; document.getElementById('p2_a2_effect').value=''; document.getElementById('p2_a2_modules').value=''; }
  // clear current extra abilities then render extras from ab[2+]
  const extras = Array.from(abilitiesContainer.querySelectorAll('.battle-ability.extra'));
  extras.forEach(e=>e.remove());
  for(let i=2;i<ab.length;i++){
    const el = createExtraAbilityElement(i, ab[i]);
    abilitiesContainer.appendChild(el);
  }
  renumberAbilities();
  document.getElementById('p2_feats').value = obj.page2?.feats || '';
  document.getElementById('p2_notes').value = obj.page2?.notes || '';

  // page3 inventory/equip
  inventoryData = (obj.page3?.inventory || []).map(s=>({img:s.img||'', caption: s.caption||''}));
  equipData = (obj.page3?.equip || []).map(s=>({img:s.img||'', caption: s.caption||''}));
  renderInventory();
  renderEquip();
  document.getElementById('p3_extra').value = obj.page3?.extra || '';

  // portrait
  if(obj.portrait) portraitImg.src = obj.portrait;
  updateStatusUI();
}

/* ---------- Storage: list / save / load / delete ---------- */
function readStore(){
  try{
    const raw = localStorage.getItem(STORAGE_KEY);
    return raw ? JSON.parse(raw) : [];
  }catch(e){
    console.error('Erro parse storage', e); return [];
  }
}
function writeStore(list){
  try{ localStorage.setItem(STORAGE_KEY, JSON.stringify(list)); } catch(e){ alert('Erro ao gravar localStorage: '+e.message); }
}

function refreshSavedList(){
  const sel = document.getElementById('savedList');
  sel.innerHTML = '';
  const list = readStore().sort((a,b)=> (b.updatedAt||b.createdAt)-(a.updatedAt||a.createdAt));
  list.forEach(item=>{
    const opt = document.createElement('option');
    opt.value = item.id;
    opt.textContent = (item.meta?.name || 'Sem nome') + ' — ' + new Date(item.updatedAt||item.createdAt).toLocaleString();
    sel.appendChild(opt);
  });
}

function saveCurrent(asNew=false){
  const data = collectAll();
  const store = readStore();
  if(asNew || !currentId){
    data.id = uid();
    data.createdAt = Date.now(); data.updatedAt = Date.now();
    store.push(data);
    currentId = data.id;
    alert('Ficha salva como: ' + (data.meta?.name || 'Sem nome'));
  } else {
    data.id = currentId;
    data.updatedAt = Date.now();
    const idx = store.findIndex(s=>s.id===currentId);
    if(idx>=0) store[idx] = Object.assign({}, store[idx], data);
    else store.push(data);
  }
  writeStore(store);
  refreshSavedList();
  updateStatusUI();
  isDirty = false;
}

function saveAs(){
  const name = prompt('Nome para salvar a ficha:', document.getElementById('p1_name').value || 'Ficha');
  if(!name) return;
  const data = collectAll();
  data.meta = data.meta || {}; data.meta.name = name;
  data.id = uid(); data.createdAt = Date.now(); data.updatedAt = Date.now();
  const store = readStore(); store.push(data); writeStore(store);
  currentId = data.id;
  refreshSavedList();
  updateStatusUI();
  isDirty = false;
  alert('Ficha salva: ' + name);
}

function loadSelected(){
  const sel = document.getElementById('savedList');
  const val = sel.value;
  if(!val){ alert('Selecione uma ficha'); return; }
  const store = readStore();
  const obj = store.find(s=>s.id===val);
  if(!obj){ alert('Ficha não encontrada'); refreshSavedList(); return; }
  if(isDirty && !confirm('Você tem alterações não salvas. Deseja prosseguir e perder essas alterações?')) return;
  populateAll(obj);
  isDirty = false;
}

function deleteSelected(){
  const sel = document.getElementById('savedList');
  const val = sel.value;
  if(!val){ alert('Selecione uma ficha'); return; }
  if(!confirm('Excluir a ficha selecionada?')) return;
  const store = readStore().filter(s=>s.id!==val);
  writeStore(store);
  refreshSavedList();
  if(currentId===val){ currentId = null; }
  updateStatusUI();
  alert('Ficha excluída');
}

/* ---------- Export / Import JSON ---------- */
document.getElementById('exportJson').addEventListener('click', ()=>{
  const data = collectAll();
  const blob = new Blob([JSON.stringify(data, null, 2)], {type:'application/json'});
  const a = document.createElement('a'); a.href = URL.createObjectURL(blob);
  a.download = (data.meta?.name || 'ficha') + '.json'; a.click();
  URL.revokeObjectURL(a.href);
});
document.getElementById('importJson').addEventListener('click', ()=> document.getElementById('importFile').click());
document.getElementById('importFile').addEventListener('change', (e)=>{
  const f = e.target.files[0]; if(!f) return;
  const r = new FileReader();
  r.onload = ()=>{
    try{
      const obj = JSON.parse(r.result);
      if(!obj) throw new Error('JSON inválido');
      if(isDirty && !confirm('Existem alterações não salvas — importar irá sobrescrever o formulário. Continuar?')) return;
      populateAll(obj);
      currentId = null;
      alert('JSON importado. Use "Salvar como..." para adicioná-lo ao armazenamento local.');
    }catch(err){ alert('Erro ao importar JSON: ' + err.message); }
  };
  r.readAsText(f);
});

/* ---------- Print functions ---------- */
document.getElementById('printPageBtn').addEventListener('click', () => {
  window.print();
});
document.getElementById('printAllBtn').addEventListener('click', ()=>{
  // create a new window with all pages content and print
  const pages = ['p1','p2','p3'].map(id => document.getElementById(id).outerHTML).join('<div style="page-break-after:always"></div>');
  const css = Array.from(document.querySelectorAll('style')).map(s=>s.innerHTML).join('\n');
  const w = window.open('', '_blank');
  w.document.write('<!doctype html><html><head><meta charset="utf-8"><title>Imprimir Ficha</title><style>' + css + '</style></head><body>' + pages + '</body></html>');
  w.document.close();
  setTimeout(()=> w.print(), 500);
});

/* ---------- Status UI ---------- */
function updateStatusUI(){
  const cur = document.getElementById('currentName');
  const time = document.getElementById('currentTime');
  if(currentId){
    const store = readStore();
    const obj = store.find(s=>s.id===currentId);
    cur.textContent = obj?.meta?.name || 'Sem nome';
    time.textContent = nowStr(obj?.updatedAt || obj?.createdAt);
  } else {
    cur.textContent = document.getElementById('p1_name').value || '—';
    time.textContent = '—';
  }
}

/* ---------- Mark dirty ---------- */
function markDirty(){ isDirty = true; scheduleAutoSave(); updateStatusUI(); }

/* attach basic listeners for static fields */
['p1_name','p1_archetype','p1_level','attr_might','attr_vitality','attr_agility','attr_instinct','attr_persona',
 'p1_notes',
 'p2_speed','p2_stagger','p2_a1_name','p2_a1_cost','p2_a1_limit','p2_a1_effect','p2_a1_modules',
 'p2_a2_name','p2_a2_cost','p2_a2_limit','p2_a2_effect','p2_a2_modules',
 'p2_feats','p2_notes','p3_extra'
].forEach(id=>{
  const el = document.getElementById(id);
  if(!el) return;
  el.addEventListener('input', markDirty);
  el.addEventListener('change', markDirty);
});

/* ---------- Buttons bindings ---------- */
document.getElementById('saveBtn').addEventListener('click', ()=> saveCurrent(false));
document.getElementById('saveAsBtn').addEventListener('click', saveAs);
document.getElementById('newBtn').addEventListener('click', ()=>{
  if(isDirty && !confirm('Alterações não salvas serão perdidas. Prosseguir?')) return;
  currentId = null;
  // clear many fields
  document.querySelectorAll('input[type=text], input[type=number], textarea').forEach(inp=>{
    if(inp.id==='fileInput') return;
    inp.value = '';
  });
  // reset known checkboxes and selects
  document.getElementById('opt_grey_skills').checked = false;
  document.getElementById('opt_grey_egos').checked = false;
  portraitImg.src = '';
  inventoryData = [];
  equipData = [];
  renderInventory(); renderEquip();
  updateHPUI(); updateCulpaUI(0);
  isDirty = false; updateStatusUI(); refreshSavedList();
});
document.getElementById('loadBtn').addEventListener('click', loadSelected);
document.getElementById('deleteBtn').addEventListener('click', deleteSelected);
document.getElementById('quickSave').addEventListener('click', ()=> saveCurrent(false));
document.getElementById('quickExport').addEventListener('click', ()=> document.getElementById('exportJson').click());

/* saved list double-click to load */
document.getElementById('savedList').addEventListener('dblclick', loadSelected);
document.getElementById('savedList').addEventListener('change', ()=>{
  // quick preview (load)
  const sel = document.getElementById('savedList');
  const val = sel.value;
  if(!val) return;
  const obj = readStore().find(s=>s.id===val);
  if(obj){
    if(isDirty && !confirm('Alterações não salvas serão perdidas. Carregar?')) return;
    populateAll(obj);
    isDirty = false;
  }
});

/* auto-save */
let autoSaveTimer = null;
document.getElementById('autoSave').addEventListener('change', ()=>{
  if(document.getElementById('autoSave').checked && !currentId){
    alert('Auto-save ativado: salve a ficha com "Salvar como..." para ativar salvamento automático nesta ficha.');
  }
});
function scheduleAutoSave(){
  if(!document.getElementById('autoSave').checked) return;
  if(!currentId) return;
  if(autoSaveTimer) clearTimeout(autoSaveTimer);
  autoSaveTimer = setTimeout(()=>{ saveCurrent(false); autoSaveTimer=null; }, 900);
}

/* ---------- Init ---------- */
(function init(){
  refreshSavedList();
  updateStatusUI();
  // init passives with two defaults
  renderPassives(['','']);
  // try to load first saved
  const list = readStore();
  if(list.length>0){
    const first = list[0];
    populateAll(first);
    isDirty = false;
  } else {
    // ensure inventory/equip initial render
    inventoryData = [];
    equipData = [];
    renderInventory(); renderEquip();
  }
})();
</script>
</body>
</html>
