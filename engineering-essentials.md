---
layout: default
title: Engineering Essentials — Aerodynamics with Santhosh
---

<!-- ENGINEERING ESSENTIALS — corrected and working -->
<script>
window.MathJax = {
  tex: { inlineMath:[['$','$'],['\\(','\\)']], displayMath:[['$$','$$'],['\\[','\\]']] },
  svg: { fontCache: 'global' }
};
</script>
<script async id="MathJax-script" src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js"></script>

<style>
  .input-group {display:flex;flex-wrap:wrap;gap:1rem;margin-top:.6rem;}
  .input-box {padding:.4rem;border-radius:8px;border:1px solid var(--ring);}
  table{width:100%;border-collapse:collapse;margin-top:.5rem;}
  th,td{padding:.35rem;text-align:left;}
  th{background:#f0f4fa;}
  details{margin-top:.4rem;}
  .formula { text-align:center; margin-top:1rem; font-size:1.05rem;}
</style>

<!-- 1. Fluid Properties Explorer -->
<div class="card">
  <div class="pill">Fluid Properties Explorer</div>
  <h2>Basic Thermophysical Properties</h2>
  <p>Select a fluid and specify conditions. Short note: density and sound speed follow ideal-gas relations for gases.</p>

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

  <div class="formula">
    $$\rho = \dfrac{p}{R\,T},\qquad a=\sqrt{\gamma R T}$$
  </div>
</div>

<!-- 2. Unit Conversions -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Unit Conversions</div>
  <h2>Bidirectional converters</h2>

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
      <button id="convTemp" class="input-box" style="background:var(--brand);color:#fff;border:0;">Convert</button>
    </div>
    <p id="tempConvOut"></p>
  </details>

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
      <button id="convLen" class="input-box" style="background:var(--brand);color:#fff;border:0;">Convert</button>
    </div>
    <p id="lenOut"></p>
  </details>

  <details>
    <summary>Pressure</summary>
    <div class="input-group">
      <input id="pressIn" type="number" value="101325" class="input-box" style="width:140px;">
      <select id="pressFrom" class="input-box">
        <option>Pa</option><option>kPa</option><option>bar</option><option>atm</option><option>psi</option>
      </select>
      <span>→</span>
      <select id="pressTo" class="input-box">
        <option>kPa</option><option>bar</option><option>atm</option><option>psi</option><option>Pa</option>
      </select>
      <button id="convPress" class="input-box" style="background:var(--brand);color:#fff;border:0;">Convert</button>
    </div>
    <p id="pressOut"></p>
  </details>

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
      <button id="convVel" class="input-box" style="background:var(--brand);color:#fff;border:0;">Convert</button>
    </div>
    <p id="velOut"></p>
  </details>
</div>

<!-- 3. Geometric Utilities -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Geometric Utilities</div>
  <h2>Shapes & Hydraulic Diameter</h2>
  <p>Compute area, perimeter and hydraulic diameter $D_h = \dfrac{4A}{P}$. Choose shape and provide dimensions.</p>

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
      <button id="calcGeo" class="input-box" style="background:var(--brand);color:#fff;border:0;">Compute</button>
    </div>
  </div>

  <div id="geoInputs" style="margin-top:1rem;"></div>
  <div id="geoResults" style="margin-top:1rem;"></div>
</div>

<!-- 4. ISA -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Standard Atmosphere (ISA)</div>
  <h2>Troposphere (0–11 km)</h2>
  <div class="input-group">
    <div>
      <label>Altitude h [m]</label><br>
      <input id="altISA" type="number" value="0" class="input-box" style="width:120px;">
    </div>
    <div style="align-self:end;">
      <button id="calcISA" class="input-box" style="background:var(--brand);color:#fff;border:0;">Compute</button>
    </div>
  </div>
  <div id="isaResult" style="margin-top:1rem;"></div>
</div>

<!-- 5. Flow Rate Converter -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Flow Rate Converter</div>
  <h2>Mass ↔ Volumetric ↔ SLM</h2>

  <div class="input-group">
    <select id="fluidSLM" class="input-box">
      <option value="air">Air</option>
      <option value="argon">Argon</option>
      <option value="nitrogen">Nitrogen</option>
      <option value="oxygen">Oxygen</option>
    </select>
    <div>
      <label>Temperature</label><br>
      <input id="tempSLM" type="number" value="20" class="input-box" style="width:100px;">
    </div>
    <div>
      <label>Value</label><br>
      <input id="flowVal" type="number" value="1" class="input-box" style="width:120px;">
    </div>
    <div>
      <label>Type</label><br>
      <select id="flowType" class="input-box">
        <option value="mDot">Mass flow [kg/s]</option>
        <option value="Q">Volumetric flow [m³/s]</option>
        <option value="SLM">SLM [L/min]</option>
      </select>
    </div>
    <div style="align-self:end;">
      <button id="calcFlow" class="input-box" style="background:var(--brand);color:#fff;border:0;">Convert</button>
    </div>
  </div>

  <div id="flowResult" style="margin-top:1rem;"></div>
</div>

<script>
document.addEventListener('DOMContentLoaded', function(){

  /* ---------- MathJax helper ---------- */
  function renderMath() {
    if(window.MathJax && MathJax.typesetPromise) return MathJax.typesetPromise();
    return Promise.resolve();
  }

  /* ---------- Fluid properties ---------- */
  const fluids = {
    air: {R:287.05, g:1.4, mu:1.8e-5, Cp:1005, k:0.026},
    water:{R:461.5,g:1.0,mu:1.0e-3,Cp:4180,k:0.6},
    argon:{R:208.1,g:1.667,mu:2.2e-5,Cp:520,k:0.017},
    nitrogen:{R:296.8,g:1.4,mu:1.76e-5,Cp:1040,k:0.026},
    oxygen:{R:259.8,g:1.4,mu:2.0e-5,Cp:918,k:0.024}
  };

  document.getElementById('calcFluid').addEventListener('click', function(){
    const f = document.getElementById('fluidSelect').value;
    let T = parseFloat(document.getElementById('tempInput').value);
    const Tunit = document.getElementById('tempUnit').value;
    if(Tunit === 'C') T = T + 273.15;
    const h = parseFloat(document.getElementById('altInput').value) || 0;

    // ISA pressure approx for gases (troposphere)
    const T0 = 288.15, p0 = 101325, L = 0.0065;
    let p = p0;
    if(['air','argon','nitrogen','oxygen'].includes(f)) {
      p = p0 * Math.pow(1 - (L * h / T0), 5.256);
    }

    const R = fluids[f].R, gamma = fluids[f].g;
    const rho = p / (R * T);
    const a = Math.sqrt(gamma * R * T);
    const mu = fluids[f].mu, Cp = fluids[f].Cp, k = fluids[f].k;

    const out = `
      <table>
        <tr><th>Property</th><th>Symbol</th><th>Value</th><th>Units</th></tr>
        <tr><td>Density</td><td>\\(\\rho\\)</td><td>${rho.toFixed(4)}</td><td>kg/m³</td></tr>
        <tr><td>Dynamic viscosity</td><td>\\(\\mu\\)</td><td>${mu.toExponential(3)}</td><td>Pa·s</td></tr>
        <tr><td>Speed of sound</td><td>\\(a\\)</td><td>${a.toFixed(2)}</td><td>m/s</td></tr>
        <tr><td>Specific heat</td><td>\\(C_p\\)</td><td>${Cp}</td><td>J/kg·K</td></tr>
        <tr><td>Thermal conductivity</td><td>\\(k\\)</td><td>${k}</td><td>W/m·K</td></tr>
      </table>
      <p style="margin-top:.5rem;"><em>Note:</em> for gases, pressure used is ISA-based at given altitude unless otherwise specified.</p>
    `;
    document.getElementById('fluidResults').innerHTML = out;
    renderMath();
  });

  /* ---------- Unit conversions ---------- */
  document.getElementById('convTemp').addEventListener('click', function(){
    const val = parseFloat(document.getElementById('tempConvIn').value);
    const f = document.getElementById('tempConvFrom').value;
    const t = document.getElementById('tempConvTo').value;
    let K = f === '°C' ? val + 273.15 : (f === '°F' ? (val - 32)/1.8 + 273.15 : val);
    let out = (t === '°C' ? (K - 273.15) : (t === '°F' ? (K - 273.15)*1.8 + 32 : K));
    document.getElementById('tempConvOut').textContent = `Result: ${out.toFixed(3)} ${t}`;
  });

  document.getElementById('convLen').addEventListener('click', function(){
    const val = parseFloat(document.getElementById('lenIn').value);
    const f = document.getElementById('lenFrom').value;
    const t = document.getElementById('lenTo').value;
    const table = {m:1, mm:0.001, cm:0.01, in:0.0254, ft:0.3048, km:1000};
    const inMeters = val * table[f];
    const out = inMeters / table[t];
    document.getElementById('lenOut').textContent = `${val} ${f} = ${out.toFixed(6)} ${t}`;
  });

  document.getElementById('convPress').addEventListener('click', function(){
    const val = parseFloat(document.getElementById('pressIn').value);
    const f = document.getElementById('pressFrom').value;
    const t = document.getElementById('pressTo').value;
    const Pa = {Pa:1, kPa:1e3, bar:1e5, atm:101325, psi:6894.757};
    const inPa = val * Pa[f];
    const out = inPa / Pa[t];
    document.getElementById('pressOut').textContent = `${val} ${f} = ${out.toFixed(6)} ${t}`;
  });

  document.getElementById('convVel').addEventListener('click', function(){
    const val = parseFloat(document.getElementById('velIn').value);
    const f = document.getElementById('velFrom').value;
    const t = document.getElementById('velTo').value;
    const ms = {'m/s':1, 'km/h':1/3.6, 'mph':0.44704};
    const inMs = val * ms[f];
    const out = inMs / ms[t];
    document.getElementById('velOut').textContent = `${val} ${f} = ${out.toFixed(4)} ${t}`;
  });

  /* ---------- Geometry inputs & compute ---------- */
  const geoInputs = document.getElementById('geoInputs');
  const geoResults = document.getElementById('geoResults');

  function buildGeoInputs(shape){
    let html = '';
    if(shape === 'Circle') {
      html = `<label>Diameter D [m]</label><br><input id="geo_D" class="input-box" type="number" value="0.1" step="any">`;
    } else if(shape === 'Rectangle') {
      html = `<label>a [m]</label><br><input id="geo_a" class="input-box" type="number" value="0.1" step="any"><label style="margin-left:.6rem">b [m]</label><br><input id="geo_b" class="input-box" type="number" value="0.05" step="any">`;
    } else if(shape === 'Square') {
      html = `<label>Side a [m]</label><br><input id="geo_a" class="input-box" type="number" value="0.1" step="any">`;
    } else if(shape === 'Semi-circle') {
      html = `<label>Diameter D [m]</label><br><input id="geo_D" class="input-box" type="number" value="0.1" step="any">`;
    } else if(shape === 'Annulus') {
      html = `<label>Outer Dₒ [m]</label><br><input id="geo_Do" class="input-box" type="number" value="0.1" step="any"><label style="margin-left:.6rem">Inner Dᵢ [m]</label><br><input id="geo_Di" class="input-box" type="number" value="0.05" step="any">`;
    } else {
      html = `<label>Area A [m²]</label><br><input id="geo_A" class="input-box" type="number" value="0.01" step="any"><label style="margin-left:.6rem">Perimeter P [m]</label><br><input id="geo_P" class="input-box" type="number" value="0.4" step="any">`;
    }
    geoInputs.innerHTML = html;
  }

  document.getElementById('shapeSelect').addEventListener('change', function(){
    buildGeoInputs(this.value);
  });
  buildGeoInputs(document.getElementById('shapeSelect').value);

  document.getElementById('calcGeo').addEventListener('click', function(){
    const shape = document.getElementById('shapeSelect').value;
    let A=0, P=0;
    try {
      if(shape === 'Circle') {
        const D = parseFloat(document.getElementById('geo_D').value);
        A = Math.PI*D*D/4; P = Math.PI*D;
      } else if(shape === 'Rectangle') {
        const a = parseFloat(document.getElementById('geo_a').value);
        const b = parseFloat(document.getElementById('geo_b').value);
        A = a*b; P = 2*(a+b);
      } else if(shape === 'Square') {
        const a = parseFloat(document.getElementById('geo_a').value);
        A = a*a; P = 4*a;
      } else if(shape === 'Semi-circle') {
        const D = parseFloat(document.getElementById('geo_D').value);
        A = 0.5*Math.PI*(D*D)/4; P = 0.5*Math.PI*D + 2*(D/2);
      } else if(shape === 'Annulus') {
        const Do = parseFloat(document.getElementById('geo_Do').value);
        const Di = parseFloat(document.getElementById('geo_Di').value);
        A = Math.PI*(Do*Do - Di*Di)/4;
        P = Math.PI*(Do + Di);
      } else {
        A = parseFloat(document.getElementById('geo_A').value);
        P = parseFloat(document.getElementById('geo_P').value);
      }

      if(!(A>0) || !(P>0)) throw new Error('A and P must be positive numbers');
      const Dh = 4*A / P;
      geoResults.innerHTML = `<p><strong>Area</strong>: ${A.toExponential(4)} m² &nbsp;&nbsp; <strong>Perimeter</strong>: ${P.toFixed(4)} m &nbsp;&nbsp; <strong>D_h</strong>: ${Dh.toFixed(4)} m</p>
        <p class="formula">$$D_h = \\dfrac{4A}{P}$$</p>`;
      renderMath();
    } catch(err){
      geoResults.innerHTML = `<p style="color:crimson">Error: ${err.message}</p>`;
    }
  });

  /* ---------- ISA ---------- */
  document.getElementById('calcISA').addEventListener('click', function(){
    const h = parseFloat(document.getElementById('altISA').value);
    const T0 = 288.15, p0 = 101325, L = 0.0065, R = 287.05, g = 9.80665, M = 0.0289644;
    const T = T0 - L * h;
    const exponent = (g * M) / (R * L);
    const p = p0 * Math.pow(T / T0, exponent);
    const rho = p / (R * T);
    document.getElementById('isaResult').innerHTML = `T = <strong>${T.toFixed(2)}</strong> K (${(T-273.15).toFixed(2)} °C) &nbsp;&nbsp; p = <strong>${p.toFixed(1)}</strong> Pa &nbsp;&nbsp; ρ = <strong>${rho.toFixed(4)}</strong> kg/m³`;
  });

  /* ---------- Flow conversions ---------- */
  const refRho = {air:1.204, argon:1.633, nitrogen:1.165, oxygen:1.331};
  document.getElementById('calcFlow').addEventListener('click', function(){
    const f = document.getElementById('fluidSLM').value;
    const val = parseFloat(document.getElementById('flowVal').value);
    const type = document.getElementById('flowType').value;
    const rho = refRho[f] || 1.0;
    let mDot=0, Q=0, SLM=0;
    if(type === 'mDot') { mDot = val; Q = mDot / rho; SLM = Q * 60000; }
    else if(type === 'Q') { Q = val; mDot = rho * Q; SLM = Q * 60000; }
    else { SLM = val; Q = SLM / 60000; mDot = rho * Q; }
    document.getElementById('flowResult').innerHTML = `Mass flow: <strong>${mDot.toExponential(4)}</strong> kg/s &nbsp;&nbsp; Volumetric: <strong>${Q.toExponential(4)}</strong> m³/s &nbsp;&nbsp; SLM: <strong>${SLM.toFixed(2)}</strong> L/min`;
  });

}); // end DOMContentLoaded
</script>
