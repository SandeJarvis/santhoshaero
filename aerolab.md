---
layout: default
title: Calculators — Aerodynamics with Santhosh
---

<div class="card">
  <div class="pill">Calculators</div>
  <h1>Engineering Calculators</h1>
  <p>Pick a category, then open the calculator you need. Each tool is self-contained with units and scientific notation.</p>

  <!-- Category Tabs -->
  <div style="display:flex;gap:.5rem;flex-wrap:wrap;margin:1rem 0;">
    <button class="tabBtn" data-tab="fluid" onclick="openTab('fluid')">Fluid Dynamics</button>
    <button class="tabBtn" data-tab="aero" onclick="openTab('aero')">Aerodynamics</button>
    <button class="tabBtn" data-tab="cfd" onclick="openTab('cfd')">CFD</button>

    <!-- Info buttons -->
    <button class="infoBtn" onclick="openInfo('fluidInfo')">ℹ︎ Fluid Info</button>
    <button class="infoBtn" onclick="openInfo('aeroInfo')">ℹ︎ Aero Info</button>
    <button class="infoBtn" onclick="openInfo('cfdInfo')">ℹ︎ CFD Info</button>
  </div>

  <!-- Tabs content wrapper -->
  <div id="tab-fluid" class="tabPanel">

    <!-- FLUID: Reynolds (internal) -->
    <div class="toolCard">
      <h3>Reynolds Number — Internal Flow</h3>
      <p><strong>Re = (ρ · V · D<sub>h</sub>) / μ</strong> &nbsp;
        <small>(ρ: kg/m³, V: m/s, D<sub>h</sub> hydraulic dia: m, μ: kg/m·s)</small>
      </p>
      <div class="grid2">
        <label>Density ρ [kg/m³]
          <input type="number" id="fi_rho" placeholder="1.225" step="any">
        </label>
        <label>Velocity V [m/s]
          <input type="number" id="fi_vel" placeholder="15" step="any">
        </label>
        <label>Hydraulic Dia Dₕ [m]
          <input type="number" id="fi_dh" placeholder="0.05" step="any">
        </label>
        <label>Viscosity μ [kg/m·s]
          <input type="number" id="fi_mu" placeholder="1.8e-5" step="any">
        </label>
      </div>
      <button onclick="calcRe_Internal()" class="primary">Calculate</button>
      <div id="fi_out" class="out"></div>
    </div>

    <!-- FLUID: Reynolds (external/general) -->
    <div class="toolCard">
      <h3>Reynolds Number — External/General</h3>
      <p><strong>Re = (ρ · V · L) / μ</strong> &nbsp;
        <small>(L: characteristic length: chord, diameter, etc.)</small>
      </p>
      <div class="grid2">
        <label>Density ρ [kg/m³]
          <input type="number" id="fe_rho" placeholder="1.225" step="any">
        </label>
        <label>Velocity V [m/s]
          <input type="number" id="fe_vel" placeholder="30" step="any">
        </label>
        <label>Length L [m]
          <input type="number" id="fe_L" placeholder="0.5" step="any">
        </label>
        <label>Viscosity μ [kg/m·s]
          <input type="number" id="fe_mu" placeholder="1.8e-5" step="any">
        </label>
      </div>
      <button onclick="calcRe_External()" class="primary">Calculate</button>
      <div id="fe_out" class="out"></div>
    </div>

    <!-- FLUID: Mass & Volume flow -->
    <div class="toolCard">
      <h3>Flow Rates</h3>
      <p>Use <strong>ṁ = ρ · Q</strong> and <strong>Q = A · V</strong>.
        <small>(ṁ: kg/s, Q: m³/s, A: m²)</small>
      </p>
      <div class="grid2">
        <label>Density ρ [kg/m³]
          <input type="number" id="fr_rho" placeholder="1.225" step="any">
        </label>
        <label>Area A [m²]
          <input type="number" id="fr_A" placeholder="0.02" step="any">
        </label>
        <label>Velocity V [m/s]
          <input type="number" id="fr_V" placeholder="10" step="any">
        </label>
      </div>
      <button onclick="calcFlowRates()" class="primary">Calculate</button>
      <div id="fr_out" class="out"></div>
    </div>

  </div> <!-- /tab-fluid -->

  <div id="tab-aero" class="tabPanel" style="display:none;">

    <!-- AERO: Lift -->
    <div class="toolCard">
      <h3>Lift Calculator</h3>
      <p><strong>L = ½ · ρ · V² · S · C<sub>L</sub></strong> &nbsp;
        <small>(L: N, ρ: kg/m³, V: m/s, S: m²)</small>
      </p>
      <div class="grid2">
        <label>Density ρ [kg/m³]
          <input type="number" id="li_rho" placeholder="1.225" step="any">
        </label>
        <label>Velocity V [m/s]
          <input type="number" id="li_V" placeholder="40" step="any">
        </label>
        <label>Wing Area S [m²]
          <input type="number" id="li_S" placeholder="1.2" step="any">
        </label>
        <label>Lift Coeff C<sub>L</sub> [-]
          <input type="number" id="li_CL" placeholder="0.8" step="any">
        </label>
      </div>
      <button onclick="calcLift()" class="primary">Calculate</button>
      <div id="li_out" class="out"></div>
    </div>

    <!-- AERO: Drag -->
    <div class="toolCard">
      <h3>Drag Calculator</h3>
      <p><strong>D = ½ · ρ · V² · S · C<sub>D</sub></strong> &nbsp;
        <small>(D: N)</small>
      </p>
      <div class="grid2">
        <label>Density ρ [kg/m³]
          <input type="number" id="dr_rho" placeholder="1.225" step="any">
        </label>
        <label>Velocity V [m/s]
          <input type="number" id="dr_V" placeholder="40" step="any">
        </label>
        <label>Ref. Area S [m²]
          <input type="number" id="dr_S" placeholder="1.2" step="any">
        </label>
        <label>Drag Coeff C<sub>D</sub> [-]
          <input type="number" id="dr_CD" placeholder="0.04" step="any">
        </label>
      </div>
      <button onclick="calcDrag()" class="primary">Calculate</button>
      <div id="dr_out" class="out"></div>
    </div>

    <!-- AERO: Prop/Thrust (simple) -->
    <div class="toolCard">
      <h3>Thrust (Prop Power Approx.)</h3>
      <p><strong>T ≈ P / V</strong> &nbsp;
        <small>(for propulsors where shaft/propulsive power → thrust via flight speed; first-order estimate)</small>
      </p>
      <div class="grid2">
        <label>Propulsive Power P [W]
          <input type="number" id="th_P" placeholder="2000" step="any">
        </label>
        <label>Flight Speed V [m/s]
          <input type="number" id="th_V" placeholder="30" step="any">
        </label>
      </div>
      <button onclick="calcThrustSimple()" class="primary">Calculate</button>
      <div id="th_out" class="out"></div>
      <p class="muted"><small>Note: This ignores prop efficiency & momentum terms. For better fidelity, include η<sub>prop</sub>: T ≈ (η<sub>prop</sub>·P)/V.</small></p>
    </div>

  </div> <!-- /tab-aero -->

  <div id="tab-cfd" class="tabPanel" style="display:none;">

    <!-- CFD: y+ estimator (flat-plate style) -->
    <div class="toolCard">
      <h3>Wall y⁺ Estimator</h3>
      <p>Target first cell height for a given y⁺ using a flat-plate skin-friction model (quick estimate).</p>
      <p><strong>y = (y⁺ · ν) / u<sub>τ</sub>, &nbsp; u<sub>τ</sub> = √(τ<sub>w</sub>/ρ), &nbsp; τ<sub>w</sub> = ½ ρ U² C<sub>f</sub></strong></p>
      <p class="muted"><small>For turbulent: C<sub>f</sub> ≈ 0.026 Re<sup>-1/7</sup>; for laminar: C<sub>f</sub> ≈ 1.328/√Re (Re based on length).</small></p>
      <div class="grid2">
        <label>Density ρ [kg/m³]
          <input type="number" id="yp_rho" placeholder="1.225" step="any">
        </label>
        <label>Viscosity μ [kg/m·s]
          <input type="number" id="yp_mu" placeholder="1.8e-5" step="any">
        </label>
        <label>Free-stream U [m/s]
          <input type="number" id="yp_U" placeholder="30" step="any">
        </label>
        <label>Length for Re [m]
          <input type="number" id="yp_L" placeholder="0.5" step="any">
        </label>
        <label>Target y⁺ [-]
          <input type="number" id="yp_yplus" placeholder="1" step="any">
        </label>
        <label>Regime
          <select id="yp_regime">
            <option value="turbulent" selected>Turbulent</option>
            <option value="laminar">Laminar</option>
          </select>
        </label>
      </div>
      <button onclick="calcYPlus()" class="primary">Estimate First Cell Height</button>
      <div id="yp_out" class="out"></div>
    </div>

    <!-- CFD: Time step (CFL) -->
    <div class="toolCard">
      <h3>Time Step Helper (CFL)</h3>
      <p><strong>Δt ≤ CFL · Δx / U</strong> &nbsp;
        <small>(enter your chosen CFL, characteristic grid size Δx, and speed U)</small>
      </p>
      <div class="grid2">
        <label>CFL [-]
          <input type="number" id="ts_cfl" placeholder="0.5" step="any">
        </label>
        <label>Δx [m]
          <input type="number" id="ts_dx" placeholder="0.002" step="any">
        </label>
        <label>Speed U [m/s]
          <input type="number" id="ts_u" placeholder="30" step="any">
        </label>
      </div>
      <button onclick="calcTimeStep()" class="primary">Calculate</button>
      <div id="ts_out" class="out"></div>
    </div>

  </div> <!-- /tab-cfd -->

