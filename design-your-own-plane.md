---
layout: default
title: Design Your Own Plane — Conceptual Playground
---

<!-- MATHJAX -->
<script>
window.MathJax = {
  tex: { inlineMath:[['$','$'],['\\(','\\)']], displayMath:[['$$','$$'],['\\[','\\]']] },
  svg: { fontCache: 'global' }
};
</script>
<script async id="MathJax-script" src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js"></script>

<!-- CHART.JS (for polars & performance) -->
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>

<style>
  .input-group {display:flex;flex-wrap:wrap;gap:1rem;margin-top:.6rem;}
  .input-box {padding:.4rem;border-radius:8px;border:1px solid var(--ring);min-width:110px}
  table{width:100%;border-collapse:collapse;margin-top:.5rem;}
  th,td{padding:.35rem;text-align:left;}
  th{background:#f0f4fa;}
  details{margin-top:.4rem;}
  .formula { text-align:center; margin:.75rem 0; font-size:1.05rem;}
  .badge {display:inline-block;padding:.2rem .5rem;border-radius:999px;font-size:.85rem;border:1px solid var(--ring);}
  .badge.green{background:#e8f8f0;color:#0f7a4f;border-color:#bde6d5}
  .badge.yellow{background:#fff8e1;color:#9c6b00;border-color:#fde1a3}
  .badge.red{background:#ffe8e8;color:#b00020;border-color:#ffcaca}
  .mini {font-size:.9rem;color:#556}
  .flex {display:flex;gap:1rem;align-items:center;flex-wrap:wrap}
  .grow {flex:1 1 280px}
  .canvas-wrap{max-width:100%;padding:.5rem;border:1px dashed var(--ring);border-radius:12px}
  .hint{color:#667; font-size:.9rem}
</style>

<div class="card">
  <div class="pill">Concept Overview</div>
  <h2>Design Your Own Plane — Conceptual Playground</h2>
  <p>Explore a lightweight, browser-friendly aircraft concept tool. Adjust geometry, weight, center of gravity (CG), velocity, and choose an airfoil. Instantly see lift, drag, pitching moment, static margin, and simple performance checks. Educational assumptions: steady, level flight, subsonic, incompressible (or low Mach), uniform wing properties.</p>
  <details>
    <summary>Key assumptions & limitations</summary>
    <ul>
      <li>Wing aerodynamic center at 25% MAC (no sweep correction).</li>
      <li>Drag polar: $C_D = C_{D0} + k C_L^2$; lift: $C_L = a\,(\alpha-\\alpha_0)$ up to $C_{L,max}$.</li>
      <li>Simple neutral point model (wing + tail) with fixed efficiencies; no sideslip/yaw dynamics.</li>
      <li>ISA troposphere density estimate for altitude effects.</li>
    </ul>
  </details>
</div>

<!-- 1. AIRCRAFT INPUTS -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Aircraft Setup</div>
  <h2>Geometry, Mass, Conditions</h2>

  <div class="input-group">
    <div>
      <label><strong>Preset</strong></label><br>
      <select id="preset" class="input-box">
        <option value="custom">Custom</option>
        <option value="glider">Glider</option>
        <option value="lsa">Light Sport</option>
        <option value="twinjet">Small Jet</option>
      </select>
    </div>

    <div>
      <label><strong>Total Mass m [kg]</strong></label><br>
      <input id="mass" type="number" class="input-box" value="600" step="1">
    </div>

    <div>
      <label><strong>Wing Area S [m²]</strong></label><br>
      <input id="S" type="number" class="input-box" value="12.0" step="0.1">
    </div>

    <div>
      <label><strong>Span b [m]</strong></label><br>
      <input id="b" type="number" class="input-box" value="10.0" step="0.1">
    </div>

    <div>
      <label><strong>Altitude h [m]</strong></label><br>
      <input id="alt" type="number" class="input-box" value="0" step="100">
    </div>

    <div>
      <label><strong>Velocity V [m/s]</strong></label><br>
      <input id="V" type="number" class="input-box" value="40" step="0.5">
    </div>

    <div>
      <label><strong>Airfoil</strong></label><br>
      <select id="airfoil" class="input-box">
        <option value="NACA2412">NACA 2412</option>
        <option value="NACA0012">NACA 0012</option>
        <option value="NACA4415">NACA 4415</option>
        <option value="NACA23012">NACA 23012</option>
        <option value="ClarkY">Clark Y</option>
      </select>
    </div>

    <div>
      <label><strong>Zero-lift AoA offset [deg]</strong></label><br>
      <input id="alpha0" type="number" class="input-box" value="-2.0" step="0.1">
    </div>

    <div style="align-self:end;">
      <button id="applyPreset" class="input-box" style="background:var(--brand);color:#fff;border:0;">Load Preset</button>
    </div>
    <div style="align-self:end;">
      <button id="calcAll" class="input-box" style="background:var(--brand);color:#fff;border:0;">Compute</button>
    </div>
  </div>

  <div class="formula">
    $$L=\\tfrac{1}{2}\\,\\rho V^2 S\\,C_L,\\quad D=\\tfrac{1}{2}\\,\\rho V^2 S\\,(C_{D0}+kC_L^2),\\quad C_L=a(\\alpha-\\alpha_0)$$
  </div>
  <p class="hint">Tip: Use presets to auto-fill typical geometry and masses; tweak as needed.</p>
</div>

<!-- 2. CG & MOMENTS -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">CG & Moments</div>
  <h2>Move CG and See Pitching Moment</h2>

  <div class="input-group">
    <div>
      <label><strong>MAC c̄ [m]</strong></label><br>
      <input id="cbar" type="number" class="input-box" value="1.2" step="0.01">
    </div>
    <div>
      <label><strong>CG x [m] (from nose)</strong></label><br>
      <input id="cgx" type="number" class="input-box" value="3.0" step="0.02">
    </div>
    <div>
      <label><strong>CG z [m] (positive up)</strong></label><br>
      <input id="cgz" type="number" class="input-box" value="0.0" step="0.01">
    </div>
    <div>
      <label><strong>Wing AC x_ac [m]</strong></label><br>
      <input id="xac" type="number" class="input-box" value="3.1" step="0.02">
    </div>
    <div>
      <label><strong>C<sub>m0</sub> (airfoil @ 25%)</strong></label><br>
      <input id="cm0" type="number" class="input-box" value="-0.05" step="0.01">
    </div>
  </div>

  <div class="flex" style="margin-top:.5rem;">
    <div class="grow">
      <div id="momentOut" class="mini"></div>
      <div class="formula">$$M_y \\approx W\\,(x_{cg}-x_{ac}) + \\tfrac{1}{2}\\,\\rho V^2 S\\,c\\,C_{m0}$$</div>
      <p class="hint">Positive $M_y$ = nose-up (about lateral $y$-axis). Sign conventions are shown in the diagram.</p>
    </div>
    <div class="grow">
      <div class="canvas-wrap">
        <svg id="cgSvg" viewBox="0 0 420 140" width="100%" height="160">
          <!-- simple side view -->
          <rect x="10" y="70" width="380" height="6" fill="#cbd5e1"/>
          <rect x="140" y="55" width="140" height="6" fill="#60a5fa"/>
          <circle id="cgDot" cx="180" cy="80" r="4" fill="#ef4444"/>
          <circle id="acDot" cx="190" cy="80" r="4" fill="#10b981"/>
          <text x="170" y="98" font-size="10" fill="#ef4444">CG</text>
          <text x="200" y="98" font-size="10" fill="#10b981">AC (25% MAC)</text>
          <line id="liftArrow" x1="210" y1="80" x2="210" y2="30" stroke="#22c55e" stroke-width="2"/>
          <polygon id="liftHead" points="206,30 214,30 210,22" fill="#22c55e"/>
          <line id="weightArrow" x1="180" y1="80" x2="180" y2="120" stroke="#ef4444" stroke-width="2"/>
          <polygon id="weightHead" points="176,120 184,120 180,128" fill="#ef4444"/>
        </svg>
      </div>
    </div>
  </div>
</div>

<!-- 3. AIRFOIL POLARS -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Airfoil Explorer</div>
  <h2>Polars & Stall</h2>
  <div class="flex">
    <div class="grow">
      <canvas id="clAlpha" height="240"></canvas>
    </div>
    <div class="grow">
      <canvas id="cdCl" height="240"></canvas>
    </div>
  </div>
  <div id="airfoilTable"></div>
  <details>
    <summary>Model notes</summary>
    <div class="formula">
      $$C_L=a(\\alpha-\\alpha_0),\\quad C_D=C_{D0}+kC_L^2,\\quad \\alpha\\in[\\alpha_{stall}^- ,\\alpha_{stall}^+]$$
    </div>
  </details>
</div>

<!-- 4. PERFORMANCE & STABILITY -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Performance & Stability</div>
  <h2>Lift/Drag, Stall & Static Margin</h2>

  <div id="perfTable"></div>

  <div class="flex" style="margin-top:.5rem;">
    <div class="grow">
      <canvas id="powerChart" height="220"></canvas>
      <p class="hint">Power required $P_R = D\\,V$. Add thrust-available (optional) to see excess power.</p>
    </div>
    <div class="grow">
      <div class="input-group">
        <div>
          <label><strong>Tail Area S<sub>t</sub> [m²]</strong></label><br>
          <input id="St" type="number" class="input-box" value="2.5" step="0.1">
        </div>
        <div>
          <label><strong>Tail arm ℓ<sub>t</sub> [m]</strong></label><br>
          <input id="lt" type="number" class="input-box" value="3.0" step="0.1">
        </div>
        <div>
          <label><strong>Efficiencies</strong></label><br>
          <select id="etaTail" class="input-box">
            <option value="0.9">η<sub>t</sub>=0.9</option>
            <option value="0.8">η<sub>t</sub>=0.8</option>
          </select>
          <select id="downwash" class="input-box">
            <option value="0.3">dε/dα=0.3</option>
            <option value="0.2">dε/dα=0.2</option>
            <option value="0.4">dε/dα=0.4</option>
          </select>
        </div>
      </div>
      <div id="stabOut" class="mini"></div>
      <div class="formula">
        $$SM=\\frac{x_{NP}-x_{CG}}{\\bar c},\\quad x_{NP}\\approx x_{ac}+\\eta_t\\,(1-\\tfrac{d\\varepsilon}{d\\alpha})\\,\\frac{S_t}{S}\\,\\frac{\\ell_t}{\\bar c}$$
      </div>
      <p id="stabBadge"></p>
    </div>
  </div>
</div>

<!-- 5. OPTIONALS -->
<div class="card" style="margin-top:1rem;">
  <div class="pill">Optional Tools</div>
  <h2>Thrust Available, Altitude Effects, Export</h2>
  <div class="input-group">
    <div>
      <label><strong>Thrust Available T<sub>avail</sub> [N]</strong></label><br>
      <input id="Tavail" type="number" class="input-box" value="2000" step="10">
    </div>
    <div>
      <label><strong>Max Power avail [kW]</strong></label><br>
      <input id="Pavail" type="number" class="input-box" value="80" step="1">
    </div>
    <div style="align-self:end;">
      <button id="updateOptionals" class="input-box" style="background:var(--brand);color:#fff;border:0;">Update Charts</button>
    </div>
    <div style="align-self:end;">
      <button id="downloadReport" class="input-box" style="background:var(--brand);color:#fff;border:0;">Download Report</button>
    </div>
  </div>

  <details>
    <summary>What the report contains</summary>
    <ul>
      <li>Inputs (geometry, mass, altitude, airfoil).</li>
      <li>Computed $\rho$, $L$, $D$, $L/D$, $V_{stall}$ and $V_{TO}\\approx1.2\\,V_{stall}$.</li>
      <li>Moments about AC and CG location.</li>
      <li>Static margin & stability indicator.</li>
    </ul>
  </details>
</div>

<script>
document.addEventListener('DOMContentLoaded', () => {
  const g = 9.80665;

  /* ---------- helpers ---------- */
  const fmtSci = (x, s=4) => {
    if (!isFinite(x)) return '—';
    const ax = Math.abs(x);
    if (ax === 0) return '0';
    return (ax >= 1e4 || ax < 1e-3) ? x.toExponential(s) : x.toFixed(Math.max(0, s-2));
  };
  const renderMath = () => (window.MathJax && MathJax.typesetPromise) ? MathJax.typesetPromise() : Promise.resolve();

  /* ---------- simple ISA density (0–11 km) ---------- */
  function isa(h){
    const T0=288.15, p0=101325, L=0.0065, R=287.05;
    const T = T0 - L*h;
    const p = p0 * Math.pow(T/T0, 5.255877);
    const rho = p/(R*T);
    return {T,p,rho};
  }

  /* ---------- airfoil library (very simplified) ---------- */
  const foils = {
    NACA2412: { a: 0.105, alpha_stall_pos: 15, alpha_stall_neg: -12, CLmax: 1.5, CD0: 0.018, k: 0.045, Cm0:-0.04 },
    NACA0012: { a: 0.11,  alpha_stall_pos: 12, alpha_stall_neg: -12, CLmax: 1.2, CD0: 0.017, k: 0.050, Cm0: 0.00 },
    NACA4415: { a: 0.100, alpha_stall_pos: 16, alpha_stall_neg: -12, CLmax: 1.7, CD0: 0.019, k: 0.045, Cm0:-0.06 },
    NACA23012:{ a: 0.105, alpha_stall_pos: 14, alpha_stall_neg: -12, CLmax: 1.5, CD0: 0.017, k: 0.047, Cm0:-0.03 },
    ClarkY:   { a: 0.095, alpha_stall_pos: 15, alpha_stall_neg: -10, CLmax: 1.4, CD0: 0.020, k: 0.048, Cm0:-0.06 }
  };
  // a is per-degree lift slope (approx). Convert deg to rad internally where needed.

  /* ---------- DOM ---------- */
  const el = (id)=>document.getElementById(id);
  const mass=el('mass'), S=el('S'), b=el('b'), alt=el('alt'), V=el('V'), airfoilSel=el('airfoil'), alpha0=el('alpha0'), cbar=el('cbar');
  const cgx=el('cgx'), cgz=el('cgz'), xac=el('xac'), cm0=el('cm0');
  const St=el('St'), lt=el('lt'), etaTail=el('etaTail'), downwash=el('downwash');
  const Tavail=el('Tavail'), Pavail=el('Pavail');

  /* ---------- presets ---------- */
  const presets = {
    glider: { mass:450, S:14, b:18, V:28, cbar:0.9, xac:3.2, cgx:3.15 },
    lsa:    { mass:600, S:12, b:10, V:40, cbar:1.2, xac:3.1, cgx:3.0  },
    twinjet:{ mass:3500,S:22, b:16, V:80, cbar:1.4, xac:6.0, cgx:5.8  }
  };
  el('applyPreset').addEventListener('click', ()=>{
    const p = presets[el('preset').value]; if(!p) return;
    mass.value=p.mass; S.value=p.S; b.value=p.b; V.value=p.V; cbar.value=p.cbar; xac.value=p.xac; cgx.value=p.cgx;
    computeAll();
  });

  /* ---------- charts ---------- */
  let clAlphaChart, cdClChart, powerChart;
  function makeOrUpdateChart(ctx, cfg, store){
    if (store) { store.data=cfg.data; store.options=cfg.options; store.update(); return store; }
    return new Chart(ctx, cfg);
  }

  /* ---------- core computations ---------- */
  function airfoilModel(name){
    const f = foils[name] || foils.NACA2412;
    // Build arrays
    const a = f.a; // per degree
    const a0 = parseFloat(alpha0.value); // deg
    const alphas = []; const CLs=[]; const CDs=[];
    for(let A=-14; A<=18; A+=0.5){
      let CL = a*(A - a0);
      // clip for stall
      CL = Math.max(Math.min(CL, f.CLmax), -0.9*f.CLmax);
      const CD = f.CD0 + f.k*CL*CL;
      alphas.push(A); CLs.push(CL); CDs.push(CD);
    }
    return { f, alphas, CLs, CDs };
  }

  function aspectRatio(){
    const bv = parseFloat(b.value), Sv= parseFloat(S.value);
    if (bv>0 && Sv>0) return bv*bv/Sv;
    return NaN;
  }

  function perfAt(Vms, rho, foil){
    const Sv = parseFloat(S.value), m = parseFloat(mass.value);
    const W = m*g;
    const a = foil.f.a, a0 = parseFloat(alpha0.value);
    // Required CL for level flight
    const q = 0.5*rho*Vms*Vms;
    const CLreq = W/(q*Sv);
    // implied alpha
    let alphaReq = CLreq/a + a0; // deg
    // limit within stall
    alphaReq = Math.max(Math.min(alphaReq, foil.f.alpha_stall_pos), foil.f.alpha_stall_neg);
    const CL = Math.max(Math.min(CLreq, foil.f.CLmax), -0.9*foil.f.CLmax);
    const CD = foil.f.CD0 + foil.f.k*CL*CL;
    const D = q*Sv*CD;
    const L = q*Sv*CL;
    return {CL, CD, L, D, alphaReq, q};
  }

  function stallSpeed(rho, foil){
    const Sv=parseFloat(S.value), m = parseFloat(mass.value), W=m*g;
    const Vs = Math.sqrt( (2*W)/(rho*Sv*foil.f.CLmax) );
    return Vs;
  }

  function momentAboutAC(rho, Vms, Cm0v){
    const Sv=parseFloat(S.value), cv=parseFloat(cbar.value);
    return 0.5*rho*Vms*Vms*Sv*cv*Cm0v;
  }

  function updateCGViz(rho, perf){
    // position along SVG: map x to pixel simply using cgx and xac
    const xcg = parseFloat(cgx.value), xacv = parseFloat(xac.value);
    const scale = 30; // px/m (just for visualization)
    const base = 150; // nose offset
    const cgX = base + xcg*scale, acX = base + xacv*scale;
    el('cgDot').setAttribute('cx', cgX);
    el('acDot').setAttribute('cx', acX);
    // arrows scale by forces (clamp visuals)
    const L = perf.L, W = parseFloat(mass.value)*g;
    const Lh = Math.min(40, 10 + 30*(L/W));
    el('liftArrow').setAttribute('y2', 80 - Lh);
    el('liftHead').setAttribute('points', `${206},${80-Lh} ${214},${80-Lh} 210,${80-Lh-8}`);
  }

  function staticMargin(rho){
    // super-simplified NP estimate
    const Sv=parseFloat(S.value), cv=parseFloat(cbar.value);
    const et = parseFloat(etaTail.value);
    const deps = parseFloat(downwash.value);
    const Stv = parseFloat(St.value), ltv = parseFloat(lt.value);
    const xacv = parseFloat(xac.value), xcg=parseFloat(cgx.value);
    const xNP = xacv + et*(1 - deps)*(Stv/Sv)*(ltv/cv);
    const SM = (xNP - xcg)/cv; // fraction of cbar
    return {xNP, SM};
  }

  function computeAll(){
    // atmosphere
    const atm = isa(parseFloat(alt.value));
    const rho = atm.rho;

    // airfoil polars
    const foilData = airfoilModel(airfoilSel.value);

    // performance at V
    const Vms = parseFloat(V.value);
    const perf = perfAt(Vms, rho, foilData);
    const LoverD = perf.L/perf.D;

    // moments
    const W = parseFloat(mass.value)*g;
    const My_weight = W*(parseFloat(cgx.value) - parseFloat(xac.value)); // N·m (lever arm in m)
    const My_aero = momentAboutAC(rho, Vms, parseFloat(cm0.value));
    const My_total = My_weight + My_aero;

    // stall & takeoff
    const Vs = stallSpeed(rho, foilData);
    const Vto = 1.2*Vs;

    // static margin
    const SMres = staticMargin(rho);
    const SMpct = (SMres.SM*100);

    // output tables
    const AR = aspectRatio();
    const table1 = `
      <table>
        <tr><th colspan="4">Flight Condition Summary</th></tr>
        <tr><td>Density</td><td>\\(\\rho\\)</td><td>${fmtSci(rho,4)}</td><td>kg·m⁻³</td></tr>
        <tr><td>Aspect Ratio</td><td>\\(AR=b^2/S\\)</td><td>${fmtSci(AR,4)}</td><td>—</td></tr>
        <tr><td>Lift</td><td>\\(L\\)</td><td>${fmtSci(perf.L,4)}</td><td>N</td></tr>
        <tr><td>Drag</td><td>\\(D\\)</td><td>${fmtSci(perf.D,4)}</td><td>N</td></tr>
        <tr><td>Lift/Drag</td><td>\\(L/D\\)</td><td>${fmtSci(LoverD,4)}</td><td>—</td></tr>
        <tr><td>Req. $C_L$</td><td>\\(C_L\\)</td><td>${perf.CL.toFixed(3)}</td><td>—</td></tr>
        <tr><td>Req. \\(\\alpha\\)</td><td>deg</td><td>${perf.alphaReq.toFixed(2)}</td><td>deg</td></tr>
        <tr><td>Stall speed</td><td>\\(V_{stall}\\)</td><td>${fmtSci(Vs,4)}</td><td>m·s⁻¹</td></tr>
        <tr><td>TO speed (est.)</td><td>\\(V_{TO}\\approx1.2V_{stall}\\)</td><td>${fmtSci(Vto,4)}</td><td>m·s⁻¹</td></tr>
      </table>
      <div class="formula">$$P_R = D\\,V$$</div>
    `;
    el('perfTable').innerHTML = table1;

    const stabBadge = SMpct>5 ? `<span class="badge green">Stable (SM=${SMpct.toFixed(1)}%)</span>`
                        : (SMpct>=0 ? `<span class="badge yellow">Marginal (SM=${SMpct.toFixed(1)}%)</span>`
                                    : `<span class="badge red">Unstable (SM=${SMpct.toFixed(1)}%)</span>`);
    el('stabOut').innerHTML = `
      <p>Neutral point \\(x_{NP}\\) = <strong>${fmtSci(SMres.xNP,4)}</strong> m; CG \\(x_{CG}\\) = <strong>${fmtSci(parseFloat(cgx.value),4)}</strong> m; Static margin \\(SM\\) = <strong>${(SMres.SM).toFixed(3)}</strong> (fraction c̄).</p>
    `;
    el('stabBadge').innerHTML = stabBadge;

    el('momentOut').innerHTML = `
      <p>Weight moment: <strong>${fmtSci(My_weight,4)}</strong> N·m &nbsp; Aero moment: <strong>${fmtSci(My_aero,4)}</strong> N·m &nbsp; Total: <strong>${fmtSci(My_total,4)}</strong> N·m</p>
    `;

    // update CG viz
    updateCGViz(rho, perf);

    // charts
    // CL vs alpha
    const clCfg = {
      type: 'line',
      data: {
        labels: foilData.alphas,
        datasets: [{ label:'C_L vs α (deg)', data: foilData.CLs, fill:false, tension:0.15 }]
      },
      options: { responsive:true, maintainAspectRatio:false, scales:{ x:{ title:{text:'α [deg]', display:true}}, y:{ title:{text:'C_L', display:true}}}}
    };
    clAlphaChart = makeOrUpdateChart(el('clAlpha'), clCfg, clAlphaChart);

    // CD vs CL
    const cdCfg = {
      type: 'line',
      data: {
        labels: foilData.CLs,
        datasets: [{ label:'C_D vs C_L', data: foilData.CDs, parsing:false,
          segment:{}, pointRadius:0,
          // need {x:CL, y:CD} pairs:
          data: foilData.CLs.map((cl,i)=>({x:cl, y:foilData.CDs[i]}))
        }]
      },
      options: { responsive:true, maintainAspectRatio:false, parsing:false,
        scales:{ x:{ title:{text:'C_L', display:true}}, y:{ title:{text:'C_D', display:true}}}}
    };
    cdClChart = makeOrUpdateChart(el('cdCl'), cdCfg, cdClChart);

    // Airfoil data table
    const f = foilData.f;
    el('airfoilTable').innerHTML = `
      <table>
        <tr><th colspan="4">Airfoil Parameters (${airfoilSel.value})</th></tr>
        <tr><td>Lift slope</td><td>\\(a\\)</td><td>${f.a.toFixed(3)} per deg</td><td>—</td></tr>
        <tr><td>Zero-lift AoA</td><td>\\(\\alpha_0\\)</td><td>${parseFloat(alpha0.value).toFixed(2)}</td><td>deg</td></tr>
        <tr><td>Max lift coeff.</td><td>\\(C_{L,max}\\)</td><td>${f.CLmax.toFixed(2)}</td><td>—</td></tr>
        <tr><td>Parasite drag</td><td>\\(C_{D0}\\)</td><td>${f.CD0.toFixed(3)}</td><td>—</td></tr>
        <tr><td>Induced factor</td><td>\\(k\\)</td><td>${f.k.toFixed(3)}</td><td>—</td></tr>
        <tr><td>Pitch mom @ 25%</td><td>\\(C_{m0}\\)</td><td>${parseFloat(cm0.value).toFixed(3)}</td><td>—</td></tr>
      </table>
    `;

    // Power curve
    const vArr = []; const pReq = []; const tAvail = []; const pAvail = [];
    const T_av = parseFloat(Tavail.value);
    const P_av = parseFloat(Pavail.value)*1000.0;
    for (let v=10; v<= (Vms*2); v+=2){
      const p = perfAt(v, rho, foilData);
      vArr.push(v);
      pReq.push(p.D * v);
      tAvail.push(T_av);
      pAvail.push(P_av);
    }
    const pwCfg = {
      type:'line',
      data:{
        labels:vArr,
        datasets:[
          {label:'Power required [W]', data:pReq, pointRadius:0},
          {label:'Thrust available [N]', data:tAvail, yAxisID:'y2', pointRadius:0},
          {label:'Power available [W]', data:pAvail, pointRadius:0}
        ]
      },
      options:{
        responsive:true, maintainAspectRatio:false,
        scales:{
          x:{title:{text:'V [m/s]', display:true}},
          y:{title:{text:'Power [W]', display:true}},
          y2:{title:{text:'Thrust [N]', display:true}, position:'right', grid:{drawOnChartArea:false}}
        }
      }
    };
    powerChart = makeOrUpdateChart(el('powerChart'), pwCfg, powerChart);

    renderMath();
  }

  /* ---------- optionals update ---------- */
  el('updateOptionals').addEventListener('click', computeAll);

  /* ---------- recompute on key changes ---------- */
  ['mass','S','b','alt','V','airfoil','alpha0','cbar','cgx','cgz','xac','cm0','St','lt','etaTail','downwash'].forEach(id=>{
    el(id).addEventListener('change', computeAll);
  });

  /* ---------- report download ---------- */
  el('downloadReport').addEventListener('click', ()=>{
    const atm = isa(parseFloat(alt.value));
    const foilData = airfoilModel(airfoilSel.value);
    const perf = perfAt(parseFloat(V.value), atm.rho, foilData);
    const Vs = stallSpeed(atm.rho, foilData);
    const report = {
      timestamp: new Date().toISOString(),
      inputs:{
        mass: parseFloat(mass.value), S: parseFloat(S.value), b: parseFloat(b.value),
        cbar: parseFloat(cbar.value), alt: parseFloat(alt.value), V: parseFloat(V.value),
        airfoil: airfoilSel.value, alpha0: parseFloat(alpha0.value)
      },
      atmosphere: { T: atm.T, p: atm.p, rho: atm.rho },
      performance: { L: perf.L, D: perf.D, CL: perf.CL, CD: perf.CD, alpha_deg: perf.alphaReq, L_over_D: perf.L/perf.D, V_stall: Vs, V_TO: 1.2*Vs },
      moments:{
        My_weight: parseFloat(mass.value)*g*(parseFloat(cgx.value)-parseFloat(xac.value)),
        My_aero: momentAboutAC(atm.rho, parseFloat(V.value), parseFloat(cm0.value))
      },
      stability: staticMargin(atm.rho)
    };
    const blob = new Blob([JSON.stringify(report, null, 2)], {type:'application/json'});
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href=url; a.download='plane_design_report.json';
    document.body.appendChild(a); a.click(); a.remove();
    URL.revokeObjectURL(url);
  });

  /* ---------- compute button ---------- */
  el('calcAll').addEventListener('click', computeAll);

  /* ---------- initial render ---------- */
  computeAll();
});
</script>

