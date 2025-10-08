---
layout: default
title: Calculators — Aerodynamics with Santhosh
---

<div class="card">
  <div class="pill">Reynolds Number Calculator</div>
  <h1>Reynolds Number Calculator</h1>
  <p>
    The Reynolds number (<em>Re</em>) characterizes the ratio of inertial to viscous forces in a flow and is defined as:
  </p>

  <div style="background:#eef3f8;padding:1rem;border-radius:10px;margin:1rem 0;font-size:1.1rem;text-align:center;">
    <strong>Re = (ρ × V × D) / μ</strong>
    <br>
    <small>
      where ρ = density (kg/m³), V = velocity (m/s), D = characteristic length (m), μ = dynamic viscosity (kg/m·s)
    </small>
  </div>

  <form id="reCalc" style="display:grid;gap:1rem;max-width:420px">
    <label>Density (ρ) [kg/m³]
      <input type="number" id="density" placeholder="e.g., 1.225" step="any" required style="width:100%;padding:.6rem;border:1px solid #ccc;border-radius:8px">
    </label>

    <label>Velocity (V) [m/s]
      <input type="number" id="velocity" placeholder="e.g., 15" step="any" required style="width:100%;padding:.6rem;border:1px solid #ccc;border-radius:8px">
    </label>

    <label>Characteristic Length (D) [m]
      <input type="number" id="length" placeholder="e.g., 0.5" step="any" required style="width:100%;padding:.6rem;border:1px solid #ccc;border-radius:8px">
    </label>

    <label>Dynamic Viscosity (μ) [kg/m·s]
      <input type="number" id="viscosity" placeholder="e.g., 1.8e-5" step="any" required style="width:100%;padding:.6rem;border:1px solid #ccc;border-radius:8px">
    </label>

    <button type="button" onclick="calcReynolds()" style="padding:.7rem 1rem;background:#0b3a6f;color:#fff;border:none;border-radius:8px;font-weight:600;cursor:pointer">
      Calculate
    </button>
  </form>

  <div id="result" style="margin-top:1.5rem;font-size:1.1rem;font-weight:600;"></div>
</div>

<script>
function calcReynolds() {
  const rho = parseFloat(document.getElementById('density').value);
  const V = parseFloat(document.getElementById('velocity').value);
  const L = parseFloat(document.getElementById('length').value);
  const mu = parseFloat(document.getElementById('viscosity').value);

  if (isNaN(rho) || isNaN(V) || isNaN(L) || isNaN(mu) || mu === 0) {
    document.getElementById('result').innerHTML = '<span style="color:red;">Please enter valid inputs.</span>';
    return;
  }

  const Re = (rho * V * L) / mu;
  const formatted = Re.toExponential(3);
  
  let flowType = '';
  if (Re < 2300) flowType = 'Laminar flow';
  else if (Re >= 2300 && Re < 4000) flowType = 'Transitional flow';
  else flowType = 'Turbulent flow';

  document.getElementById('result').innerHTML = `
    <div style="background:#eef3f8;padding:1rem;border-radius:10px;">
      <p style="margin:0;">Reynolds Number (Re): <span style="color:#0b3a6f;">${formatted}</span></p>
      <p style="margin:0.4rem 0 0 0;color:#555;">Flow regime: <strong>${flowType}</strong></p>
    </div>`;
}
</script>