</div> <!-- /card -->

<!-- Info Modals -->
<div id="fluidInfo" class="modal" onclick="closeInfo(event,'fluidInfo')">
  <div class="modalInner">
    <h3>Fluid Dynamics</h3>
    <p>General tools for internal/external flows: Reynolds number, flow rates, and section-wise parameters. Use SI units and characteristic length consistently.</p>
    <button class="primary" onclick="hide('fluidInfo')">Close</button>
  </div>
</div>

<div id="aeroInfo" class="modal" onclick="closeInfo(event,'aeroInfo')">
  <div class="modalInner">
    <h3>Aerodynamics</h3>
    <p>Wing/airframe estimates using classic formulas (lift/drag). Provide appropriate coefficients (C<sub>L</sub>, C<sub>D</sub>) for your configuration and Reynolds regime.</p>
    <button class="primary" onclick="hide('aeroInfo')">Close</button>
  </div>
</div>

<div id="cfdInfo" class="modal" onclick="closeInfo(event,'cfdInfo')">
  <div class="modalInner">
    <h3>CFD Helpers</h3>
    <p>Quick pre-processing aids: first cell height from target y⁺ and a stable explicit Δt from CFL. These are first-order estimates—validate against your solver’s guidance.</p>
    <button class="primary" onclick="hide('cfdInfo')">Close</button>
  </div>
