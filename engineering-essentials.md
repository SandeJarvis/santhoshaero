---
layout: default
title: Engineering Essentials — Aerodynamics with Santhosh
---

<!-- ============================================================
 Engineering Essentials
 Author: Santhosh
 Purpose: Reference hub for basic engineering & fluid data
 ============================================================ -->

<!-- ===== MathJax for scientific equations ===== -->
<script>
window.MathJax = { tex: { inlineMath:[["$","$"],["\\(","\\)"]], displayMath:[["$$","$$"],["\\[","\\]"]] } };
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

<!-- ============================================================
 1. FLUID PROPERTIES EXPLORER
 ============================================================ -->
<div class="card">
  <div class="pill">Fluid Properties Explorer</div>
  <h2>Basic Thermophysical Properties</h2>
  <p>Select a fluid and specify conditions to estimate its properties.</p>

  <div style="display:flex;flex-wrap:wrap;gap:1rem;margin-top:1rem;">
    <div>
      <label><strong>Fluid</strong></label><br>
      <select id="fluidSelect" style="padding:.4rem;border-radius:8px;">
        <option value="air">Air</option>
        <option value="water">Water</option>
        <option value="argon">Argon</option>
        <option value="nitrogen">Nitrogen</option>
        <option value="oxygen">Oxygen</option>
      </select>
    </div>
    <div>
      <label><strong>Temperature [°C]</strong></label><br>
      <input id="tempInput" type="number" value="15" step="0.1" style="width:100px;padding:.4rem;border-radius:8px;">
    </div>
    <div>
      <label><strong>Altitude [m]</strong></label><br>
      <input id="altInput" type="number" value="0" step="1" style="width:100px;padding:.4rem;border-radius:8px;">
    </div>
    <div style="align-self:end;">
      <button id="calcFluid" style="padding:.45rem 1rem;border-radius:8px;border:0;background:var(--brand);color:#fff;cursor:pointer;">Calculate</button>
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
  <details open>
    <summary><strong>Temperature</strong></summary>
    <p>$T(K)=T(°C)+273.15$  $T(°F)=1.8T(°C)+32$</p>
  </details>
  <details>
    <summary><strong>Length</strong></summary>
    <p>1 m = 1000 mm = 39.37 in = 3.281 ft</p>
  </details>
  <details>
    <summary><strong>Pressure</strong></summary>
    <p>1 atm = 101325 Pa = 1.01325 bar = 14.696 psi</p>
  </details>
  <details>
    <summary><strong>Velocity</strong></summary>
    <p>1 m/s = 3.6 km/h = 2.237 mph</p>
  </details>
</div>

<!-- ============================================================
 3. GEOMETRIC UTILITIES
 ============================================================ -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Geometric Utilities</div>
  <h2>Hydraulic Diameter</h2>
  <p>$$D_h = \\frac{4A}{P}$$</p>
  <div style="display:flex;gap:1rem;flex-wrap:wrap;">
    <div>
      <label>Area A [m²]</label><br>
      <input id="areaInput" type="number" step="any" value="0.01" style="width:120px;padding:.4rem;border-radius:8px;">
    </div>
    <div>
      <label>Perimeter P [m]</label><br>
      <input id="periInput" type="number" step="any" value="0.4" style="width:120px;padding:.4rem;border-radius:8px;">
    </div>
    <div style="align-self:end;">
      <button id="calcDh" style="padding:.45rem 1rem;border-radius:8px;border:0;background:var(--brand);color:#fff;cursor:pointer;">Compute</button>
    </div>
  </div>
  <p id="dhResult" style="margin-top:1rem;"></p>
</div>

<!-- ============================================================
 4. STANDARD ATMOSPHERE (ISA)
 ============================================================ -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Standard Atmosphere (ISA)</div>
  <h2>Troposphere Model (0–11 km)</h2>
  <p>$$T=T_0-Lh,\\quad p=p_0\\left(\\frac{T}{T_0}\\right)^{\\frac{gM}{RL}},\\quad \\rho=\\frac{p}{RT}$$</p>
  <div style="display:flex;gap:1rem;flex-wrap:wrap;">
    <div>
      <label>Altitude h [m]</label><br>
      <input id="altISA" type="number" value="0" step="10" style="width:120px;padding:.4rem;border-radius:8px;">
    </div>
    <div style="align-self:end;">
      <button id="calcISA" style="padding:.45rem 1rem;border-radius:8px;border:0;background:var(--brand);color:#fff;cursor:pointer;">Compute</button>
    </div>
  </div>
  <p id="isaResult" style="margin-top:1rem;"></p>
</div>

<!-- ============================================================
 5. MASS FLOW ↔ SLM CONVERTER
 ============================================================ -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Mass Flow ↔ SLM Converter</div>
  <h2>Convert volumetric flow at standard conditions</h2>

  <div style="display:flex;flex-wrap:wrap;gap:1rem;">
    <div>
      <label>Fluid</label><br>
      <select id="fluidSLM" style="padding:.4rem;border-radius:8px;">
        <option value="air">Air</option>
        <option value="argon">Argon</option>
        <option value="nitrogen">Nitrogen</option>
        <option value="oxygen">Oxygen</option>
      </select>
    </div>
    <div>
      <label>Temperature [°C]</label><br>
      <input id="tempSLM" type="number" value="20" step="0.1" style="width:100px;padding:.4rem;border-radius:8px;">
    </div>
    <div>
      <label>Mass flow (kg/s)</label><br>
      <input id="mflow" type="number" value="0.001" step="any" style="width:120px;padding:.4rem;border-radius:8px;">
    </div>
    <div style="align-self:end;">
      <button id="calcSLM" style="padding:.45rem 1rem;border-radius:8px;border:0;background:var(--brand);color:#fff;cursor:pointer;">Convert</button>
    </div>
  </div>
  <p id="slmResult" style="margin-top:1rem;"></p>
