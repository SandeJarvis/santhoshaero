---
layout: default
title: Engineering Essentials — Aerodynamics with Santhosh
---

<!-- ============================================================
 ENGINEERING ESSENTIALS — INTERACTIVE HUB
 Author: Santhosh
 ============================================================ -->

<!-- ===== Load MathJax for equations ===== -->
<script>
window.MathJax = {
  tex: {inlineMath:[["$","$"],["\\(","\\)"]], displayMath:[["$$","$$"],["\\[","\\]"]]},
  options:{renderActions:{addMenu:[0,"",null]}}
};
</script>
<script async id="MathJax-script" src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

<style>
  .input-group {display:flex;flex-wrap:wrap;gap:1rem;margin-top:.6rem;}
  .input-box {padding:.4rem;border-radius:8px;border:1px solid var(--ring);}
  table{width:100%;border-collapse:collapse;margin-top:.5rem;}
  th,td{padding:.35rem;text-align:left;}
  th{background:#f0f4fa;}
  summary{cursor:pointer;padding:.4rem 0;font-weight:600;}
  details{margin-top:.4rem;}
</style>

<!-- ============================================================
 1. FLUID PROPERTIES EXPLORER
 ============================================================ -->
<div class="card">
  <div class="pill">Fluid Properties Explorer</div>
  <h2>Basic Thermophysical Properties</h2>
  <p>Select a fluid and specify conditions to estimate its properties.<br>
  <em>For ideal gases, density and speed of sound depend on local temperature and pressure.</em></p>

  <div class="input-group">
    <div>
      <label><strong>Fluid</strong></label><br>
      <select id="fluidSelect" class="input-box">
        <option value="air">Air</option>
        <option value="water">Water</option>
        <option value="argon">Argon</option>
        <option value="nitrogen">Nitrogen</option>
        <option value="oxygen">Oxygen</option>
      </select>
    </div>
    <div>
      <label><strong>Temperature</strong></label><br>
      <input id="tempInput" type="number" value="15" step="0.1" class="input-box" style="width:100px;">
      <select id="tempUnit" class="input-box">
        <option value="C">°C</option>
        <option value="K">K</option>
      </select>
    </div>
    <div>
      <label><strong>Altitude [m]</strong></label><br>
      <input id="altInput" type="number" value="0" step="1" class="input-box" style="width:100px;">
    </div>
    <div style="align-self:end;">
      <button id="calcFluid" style="padding:.45rem 1rem;border-radius:8px;border:0;background:var(--brand);color:#fff;">Calculate</button>
    </div>
  </div>

  <div id="fluidResults" style="margin-top:1rem;"></div>
  <div style="text-align:center;margin-top:1rem;">
    $$\\rho = \\frac{p}{RT}, \\qquad a = \\sqrt{\\gamma RT}$$
  </div>
</div>

<!-- ============================================================
 2. UNIT CONVERSIONS
 ============================================================ -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Unit Conversions</div>
  <h2>Common Engineering Conversions</h2>

  <!-- Temperature -->
  <details open>
    <summary>Temperature</summary>
    <div class="input-group">
      <input id="tempConvIn" type="number" value="25" class="input-box" style="width:120px;">
      <select id="tempConvFrom" class="input-box">
        <option>°C</option><option>K</option><option>°F</option>
      </select>
      <span>→</span>
      <select id="tempConvTo" class="input-box">
        <option>K</option><option>°C</option><option>°F</option>
      </select>
      <button id="convTemp" style="padding:.4rem 1rem;background:var(--brand);color:#fff;border:0;border-radius:8px;">Convert</button>
    </div>
    <p id="tempConvOut"></p>
  </details>

  <!-- Length -->
  <details>
    <summary>Length</summary>
    <div class="input-group">
      <input id="lenIn" type="number" value="1" class="input-box" style="width:120px;">
      <select id="lenFrom" class="input-box">
        <option>m</option><option>mm</option><option>cm</option><option>in</option><option>ft</option><option>km</option>
      </select>
      <span>→</span>
      <select id="lenTo" class="input-box">
        <option>mm</option><option>cm</option><option>in</option><option>ft</option><option>m</option><option>km</option>
      </select>
      <button id="convLen" style="padding:.4rem 1rem;background:var(--brand);color:#fff;border:0;border-radius:8px;">Convert</button>
    </div>
    <p id="lenOut"></p>
  </details>

  <!-- Pressure -->
  <details>
    <summary>Pressure</summary>
    <div class="input-group">
      <input id="pressIn" type="number" value="1" class="input-box" style="width:120px;">
      <select id="pressFrom" class="input-box">
        <option>Pa</option><option>kPa</option><option>bar</option><option>atm</option><option>psi</option>
      </select>
      <span>→</span>
      <select id="pressTo" class="input-box">
        <option>kPa</option><option>bar</option><option>atm</option><option>psi</option><option>Pa</option>
      </select>
      <button id="convPress" style="padding:.4rem 1rem;background:var(--brand);color:#fff;border:0;border-radius:8px;">Convert</button>
    </div>
    <p id="pressOut"></p>
  </details>

  <!-- Velocity -->
  <details>
    <summary>Velocity</summary>
    <div class="input-group">
      <input id="velIn" type="number" value="10" class="input-box" style="width:120px;">
      <select id="velFrom" class="input-box">
        <option>m/s</option><option>km/h</option><option>mph</option>
      </select>
      <span>→</span>
      <select id="velTo" class="input-box">
        <option>km/h</option><option>mph</option><option>m/s</option>
      </select>
      <button id="convVel" style="padding:.4rem 1rem;background:var(--brand);color:#fff;border:0;border-radius:8px;">Convert</button>
    </div>
    <p id="velOut"></p>
  </details>
</div>

<!-- ============================================================
 3. GEOMETRIC UTILITIES
 ============================================================ -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Geometric Utilities</div>
  <h2>Cross-Sectional Shapes & Hydraulic Diameter</h2>
  <p>Choose a geometry and input parameters to compute area, perimeter, and $D_h = \\frac{4A}{P}$</p>

  <div class="input-group">
    <div>
      <label>Shape</label><br>
      <select id="shapeSelect" class="input-box">
        <option>Circle</option>
        <option>Rectangle</option>
        <option>Square</option>
        <option>Semi-circle</option>
        <option>Annulus</option>
        <option>Custom (A,P)</option>
      </select>
    </div>
    <div style="align-self:end;">
      <button id="calcGeo" style="padding:.45rem 1rem;border-radius:8px;border:0;background:var(--brand);color:#fff;">Compute</button>
    </div>
  </div>
  <div id="geoInputs" style="margin-top:1rem;"></div>
  <div id="geoResults" style="margin-top:1rem;"></div>
</div>

<!-- ============================================================
 4. STANDARD ATMOSPHERE (ISA)
 ============================================================ -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Standard Atmosphere (ISA)</div>
  <h2>Troposphere Model (0–11 km)</h2>
  <p>$$T=T_0-Lh,\\quad p=p_0\\left(\\frac{T}{T_0}\\right)^{\\frac{gM}{RL}},\\quad \\rho=\\frac{p}{RT}$$</p>

  <div class="input-group">
    <div>
      <label>Altitude h [m]</label><br>
      <input id="altISA" type="number" value="0" class="input-box" style="width:120px;">
    </div>
    <div style="align-self:end;">
      <button id="calcISA" style="padding:.45rem 1rem;border-radius:8px;border:0;background:var(--brand);color:#fff;">Compute</button>
    </div>
  </div>
  <p id="isaResult" style="margin-top:1rem;"></p>
</div>

<!-- ============================================================
 5. MASS FLOW ↔ SLM ↔ VOLUMETRIC FLOW
 ============================================================ -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Flow Rate Converter</div>
  <h2>Mass Flow ↔ SLM ↔ Volumetric Flow</h2>
  <p>1 SLM = 1 L/min at standard conditions (ρ ≈ 1.204 kg/m³ for air at 20 °C).</p>

  <div class="input-group">
    <select id="fluidSLM" class="input-box">
      <option value="air">Air</option>
      <option value="argon">Argon</option>
      <option value="nitrogen">Nitrogen</option>
      <option value="oxygen">Oxygen</option>
    </select>
    <input id="tempSLM" type="number" value="20" class="input-box" style="width:100px;">
    <span>°C</span>
    <input id="flowVal" type="number" value="1" class="input-box" style="width:100px;">
    <select id="flowType" class="input-box">
      <option value="mDot">Mass flow [kg/s]</option>
      <option value="Q">Volumetric flow [m³/s]</option>
      <option value="SLM">SLM [L/min]</option>
    </select>
    <div style="align-self:end;">
      <button id="calcFlow" style="padding:.45rem 1rem;border-radius:8px;border:0;background:var(--brand);color:#fff;">Convert</button>
    </div>
  </div>
  <p id="flowResult" style="margin-top:1rem;"></p>
</div>

<!-- ============================================================
 JAVASCRIPT FUNCTIONS
 ============================================================ -->
<script>
// ===== FLUID PROPERTIES =====
const fluids={air:{R:287,g:1.4,mu:1.8e-5,Cp:1005,k:0.026},
              water:{R:461.5,g:1.0,mu:1e-3,Cp:4180,k:0.6},
              argon:{R:208,g:1.67,mu:2.2e-5,Cp:520,k:0.017},
              nitrogen:{R:296.8,g:1.4,mu:1.76e-5,Cp:1040,k:0.026},
              oxygen:{R:259.8,g:1.4,mu:2e-5,Cp:918,k:0.024}};
document.getElementById("calcFluid").onclick=()=>{
  const f=document.getElementById("fluidSelect").value;
  const Tunit=document.getElementById("tempUnit").value;
  let T=parseFloat(document.getElementById("tempInput").value);
  if(Tunit==="C")T+=273.15;
  const h=parseFloat(document.getElementById("altInput").value);
  const T0=288.15,p0=101325,L=0.0065;
  const p=(f==="air"||f==="argon"||f==="nitrogen"||f==="oxygen")?p0*Math.pow(1-L*h/T0,5.256):p0;
  const R=fluids[f].R,gamma=fluids[f].g;
  const rho=p/(R*T),a=Math.sqrt(gamma*R*T);
  const mu=fluids[f].mu,Cp=fluids[f].Cp,k=fluids[f].k;
  document.getElementById("fluidResults").innerHTML=`
  <table><tr><th>Property</th><th>Symbol</th><th>Value</th><th>Units</th></tr>
  <tr><td>Density</td><td>ρ</td><td>${rho.toFixed(3)}</td><td>kg/m³</td></tr>
  <tr><td>Dynamic viscosity</td><td>μ</td><td>${mu.toExponential(3)}</td><td>Pa·s</td></tr>
  <tr><td>Speed of sound</td><td>a</td><td>${a.toFixed(2)}</td><td>m/s</td></tr>
  <tr><td>Specific heat</td><td>Cₚ</td><td>${Cp}</td><td>J/kg·K</td></tr>
  <tr><td>Thermal conductivity</td><td>k</td><td>${k}</td><td>W/m·K</td></tr></table>`;
};

// ===== UNIT CONVERSIONS =====
document.getElementById("convTemp").onclick=()=>{
  const val=parseFloat(tempConvIn.value),f=tempConvFrom.value,t=tempConvTo.value;
  let K=0;
  if(f==="°C")K=val+273.15;else if(f==="°F")K=(val-32)/1.8+273.15;else K=val;
  let out=K;
  if(t==="°C")out=K-273.15;else if(t==="°F")out=(K-273.15)*1.8+32;
  tempConvOut.textContent=`Result: ${out.toFixed(3)} ${t}`;
};

document.getElementById("convLen").onclick=()=>{
  const val=parseFloat(lenIn.value),f=lenFrom.value,t=lenTo.value;
  const mTable={mm:0.001,cm:0.01,in:0.0254,ft:0.3048,km:1000,m:1};
  const m=val*mTable[f]/mTable[t];
  lenOut.textContent=`${val} ${f} = ${m.toFixed(4)} ${t}`;
};

document.getElementById("convPress").onclick=()=>{
  const val=parseFloat(pressIn.value),f=pressFrom.value,t=pressTo.value;
  const Pa={Pa:1,kPa:1e3,bar:1e5,atm:101325,psi:6894.76};
  const result=val*Pa[f]/Pa[t];
  pressOut.textContent=`${val} ${f} = ${result.toFixed(3)} ${t}`;
};

document.getElementById("convVel").onclick=()=>{
  const val=parseFloat(velIn.value),f=velFrom.value,t=velTo.value;
  const ms={ "m/s":1,"km/h":1/3.6,"mph":0.44704};
  const result=val*ms[f]/ms[t];
  velOut.textContent=`${val} ${f} = ${result.toFixed(3)} ${t}`;
};

// ===== GEOMETRIC UTILITIES =====
const geoDiv=document.getElementById("geoInputs");
document.getElementById("shapeSelect").onchange=()=>{
  const s=shapeSelect.value;
  let html="";
  if(s==="Circle")html=`<label>Diameter D [m]</label><input id="D" type="number" class="input-box" value="0.1">`;
  if(s==="Rectangle")html=`<label>a [m]</label><input id="a" class="input-box" value="0.1"><label>b [m]</label><input id="b" class="input-box" value="0.05">`;
  if(s==="Square")html=`<label>Side a [m]</label><input id="a" class="input-box" value="0.1">`;
  if(s==="Semi-circle")html=`<label>Diameter D [m]</label><input id="D" class="input-box" value="0.1">`;
  if(s==="Annulus")html=`<label>Outer Dₒ [m]</label><input id="Do" class="input-box" value="0.1"><label>Inner Dᵢ [m]</label><input id="Di" class="input-box" value="0.05">`;
  if(s==="Custom (A,P)")html=`<label>Area A [m²]</label><input id="A" class="input-box" value="0.01"><label>Perimeter P [m]</label><input id="P" class="input-box" value="0.4">`;
  geoDiv.innerHTML=html;
};
shapeSelect.onchange();

document.getElementById("calcGeo").onclick=()=>{
  const s=shapeSelect.value;
  let A=0,P=0;
  if(s==="Circle"){const D=parseFloat(D.value);A=Math.PI*(D**2)/4;P=Math.PI*D;}
  if(s==="Rectangle"){const a=parseFloat(a.value),b=parseFloat(b.value);A=a*b;P=2*(a+b);}
  if(s==="Square"){const a=parseFloat(a.value);A=a**2;P=4*a;}
  if(s==="Semi-circle"){const D=parseFloat(D.value);A=0.5*Math.PI*(D**2)/4;P=Math.PI*D/2+2*(D/2);}
  if(s==="Annulus"){const Do=parseFloat(Do.value),Di=parseFloat(Di.value);A=Math.PI*(Do**2-Di**2)/4;P=Math.PI*(Do+Di);}
  if(s==="Custom (A,P)"){A=parseFloat(A.value);P=parseFloat(P.value);}
  const Dh=4*A/P;
  geoResults.innerHTML=`A=${A.toExponential(3)} m², P=${P.toFixed(3)} m, Dₕ=${Dh.toFixed(4)} m`;
};

// ===== STANDARD ATMOSPHERE =====
document.getElementById("calcISA").onclick=()=>{
  const h=parseFloat(altISA.value);
  const T0=288.15,p0=101325,L=0.0065,R=287,g=9.80665,M=0.0289644;
  const T=T0-L*h;
  const p=p0*Math.pow(T/T0,g*M/(R*L));
  const rho=p/(R*T);
  isaResult.innerHTML=`T = ${T.toFixed(2)} K (${(T-273.15).toFixed(2)} °C), p = ${p.toFixed(1)} Pa, ρ = ${rho.toFixed(3)} kg/m³`;
};

// ===== MASS FLOW / SLM / VOLUMETRIC =====
const refRho={air:1.204,argon:1.633,nitrogen:1.165,oxygen:1.331};
document.getElementById("calcFlow").onclick=()=>{
  const f=fluidSLM.value;
  const rho=refRho[f];
  const val=parseFloat(flowVal.value);
  const type=flowType.value;
  let mDot=0,Q=0,SLM=0;
  if(type==="mDot"){mDot=val;Q=mDot/rho;SLM=Q*60000;}
  if(type==="Q"){Q=val;mDot=rho*Q;SLM=Q*60000;}
  if(type==="SLM"){SLM=val;Q=SLM/60000;mDot=rho*Q;}
  flowResult.innerHTML=`Mass flow: ${mDot.toExponential(3)} kg/s, Volumetric: ${Q.toExponential(3)} m³/s, SLM: ${SLM.toFixed(2)} L/min`;
};
</script>
