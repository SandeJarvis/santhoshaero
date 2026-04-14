---
layout: default
title: Fluid Mechanics & Flow Lab
---

# Fluid Mechanics & Flow Lab

Understanding flow regimes is critical for precision engineering. Below is an interactive tool I built to validate Reynolds Number calculations for pipe flow.

## 1. Interactive Reynolds Number Calculator
The Reynolds Number ($Re$) helps predict flow patterns ($Laminar$ vs $Turbulent$).

$$Re = \frac{\rho \cdot v \cdot D}{\mu}$$

<div class="calculator-box">
    <label>Density ($\rho$) [kg/m³]:</label>
    <input type="number" id="rho" value="1.225">
    
    <label>Velocity ($v$) [m/s]:</label>
    <input type="number" id="velocity" value="10">
    
    <label>Diameter ($D$) [m]:</label>
    <input type="number" id="diameter" value="0.05">
    
    <label>Dynamic Viscosity ($\mu$):</label>
    <input type="number" id="mu" value="0.0000181">
    
    <button onclick="calcRe()">Calculate Re</button>
    <p>Result: <strong id="re-result">--</strong></p>
    <p>Flow Regime: <strong id="regime">--</strong></p>
</div>

<script>
function calcRe() {
    const rho = document.getElementById('rho').value;
    const v = document.getElementById('velocity').value;
    const D = document.getElementById('diameter').value;
    const mu = document.getElementById('mu').value;
    const re = (rho * v * D) / mu;
    
    document.getElementById('re-result').innerText = re.toLocaleString();
    document.getElementById('regime').innerText = re > 4000 ? "Turbulent" : (re < 2300 ? "Laminar" : "Transitional");
}
</script>

## 2. Theoretical Background
Hover over the terms below to see the underlying physics:
* <span class="popup" data-tippy-content="The ratio of inertial forces to viscous forces.">Reynolds Number</span>
* <span class="popup" data-tippy-content="A flow regime characterized by high momentum diffusion and low momentum convection.">Laminar Flow</span>