</div>

<!-- ============================================================
 6. CONSTANTS TABLE
 ============================================================ -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Key Constants</div>
  <table style="width:100%;border-collapse:collapse;">
    <tr><th style="text-align:left;">Symbol</th><th>Name</th><th>Value</th><th>Units</th></tr>
    <tr><td>R</td><td>Universal gas constant</td><td>8.314</td><td>J mol⁻¹ K⁻¹</td></tr>
    <tr><td>g</td><td>Acceleration due to gravity</td><td>9.80665</td><td>m s⁻²</td></tr>
    <tr><td>p₀</td><td>Standard pressure</td><td>101325</td><td>Pa</td></tr>
    <tr><td>T₀</td><td>Standard temperature</td><td>288.15</td><td>K</td></tr>
    <tr><td>γ</td><td>Specific heat ratio (Air)</td><td>1.4</td><td>–</td></tr>
  </table>
</div>

<!-- ============================================================
 JAVASCRIPT LOGIC
 ============================================================ -->
<script>
// ---------- 1. Fluid property approximations (very simplified ideal-gas + fixed data) ----------
const fluidData = {
  air:{R:287, gamma:1.4, mu:1.8e-5, Cp:1005, k:0.026},
  water:{R:461.5, gamma:1.0, mu:1.0e-3, Cp:4180, k:0.6},
  argon:{R:208, gamma:1.67, mu:2.2e-5, Cp:520, k:0.017},
  nitrogen:{R:296.8, gamma:1.4, mu:1.76e-5, Cp:1040, k:0.026},
  oxygen:{R:259.8, gamma:1.4, mu:2.0e-5, Cp:918, k:0.024}
};
document.getElementById('calcFluid').onclick = ()=>{
  const f = document.getElementById('fluidSelect').value;
  const T = parseFloat(document.getElementById('tempInput').value)+273.15;
  const h = parseFloat(document.getElementById('altInput').value);
  const p0=101325, T0=288.15, L=0.0065, g=9.80665;
  const p = f==='air'||f==='argon'||f==='nitrogen'||f==='oxygen' ? p0*Math.pow(1-L*h/T0,5.256) : p0;
  const R=fluidData[f].R, gamma=fluidData[f].gamma;
  const rho=p/(R*T);
  const a=Math.sqrt(gamma*R*T);
  const mu=fluidData[f].mu, Cp=fluidData[f].Cp, k=fluidData[f].k;
  document.getElementById('fluidResults').innerHTML=
  `<table style="width:100%;border-collapse:collapse;">
    <tr><th>Property</th><th>Symbol</th><th>Value</th><th>Units</th></tr>
    <tr><td>Density</td><td>ρ</td><td>${rho.toFixed(3)}</td><td>kg/m³</td></tr>
    <tr><td>Dynamic viscosity</td><td>μ</td><td>${mu.toExponential(3)}</td><td>Pa·s</td></tr>
    <tr><td>Speed of sound</td><td>a</td><td>${a.toFixed(1)}</td><td>m/s</td></tr>
    <tr><td>Specific heat</td><td>Cₚ</td><td>${Cp}</td><td>J/kg·K</td></tr>
    <tr><td>Thermal conductivity</td><td>k</td><td>${k}</td><td>W/m·K</td></tr>
  </table>`;
};

// ---------- 2. Hydraulic diameter ----------
document.getElementById('calcDh').onclick=()=>{
  const A=parseFloat(document.getElementById('areaInput').value);
  const P=parseFloat(document.getElementById('periInput').value);
  if(A>0 && P>0){
    const Dh=4*A/P;
    document.getElementById('dhResult').innerHTML=`Hydraulic diameter D<sub>h</sub> = <strong>${Dh.toFixed(4)}</strong> m`;
  }
};

// ---------- 3. ISA model ----------
document.getElementById('calcISA').onclick=()=>{
  const h=parseFloat(document.getElementById('altISA').value);
  const T0=288.15,p0=101325,L=0.0065,R=287,g=9.80665;
  const T=T0-L*h;
  const p=p0*Math.pow(T/T0,g/(R*L/1000));  // simplified exponent
  const rho=p/(R*T);
  document.getElementById('isaResult').innerHTML=
  `T = <strong>${T.toFixed(2)}</strong> K,  p = <strong>${p.toFixed(0)}</strong> Pa,  ρ = <strong>${rho.toFixed(3)}</strong> kg/m³`;
};

// ---------- 4. Mass flow ↔ SLM ----------
const refDensity={air:1.204,argon:1.633,nitrogen:1.165,oxygen:1.331};
document.getElementById('calcSLM').onclick=()=>{
  const f=document.getElementById('fluidSLM').value;
  const T=parseFloat(document.getElementById('tempSLM').value)+273.15;
  const rhoRef=refDensity[f];
  const mDot=parseFloat(document.getElementById('mflow').value);
  const SLM=(mDot*60)/rhoRef;
  document.getElementById('slmResult').innerHTML=
  `At ${(T-273.15).toFixed(1)} °C, ${f.charAt(0).toUpperCase()+f.slice(1)}: SLM = <strong>${SLM.toFixed(2)}</strong> L/min`;
};
</script>

