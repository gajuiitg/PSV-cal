<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PSV Sizing Calculator — API RP 520 / 521 (Metric)</title>
<style>
:root{
  --navy:#0f2d4a; --steel:#1e5288; --steel-lt:#e8f0f8; --accent:#c0392b;
  --grey:#5a6672; --line:#c9d3dc; --ok:#1e7e34; --warn:#b8860b; --bg:#f4f6f8;
}
*{box-sizing:border-box;}
body{
  font-family:"Segoe UI",Arial,sans-serif; background:var(--bg); color:#1a232e;
  margin:0; padding:10px; font-size:clamp(11px, 2.5vw, 13.5px); line-height:1.45;
}
.sheet{width:100%;max-width:1200px;margin:0 auto;background:#fff;border:1px solid var(--line);box-shadow:0 2px 10px rgba(0,0,0,.08);}
header.top{background:linear-gradient(135deg,var(--navy),var(--steel));color:#fff;padding:clamp(10px, 3vw, 18px) clamp(15px, 4vw, 24px);}
header.top h1{margin:0 0 4px;font-size:clamp(16px, 5vw, 20px);letter-spacing:.3px;}
header.top .sub{font-size:clamp(10px, 2.5vw, 12px);opacity:.9;}
.toolbar{display:flex;gap:clamp(5px, 2vw, 10px);padding:clamp(8px, 2vw, 10px) clamp(15px, 4vw, 24px);background:var(--steel-lt);border-bottom:1px solid var(--line);flex-wrap:wrap;align-items:center;}
.toolbar button{background:var(--steel);color:#fff;border:none;padding:clamp(6px, 1.5vw, 8px) clamp(12px, 3vw, 16px);border-radius:3px;font-size:clamp(11px, 2.5vw, 12.5px);cursor:pointer;font-weight:600;}
.toolbar button.secondary{background:#fff;color:var(--steel);border:1px solid var(--steel);}
.toolbar button:hover{filter:brightness(1.1);}
.content{padding:clamp(15px, 3vw, 20px) clamp(15px, 4vw, 24px);}
h2.section{
  background:var(--navy);color:#fff;font-size:13.5px;padding:7px 12px;margin:26px 0 12px;
  letter-spacing:.4px;text-transform:uppercase;border-radius:2px;
}
h2.section:first-child{margin-top:0;}
h3.sub{font-size:13px;color:var(--navy);border-bottom:2px solid var(--steel);padding-bottom:4px;margin:16px 0 10px;}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(clamp(150px, 40vw, 220px),1fr));gap:clamp(8px, 2vw, 10px) clamp(10px, 3vw, 18px);}
.field{display:flex;flex-direction:column;gap:3px;margin-bottom:6px;position:relative;}
.field label{font-size:11.5px;color:var(--grey);font-weight:600;}
.field .hint{font-size:10px;color:#8892a0;font-weight:400;}
.infobtn{display:inline-flex;align-items:center;justify-content:center;width:16px;height:16px;border-radius:50%;background:var(--steel);color:#fff;font-size:10px;font-weight:700;cursor:pointer;margin-left:4px;vertical-align:middle;user-select:none;}
.infobtn:hover,.infobtn:active{background:var(--navy);}
.tip{display:none;position:absolute;top:100%;left:0;z-index:50;background:#1a232e;color:#fff;font-size:11px;font-weight:400;line-height:1.5;padding:9px 11px;border-radius:4px;box-shadow:0 4px 14px rgba(0,0,0,.3);width:min(300px,80vw);margin-top:4px;}
.tip.show{display:block;}
.tip b{color:#8fc4ff;}
.tip .close-tip{float:right;cursor:pointer;color:#aab4c0;font-weight:700;margin-left:8px;}
input[type=number],input[type=text],select{
  padding:6px 7px;border:1px solid var(--line);border-radius:3px;font-size:13px;background:#fff;color:#1a232e;
}
input:focus,select:focus{outline:2px solid var(--steel);outline-offset:0;}
.note{background:#fff8ea;border-left:3px solid var(--warn);padding:8px 12px;font-size:11.5px;color:#5a4a1a;margin:10px 0;}
.assume{background:var(--steel-lt);border-left:3px solid var(--steel);padding:8px 12px;font-size:11.5px;color:#1a3550;margin:10px 0;}
.equip-row{border:1px solid var(--line);border-radius:5px;padding:12px 14px;margin-bottom:10px;background:#fbfcfd;position:relative;}
.equip-row .eq-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;}
.equip-row .eq-title{font-weight:700;color:var(--navy);font-size:12.5px;}
.equip-row .eq-remove{background:var(--accent);color:#fff;border:none;padding:4px 10px;border-radius:3px;font-size:11px;cursor:pointer;font-weight:700;}
.equip-row .eq-area{font-size:11.5px;color:var(--steel);font-weight:700;margin-top:6px;}
.duty-select{display:flex;gap:10px;margin:10px 0;flex-wrap:wrap;}
.dutybtn{flex:1;min-width:180px;padding:14px 10px;font-size:13.5px;font-weight:700;border:2px solid var(--line);background:#fff;color:var(--navy);border-radius:5px;cursor:pointer;letter-spacing:.3px;}
.dutybtn.active{background:var(--steel);border-color:var(--navy);color:#fff;box-shadow:0 2px 6px rgba(15,45,74,.25);}
.dutybtn:hover{border-color:var(--steel);}
.tabs{display:flex;flex-wrap:wrap;gap:4px;margin-top:10px;border-bottom:2px solid var(--steel);}
.tabbtn{padding:8px 14px;background:#e2e8ee;border:1px solid var(--line);border-bottom:none;border-radius:4px 4px 0 0;font-size:12px;cursor:pointer;font-weight:600;color:var(--navy);}
.tabbtn.active{background:var(--steel);color:#fff;}
.tabpanel{display:none;border:1px solid var(--line);border-top:none;padding:16px;background:#fbfcfd;}
.tabpanel.active{display:block;}
table{width:100%;border-collapse:collapse;margin:10px 0;font-size:12px;}
th,td{border:1px solid var(--line);padding:6px 8px;text-align:left;}
th{background:var(--navy);color:#fff;font-size:11px;text-transform:uppercase;letter-spacing:.3px;}
tr:nth-child(even) td{background:#f5f8fa;}
.result-box{background:#fff;border:2px solid var(--steel);border-radius:4px;padding:12px 16px;margin-top:12px;}
.result-box .big{font-size:22px;font-weight:700;color:var(--navy);}
.result-box .label{font-size:11px;color:var(--grey);text-transform:uppercase;letter-spacing:.4px;}
.gov{background:#fdecea !important;font-weight:700;}
.badge{display:inline-block;padding:2px 8px;border-radius:10px;font-size:10.5px;font-weight:700;color:#fff;background:var(--accent);}
.badge.ok{background:var(--ok);}
.calc-btn{background:var(--steel);color:#fff;border:none;padding:7px 14px;border-radius:3px;font-size:12px;cursor:pointer;font-weight:600;margin-top:8px;}
.calc-btn:hover{filter:brightness(1.1);}
.two-col{display:grid;grid-template-columns:1fr;gap:clamp(15px, 3vw, 20px);}@media(min-width:768px){.two-col{grid-template-columns:1fr 1fr;}}
footer.sig{margin-top:24px;padding-top:10px;border-top:1px solid var(--line);font-size:10.5px;color:var(--grey);}
.chk-title{font-weight:700;color:var(--navy);margin-top:2px;}
@media(max-width:768px){
  body{padding:8px;}
  .sheet{border:none;}
  header.top{padding:12px;}
  .content{padding:12px;}
  .toolbar{flex-direction:column;gap:8px;}
  .toolbar button{width:100%;}
  .duty-select{flex-direction:column;}
  .dutybtn{min-width:100%;}
  .tabs{flex-direction:column;}
  .tabbtn{width:100%;border-radius:3px 3px 0 0;}
  .result-box .big{font-size:clamp(18px, 5vw, 22px);}
  input[type=number],input[type=text],select{font-size:16px;padding:8px;}
}
@media(max-width:480px){
  body{padding:5px;}
  .content{padding:8px 10px;}
  .toolbar button{padding:8px 12px;font-size:11px;}
  h2.section{padding:5px 8px;font-size:12px;margin:15px 0 8px;}
  h3.sub{font-size:12px;}
  .grid{grid-template-columns:1fr;}
  .field label{font-size:10.5px;}
  table{font-size:10px;}
  th,td{padding:4px 6px;}
  .result-box{padding:10px 12px;}
  .result-box .big{font-size:18px;}
}
@media print{
  @page{size:A4;margin:12mm;}
  body{background:#fff;padding:0;font-size:10.5px;}
  .sheet{box-shadow:none;border:none;max-width:100%;}
  .toolbar{display:none;}
  header.top{background:var(--navy) !important;-webkit-print-color-adjust:exact;print-color-adjust:exact;padding:10px 14px;}
  h2.section{-webkit-print-color-adjust:exact;print-color-adjust:exact;page-break-after:avoid;}
  .tabs{display:none;}
  .duty-select{display:none;}
  .tabpanel{display:none;border:1px solid var(--line);margin-bottom:10px;}
  .tabpanel.print-show{display:block;}
  .result-box{page-break-inside:avoid;}
  #api526_table{font-size:9px;}
  table{page-break-inside:avoid;}
  th{-webkit-print-color-adjust:exact;print-color-adjust:exact;}
  .tip{display:none !important;}
  .eq-remove{display:none;}
  .calc-btn{display:none;}
  #equip_list .equip-row button{display:none;}
  .no-print{display:none;}
}
</style>
</head>
<body>
<div class="sheet">

<header class="top">
  <h1>Pressure Safety Valve (PSV) Sizing Calculator</h1>
  <div class="sub">API RP 520 (Sizing &amp; Selection) &amp; API RP 521 (Overpressure Protection / Fire Case) — Metric Units (Kg/cm²g, °C, Kg/hr, cP)</div>
</header>

<div class="toolbar">
  <button onclick="calculateAll()">⚙ Calculate All Cases</button>
  <button class="secondary" onclick="window.print()">🖨 Print (A4)</button>
  <span style="font-size:11px;color:var(--grey);margin-left:auto;">Formulas: API RP 520 Part I (9th/10th Ed. metric), API RP 521 (fire case)</span>
</div>

<div class="content">

<div class="note">
<b>Engineering note:</b> This tool performs preliminary PSV orifice sizing per the standard API RP 520 metric equations. Final valve selection, Kb/Kw/Kv correction factors, rated capacity certification, inlet/outlet piping (3% / 10% pressure-drop checks per API 520 Part II), and relief-header backpressure analysis must be verified by the responsible process/safety engineer and cross-checked against vendor capacity certification (NB/ASME) data before issue for construction / MOC closure.
</div>

<!-- ================= GENERAL DATA ================= -->
<h2 class="section">1. General / Common Data</h2>
<div class="grid">
  <div class="field"><label>Tag No.</label><input id="g_tag" type="text" value="PSV-XXXX"></div>
  <div class="field"><label>Equipment / Service</label><input id="g_service" type="text" value=""></div>
  <div class="field"><label>Fluid</label><input id="g_fluid" type="text" value=""></div>
  <div class="field"><label>Set Pressure, kg/cm²g</label><input id="g_setP" type="number" step="any" value="10.5"></div>
  <div class="field"><label>Allowable Overpressure, %</label><input id="g_op" type="number" step="any" value="10"><span class="hint">10% single valve; 16% fire case; 21% supplemental</span></div>
  <div class="field"><label>Built-up Backpressure, kg/cm²g</label><input id="g_bp" type="number" step="any" value="0.3"></div>
  <div class="field"><label>Atmospheric Pressure, kg/cm²a</label><input id="g_atm" type="number" step="any" value="1.033"></div>
  <div class="field"><label>Molecular Weight, kg/kmol</label><input id="g_M" type="number" step="any" value="28"></div>
  <div class="field"><label>k = Cp/Cv</label><input id="g_k" type="number" step="any" value="1.3"></div>
  <div class="field"><label>Compressibility Factor, Z</label><input id="g_Z" type="number" step="any" value="1.0"></div>
  <div class="field"><label>Relieving Temperature, °C</label><input id="g_T" type="number" step="any" value="65"></div>
  <div class="field"><label>Liquid Specific Gravity, G (rel. water)</label><input id="g_G" type="number" step="any" value="0.55"></div>
  <div class="field"><label>Liquid Viscosity, cP</label><input id="g_visc" type="number" step="any" value="0.3"></div>
  <div class="field"><label>Kd — Discharge Coeff. (vapor) <span class="infobtn" onclick="toggleTip('tip_Kdv')">i</span></label><input id="g_Kd_v" type="number" step="any" value="0.975">
    <div class="tip" id="tip_Kdv"><span class="close-tip" onclick="toggleTip('tip_Kdv')">✕</span><b>Kd — Effective Coefficient of Discharge (vapor/steam).</b> Standard value 0.975 for a certified PRV. Not read from a curve — it is the ASME/NB-certified value stamped on the valve nameplate. <br><i>Ref: API RP 520 Part I, §5.6.</i></div>
  </div>
  <div class="field"><label>Kd — Discharge Coeff. (liquid) <span class="infobtn" onclick="toggleTip('tip_Kdl')">i</span></label><input id="g_Kd_l" type="number" step="any" value="0.65">
    <div class="tip" id="tip_Kdl"><span class="close-tip" onclick="toggleTip('tip_Kdl')">✕</span><b>Kd — Effective Coefficient of Discharge (liquid).</b> Standard value 0.65 for a certified PRV in liquid service; 0.62 when sizing a rupture disc alone (no PRV). <br><i>Ref: API RP 520 Part I, §5.6.</i></div>
  </div>
  <div class="field"><label>Kb — Backpressure Corr. (vapor) <span class="infobtn" onclick="toggleTip('tip_Kb')">i</span></label><input id="g_Kb" type="number" step="any" value="1.0"><span class="hint">1.0 conventional; from Fig.30/31 for bellows</span>
    <div class="tip" id="tip_Kb"><span class="close-tip" onclick="toggleTip('tip_Kb')">✕</span><b>Kb — Capacity Correction Factor for Backpressure, vapor/gas.</b> Kb = 1.0 for conventional (non-bellows) valves within the allowable backpressure limit. For balanced-bellows valves, read from the backpressure-ratio curve. <br><i>Ref (7th Ed.): Fig.30 (bellows, vapor/gas); Fig.35 (conventional, when backpressure exceeds normal limit). Figure numbers shift between editions — confirm against your copy of API RP 520 Part I.</i></div>
  </div>
  <div class="field"><label>Kw — Backpressure Corr. (liquid) <span class="infobtn" onclick="toggleTip('tip_Kw')">i</span></label><input id="g_Kw" type="number" step="any" value="1.0">
    <div class="tip" id="tip_Kw"><span class="close-tip" onclick="toggleTip('tip_Kw')">✕</span><b>Kw — Capacity Correction Factor for Backpressure, liquid, balanced-bellows valves.</b> Kw = 1.0 for conventional valves; for bellows valves, read from the backpressure-ratio curve. <br><i>Ref (7th Ed.): Fig.31. Numbering varies by edition — confirm against your copy.</i></div>
  </div>
  <div class="field"><label>Kc — Rupture Disc Combination <span class="infobtn" onclick="toggleTip('tip_Kc')">i</span></label><input id="g_Kc" type="number" step="any" value="1.0"><span class="hint">1.0 = no RD upstream; 0.9 = with RD</span>
    <div class="tip" id="tip_Kc"><span class="close-tip" onclick="toggleTip('tip_Kc')">✕</span><b>Kc — Combination Correction Factor, rupture disc upstream of PRV.</b> Kc = 1.0 with no rupture disc; 0.9 when a disc + PRV combination has not been NB-certified together (use the certified Combination Capacity Factor if available). Formula/table-based, not read from a figure. <br><i>Ref: API RP 520 Part I, §5.6.5 / §5.7.</i></div>
  </div>
  <div class="field"><label>Kv — Viscosity Correction (liquid) <span class="infobtn" onclick="toggleTip('tip_Kv')">i</span></label><input id="g_Kv" type="number" step="any" value="1.0"><span class="hint">1.0 if Re&gt;~100,000 (light HC); else from API 520 curve</span>
    <div class="tip" id="tip_Kv"><span class="close-tip" onclick="toggleTip('tip_Kv')">✕</span><b>Kv — Viscosity Correction Factor, liquid service.</b> Function of Reynolds number at the trial orifice area (iterative). Kv = 1.0 for turbulent flow (Re typically &gt; ~16,000–100,000, most light hydrocarbons). <br><i>Ref: API RP 520 Part I, viscosity-correction curve (numbered Fig.33/34 depending on edition — confirm against your copy).</i></div>
  </div>
</div>

<!-- ================= EQUIPMENT AREA MODULE ================= -->
<h2 class="section">2. Equipment Fire-Exposed Area Module (API RP 521 §4.4 / Annex D)</h2>
<div class="assume">Add every item of equipment within the common fire-exposed zone (vessel, drum, exchanger shell, compressor casing, etc.) protected by this PSV / relief header. Each item computes its own <b>wetted</b> (liquid-containing) or <b>total exposed</b> (gas-filled) surface area from its geometry, or a direct area entry — the areas are then summed to a single Total Fire-Exposed Area which feeds the Fire Case tab. One common Environmental Factor F and drainage credit is applied to the summed area (standard API 521 practice for a shared fire zone).</div>

<div id="equip_list"></div>
<button class="calc-btn" onclick="addEquipRow()" style="background:var(--ok);">＋ Add Equipment</button>
<button class="calc-btn" onclick="computeArea()">Compute Total Fire-Exposed Area</button>

<div class="grid" style="margin-top:14px;">
  <div class="field"><label>Drainage &amp; Fire-fighting (applies to group total)</label>
    <select id="eq_drain">
      <option value="43200">Adequate drainage &amp; firefighting (C₁=43,200)</option>
      <option value="70900">Inadequate drainage / no firefighting (C₁=70,900)</option>
    </select>
  </div>
  <div class="field"><label>Environmental Factor, F (applies to group total)</label>
    <select id="eq_F" onchange="document.getElementById('eq_Fcustom').value=this.value">
      <option value="1.0">Bare vessel (F=1.0)</option>
      <option value="0.3">Insulated — typical 1&quot; (F=0.3)</option>
      <option value="0.15">Insulated — typical 2&quot; (F=0.15)</option>
      <option value="0.075">Insulated — typical 4&quot; (F=0.075)</option>
      <option value="1.0">Water-application facility (F=1.0, credit via C₁ instead)</option>
      <option value="0.03">Earth-covered storage (F=0.03)</option>
      <option value="0.0">Below-grade / underground (F=0.0)</option>
    </select>
  </div>
  <div class="field"><label>F — custom value used in calc</label><input id="eq_Fcustom" type="number" step="any" value="1.0"></div>
</div>

<table id="equip_breakdown_table" style="display:none;">
  <thead><tr><th>Equipment</th><th>Geometry</th><th>Computed Area, m²</th></tr></thead>
  <tbody id="equip_breakdown_body"></tbody>
</table>

<div class="result-box" id="eq_result" style="margin-top:10px;">
  <span class="label">Total Fire-Exposed Area (sum of all equipment), A</span><br>
  <span class="big" id="eq_A_out">—</span> m²
</div>

<div class="note" style="margin-top:10px;">
  <label style="display:flex;align-items:center;gap:8px;font-weight:700;cursor:pointer;">
    <input type="checkbox" id="eq_override_chk" onchange="toggleAreaOverride()" style="width:16px;height:16px;">
    Manually override Total Fire-Exposed Area (skip the geometry calculation above)
  </label>
  <div id="eq_override_field" style="display:none;margin-top:8px;">
    <div class="field" style="max-width:260px;"><label>Manual Total Area, m²</label><input id="eq_override_val" type="number" step="any" value="25"></div>
  </div>
</div>

<!-- ================= RELIEF CASES ================= -->
<h2 class="section">3. Relief Load Cases</h2>

<h3 class="sub" style="margin-top:0;">Step 1 — Select PSV Duty / Fluid State</h3>
<div class="duty-select">
  <button class="dutybtn active" id="duty_gas" onclick="setDuty('gas')">⛽ GAS / VAPOR PSV</button>
  <button class="dutybtn" id="duty_liquid" onclick="setDuty('liquid')">💧 LIQUID PSV</button>
  <button class="dutybtn" id="duty_steam" onclick="setDuty('steam')">♨ STEAM PSV</button>
</div>
<div class="note" id="duty_hint">Gas/Vapor PSV selected — applicable relief scenarios shown below: External Fire, Blocked Outlet/CV Fail, Tube Rupture. Switch above to change fluid state; the summary in Section 4 will only compare cases relevant to the selected duty.</div>

<h3 class="sub">Step 2 — Applicable Relief Scenarios</h3>
<div class="tabs">
  <div class="tabbtn active" data-duty="gas steam" onclick="showTab('fire')">Case 1: External Fire</div>
  <div class="tabbtn" data-duty="gas steam" onclick="showTab('blocked')">Case 2: Blocked Outlet / CV Fail</div>
  <div class="tabbtn" data-duty="liquid" onclick="showTab('thermal')">Case 3: Liquid Thermal Expansion</div>
  <div class="tabbtn" data-duty="gas liquid" onclick="showTab('tube')">Case 4: Exchanger Tube Rupture</div>
  <div class="tabbtn" data-duty="liquid" onclick="showTab('liquid')">Case 5: Blocked Outlet (Liquid)</div>
</div>

<!-- CASE 1: FIRE -->
<div class="tabpanel active case-block" id="tab_fire">
  <h3 class="sub">Case 1 — External Pool Fire (API RP 521 §4.4)</h3>
  <div class="grid">
    <div class="field"><label>Fluid Generated</label>
      <select id="f_fluidtype" onchange="toggleSteam('f')"><option value="gas">Gas / Vapor (hydrocarbon)</option><option value="steam">Steam</option></select>
    </div>
    <div class="field"><label>Latent Heat of Vaporization, kJ/kg</label><input id="f_latent" type="number" step="any" value="350"></div>
    <div class="field"><label>Flow Type</label>
      <select id="f_flowtype"><option value="critical">Critical Flow (to flare header)</option><option value="sub">Sub-critical Flow</option></select>
    </div>
    <div class="field" id="f_Ksh_field" style="display:none;"><label>Ksh — Superheat Correction <span class="infobtn" onclick="toggleTip('tip_f_Ksh')">i</span></label><input id="f_Ksh" type="number" step="any" value="1.0">
      <div class="tip" id="tip_f_Ksh"><span class="close-tip" onclick="toggleTip('tip_f_Ksh')">✕</span><b>Ksh — Steam Superheat Correction Factor.</b> Ksh = 1.0 for saturated steam. For superheated steam, read from the superheat-correction table (interpolated by pressure and temperature). <br><i>Ref: API RP 520 Part I, Superheat Steam Correction Factor table (commonly Table 8/9 — confirm against your edition).</i></div>
    </div>
    <div class="field" id="f_Kn_field" style="display:none;"><label>Kn — Napier Correction (steam) <span class="infobtn" onclick="toggleTip('tip_f_Kn')">i</span></label><input id="f_Kn" type="number" step="any" value="1.0">
      <div class="tip" id="tip_f_Kn"><span class="close-tip" onclick="toggleTip('tip_f_Kn')">✕</span><b>Kn — Napier Steam Correction Factor.</b> Kn = 1.0 for set pressures below ~10,340 kPa (1500 psig). Above this, apply the Napier correction curve/table up to ~20,680 kPa (3000 psig); beyond that, use the critical-flow steam model directly. <br><i>Ref: API RP 520 Part I, Napier Correction Factor table (commonly Table 8 — confirm against your edition).</i></div>
    </div>
  </div>
  <button class="calc-btn" onclick="calcFire()">Calculate Fire Case</button>
  <div class="two-col">
    <div class="result-box"><span class="label">Heat Input, Q</span><br><span class="big" id="f_Q_out">—</span> kW</div>
    <div class="result-box"><span class="label">Vapor Relief Load, W</span><br><span class="big" id="f_W_out">—</span> kg/hr</div>
  </div>
  <div class="result-box"><span class="label">Required Orifice Area</span><br><span class="big" id="f_A_out">—</span> mm²</div>
</div>

<!-- CASE 2: BLOCKED OUTLET / CV FAIL VAPOR -->
<div class="tabpanel case-block" id="tab_blocked">
  <h3 class="sub">Case 2 — Blocked Discharge / Control Valve Fail-Open / Gas Blowby (Vapor)</h3>
  <div class="grid">
    <div class="field"><label>Relief Load, W, kg/hr</label><input id="b_W" type="number" step="any" value="15000"></div>
    <div class="field"><label>Fluid Type</label>
      <select id="b_fluidtype" onchange="toggleSteam('b')"><option value="gas">Gas / Vapor (hydrocarbon)</option><option value="steam">Steam</option></select>
    </div>
    <div class="field"><label>Flow Type</label>
      <select id="b_flowtype"><option value="critical">Critical Flow</option><option value="sub">Sub-critical Flow</option></select>
    </div>
    <div class="field" id="b_Ksh_field" style="display:none;"><label>Ksh — Superheat Correction <span class="infobtn" onclick="toggleTip('tip_b_Ksh')">i</span></label><input id="b_Ksh" type="number" step="any" value="1.0">
      <div class="tip" id="tip_b_Ksh"><span class="close-tip" onclick="toggleTip('tip_b_Ksh')">✕</span><b>Ksh — Steam Superheat Correction Factor.</b> Ksh = 1.0 for saturated steam; for superheated steam, read from the superheat-correction table (interpolated by pressure and temperature). <br><i>Ref: API RP 520 Part I, Superheat Steam Correction Factor table (commonly Table 8/9 — confirm against your edition).</i></div>
    </div>
    <div class="field" id="b_Kn_field" style="display:none;"><label>Kn — Napier Correction (steam) <span class="infobtn" onclick="toggleTip('tip_b_Kn')">i</span></label><input id="b_Kn" type="number" step="any" value="1.0">
      <div class="tip" id="tip_b_Kn"><span class="close-tip" onclick="toggleTip('tip_b_Kn')">✕</span><b>Kn — Napier Steam Correction Factor.</b> Kn = 1.0 for set pressures below ~10,340 kPa (1500 psig); above this apply the Napier correction curve/table up to ~20,680 kPa (3000 psig), beyond which the critical-flow steam model is used directly. <br><i>Ref: API RP 520 Part I, Napier Correction Factor table (commonly Table 8 — confirm against your edition).</i></div>
    </div>
  </div>
  <button class="calc-btn" onclick="calcBlocked()">Calculate Blocked Outlet Case</button>
  <div class="result-box"><span class="label">Required Orifice Area</span><br><span class="big" id="b_A_out">—</span> mm²</div>
</div>

<!-- CASE 3: THERMAL EXPANSION -->
<div class="tabpanel case-block" id="tab_thermal">
  <h3 class="sub">Case 3 — Liquid Thermal Expansion (blocked-in liquid-full line/exchanger, API 521 §4.14)</h3>
  <div class="assume">Q_relief (m³/hr) = (β × H × 3600) / (ρ × Cp) &nbsp;—&nbsp; β = cubical expansion coeff. (1/°C), H = heat input (kW), ρ = density (kg/m³), Cp = specific heat (kJ/kg·°C). This case typically governs the smallest orifice (often D or E) and is rarely limiting.</div>

  <h3 class="sub" style="margin-top:14px;">Cubical Expansion Coefficient, β — Guideline (API RP 521, Table 2)</h3>
  <div class="grid">
    <div class="field"><label>Quick-pick β by liquid gravity <span class="infobtn" onclick="toggleTip('tip_beta')">i</span>
      <div class="tip" id="tip_beta"><span class="close-tip" onclick="toggleTip('tip_beta')">✕</span><b>API RP 521, Table 2 — Typical Values of Cubic Expansion Coefficient for Hydrocarbon Liquids and Water</b> (at 60°F/15.6°C basis). These are generic hydrocarbon-liquid correlations by gravity band; for a specific fluid/mixture, use actual process/simulation data (e.g. HYSYS/Aspen) where available — the API table is a fallback when fluid-specific data isn't at hand. Water does not follow the hydrocarbon correlation (its real β is much lower and non-linear with temperature) — use the dedicated Water row.</div>
    </label>
      <select id="t_beta_pick" onchange="applyBetaPick()">
        <option value="">— select to auto-fill β —</option>
        <option value="0.00072">°API 3–34.9 (SG 1.052–0.850) — β = 0.00072 /°C (0.0004 /°F)</option>
        <option value="0.0009">°API 35–50.9 (SG 0.850–0.775) — β = 0.0009 /°C (0.0005 /°F)</option>
        <option value="0.00108">°API 51–63.9 (SG 0.775–0.724) — β = 0.00108 /°C (0.0006 /°F)</option>
        <option value="0.00126">°API 64–78.9 (SG 0.724–0.672) — β = 0.00126 /°C (0.0007 /°F)</option>
        <option value="0.00144">°API 79–88.9 (SG 0.672–0.642) — β = 0.00144 /°C (0.0008 /°F)</option>
        <option value="0.00153">°API 89–93.9 (SG 0.642–0.628) — β = 0.00153 /°C (0.00085 /°F)</option>
        <option value="0.00162">°API 94–100+ / lighter (SG 0.628–0.611) — β = 0.00162 /°C (0.0009 /°F)</option>
        <option value="0.00018">Water (SG 1.000) — β = 0.00018 /°C (0.0001 /°F)</option>
      </select>
    </div>
  </div>
  <div class="grid">
    <div class="field"><label>Cubical Expansion Coeff. β, 1/°C</label><input id="t_beta" type="number" step="any" value="0.0012"><span class="hint">heavier liquid (higher SG) → lower β; lighter liquid → higher β</span></div>
    <div class="field"><label>Liquid Density, kg/m³</label><input id="t_rho" type="number" step="any" value="550"></div>
    <div class="field"><label>Liquid Specific Heat, Cp, kJ/kg·°C</label><input id="t_cp" type="number" step="any" value="2.3"></div>
  </div>

  <h3 class="sub" style="margin-top:14px;">Heat Input, H — Guideline &amp; Helper</h3>
  <div class="assume">
    Two recognized bases are commonly used for the blocked-in thermal relief heat input, per API RP 521 and widely-published industry practice (not a single fixed API equation — engineering judgment applies):
    <ul style="margin:6px 0 4px 18px;padding:0;">
      <li><b>Solar radiation</b> on the exposed surface of the blocked-in, liquid-full line/equipment: typical design flux <b>0.79–1.04 kW/m²</b> (≈250–330 Btu/hr·ft²), applied to the exposed (or projected) surface area. Use the lower end for temperate climates / part-insulated lines, the upper end for full tropical sun exposure on bare pipe.</li>
      <li><b>Heat exchanger duty</b>, when the blocked-in liquid is on one side of an exchanger and the other side continues to circulate a hot medium — use the actual exchanger duty from the datasheet/simulation (this is normally far larger than the solar case and will govern if applicable).</li>
    </ul>
    In practice many operating companies simply fit the smallest standard PSV (¾"×1", orifice D/E) on blocked-in liquid-full segments without a rigorous heat balance, since the computed relief rate is almost always negligible — reserve the full calculation for larger-bore / long-length blocked segments or where an exchanger duty applies.
  </div>
  <div class="grid">
    <div class="field"><label>H Estimation Method</label>
      <select id="t_Hmethod" onchange="toggleHMethod()">
        <option value="manual">Manual / Direct Value (kW)</option>
        <option value="solar">Solar Radiation on Exposed Area</option>
        <option value="exchanger">Heat Exchanger Duty (from datasheet)</option>
      </select>
    </div>
  </div>
  <div class="grid" id="t_solar_fields" style="display:none;">
    <div class="field"><label>Exposed Surface Area, m²</label><input id="t_solarA" type="number" step="any" value="10"><span class="hint">use the Equipment Area module (Section 2) result if applicable, or pipe OD×length</span></div>
    <div class="field"><label>Solar Flux, kW/m²</label>
      <select id="t_solarFlux" onchange="document.getElementById('t_solarFluxCustom').value=this.value">
        <option value="0.79">Temperate climate / typical (0.79 kW/m² ≈ 250 Btu/hr·ft²)</option>
        <option value="0.94">Moderate-high sun (0.94 kW/m² ≈ 300 Btu/hr·ft²)</option>
        <option value="1.04">Full tropical sun, bare pipe (1.04 kW/m² ≈ 330 Btu/hr·ft²)</option>
      </select>
    </div>
    <div class="field"><label>Flux — custom value used in calc</label><input id="t_solarFluxCustom" type="number" step="any" value="0.79"></div>
    <div class="field" style="align-self:flex-end;"><button class="calc-btn" onclick="applySolarH()" style="background:var(--ok);">Apply Solar H to field below</button></div>
  </div>
  <div class="grid">
    <div class="field"><label>Heat Input, H, kW</label><input id="t_H" type="number" step="any" value="15"><span class="hint">solar / fire exposure / adjacent hot stream</span></div>
  </div>
  <button class="calc-btn" onclick="calcThermal()">Calculate Thermal Relief Case</button>
  <div class="two-col">
    <div class="result-box"><span class="label">Volumetric Relief Rate, Q</span><br><span class="big" id="t_Q_out">—</span> m³/hr</div>
  </div>
  <div class="result-box"><span class="label">Required Orifice Area</span><br><span class="big" id="t_A_out">—</span> mm²</div>
</div>

<!-- CASE 4: TUBE RUPTURE -->
<div class="tabpanel case-block" id="tab_tube">
  <h3 class="sub">Case 4 — Heat Exchanger Tube Rupture (API 521 §4.9, single-tube rupture rule)</h3>
  <div class="assume">Flow through a single ruptured tube is taken as twice the flow area of one tube (conservative rule-of-thumb, full-bore rupture), based on the high-pressure side conditions flashing/flowing into the low-pressure side. Flow computed via nozzle equation at tube-rupture ΔP.</div>
  <div class="grid">
    <div class="field"><label>Tube Fluid Phase</label>
      <select id="r_phase" onchange="toggleTubePhase()"><option value="gas">Gas / Vapor</option><option value="liquid">Liquid</option></select>
    </div>
    <div class="field"><label>Tube ID, mm</label><input id="r_id" type="number" step="any" value="21.2"></div>
    <div class="field"><label>High-Pressure Side Pressure, kg/cm²g</label><input id="r_Phs" type="number" step="any" value="45"></div>
    <div class="field"><label>Low-Pressure Side (relief set) Pressure, kg/cm²g</label><input id="r_Pls" type="number" step="any" value="10.5"></div>
    <div class="field" id="r_rho_field" style="display:none;"><label>HP-side Liquid Density, kg/m³</label><input id="r_rho" type="number" step="any" value="750"></div>
  </div>
  <button class="calc-btn" onclick="calcTube()">Calculate Tube Rupture Case</button>
  <div class="two-col">
    <div class="result-box"><span class="label">Tube-Rupture Relief Load, W</span><br><span class="big" id="r_W_out">—</span> kg/hr</div>
  </div>
  <div class="result-box"><span class="label">Required Orifice Area</span><br><span class="big" id="r_A_out">—</span> mm²</div>
</div>

<!-- CASE 5: LIQUID BLOCKED OUTLET -->
<div class="tabpanel case-block" id="tab_liquid">
  <h3 class="sub">Case 5 — Blocked Outlet / Pump Deadhead / Overfilling (Liquid)</h3>
  <div class="grid">
    <div class="field"><label>Relief Load, Q, m³/hr</label><input id="l_Q" type="number" step="any" value="40"></div>
  </div>
  <button class="calc-btn" onclick="calcLiquid()">Calculate Liquid Blocked Outlet Case</button>
  <div class="result-box"><span class="label">Required Orifice Area</span><br><span class="big" id="l_A_out">—</span> mm²</div>
</div>

<!-- ================= SUMMARY ================= -->
<h2 class="section">4. Governing Case Summary &amp; PSV Selection</h2>
<table id="summary_table">
  <thead><tr><th>Relief Case</th><th>Basis</th><th>Relief Load</th><th>Required Area, mm²</th><th>Selected Std. Orifice</th><th>Orifice Area, mm²</th></tr></thead>
  <tbody id="summary_body">
    <tr><td colspan="6" style="text-align:center;color:var(--grey);">Click "Calculate All Cases" to populate summary</td></tr>
  </tbody>
</table>

<div class="result-box" style="border-color:var(--accent);">
  <span class="label">Governing Case (Maximum Required Area)</span><br>
  <span class="big" id="gov_case_out" style="color:var(--accent);">—</span>
</div>

<h3 class="sub">API Standard Orifice Reference — API 526 (Horizontal Table)</h3>
<table id="api526_table" style="font-size:11px;">
  <tbody id="api526_body"></tbody>
</table>
<div class="note">Multiple flange-rating combinations exist per API 526 for a given orifice letter (e.g., 3J4, 3"×4" 150#/300#/600# etc.). The table above lists the most commonly applied inlet×outlet flange size; confirm final selection with valve vendor GA drawing, inlet piping 3% pressure-drop check and outlet piping built-up backpressure check (API 520 Part II) before MOC/PO issue.</div>

<footer class="sig">
  <div class="chk-title">Prepared / Reviewed</div>
  <table style="margin-top:4px;">
    <tr><td style="width:25%;">Prepared By</td><td style="width:25%;"></td><td style="width:25%;">Reviewed By</td><td style="width:25%;"></td></tr>
    <tr><td>Date</td><td></td><td>Date</td><td></td></tr>
  </table>
  <div style="margin-top:8px;">Reference: API RP 520 Part I (Sizing &amp; Selection), API RP 520 Part II (Installation), API RP 521 (Pressure-relieving &amp; Depressuring Systems), API STD 526 (Flanged Steel Pressure-relief Valves). Tool for preliminary engineering use only.</div>
</footer>
   <footer class="no-print">
   <h3>Developer Information</h3>
   <p><strong>Gajanand Yadav</strong></p>
   <p>Chemical Engineer, IIT Guwahati</p>
   <p>Email: <a href="mailto:gajanandiitg@gmail.com">gajanandiitg@gmail.com</a> |
    Mobile: <a href="tel:+918369354472">+91-8369354472</a></p>
   <p>For property calculation, Density,Cp, saturation condition visit below link</p>
   <a href="https://gajuiitg.github.io/Thermocal/">Clickable Here</a>
      </footer>
</div>
</div>

<script>
// ---------- Standard API orifice table ----------
const ORIFICES = [
 {letter:"D", in2:0.110, mm2:70.97, flange:"1\" x 2\""},
 {letter:"E", in2:0.196, mm2:126.45,flange:"1\" x 2\" / 1.5\" x 2.5\""},
 {letter:"F", in2:0.307, mm2:198.06,flange:"1.5\" x 2.5\""},
 {letter:"G", in2:0.503, mm2:324.52,flange:"1.5\" x 2.5\" / 2\" x 3\""},
 {letter:"H", in2:0.785, mm2:506.45,flange:"2\" x 3\""},
 {letter:"J", in2:1.287, mm2:830.32,flange:"3\" x 4\""},
 {letter:"K", in2:1.838, mm2:1185.8,flange:"3\" x 4\""},
 {letter:"L", in2:2.853, mm2:1840.6,flange:"4\" x 6\""},
 {letter:"M", in2:3.60,  mm2:2322.6,flange:"4\" x 6\""},
 {letter:"N", in2:4.34,  mm2:2800.0,flange:"4\" x 6\""},
 {letter:"P", in2:6.38,  mm2:4116.8,flange:"6\" x 8\""},
 {letter:"Q", in2:11.05, mm2:7129.0,flange:"6\" x 8\""},
 {letter:"R", in2:16.0,  mm2:10322.6,flange:"8\" x 10\""},
 {letter:"T", in2:26.0,  mm2:16774.2,flange:"8\" x 10\""}
];

function populateAPI526(){
  const tb=document.getElementById('api526_body');
  const rowHead = (label)=>`<th style="text-align:left;background:var(--steel);white-space:nowrap;">${label}</th>`;
  const rLetter = '<tr>'+rowHead('Orifice Designation')+ORIFICES.map(o=>`<td style="text-align:center;font-weight:700;">${o.letter}</td>`).join('')+'</tr>';
  const rIn2    = '<tr>'+rowHead('Area, in²')+ORIFICES.map(o=>`<td style="text-align:center;">${o.in2}</td>`).join('')+'</tr>';
  const rMm2    = '<tr>'+rowHead('Area, mm²')+ORIFICES.map(o=>`<td style="text-align:center;">${o.mm2.toFixed(1)}</td>`).join('')+'</tr>';
  const rFlange = '<tr>'+rowHead('Typical API 526 Inlet × Outlet')+ORIFICES.map(o=>`<td style="text-align:center;">${o.flange}</td>`).join('')+'</tr>';
  tb.innerHTML = rLetter+rIn2+rMm2+rFlange;
}
populateAPI526();

function selectOrifice(area_mm2){
  for(const o of ORIFICES){ if(o.mm2 >= area_mm2) return o; }
  return {letter:"> T (special order)", mm2: area_mm2, in2:(area_mm2/645.16).toFixed(2), flange:"consult vendor"};
}

// ---------- Unit helpers ----------
function P_abs_kPa(p_gauge_kgcm2, atm_kgcm2){ return (parseFloat(p_gauge_kgcm2)+parseFloat(atm_kgcm2))*98.0665; }
function T_K(t_degC){ return parseFloat(t_degC)+273.15; }

// ---------- Core API 520 sizing equations (metric) ----------
// Gas/vapor CRITICAL flow: A(mm2) = W/(C*Kd*P1*Kb*Kc) * sqrt(T*Z/M) ; W kg/h, P1 kPa abs, T K, M kg/kmol
function gasCriticalArea(W,P1,T,Z,M,k,Kd,Kb,Kc){
  const C = 0.03948*Math.sqrt(k*Math.pow(2/(k+1),(k+1)/(k-1)));
  return W/(C*Kd*P1*Kb*Kc) * Math.sqrt(T*Z/M);
}
// Gas/vapor SUB-CRITICAL flow: A(mm2)=4.972*W/(F2*Kd*Kc)*sqrt(T*Z/(M*P1*(P1-P2)))
function gasSubcriticalArea(W,P1,P2,T,Z,M,k,Kd,Kc){
  const r = P2/P1;
  const F2 = Math.sqrt( (k/(k-1)) * Math.pow(r,2/k) * ((1-Math.pow(r,(k-1)/k))/(1-r)) );
  return 4.972*W/(F2*Kd*Kc) * Math.sqrt(T*Z/(M*P1*(P1-P2)));
}
// Steam CRITICAL: A(mm2)=190.4*W/(P1*Kd*Kb*Kc*Ksh*Kn)
function steamArea(W,P1,Kd,Kb,Kc,Ksh,Kn){
  return 190.4*W/(P1*Kd*Kb*Kc*Ksh*Kn);
}
// Liquid: A(mm2)=103.5*Q(m3/h)/(Kd*Kw*Kc*Kv)*sqrt(G/dP(kPa))
function liquidArea(Q,G,dP,Kd,Kw,Kc,Kv){
  return 103.5*Q/(Kd*Kw*Kc*Kv) * Math.sqrt(G/dP);
}

// ---------- UI: tabs ----------
// ---------- Tap/click tooltips (works on touchscreens, unlike hover-only title attr) ----------
function toggleTip(id){
  const el = document.getElementById(id);
  const wasOpen = el.classList.contains('show');
  document.querySelectorAll('.tip.show').forEach(t=>t.classList.remove('show'));
  if(!wasOpen) el.classList.add('show');
}
document.addEventListener('click', function(e){
  if(!e.target.classList.contains('infobtn') && !e.target.closest('.tip')){
    document.querySelectorAll('.tip.show').forEach(t=>t.classList.remove('show'));
  }
});

function showTab(name){
  document.querySelectorAll('.tabpanel').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.tabbtn').forEach(b=>b.classList.remove('active'));
  document.getElementById('tab_'+name).classList.add('active');
  event.target.classList.add('active');
}
function toggleEquipGeom(rowId){
  const t=document.getElementById('eqt_'+rowId).value;
  document.getElementById('eqf_direct_'+rowId).style.display = (t==='direct')?'flex':'none';
  document.getElementById('eqf_len_'+rowId).style.display = (t==='direct'||t==='sphere')?'none':'flex';
  document.getElementById('eqf_ll_'+rowId).style.display = (t==='direct')?'none':'flex';
  document.getElementById('eqf_elev_'+rowId).style.display = (t==='direct')?'none':'flex';
  document.getElementById('eqf_D_'+rowId).style.display = (t==='direct')?'none':'flex';
}
function toggleSteam(prefix){
  const isSteam = document.getElementById(prefix+'_fluidtype').value==='steam';
  document.getElementById(prefix+'_Ksh_field').style.display = isSteam?'flex':'none';
  document.getElementById(prefix+'_Kn_field').style.display = isSteam?'flex':'none';
}
function toggleTubePhase(){
  document.getElementById('r_rho_field').style.display = (document.getElementById('r_phase').value==='liquid')?'flex':'none';
}

// ---------- PSV Duty selection (Gas / Liquid / Steam) ----------
let currentDuty = 'gas';
const DUTY_HINTS = {
  gas:"Gas/Vapor PSV selected — applicable relief scenarios shown below: External Fire, Blocked Outlet/CV Fail, Tube Rupture. Switch above to change fluid state; the summary in Section 4 will only compare cases relevant to the selected duty.",
  liquid:"Liquid PSV selected — applicable relief scenarios shown below: Liquid Thermal Expansion, Tube Rupture (liquid), Blocked Outlet/Overfill (Liquid). Fire case is not normally governing for a liquid-full, non-flashing system and is hidden; switch to Gas/Vapor duty if a two-phase/flashing fire relief check is also required.",
  steam:"Steam PSV selected — applicable relief scenarios shown below: External Fire (steam generation) and Blocked Outlet/CV Fail, both using the API 520 steam (Napier) sizing equation. Ksh/Kn correction fields are shown automatically."
};
function setDuty(duty){
  currentDuty = duty;
  document.querySelectorAll('.dutybtn').forEach(b=>b.classList.remove('active'));
  document.getElementById('duty_'+duty).classList.add('active');
  document.getElementById('duty_hint').textContent = DUTY_HINTS[duty];

  const tabs = document.querySelectorAll('.tabbtn');
  let firstVisible = null;
  tabs.forEach(t=>{
    const applicable = t.getAttribute('data-duty').split(' ').includes(duty);
    t.style.display = applicable ? 'inline-block' : 'none';
    if(applicable && !firstVisible) firstVisible = t;
  });
  document.querySelectorAll('.tabpanel').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.tabbtn').forEach(b=>b.classList.remove('active'));
  if(firstVisible){
    firstVisible.classList.add('active');
    const name = firstVisible.getAttribute('onclick').match(/'(\w+)'/)[1];
    document.getElementById('tab_'+name).classList.add('active');
  }
  if(duty==='steam'){
    const bft=document.getElementById('b_fluidtype'); if(bft){bft.value='steam'; toggleSteam('b');}
    const fft=document.getElementById('f_fluidtype'); if(fft){fft.value='steam'; toggleSteam('f');}
  } else if(duty==='gas'){
    const bft=document.getElementById('b_fluidtype'); if(bft){bft.value='gas'; toggleSteam('b');}
    const fft=document.getElementById('f_fluidtype'); if(fft){fft.value='gas'; toggleSteam('f');}
    const rp=document.getElementById('r_phase'); if(rp){rp.value='gas'; toggleTubePhase();}
  } else if(duty==='liquid'){
    const rp=document.getElementById('r_phase'); if(rp){rp.value='liquid'; toggleTubePhase();}
  }
  if(typeof updateSummary==='function') updateSummary();
}

// ---------- Equipment area module (multiple equipment, summed) ----------
let lastArea_m2 = 0;
let equipCounter = 0;

function addEquipRow(){
  equipCounter++;
  const id = equipCounter;
  const div = document.createElement('div');
  div.className = 'equip-row';
  div.id = 'eqrow_'+id;
  div.innerHTML = `
    <div class="eq-head">
      <span class="eq-title">Equipment #${id}</span>
      <button class="eq-remove" onclick="removeEquipRow(${id})">✕ Remove</button>
    </div>
    <div class="grid">
      <div class="field"><label>Tag / Description</label><input id="eqn_${id}" type="text" value="Equipment-${id}"></div>
      <div class="field"><label>Geometry Type</label>
        <select id="eqt_${id}" onchange="toggleEquipGeom(${id})">
          <option value="vert">Vertical Vessel (2:1 SE heads)</option>
          <option value="horz">Horizontal Vessel (2:1 SE heads)</option>
          <option value="sphere">Sphere</option>
          <option value="direct">Direct Area Input (compressor/exchanger/other)</option>
        </select>
      </div>
      <div class="field" id="eqf_D_${id}"><label>Diameter, m</label><input id="eqD_${id}" type="number" step="any" value="2.0"></div>
      <div class="field" id="eqf_len_${id}"><label>Tan-Tan Length / Height, m</label><input id="eqL_${id}" type="number" step="any" value="6.0"></div>
      <div class="field" id="eqf_ll_${id}"><label>Liquid Level, % (of height/dia)</label><input id="eqLL_${id}" type="number" step="any" value="50"></div>
      <div class="field" id="eqf_elev_${id}"><label>Elevation of Bottom above Grade, m</label><input id="eqE_${id}" type="number" step="any" value="1.5"></div>
      <div class="field" id="eqf_direct_${id}" style="display:none;"><label>Exposed Area, m² (direct)</label><input id="eqDir_${id}" type="number" step="any" value="25"></div>
    </div>
    <div class="eq-area" id="eqarea_${id}">Area not yet computed — click "Compute Total Fire-Exposed Area"</div>
  `;
  document.getElementById('equip_list').appendChild(div);
  toggleEquipGeom(id);
}
function removeEquipRow(id){
  const el = document.getElementById('eqrow_'+id);
  if(el) el.remove();
  computeArea();
}
function computeRowArea(id){
  const type = document.getElementById('eqt_'+id).value;
  const name = document.getElementById('eqn_'+id).value || ('Equipment #'+id);
  const D = parseFloat(document.getElementById('eqD_'+id).value)||0;
  let A=0, geomLabel='';
  if(type==='direct'){
    A = parseFloat(document.getElementById('eqDir_'+id).value)||0;
    geomLabel='Direct input';
  } else if(type==='sphere'){
    const LLpct = parseFloat(document.getElementById('eqLL_'+id).value)/100;
    const h = D*LLpct;
    A = Math.PI*D*h;
    geomLabel='Sphere';
  } else if(type==='vert'){
    const H = parseFloat(document.getElementById('eqL_'+id).value);
    const LLpct = parseFloat(document.getElementById('eqLL_'+id).value)/100;
    const elev = parseFloat(document.getElementById('eqE_'+id).value);
    const liqHeight = H*LLpct;
    const fireLimit = Math.max(0, 7.6-elev); // API 521 25ft/7.6m grade credit
    const effHeight = Math.min(liqHeight, fireLimit);
    const headArea = 1.09*Math.PI*D*D/4; // approx 2:1 SE head area
    A = Math.PI*D*effHeight + (effHeight>0? headArea:0);
    geomLabel='Vertical vessel';
  } else if(type==='horz'){
    const L = parseFloat(document.getElementById('eqL_'+id).value);
    const LLpct = parseFloat(document.getElementById('eqLL_'+id).value)/100;
    const elev = parseFloat(document.getElementById('eqE_'+id).value);
    const R = D/2;
    const h_full = D*LLpct;
    const fireLimit = Math.max(0, 7.6-elev);
    const h = Math.min(h_full, D, elev+D<=7.6? h_full : Math.max(0,fireLimit));
    const ratio = Math.max(0,Math.min(1, h/R));
    const theta = 2*Math.acos(1-ratio); // wetted arc angle, radians
    const shellArea = L*theta*R;
    const headAreaEach = 1.09*Math.PI*D*D/4;
    const headWetted = 2*headAreaEach*(h/D); // linear approx per head
    A = shellArea + headWetted;
    geomLabel='Horizontal vessel';
  }
  return {name, geomLabel, area:A};
}
function toggleAreaOverride(){
  const chk = document.getElementById('eq_override_chk').checked;
  document.getElementById('eq_override_field').style.display = chk?'block':'none';
  computeArea();
}
function computeArea(){
  const overrideChk = document.getElementById('eq_override_chk').checked;
  if(overrideChk){
    const A = parseFloat(document.getElementById('eq_override_val').value)||0;
    lastArea_m2 = A;
    document.getElementById('eq_A_out').textContent = A.toFixed(2) + ' (manual override)';
    document.getElementById('equip_breakdown_table').style.display='none';
    return A;
  }
  const rows = document.querySelectorAll('.equip-row');
  let total = 0;
  const breakdown = [];
  rows.forEach(row=>{
    const id = row.id.replace('eqrow_','');
    const r = computeRowArea(id);
    total += r.area;
    breakdown.push(r);
    const areaEl = document.getElementById('eqarea_'+id);
    if(areaEl) areaEl.textContent = `Computed Area: ${r.area.toFixed(2)} m²`;
  });
  lastArea_m2 = total;
  document.getElementById('eq_A_out').textContent = total.toFixed(2);
  const tbl = document.getElementById('equip_breakdown_table');
  if(breakdown.length>0){
    tbl.style.display='table';
    document.getElementById('equip_breakdown_body').innerHTML = breakdown.map(b=>`<tr><td>${b.name}</td><td>${b.geomLabel}</td><td>${b.area.toFixed(2)}</td></tr>`).join('');
  } else {
    tbl.style.display='none';
  }
  return total;
}

// ---------- Case calculations ----------
function commonInputs(){
  return {
    setP: parseFloat(document.getElementById('g_setP').value),
    op: parseFloat(document.getElementById('g_op').value),
    bp: parseFloat(document.getElementById('g_bp').value),
    atm: parseFloat(document.getElementById('g_atm').value),
    M: parseFloat(document.getElementById('g_M').value),
    k: parseFloat(document.getElementById('g_k').value),
    Z: parseFloat(document.getElementById('g_Z').value),
    T: parseFloat(document.getElementById('g_T').value),
    G: parseFloat(document.getElementById('g_G').value),
    Kd_v: parseFloat(document.getElementById('g_Kd_v').value),
    Kd_l: parseFloat(document.getElementById('g_Kd_l').value),
    Kb: parseFloat(document.getElementById('g_Kb').value),
    Kw: parseFloat(document.getElementById('g_Kw').value),
    Kc: parseFloat(document.getElementById('g_Kc').value),
    Kv: parseFloat(document.getElementById('g_Kv').value)
  };
}

let results = {}; // store per-case {basis, load, area}

function calcFire(overpressureOverride){
  const c = commonInputs();
  const op = overpressureOverride || 16; // fire case typically 16 or 21%
  const P1 = P_abs_kPa(c.setP*(1+op/100), c.atm);
  const P2 = P_abs_kPa(c.bp, c.atm);
  const Tk = T_K(c.T);
  const A_wetted = lastArea_m2>0? lastArea_m2 : computeArea();
  const C1 = parseFloat(document.getElementById('eq_drain').value);
  const F = parseFloat(document.getElementById('eq_Fcustom').value);
  const Q_W = C1*F*Math.pow(A_wetted,0.82); // Watts
  const Q_kW = Q_W/1000;
  const latent = parseFloat(document.getElementById('f_latent').value);
  const W = (Q_kW*3600)/latent; // kg/hr
  const flowType = document.getElementById('f_flowtype').value;
  const fluidType = document.getElementById('f_fluidtype').value;
  let A;
  if(fluidType==='steam'){
    const Ksh = parseFloat(document.getElementById('f_Ksh').value);
    const Kn = parseFloat(document.getElementById('f_Kn').value);
    A = steamArea(W,P1,c.Kd_v,c.Kb,c.Kc,Ksh,Kn);
  } else if(flowType==='critical'){
    A = gasCriticalArea(W,P1,Tk,c.Z,c.M,c.k,c.Kd_v,c.Kb,c.Kc);
  } else {
    A = gasSubcriticalArea(W,P1,P2,Tk,c.Z,c.M,c.k,c.Kd_v,c.Kc);
  }
  document.getElementById('f_Q_out').textContent = Q_kW.toFixed(2);
  document.getElementById('f_W_out').textContent = W.toFixed(1);
  document.getElementById('f_A_out').textContent = A.toFixed(1);
  results.fire = {basis:`Fire, F=${F}, A_wetted=${A_wetted.toFixed(2)} m², ${op}% OP`, load:W.toFixed(1)+" kg/hr", area:A};
  updateSummary();
  return A;
}

function calcBlocked(){
  const c = commonInputs();
  const P1 = P_abs_kPa(c.setP*(1+c.op/100), c.atm);
  const P2 = P_abs_kPa(c.bp, c.atm);
  const Tk = T_K(c.T);
  const W = parseFloat(document.getElementById('b_W').value);
  const fluidType = document.getElementById('b_fluidtype').value;
  const flowType = document.getElementById('b_flowtype').value;
  let A;
  if(fluidType==='steam'){
    const Ksh = parseFloat(document.getElementById('b_Ksh').value);
    const Kn = parseFloat(document.getElementById('b_Kn').value);
    A = steamArea(W,P1,c.Kd_v,c.Kb,c.Kc,Ksh,Kn);
  } else if(flowType==='critical'){
    A = gasCriticalArea(W,P1,Tk,c.Z,c.M,c.k,c.Kd_v,c.Kb,c.Kc);
  } else {
    A = gasSubcriticalArea(W,P1,P2,Tk,c.Z,c.M,c.k,c.Kd_v,c.Kc);
  }
  document.getElementById('b_A_out').textContent = A.toFixed(1);
  results.blocked = {basis:`Blocked outlet / CV fail, ${fluidType}, ${flowType}`, load:W+" kg/hr", area:A};
  updateSummary();
  return A;
}

// ---------- Case 3 helpers: beta quick-pick and solar heat-input estimator ----------
function applyBetaPick(){
  const v = document.getElementById('t_beta_pick').value;
  if(v) document.getElementById('t_beta').value = v;
}
function toggleHMethod(){
  const m = document.getElementById('t_Hmethod').value;
  document.getElementById('t_solar_fields').style.display = (m==='solar')?'grid':'none';
}
function applySolarH(){
  const A = parseFloat(document.getElementById('t_solarA').value)||0;
  const flux = parseFloat(document.getElementById('t_solarFluxCustom').value)||0;
  const H = A*flux; // kW
  document.getElementById('t_H').value = H.toFixed(3);
}

function calcThermal(){
  const c = commonInputs();
  const beta = parseFloat(document.getElementById('t_beta').value);
  const H = parseFloat(document.getElementById('t_H').value); // kW
  const rho = parseFloat(document.getElementById('t_rho').value);
  const cp = parseFloat(document.getElementById('t_cp').value);
  const Q = (beta*H*3600)/(rho*cp); // m3/hr  [H in kW=kJ/s -> kJ/hr = H*3600]
  const P1 = c.setP*(1+c.op/100)+c.atm; // kg/cm2a
  const dP_kgcm2 = Math.max(P1 - (c.bp+c.atm), 0.1);
  const dP_kPa = dP_kgcm2*98.0665;
  const A = liquidArea(Q, c.G, dP_kPa, c.Kd_l, c.Kw, c.Kc, c.Kv);
  document.getElementById('t_Q_out').textContent = Q.toFixed(4);
  document.getElementById('t_A_out').textContent = A.toFixed(1);
  results.thermal = {basis:"Liquid thermal expansion", load:Q.toFixed(4)+" m³/hr", area:A};
  updateSummary();
  return A;
}

function calcTube(){
  const c = commonInputs();
  const phase = document.getElementById('r_phase').value;
  const id_mm = parseFloat(document.getElementById('r_id').value);
  const Phs = parseFloat(document.getElementById('r_Phs').value);
  const Pls = parseFloat(document.getElementById('r_Pls').value);
  const tubeArea_mm2 = Math.PI*Math.pow(id_mm,2)/4;
  const flowArea_mm2 = 2*tubeArea_mm2; // rule of thumb: 2x single tube bore area
  const dP_kgcm2 = Math.max(Phs-Pls, 0.1);
  const dP_kPa = dP_kgcm2*98.0665;
  let W;
  if(phase==='liquid'){
    const rho = parseFloat(document.getElementById('r_rho').value);
    // W = Kd * A * sqrt(2*rho*dP) ; A in m2, dP in Pa, W in kg/s
    const A_m2 = flowArea_mm2/1e6;
    const W_kgs = c.Kd_l*A_m2*Math.sqrt(2*rho*dP_kPa*1000);
    W = W_kgs*3600;
  } else {
    // Choked gas flow through the rupture orifice itself (nozzle equation), then that W is the relief load
    const P1_abs_kPa = (Phs+c.atm)*98.0665;
    const Tk = T_K(c.T);
    const Cc = 0.03948*Math.sqrt(c.k*Math.pow(2/(c.k+1),(c.k+1)/(c.k-1)));
    // invert critical area formula to get W from a given A
    const A_mm2 = flowArea_mm2;
    W = A_mm2*Cc*1.0*P1_abs_kPa*1.0*1.0/Math.sqrt(Tk*c.Z/c.M);
  }
  const P1r = P_abs_kPa(c.setP*(1+c.op/100), c.atm);
  const Tk = T_K(c.T);
  let A;
  if(phase==='liquid'){
    const P1_kgcm2a = c.setP*(1+c.op/100)+c.atm;
    const dP2_kPa = Math.max(P1_kgcm2a-(c.bp+c.atm),0.1)*98.0665;
    // convert W (kg/hr) to Q (m3/hr) using HP-side liquid density for the PSV liquid sizing equation
    const rho = parseFloat(document.getElementById('r_rho').value);
    const Qm3h = W/rho;
    A = liquidArea(Qm3h, c.G, dP2_kPa, c.Kd_l, c.Kw, c.Kc, c.Kv);
  } else {
    A = gasCriticalArea(W,P1r,Tk,c.Z,c.M,c.k,c.Kd_v,c.Kb,c.Kc);
  }
  document.getElementById('r_W_out').textContent = W.toFixed(1);
  document.getElementById('r_A_out').textContent = A.toFixed(1);
  results.tube = {basis:`Tube rupture (${phase}), 2x tube bore=${flowArea_mm2.toFixed(1)} mm²`, load:W.toFixed(1)+" kg/hr", area:A};
  updateSummary();
  return A;
}

function calcLiquid(){
  const c = commonInputs();
  const Q = parseFloat(document.getElementById('l_Q').value);
  const P1 = c.setP*(1+c.op/100)+c.atm;
  const dP_kPa = Math.max(P1-(c.bp+c.atm),0.1)*98.0665;
  const A = liquidArea(Q,c.G,dP_kPa,c.Kd_l,c.Kw,c.Kc,c.Kv);
  document.getElementById('l_A_out').textContent = A.toFixed(1);
  results.liquid = {basis:"Blocked outlet / overfill (liquid)", load:Q+" m³/hr", area:A};
  updateSummary();
  return A;
}

// ---------- Master calculate + summary ----------
const CASE_DUTY = {fire:"gas steam", blocked:"gas steam", thermal:"liquid", tube:"gas liquid", liquid:"liquid"};
const CASE_LABELS = {fire:"1. External Fire", blocked:"2. Blocked Outlet / CV Fail", thermal:"3. Liquid Thermal Expansion", tube:"4. Exchanger Tube Rupture", liquid:"5. Blocked Outlet (Liquid)"};

function updateSummary(){
  let maxArea=-1, maxKey=null;
  const rows=[];
  for(const key of ["fire","blocked","thermal","tube","liquid"]){
    if(!CASE_DUTY[key].split(' ').includes(currentDuty)) continue; // only cases applicable to selected PSV duty
    const r = results[key];
    if(!r) continue;
    const o = selectOrifice(r.area);
    rows.push({key, label:CASE_LABELS[key], basis:r.basis, load:r.load, area:r.area, orifice:o});
    if(r.area>maxArea){ maxArea=r.area; maxKey=key; }
  }
  const tbody = document.getElementById('summary_body');
  if(rows.length===0){
    tbody.innerHTML = '<tr><td colspan="6" style="text-align:center;color:var(--grey);">No cases calculated yet for the selected PSV duty — use the Calculate buttons in Section 3, or "Calculate All Cases" above.</td></tr>';
    document.getElementById('gov_case_out').textContent = '—';
    return;
  }
  tbody.innerHTML = rows.map(r=>{
    const govClass = (r.key===maxKey)?'gov':'';
    return `<tr class="${govClass}"><td>${r.label}${r.key===maxKey?' <span class="badge">GOVERNING</span>':''}</td><td>${r.basis}</td><td>${r.load}</td><td>${r.area.toFixed(1)}</td><td>${r.orifice.letter}</td><td>${(r.orifice.mm2||0).toFixed?r.orifice.mm2.toFixed(1):r.orifice.mm2}</td></tr>`;
  }).join('');

  const govRow = rows.find(r=>r.key===maxKey);
  if(govRow){
    document.getElementById('gov_case_out').textContent =
      `${govRow.label} — Required Area ${govRow.area.toFixed(1)} mm² → Select Orifice "${govRow.orifice.letter}" (${govRow.orifice.mm2.toFixed ? govRow.orifice.mm2.toFixed(1):govRow.orifice.mm2} mm²), Flange: ${govRow.orifice.flange}`;
  }
}

function calculateAll(){
  computeArea();
  calcFire();
  calcBlocked();
  calcThermal();
  calcTube();
  calcLiquid();
  updateSummary();
}
addEquipRow();
computeArea();
setDuty('gas');

// ---------- Print: show only the panels relevant to the selected PSV duty (kept consistent with the summary table) ----------
window.addEventListener('beforeprint', function(){
  document.querySelectorAll('.tabpanel').forEach(p=>{
    const key = p.id.replace('tab_','');
    const applicable = (CASE_DUTY[key]||'').split(' ').includes(currentDuty);
    p.classList.toggle('print-show', applicable);
  });
});
window.addEventListener('afterprint', function(){
  document.querySelectorAll('.tabpanel').forEach(p=>p.classList.remove('print-show'));
});
</script>

</body>
</html>
