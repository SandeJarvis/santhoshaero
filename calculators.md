---
layout: default
title: Calculators — Aerodynamics with Santhosh
---

<div class="card">
  <div class="pill">Reynolds Number Calculator</div>
  <h1>Reynolds Number Calculator</h1>
  <p>Enter flow parameters below to compute the Reynolds number (Re = ρVD/μ).</p>

  <form id="reCalc" style="display:grid;gap:1rem;max-width:420px">
    <label>Density (ρ) in kg/m³
      <input type="number" id="density" placeholder="e.g., 1.225" step="any" required style="width:100%;padding:.6rem;border:1px solid #ccc;border-radius:8px">
    </label>

    <label>Velocity (V) in m/s
      <input type="number" id="velocity" placeholder="e.g., 15" step="any" required style="width:100%;padding:.6rem;border:1px solid #ccc;border-radius:8px">
    </label>

    <label>Characteristic Length (D) in m
      <input type="number" id="length" placeholder="e.g., 0.5" step="any" required style="width:100%;padding:.6rem;border:1px solid #ccc;border-radius:8px">
    </label>

    <label>Dynamic Viscosity (μ) in kg/m·s
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
  document.getElementById('result').innerHTML = 
    `Reynolds Number (Re): <span style="color:#0b3a6f;">${formatted}</span>`;
}
</script>

