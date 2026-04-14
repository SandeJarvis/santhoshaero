---
layout: default
title: Aerodynamics Lab — Santhosh Kumar Sankar
---

<!-- MathJax for formulas -->
<script>
window.MathJax = {
  tex: { inlineMath:[['$','$'],['\\(','\\)']], displayMath:[['$$','$$'],['\\[','\\]']] },
  svg: { fontCache:'global' }
};
</script>
<script async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js"></script>

<style>
/* ── PAGE WRAPPER ─────────────────────────────────────────── */
.aero-page { max-width:1100px; margin:0 auto; padding:2rem 1.5rem; }

/* ── PAGE HEADER ─────────────────────────────────────────── */
.page-hero { margin-bottom:2.5rem; }
.page-hero h1 { font-size:2.2rem; color:#00f5ff; letter-spacing:2px; margin:0 0 .4rem; }
.page-hero p  { color:#aaa; font-size:1.05rem; max-width:720px; line-height:1.6; }

/* ── TAB BAR ─────────────────────────────────────────────── */
.tab-bar { display:flex; gap:0; border-bottom:2px solid rgba(255,255,255,0.12); margin-bottom:2rem; flex-wrap:wrap; }
.tab-btn {
  padding:.75rem 2rem; background:transparent; border:none; border-bottom:3px solid transparent;
  color:#888; font-size:.95rem; font-weight:600; cursor:pointer; letter-spacing:1px;
  transition:all .2s; margin-bottom:-2px;
}
.tab-btn.active { border-bottom-color:#00f5ff; color:#00f5ff; }
.tab-btn:hover:not(.active) { color:#ccc; }
.tab-panel { display:none; }
.tab-panel.active { display:block; }

/* ── SECTION CARDS ───────────────────────────────────────── */
.aero-section {
  background:rgba(255,255,255,0.04); border:1px solid rgba(0,245,255,0.12);
  border-radius:16px; padding:2rem; margin-bottom:1.5rem;
}
.aero-section h2 { color:#00f5ff; font-size:1.3rem; margin:0 0 .6rem; letter-spacing:1px; }
.aero-section h3 { color:#e2e8f0; font-size:1.05rem; margin:1.2rem 0 .5rem; }
.aero-section p  { color:#bbb; line-height:1.7; margin:.4rem 0; }

/* ── CONCEPT TAGS (clickable terms) ─────────────────────── */
.concept {
  color:#00f5ff; border-bottom:1px dashed #00f5ff; cursor:pointer;
  transition:background .15s; border-radius:3px; padding:0 2px;
}
.concept:hover { background:rgba(0,245,255,0.12); }

/* ── FORMULA BOX ─────────────────────────────────────────── */
.formula-box {
  background:rgba(0,0,0,0.4); border-left:3px solid #00f5ff;
  border-radius:8px; padding:1rem 1.5rem; margin:1rem 0; overflow-x:auto;
}

/* ── METRIC GRID ─────────────────────────────────────────── */
.metric-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(180px,1fr)); gap:1rem; margin:1rem 0; }
.metric-card {
  background:rgba(0,245,255,0.05); border:1px solid rgba(0,245,255,0.2);
  border-radius:12px; padding:1.2rem; text-align:center;
}
.metric-card .label { color:#888; font-size:.8rem; letter-spacing:1px; text-transform:uppercase; }
.metric-card .value { color:#00f5ff; font-size:1.6rem; font-weight:700; margin:.3rem 0; }
.metric-card .unit  { color:#aaa; font-size:.8rem; }

/* ── CALCULATOR CARD ─────────────────────────────────────── */
.calc-card {
  background:rgba(0,0,0,0.3); border:1px solid rgba(0,245,255,0.2);
  border-radius:12px; padding:1.5rem; margin-top:1rem;
}
.calc-card h4 { color:#00f5ff; margin:0 0 1rem; font-size:1rem; }
.calc-row { display:flex; flex-wrap:wrap; gap:.8rem; align-items:flex-end; margin-bottom:.8rem; }
.calc-field label { display:block; color:#999; font-size:.8rem; margin-bottom:.3rem; letter-spacing:.5px; }
.calc-field input, .calc-field select {
  background:rgba(255,255,255,0.07); border:1px solid rgba(255,255,255,0.15);
  color:#fff; border-radius:8px; padding:.45rem .8rem; font-size:.95rem; width:130px;
}
.calc-field input:focus { outline:1px solid #00f5ff; }
.calc-btn {
  background:#00f5ff; color:#000; font-weight:700; border:none;
  border-radius:8px; padding:.5rem 1.4rem; cursor:pointer; font-size:.9rem;
  transition:opacity .2s;
}
.calc-btn:hover { opacity:.85; }
.calc-result {
  margin-top:.8rem; padding:.8rem 1rem;
  background:rgba(0,245,255,0.08); border-radius:8px; color:#00f5ff;
  font-size:1rem; font-weight:600; display:none;
}

/* ── TOOLS/SOFTWARE PILLS ────────────────────────────────── */
.pill-grid { display:flex; flex-wrap:wrap; gap:.6rem; margin:.8rem 0; }
.pill {
  background:rgba(0,245,255,0.1); border:1px solid rgba(0,245,255,0.3);
  color:#00f5ff; border-radius:20px; padding:.3rem .9rem; font-size:.82rem;
  font-weight:600; letter-spacing:.5px;
}

/* ── EXPERIENCE TIMELINE ─────────────────────────────────── */
.timeline { position:relative; padding-left:2rem; }
.timeline::before {
  content:''; position:absolute; left:0; top:0; bottom:0;
  width:2px; background:linear-gradient(to bottom,#00f5ff,transparent);
}
.timeline-item { position:relative; margin-bottom:2rem; }
.timeline-item::before {
  content:'◉'; position:absolute; left:-2.1rem; top:0;
  color:#00f5ff; font-size:.9rem;
}
.timeline-item .role { color:#fff; font-weight:700; font-size:1.05rem; }
.timeline-item .org  { color:#00f5ff; font-size:.9rem; }
.timeline-item .date { color:#888; font-size:.82rem; margin-bottom:.5rem; }
.timeline-item ul { color:#bbb; margin:.5rem 0; padding-left:1.2rem; line-height:1.8; }

/* ── POPUP MODAL ─────────────────────────────────────────── */
#concept-modal {
  display:none; position:fixed; inset:0; z-index:9999;
  background:rgba(0,0,0,.7); backdrop-filter:blur(4px);
  align-items:center; justify-content:center;
}
#concept-modal.open { display:flex; }
.modal-box {
  background:#0d1117; border:1px solid #00f5ff;
  border-radius:16px; max-width:560px; width:90%; padding:2rem;
  position:relative; max-height:80vh; overflow-y:auto;
}
.modal-box h3  { color:#00f5ff; margin:0 0 .8rem; font-size:1.3rem; }
.modal-box p   { color:#ccc; line-height:1.7; }
.modal-close {
  position:absolute; top:1rem; right:1.2rem;
  background:transparent; border:none; color:#888;
  font-size:1.4rem; cursor:pointer; line-height:1;
}
.modal-close:hover { color:#fff; }
.modal-formula {
  background:rgba(0,245,255,0.07); border-radius:8px;
  padding:1rem; margin:1rem 0; text-align:center;
}
</style>

<!-- ══════════════════════════════════════════════════════════ -->
<!--                        PAGE CONTENT                       -->
<!-- ══════════════════════════════════════════════════════════ -->

<div class="aero-page">

  <!-- Page header -->
  <div class="page-hero">
    <h1>⚡ AERODYNAMICS LAB</h1>
    <p>7+ years of hands-on aerodynamic research — UAV ducts, eVTOL blades, plasma jets, superhydrophobic surfaces.
       Click any <span class="concept" data-key="highlighted_term" style="pointer-events:none">highlighted term</span>
       to see its definition, formula, and calculator.</p>
  </div>

  <!-- ── TAB BAR ── -->
  <div class="tab-bar">
    <button class="tab-btn active" onclick="showAeroTab('external')">EXTERNAL AERODYNAMICS</button>
    <button class="tab-btn" onclick="showAeroTab('internal')">INTERNAL FLUID DYNAMICS</button>
    <button class="tab-btn" onclick="showAeroTab('experience')">EXPERIENCE TIMELINE</button>
    <button class="tab-btn" onclick="showAeroTab('calcs')">QUICK CALCULATORS</button>
  </div>

  <!-- ══════════════════════════════════ -->
  <!--  TAB 1 — EXTERNAL AERODYNAMICS   -->
  <!-- ══════════════════════════════════ -->
  <div id="tab-external" class="tab-panel active">

    <!-- Key metrics -->
    <div class="metric-grid">
      <div class="metric-card">
        <div class="label">Experience</div>
        <div class="value">7+</div>
        <div class="unit">Years aerodynamics</div>
      </div>
      <div class="metric-card">
        <div class="label">Setup Time Reduction</div>
        <div class="value">60%</div>
        <div class="unit">Robotic test automation</div>
      </div>
      <div class="metric-card">
        <div class="label">Reynolds Range</div>
        <div class="value">10³–10⁷</div>
        <div class="unit">Re tested across projects</div>
      </div>
      <div class="metric-card">
        <div class="label">Mach Regime</div>
        <div class="value">0–0.8</div>
        <div class="unit">Subsonic focus</div>
      </div>
    </div>

    <!-- UAV / eVTOL Duct Aerodynamics -->
    <div class="aero-section">
      <h2>UAV & eVTOL Duct Aerodynamics</h2>
      <p>
        Ducted fans are used in eVTOL and UAV designs to improve
        <span class="concept" data-key="thrust_efficiency">thrust efficiency</span>
        versus open rotors at the same disc loading. The duct accelerates inflow,
        raising the effective <span class="concept" data-key="mass_flow">mass flow rate</span>
        through the rotor plane. I worked on both steady-state and
        <span class="concept" data-key="unsteady_flow">unsteady flow</span>
        configurations using high-fidelity <span class="concept" data-key="rans">RANS</span>
        and <span class="concept" data-key="les">LES</span> solvers.
      </p>
      <h3>Duct Thrust Formula</h3>
      <div class="formula-box">
        $$T = \dot{m}(V_{exit} - V_{inlet}) = \rho A V_{exit}(V_{exit} - V_{\infty})$$
      </div>
      <p>
        Key design variables: duct lip radius, diffuser angle, rotor-to-duct gap.
        I used <span class="concept" data-key="adjoint_method">adjoint-based optimisation</span>
        to minimise total pressure loss across the duct.
      </p>
      <div class="pill-grid">
        <span class="pill">ANSYS Fluent</span>
        <span class="pill">OpenFOAM</span>
        <span class="pill">SolidWorks</span>
        <span class="pill">CATIA V5</span>
        <span class="pill">Python post-processing</span>
      </div>
    </div>

    <!-- Flexible Flaps & Surface Modification -->
    <div class="aero-section">
      <h2>Flexible Flaps & Superhydrophobic Surfaces</h2>
      <p>
        Passive flow control via flexible trailing-edge flaps can delay
        <span class="concept" data-key="flow_separation">flow separation</span>
        on UAV wings at high
        <span class="concept" data-key="angle_of_attack">angles of attack</span>.
        I tested morphing flap geometries in wind tunnel experiments supported by
        <span class="concept" data-key="piv">PIV (Particle Image Velocimetry)</span>
        measurements.
      </p>
      <p>
        Superhydrophobic surface coatings modify the effective
        <span class="concept" data-key="wall_slip">wall slip condition</span>,
        reducing skin friction drag by up to 10–20% in low-Re laminar boundary layers.
        Applied to wing lower surfaces in our UAV research program.
      </p>
      <h3>Skin Friction Drag Coefficient (Turbulent flat plate)</h3>
      <div class="formula-box">
        $$C_f = \frac{0.074}{Re_L^{1/5}} \quad \text{(Prandtl, turbulent)}$$
      </div>
    </div>

    <!-- Boundary Layer -->
    <div class="aero-section">
      <h2>Boundary Layer Theory & Transition</h2>
      <p>
        Understanding <span class="concept" data-key="boundary_layer">boundary layer</span>
        growth and the laminar-to-turbulent
        <span class="concept" data-key="transition">transition</span> point is critical
        for predicting drag and stall on UAV wings. At low
        <span class="concept" data-key="reynolds_number">Reynolds numbers</span>
        (typical UAV flight Re 10⁴–10⁶), transition is highly sensitive to
        surface roughness, freestream turbulence intensity, and pressure gradient.
      </p>
      <h3>Blasius Boundary Layer Thickness</h3>
      <div class="formula-box">
        $$\delta \approx \frac{5x}{\sqrt{Re_x}} \qquad Re_x = \frac{U_\infty x}{\nu}$$
      </div>
      <h3>Displacement Thickness</h3>
      <div class="formula-box">
        $$\delta^* = \int_0^\infty \left(1 - \frac{u}{U_\infty}\right) dy \approx \frac{1.72 x}{\sqrt{Re_x}}$$
      </div>
    </div>

  </div><!-- end tab-external -->

  <!-- ══════════════════════════════════ -->
  <!--  TAB 2 — INTERNAL FLUID DYNAMICS  -->
  <!-- ══════════════════════════════════ -->
  <div id="tab-internal" class="tab-panel">

    <div class="aero-section">
      <h2>Microchannel Gas Flows</h2>
      <p>
        At the microscale, continuum assumptions begin to break down when the
        <span class="concept" data-key="knudsen_number">Knudsen number</span>
        Kn > 0.001. I studied compressible gas flows in microchannels with
        characteristic dimensions 50–500 µm, relevant to plasma jet nozzles and
        microreactors. <span class="concept" data-key="rarefaction">Rarefaction effects</span>
        require slip-velocity boundary conditions rather than the standard no-slip wall.
      </p>
      <div class="formula-box">
        $$Kn = \frac{\lambda}{L} \qquad \lambda = \frac{\mu}{\rho}\sqrt{\frac{\pi}{2RT}}$$
      </div>
      <p>
        where λ is the <span class="concept" data-key="mean_free_path">mean free path</span>
        and L is the characteristic channel dimension.
      </p>
      <div class="pill-grid">
        <span class="pill">Fluent — Knudsen slip BC</span>
        <span class="pill">DSMC</span>
        <span class="pill">Python (post)</span>
      </div>
    </div>

    <div class="aero-section">
      <h2>Plasma Jets — CAPPJ & kINPen</h2>
      <p>
        Cold Atmospheric Pressure Plasma Jets (CAPPJs) generate reactive species for
        biomedical, surface treatment, and flow-control applications. I worked on the
        fluid dynamics of the carrier gas jet (He/Ar/air mixtures) for the kINPen device,
        characterising the <span class="concept" data-key="jet_entrainment">jet entrainment</span>
        and <span class="concept" data-key="turbulent_mixing">turbulent mixing</span>
        using planar laser-induced fluorescence (PLIF).
      </p>
      <p>
        The effective <span class="concept" data-key="reynolds_number">Reynolds number</span>
        of the plasma jet (Re ≈ 200–600) keeps the core flow laminar, which is critical
        for uniform reactive species delivery to a target surface.
      </p>
      <div class="formula-box">
        $$Re_{jet} = \frac{\rho_{He} \bar{V} D_{nozzle}}{\mu_{He}} \approx 200\text{–}600$$
      </div>
      <div class="pill-grid">
        <span class="pill">PLIF measurements</span>
        <span class="pill">Schlieren imaging</span>
        <span class="pill">kINPen device</span>
        <span class="pill">CAPPJ characterisation</span>
      </div>
    </div>

    <div class="aero-section">
      <h2>Free-Jet Studies</h2>
      <p>
        A free jet exhausting into quiescent ambient entrains surrounding fluid through
        <span class="concept" data-key="turbulent_mixing">turbulent mixing</span>.
        The jet half-width grows linearly: $r_{1/2} \propto x$ in the
        self-similar region. I mapped axial velocity decay and turbulence intensity
        profiles for He and Ar jets used in plasma applications.
      </p>
      <div class="formula-box">
        $$\frac{U_c}{U_0} = \frac{B \cdot D}{x - x_0} \qquad \text{(round jet centreline decay)}$$
      </div>
    </div>

  </div><!-- end tab-internal -->

  <!-- ══════════════════════════════════ -->
  <!--  TAB 3 — EXPERIENCE TIMELINE      -->
  <!-- ══════════════════════════════════ -->
  <div id="tab-experience" class="tab-panel">

    <div class="aero-section">
      <h2>Experience — Aerodynamics & Research</h2>
      <p style="color:#888; margin-bottom:1.5rem;">Click any highlighted term for a definition + formula.</p>

      <div class="timeline">

        <div class="timeline-item">
          <div class="role">Aerodynamics Researcher / CFD Engineer</div>
          <div class="org">University of New South Wales (UNSW) — Sydney</div>
          <div class="date">2020 – Present</div>
          <ul>
            <li>Designed and simulated ducted-fan UAV geometries using
                <span class="concept" data-key="rans">RANS</span> and
                <span class="concept" data-key="les">LES</span> in ANSYS Fluent and OpenFOAM</li>
            <li>Built Python-automated robotic wind tunnel test rig — reduced setup time by
                <strong style="color:#00f5ff">60%</strong></li>
            <li>Investigated <span class="concept" data-key="flow_separation">flow separation</span>
                on flexible flap geometries via PIV + CFD correlation</li>
            <li>Applied <span class="concept" data-key="superhydrophobic">superhydrophobic coatings</span>
                to wing surfaces — measured drag reduction up to 12%</li>
          </ul>
        </div>

        <div class="timeline-item">
          <div class="role">Plasma Fluid Dynamics Researcher</div>
          <div class="org">Research collaboration — CAPPJ / kINPen</div>
          <div class="date">2019 – 2022</div>
          <ul>
            <li>Characterised helium and argon plasma jets using PLIF and Schlieren imaging</li>
            <li>Modelled microchannel compressible flows with
                <span class="concept" data-key="knudsen_number">Knudsen slip</span> boundary conditions</li>
            <li>Mapped <span class="concept" data-key="turbulent_mixing">turbulent mixing</span>
                in free-jet near-field (Re 200–600)</li>
          </ul>
        </div>

        <div class="timeline-item">
          <div class="role">Aerospace Design Engineer</div>
          <div class="org">Earlier industry / academic role</div>
          <div class="date">2017 – 2019</div>
          <ul>
            <li>Conceptual design of fixed-wing UAVs — wing planform, aerofoil selection,
                <span class="concept" data-key="cl_cd">C_L / C_D</span> optimisation</li>
            <li>Used CATIA V5 + SolidWorks for 3D geometry; XFOIL for rapid aerofoil
                <span class="concept" data-key="polar">polar</span> estimation</li>
            <li>Performed <span class="concept" data-key="vortex_lattice">Vortex Lattice Method</span>
                (VLM) analysis for initial aerodynamic sizing</li>
          </ul>
        </div>

      </div>
    </div>

  </div><!-- end tab-experience -->

  <!-- ══════════════════════════════════ -->
  <!--  TAB 4 — QUICK CALCULATORS        -->
  <!-- ══════════════════════════════════ -->
  <div id="tab-calcs" class="tab-panel">

    <!-- Reynolds Number Calculator -->
    <div class="aero-section">
      <h2>Reynolds Number Calculator</h2>
      <p>Determines whether your flow is laminar, transitional, or turbulent.</p>
      <div class="formula-box">
        $$Re = \frac{\rho V L}{\mu}$$
      </div>
      <div class="calc-card">
        <h4>⚙ Calculate Re</h4>
        <div class="calc-row">
          <div class="calc-field">
            <label>Fluid</label>
            <select id="re-fluid" onchange="setFluidRe()">
              <option value="air">Air (20°C, sea level)</option>
              <option value="water">Water (20°C)</option>
              <option value="custom">Custom</option>
            </select>
          </div>
          <div class="calc-field">
            <label>Density ρ [kg/m³]</label>
            <input type="number" id="re-rho" value="1.204">
          </div>
          <div class="calc-field">
            <label>Viscosity μ [Pa·s]</label>
            <input type="number" id="re-mu" value="1.81e-5">
          </div>
          <div class="calc-field">
            <label>Velocity V [m/s]</label>
            <input type="number" id="re-v" placeholder="e.g. 20">
          </div>
          <div class="calc-field">
            <label>Length L [m]</label>
            <input type="number" id="re-l" placeholder="e.g. 0.5">
          </div>
          <button class="calc-btn" onclick="calcRe()">Calculate</button>
        </div>
        <div class="calc-result" id="re-result"></div>
      </div>
    </div>

    <!-- Lift & Drag Calculator -->
    <div class="aero-section">
      <h2>Lift & Drag Force Calculator</h2>
      <p>Computes aerodynamic forces from dimensionless coefficients and flow conditions.</p>
      <div class="formula-box">
        $$q = \tfrac{1}{2}\rho V^2 \qquad L = C_L \cdot q \cdot A \qquad D = C_D \cdot q \cdot A$$
      </div>
      <div class="calc-card">
        <h4>⚙ Calculate L & D</h4>
        <div class="calc-row">
          <div class="calc-field">
            <label>Density ρ [kg/m³]</label>
            <input type="number" id="ld-rho" value="1.204">
          </div>
          <div class="calc-field">
            <label>Velocity V [m/s]</label>
            <input type="number" id="ld-v" placeholder="e.g. 25">
          </div>
          <div class="calc-field">
            <label>Ref. Area A [m²]</label>
            <input type="number" id="ld-a" placeholder="e.g. 0.3">
          </div>
          <div class="calc-field">
            <label>C_L</label>
            <input type="number" id="ld-cl" placeholder="e.g. 0.8">
          </div>
          <div class="calc-field">
            <label>C_D</label>
            <input type="number" id="ld-cd" placeholder="e.g. 0.05">
          </div>
          <button class="calc-btn" onclick="calcLD()">Calculate</button>
        </div>
        <div class="calc-result" id="ld-result"></div>
      </div>
    </div>

    <!-- Mach Number Calculator -->
    <div class="aero-section">
      <h2>Mach Number Calculator</h2>
      <p>Ratio of flow velocity to local speed of sound. Critical for compressibility assessment.</p>
      <div class="formula-box">
        $$M = \frac{V}{a} \qquad a = \sqrt{\gamma R T}$$
      </div>
      <div class="calc-card">
        <h4>⚙ Calculate Mach Number</h4>
        <div class="calc-row">
          <div class="calc-field">
            <label>Velocity V [m/s]</label>
            <input type="number" id="mach-v" placeholder="e.g. 100">
          </div>
          <div class="calc-field">
            <label>Temperature T [°C]</label>
            <input type="number" id="mach-t" value="15">
          </div>
          <button class="calc-btn" onclick="calcMach()">Calculate</button>
        </div>
        <div class="calc-result" id="mach-result"></div>
      </div>
    </div>

    <!-- Boundary Layer Thickness -->
    <div class="aero-section">
      <h2>Boundary Layer Thickness (Blasius)</h2>
      <p>Laminar flat-plate boundary layer thickness at distance x from leading edge.</p>
      <div class="formula-box">
        $$\delta = \frac{5x}{\sqrt{Re_x}} \qquad Re_x = \frac{U_\infty x}{\nu}$$
      </div>
      <div class="calc-card">
        <h4>⚙ Calculate δ</h4>
        <div class="calc-row">
          <div class="calc-field">
            <label>Velocity U∞ [m/s]</label>
            <input type="number" id="bl-u" placeholder="e.g. 15">
          </div>
          <div class="calc-field">
            <label>Distance x [m]</label>
            <input type="number" id="bl-x" placeholder="e.g. 0.2">
          </div>
          <div class="calc-field">
            <label>Kinematic ν [m²/s]</label>
            <input type="number" id="bl-nu" value="1.5e-5">
          </div>
          <button class="calc-btn" onclick="calcBL()">Calculate</button>
        </div>
        <div class="calc-result" id="bl-result"></div>
      </div>
    </div>

  </div><!-- end tab-calcs -->

</div><!-- end aero-page -->

<!-- ══════════════════════════════════════════════════════════ -->
<!--                    CONCEPT POPUP MODAL                    -->
<!-- ══════════════════════════════════════════════════════════ -->
<div id="concept-modal">
  <div class="modal-box">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <h3 id="modal-title"></h3>
    <p  id="modal-def"></p>
    <div class="modal-formula" id="modal-formula"></div>
    <div id="modal-extra"></div>
  </div>
</div>

<!-- ══════════════════════════════════════════════════════════ -->
<!--                        JAVASCRIPT                         -->
<!-- ══════════════════════════════════════════════════════════ -->
<script>
// ── TAB SWITCHING ──────────────────────────────────────────
function showAeroTab(id) {
  document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('tab-' + id).classList.add('active');
  event.target.classList.add('active');
}

// ── CONCEPTS DATABASE ──────────────────────────────────────
const concepts = {
  reynolds_number: {
    title: "Reynolds Number (Re)",
    def: "The ratio of inertial forces to viscous forces in a flow. It is the most important dimensionless number in fluid mechanics — it tells you whether your flow will be smooth (laminar) or chaotic (turbulent). For UAV wings, Re typically ranges from 10⁴ to 10⁶.",
    formula: "$$Re = \\frac{\\rho V L}{\\mu} = \\frac{V L}{\\nu}$$",
    extra: "Rule of thumb: Re < 2300 → Laminar &nbsp;|&nbsp; 2300–4000 → Transitional &nbsp;|&nbsp; Re > 4000 → Turbulent"
  },
  rans: {
    title: "RANS — Reynolds-Averaged Navier-Stokes",
    def: "The most common CFD approach for engineering flows. Instead of resolving every turbulent eddy (which would be too expensive), RANS time-averages the Navier-Stokes equations and models the effect of turbulence using a turbulence model like k-ω SST or k-ε. Fast and practical — used in ANSYS Fluent and OpenFOAM.",
    formula: "$$\\frac{\\partial \\bar{u}_i}{\\partial t} + \\bar{u}_j \\frac{\\partial \\bar{u}_i}{\\partial x_j} = -\\frac{1}{\\rho}\\frac{\\partial \\bar{p}}{\\partial x_i} + \\frac{\\partial}{\\partial x_j}\\left[(\\nu + \\nu_t)\\frac{\\partial \\bar{u}_i}{\\partial x_j}\\right]$$",
    extra: "ν_t is the turbulent (eddy) viscosity — this is what the turbulence model provides."
  },
  les: {
    title: "LES — Large Eddy Simulation",
    def: "More accurate (and expensive) than RANS. LES resolves large turbulent eddies directly and only models the smallest (sub-grid) scales. Used when you need accurate prediction of unsteady flow features like vortex shedding, acoustic noise, or dynamic stall on a flexible flap.",
    formula: "$$\\frac{\\partial \\bar{u}_i}{\\partial t} + \\frac{\\partial \\bar{u}_i \\bar{u}_j}{\\partial x_j} = -\\frac{1}{\\rho}\\frac{\\partial \\bar{p}}{\\partial x_i} + \\nu \\frac{\\partial^2 \\bar{u}_i}{\\partial x_j^2} - \\frac{\\partial \\tau_{ij}^{SGS}}{\\partial x_j}$$",
    extra: "τᵢⱼ_SGS is the sub-grid-scale stress tensor — modelled using the Smagorinsky or dynamic Smagorinsky model."
  },
  flow_separation: {
    title: "Flow Separation",
    def: "When the boundary layer can no longer follow the surface against an adverse pressure gradient (pressure increasing in flow direction), it detaches — this is separation. On a wing, separation causes a sudden loss of lift (stall). Preventing or delaying separation is the main goal of most aerodynamic optimisation.",
    formula: "$$\\frac{\\partial p}{\\partial x} > 0 \\Rightarrow \\text{adverse pressure gradient} \\Rightarrow \\text{risk of separation}$$",
    extra: "Flexible trailing-edge flaps can suppress separation by energising the boundary layer near the trailing edge."
  },
  boundary_layer: {
    title: "Boundary Layer",
    def: "The thin layer of fluid immediately adjacent to a solid surface where viscosity matters. Outside the boundary layer, the flow behaves as if it were inviscid. The boundary layer grows in thickness along a surface as viscous effects accumulate. It produces skin friction drag and, if it separates, pressure drag.",
    formula: "$$\\delta \\approx \\frac{5x}{\\sqrt{Re_x}} \\quad \\text{(Blasius, laminar flat plate)}$$",
    extra: "The displacement thickness δ* is the effective thickness by which the outer flow is displaced outward due to the boundary layer."
  },
  angle_of_attack: {
    title: "Angle of Attack (α)",
    def: "The angle between the chord line of a wing and the oncoming freestream flow direction. Increasing α increases lift — up to the stall angle (typically 12–18° for conventional aerofoils). Beyond stall, the flow separates massively and lift drops sharply.",
    formula: "$$C_L \\approx C_{L,\\alpha} \\cdot (\\alpha - \\alpha_0) \\quad \\text{(thin aerofoil theory: } C_{L,\\alpha} = 2\\pi \\text{/rad)}$$",
    extra: "α₀ is the zero-lift angle — negative for cambered aerofoils (they generate lift even at α=0)."
  },
  piv: {
    title: "PIV — Particle Image Velocimetry",
    def: "An experimental technique to measure velocity fields in a flow. Tiny tracer particles (micron-scale) are seeded into the flow and illuminated by a laser sheet. Two consecutive laser pulses image the particles; cross-correlation of the two images gives the displacement vector field — hence the velocity field.",
    formula: "$$\\vec{V}(x,y) = \\frac{\\Delta \\vec{x}}{\\Delta t} \\quad \\text{(displacement / time between laser pulses)}$$",
    extra: "PIV gives full-field 2D velocity data. Stereo PIV adds a third camera to recover the out-of-plane component."
  },
  knudsen_number: {
    title: "Knudsen Number (Kn)",
    def: "The ratio of the molecular mean free path to a characteristic flow dimension. When Kn > 0.001, continuum fluid mechanics starts to break down and you need slip boundary conditions or molecular simulation methods (DSMC).",
    formula: "$$Kn = \\frac{\\lambda}{L} \\qquad \\lambda = \\frac{\\mu}{\\rho}\\sqrt{\\frac{\\pi}{2RT}}$$",
    extra: "Kn < 0.001: Continuum | 0.001–0.1: Slip flow | 0.1–10: Transition | > 10: Free molecular"
  },
  turbulent_mixing: {
    title: "Turbulent Mixing",
    def: "Turbulent flows mix momentum, heat, and species much faster than laminar flows due to chaotic eddy motion. Turbulent mixing is characterised by the turbulent diffusivity (or eddy diffusivity), which can be 100–1000× larger than molecular diffusivity.",
    formula: "$$\\Gamma_t = \\frac{\\mu_t}{\\rho Sc_t} \\qquad \\text{where } Sc_t \\approx 0.7 \\text{ (turbulent Schmidt number)}$$",
    extra: "In plasma jet studies, turbulent mixing determines how quickly the reactive gas dilutes into the ambient air."
  },
  thrust_efficiency: {
    title: "Thrust Efficiency / Figure of Merit",
    def: "For a rotor or ducted fan, thrust efficiency compares the actual thrust produced to the ideal (Betz limit) thrust for the same power input. A duct improves thrust efficiency by reducing the induced velocity required for a given thrust — effectively increasing the effective disc area.",
    formula: "$$FM = \\frac{T^{3/2}}{\\sqrt{2\\rho A} \\cdot P} \\qquad T = 2\\rho A v_i^2 \\quad \\text{(actuator disc)}$$",
    extra: "FM = 1.0 is ideal. Typical hover rotors: FM ≈ 0.6–0.8. Ducted fans can exceed open-rotor FM at the same disc loading."
  },
  mass_flow: {
    title: "Mass Flow Rate (ṁ)",
    def: "The mass of fluid passing through a cross-section per unit time. Conservation of mass (continuity equation) requires ṁ to be constant along a streamtube for steady, incompressible flow.",
    formula: "$$\\dot{m} = \\rho A V \\quad [\\text{kg/s}] \\qquad A_1 V_1 = A_2 V_2 \\text{ (incompressible)}$$",
    extra: "For compressible flows, ṁ = ρAV is still constant but ρ varies — you need the energy equation to close the system."
  },
  unsteady_flow: {
    title: "Unsteady Flow",
    def: "Flow in which conditions change with time at a fixed point in space. Unsteady aerodynamics (e.g. dynamic stall, vortex shedding, blade-vortex interaction) requires time-accurate simulation — you can't use steady-state RANS alone.",
    formula: "$$\\frac{\\partial \\rho}{\\partial t} + \\nabla \\cdot (\\rho \\vec{V}) = 0 \\quad \\text{(unsteady continuity)}$$",
    extra: "Time step selection (CFL condition): Δt < CFL · Δx / V_max ensures numerical stability."
  },
  cl_cd: {
    title: "Lift & Drag Coefficients (C_L, C_D)",
    def: "Dimensionless coefficients that characterise the aerodynamic performance of a body. C_L and C_D normalise lift and drag forces by dynamic pressure and reference area, making comparisons across scales possible.",
    formula: "$$C_L = \\frac{L}{q S} \\qquad C_D = \\frac{D}{q S} \\qquad q = \\tfrac{1}{2}\\rho V^2$$",
    extra: "The ratio L/D = C_L/C_D is the aerodynamic efficiency. Maximising L/D for cruise and C_L for low-speed manoeuvre are usually competing objectives."
  },
  vortex_lattice: {
    title: "Vortex Lattice Method (VLM)",
    def: "A linear, potential-flow panel method for 3D wing aerodynamics. The wing is divided into a grid of panels, each carrying a horseshoe vortex. The no-penetration boundary condition applied at each control point gives a system of linear equations for the circulation strengths — from which C_L, induced drag, and spanwise load distribution are calculated.",
    formula: "$$\\sum_{j=1}^N \\frac{\\Gamma_j}{4\\pi} \\oint \\frac{d\\vec{l} \\times \\hat{r}}{r^2} \\cdot \\hat{n}_i = -V_\\infty \\cos(\\alpha)$$",
    extra: "VLM is extremely fast (seconds vs hours for CFD) — ideal for parametric design sweeps in early conceptual design."
  },
  polar: {
    title: "Aerofoil Polar",
    def: "A plot of C_L vs C_D (or C_L vs α) for an aerofoil or wing. The polar summarises the full aerodynamic performance envelope — showing the design point, stall angle, and minimum drag. Generated by XFOIL (2D aerofoil) or CFD (3D wing).",
    formula: "$$C_{D,total} = C_{D,0} + \\frac{C_L^2}{\\pi e AR} \\quad \\text{(parabolic drag polar, 3D wing)}$$",
    extra: "e is Oswald's efficiency factor (≈0.7–0.95). AR is aspect ratio = b²/S. The second term is induced drag."
  },
  adjoint_method: {
    title: "Adjoint-Based Optimisation",
    def: "A mathematical method for computing the gradient of an objective function (e.g. drag) with respect to many design variables (e.g. surface shape) in a single solve — regardless of how many design variables there are. Makes gradient-based aerodynamic shape optimisation practical.",
    formula: "$$\\frac{dJ}{d\\alpha} = \\frac{\\partial J}{\\partial \\alpha} + \\lambda^T \\frac{\\partial R}{\\partial \\alpha} = 0 \\quad \\text{(adjoint equation)}$$",
    extra: "Used in ANSYS Fluent's adjoint solver and OpenFOAM adjointOptimisation. Santhosh applied this to minimise total pressure loss in UAV duct designs."
  },
  mean_free_path: {
    title: "Mean Free Path (λ)",
    def: "The average distance a gas molecule travels between successive collisions. At standard atmospheric conditions for air, λ ≈ 68 nm. In microchannels with characteristic dimensions below ~100 µm, λ becomes comparable to the geometry and continuum mechanics breaks down.",
    formula: "$$\\lambda = \\frac{\\mu}{\\rho} \\sqrt{\\frac{\\pi}{2RT}} \\approx 68 \\text{ nm (air, 20°C, 1 atm)}$$",
    extra: "At low pressures or in microfabricated devices, λ increases and slip-flow or free-molecular regimes become relevant."
  },
  rarefaction: {
    title: "Rarefaction Effects",
    def: "When Kn > 0.001, gas molecules near a wall no longer equilibrate through enough collisions to satisfy the no-slip condition. The gas slips along the wall with a finite velocity — this is the velocity slip boundary condition. Rarefaction also causes temperature jump at heated/cooled walls.",
    formula: "$$u_{slip} = -\\frac{2-\\sigma}{\\sigma} \\lambda \\left.\\frac{\\partial u}{\\partial n}\\right|_{wall}$$",
    extra: "σ is the tangential momentum accommodation coefficient (≈0.9 for most engineering surfaces)."
  },
  jet_entrainment: {
    title: "Jet Entrainment",
    def: "A turbulent jet draws surrounding quiescent fluid inward — this is entrainment. The mass flow rate in the jet increases with axial distance due to entrainment, even with no external source of fluid. Entrainment determines how quickly a plasma jet mixes with the surrounding air.",
    formula: "$$\\dot{m}(x) = \\dot{m}_0 \\cdot \\frac{x}{D} \\cdot \\text{const} \\quad \\text{(round jet)}$$",
    extra: "Entrainment rate depends on the jet turbulence level and density ratio between jet and ambient."
  },
  transition: {
    title: "Laminar-Turbulent Transition",
    def: "The process by which a smooth (laminar) boundary layer breaks down into chaotic (turbulent) flow. Transition location strongly affects skin friction drag and heat transfer. At low Reynolds numbers typical of UAVs, transition can be delayed — exploited in natural laminar flow (NLF) aerofoil design.",
    formula: "$$Re_{x,tr} \\approx 5 \\times 10^5 \\quad \\text{(flat plate, low freestream turbulence)}$$",
    extra: "Transition prediction methods: Michel's criterion, e^N method (linear stability theory), or γ-Reθ model in CFD."
  },
  wall_slip: {
    title: "Wall Slip Condition",
    def: "In classical viscous flow (no-slip), fluid velocity at a wall equals the wall velocity (zero for a stationary wall). Superhydrophobic surfaces with trapped air pockets create an effective slip length β — the fluid behaves as if the wall is displaced inward by β, reducing skin friction.",
    formula: "$$u|_{wall} = \\beta \\left.\\frac{\\partial u}{\\partial n}\\right|_{wall} \\qquad \\beta = \\text{slip length (10–100 µm)}$$",
    extra: "Effective drag reduction depends on the flow regime and channel geometry. More effective at low Re and small channel dimensions."
  },
  superhydrophobic: {
    title: "Superhydrophobic Surfaces",
    def: "Surfaces with water contact angle > 150° and very low contact angle hysteresis. Microscale or nanoscale texture traps air pockets (Cassie-Baxter state), creating a partial gas lubrication layer that reduces skin friction drag and repels water/ice.",
    formula: "$$C_f^{SH} \\approx C_f^{smooth} \\cdot \\left(1 - \\frac{\\beta \\delta}{\\delta + \\beta}\\right) \\text{ (simplified)}$$",
    extra: "Applied to UAV wing lower surfaces in your research — measured drag reduction up to 12% at Re ~ 10⁵."
  }
};

// ── POPUP SYSTEM ──────────────────────────────────────────────
document.addEventListener('click', function(e) {
  const el = e.target.closest('.concept');
  if (!el) return;
  const key = el.dataset.key;
  const c = concepts[key];
  if (!c) return;
  document.getElementById('modal-title').textContent = c.title;
  document.getElementById('modal-def').textContent = c.def;
  document.getElementById('modal-formula').innerHTML = c.formula || '';
  document.getElementById('modal-extra').innerHTML = c.extra
    ? `<p style="color:#888;font-size:.88rem;margin-top:.6rem">${c.extra}</p>` : '';
  document.getElementById('concept-modal').classList.add('open');
  if (window.MathJax && MathJax.typesetPromise) MathJax.typesetPromise();
});

document.getElementById('concept-modal').addEventListener('click', function(e) {
  if (e.target === this) closeModal();
});
function closeModal() {
  document.getElementById('concept-modal').classList.remove('open');
}

// ── CALCULATORS ───────────────────────────────────────────────
const fluids = {
  air:   { rho: 1.204, mu: 1.81e-5 },
  water: { rho: 998,   mu: 1.002e-3 }
};

function setFluidRe() {
  const f = document.getElementById('re-fluid').value;
  if (fluids[f]) {
    document.getElementById('re-rho').value = fluids[f].rho;
    document.getElementById('re-mu').value  = fluids[f].mu;
  }
}

function showResult(id, html) {
  const el = document.getElementById(id);
  el.innerHTML = html;
  el.style.display = 'block';
  if (window.MathJax && MathJax.typesetPromise) MathJax.typesetPromise([el]);
}

function calcRe() {
  const rho = parseFloat(document.getElementById('re-rho').value);
  const mu  = parseFloat(document.getElementById('re-mu').value);
  const v   = parseFloat(document.getElementById('re-v').value);
  const l   = parseFloat(document.getElementById('re-l').value);
  if ([rho,mu,v,l].some(isNaN)) return showResult('re-result','⚠ Enter all values');
  const Re = (rho * v * l) / mu;
  const regime = Re < 2300 ? 'Laminar 🟢' : Re < 4000 ? 'Transitional 🟡' : 'Turbulent 🔴';
  showResult('re-result', `Re = <strong>${Re.toExponential(4)}</strong> &nbsp;→&nbsp; ${regime}`);
}

function calcLD() {
  const rho = parseFloat(document.getElementById('ld-rho').value);
  const v   = parseFloat(document.getElementById('ld-v').value);
  const a   = parseFloat(document.getElementById('ld-a').value);
  const cl  = parseFloat(document.getElementById('ld-cl').value);
  const cd  = parseFloat(document.getElementById('ld-cd').value);
  if ([rho,v,a,cl,cd].some(isNaN)) return showResult('ld-result','⚠ Enter all values');
  const q    = 0.5 * rho * v * v;
  const lift = cl * q * a;
  const drag = cd * q * a;
  showResult('ld-result',
    `q = ${q.toFixed(2)} Pa &nbsp;|&nbsp; <strong>L = ${lift.toFixed(2)} N</strong> &nbsp;|&nbsp; <strong>D = ${drag.toFixed(2)} N</strong> &nbsp;|&nbsp; L/D = ${(lift/drag).toFixed(1)}`
  );
}

function calcMach() {
  const v = parseFloat(document.getElementById('mach-v').value);
  const t = parseFloat(document.getElementById('mach-t').value) + 273.15;
  if ([v,t].some(isNaN)) return showResult('mach-result','⚠ Enter all values');
  const a = Math.sqrt(1.4 * 287.05 * t);
  const M = v / a;
  const regime = M < 0.8 ? 'Subsonic' : M < 1.2 ? 'Transonic' : M < 5 ? 'Supersonic' : 'Hypersonic';
  showResult('mach-result',
    `Speed of sound a = ${a.toFixed(1)} m/s &nbsp;|&nbsp; <strong>M = ${M.toFixed(4)}</strong> &nbsp;→&nbsp; ${regime}`
  );
}

function calcBL() {
  const u   = parseFloat(document.getElementById('bl-u').value);
  const x   = parseFloat(document.getElementById('bl-x').value);
  const nu  = parseFloat(document.getElementById('bl-nu').value);
  if ([u,x,nu].some(isNaN)) return showResult('bl-result','⚠ Enter all values');
  const Rex   = (u * x) / nu;
  const delta = (5 * x) / Math.sqrt(Rex);
  const dstar = (1.72 * x) / Math.sqrt(Rex);
  if (Rex > 5e5) {
    showResult('bl-result','⚠ Re_x > 5×10⁵ — flow likely turbulent. Blasius (laminar) formula not valid here.');
    return;
  }
  showResult('bl-result',
    `Re_x = ${Rex.toExponential(3)} &nbsp;|&nbsp; <strong>δ = ${(delta*1000).toFixed(2)} mm</strong> &nbsp;|&nbsp; δ* = ${(dstar*1000).toFixed(2)} mm`
  );
}
</script>