</div>

<style>
  .tabBtn,.infoBtn,.primary{
    padding:.55rem .9rem;border:none;border-radius:10px;cursor:pointer;font-weight:600
  }
  .tabBtn{background:#e8eef6;color:#0b3a6f}
  .tabBtn.active{background:#0b3a6f;color:#fff}
  .infoBtn{background:#f0f0f0}
  .primary{background:#0b3a6f;color:#fff}
  .tabPanel{margin-top:1rem}
  .toolCard{border:1px solid #e7ebf1;border-radius:14px;padding:1rem;margin:1rem 0;background:#fff}
  .grid2{display:grid;grid-template-columns:1fr;gap:.8rem}
  @media(min-width:720px){.grid2{grid-template-columns:1fr 1fr}}
  .toolCard input,.toolCard select, .toolCard textarea{
    width:100%;padding:.6rem;border:1px solid #cbd5e1;border-radius:8px
  }
  .out{margin-top:.8rem;font-weight:600}
  .muted{color:#6b7280}
  .modal{
    display:none;position:fixed;inset:0;background:rgba(0,0,0,.4);
    align-items:center;justify-content:center;padding:1rem;z-index:99
  }
  .modalInner{
    background:#fff;max-width:520px;width:100%;border-radius:14px;padding:1rem 1.2rem;box-shadow:0 8px 28px rgba(0,0,0,.2)
  }
</style>

<script>
/* --- Tabs --- */
function openTab(name){
  document.querySelectorAll('.tabPanel').forEach(p=>p.style.display='none');
  document.getElementById('tab-'+name).style.display='block';
  document.querySelectorAll('.tabBtn').forEach(b=>b.classList.remove('active'));
  document.querySelector('.tabBtn[data-tab="'+name+'"]').classList.add('active');
}
openTab('fluid'); // default

/* --- Info modals --- */
function openInfo(id){ document.getElementById(id).style.display='flex'; }
function hide(id){ document.getElementById(id).style.display='none'; }
function closeInfo(e,id){ if(e.target.id===id) hide(id); }

/* --- Format helper (scientific notation) --- */
function sci(x){ return Number(x).toExponential(3); }

/* --- FLUID: Reynolds Internal --- */
function calcRe_Internal(){
  const rho = +document.getElementById('fi_rho').value || NaN;
  const V   = +document.getElementById('fi_vel').value || NaN;
  const Dh  = +document.getElementById('fi_dh').value  || NaN;
  const mu  = +document.getElementById('fi_mu').value  || NaN;
  const out = document.getElementById('fi_out');

  if([rho,V,Dh,mu].some(isNaN) || mu===0){ out.innerHTML = '<span style="color:red">Enter valid inputs.</span>'; return; }
  const Re = rho*V*Dh/mu;
  let regime = (Re<2300)?'Laminar':(Re<4000?'Transitional':'Turbulent');
  out.innerHTML = `Re = <span style="color:#0b3a6f">${sci(Re)}</span> &nbsp; <span class="muted">(${regime})</span>`;
}

/* --- FLUID: Reynolds External/General --- */
function calcRe_External(){
  const rho = +document.getElementById('fe_rho').value || NaN;
  const V   = +document.getElementById('fe_vel').value || NaN;
  const L   = +document.getElementById('fe_L').value   || NaN;
  const mu  = +document.getElementById('fe_mu').value  || NaN;
  const out = document.getElementById('fe_out');

  if([rho,V,L,mu].some(isNaN) || mu===0){ out.innerHTML = '<span style="color:red">Enter valid inputs.</span>'; return; }
  const Re = rho*V*L/mu;
  let regime = (Re<5e5)?'Likely laminar (flat plate guideline)':'Likely transitional/turbulent';
  out.innerHTML = `Re = <span style="color:#0b3a6f">${sci(Re)}</span> &nbsp; <span class="muted">${regime}</span>`;
}

/* --- FLUID: Flow rates --- */
function calcFlowRates(){
  const rho = +document.getElementById('fr_rho').value || NaN;
  const A   = +document.getElementById('fr_A').value   || NaN;
  const V   = +document.getElementById('fr_V').value   || NaN;
  const out = document.getElementById('fr_out');

  if([rho,A,V].some(isNaN)){ out.innerHTML = '<span style="color:red">Enter valid inputs.</span>'; return; }
  const Q  = A*V;       // m^3/s
  const md = rho*Q;     // kg/s
  out.innerHTML = `Q = <span style="color:#0b3a6f">${sci(Q)}</span> m³/s, &nbsp; ṁ = <span style="color:#0b3a6f">${sci(md)}</span> kg/s`;
}

/* --- AERO: Lift --- */
function calcLift(){
  const rho = +document.getElementById('li_rho').value || NaN;
  const V   = +document.getElementById('li_V').value   || NaN;
  const S   = +document.getElementById('li_S').value   || NaN;
  const CL  = +document.getElementById('li_CL').value  || NaN;
  const out = document.getElementById('li_out');

  if([rho,V,S,CL].some(isNaN)){ out.innerHTML = '<span style="color:red">Enter valid inputs.</span>'; return; }
  const L = 0.5*rho*V*V*S*CL;
  out.innerHTML = `L = <span style="color:#0b3a6f">${sci(L)}</span> N`;
}

/* --- AERO: Drag --- */
function calcDrag(){
  const rho = +document.getElementById('dr_rho').value || NaN;
  const V   = +document.getElementById('dr_V').value   || NaN;
  const S   = +document.getElementById('dr_S').value   || NaN;
  const CD  = +document.getElementById('dr_CD').value  || NaN;
  const out = document.getElementById('dr_out');

  if([rho,V,S,CD].some(isNaN)){ out.innerHTML = '<span style="color:red">Enter valid inputs.</span>'; return; }
  const D = 0.5*rho*V*V*S*CD;
  out.innerHTML = `D = <span style="color:#0b3a6f">${sci(D)}</span> N`;
}

/* --- AERO: Thrust (simple) --- */
function calcThrustSimple(){
  const P = +document.getElementById('th_P').value || NaN;
  const V = +document.getElementById('th_V').value || NaN;
  const out = document.getElementById('th_out');

  if([P,V].some(isNaN) || V===0){ out.innerHTML = '<span style="color:red">Enter valid inputs (V > 0).</span>'; return; }
  const T = P / V;
  out.innerHTML = `T ≈ <span style="color:#0b3a6f">${sci(T)}</span> N <span class="muted">(first-order)</span>`;
}

/* --- CFD: y+ estimator --- */
function calcYPlus(){
  const rho = +document.getElementById('yp_rho').value || NaN;
  const mu  = +document.getElementById('yp_mu').value  || NaN;
  const U   = +document.getElementById('yp_U').value   || NaN;
  const L   = +document.getElementById('yp_L').value   || NaN;
  const yP  = +document.getElementById('yp_yplus').value || NaN;
  const reg = document.getElementById('yp_regime').value;
  const out = document.getElementById('yp_out');

  if([rho,mu,U,L,yP].some(isNaN) || mu===0){ out.innerHTML = '<span style="color:red">Enter valid inputs.</span>'; return; }

  const nu = mu / rho;               // m^2/s
  const ReL = rho*U*L/mu;
  let Cf;
  if(reg==='laminar'){
    if(ReL<=0){ out.innerHTML = '<span style="color:red">Invalid Re.</span>'; return; }
    Cf = 1.328/Math.sqrt(ReL);
  }else{
    Cf = 0.026*Math.pow(ReL, -1/7);  // turbulent flat-plate estimate
  }
  const tauw = 0.5*rho*U*U*Cf;       // wall shear stress
  const utau = Math.sqrt(tauw/rho);  // friction velocity
  const y = (yP*nu)/utau;            // first cell height (m)

  out.innerHTML = `Estimated first cell height: <span style="color:#0b3a6f">${sci(y)}</span> m &nbsp; <span class="muted">(Re<sub>L</sub>=${sci(ReL)}, C<sub>f</sub>=${sci(Cf)})</span>`;
}

/* --- CFD: time step (CFL) --- */
function calcTimeStep(){
  const CFL = +document.getElementById('ts_cfl').value || NaN;
  const dx  = +document.getElementById('ts_dx').value  || NaN;
  const U   = +document.getElementById('ts_u').value   || NaN;
  const out = document.getElementById('ts_out');

  if([CFL,dx,U].some(isNaN) || U===0){ out.innerHTML = '<span style="color:red">Enter valid inputs (U > 0).</span>'; return; }
  const dt = CFL*dx/U;
  out.innerHTML = `Δt ≤ <span style="color:#0b3a6f">${sci(dt)}</span> s`;
}
</script>
