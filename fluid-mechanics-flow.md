---
layout: default
title: Fluid Mechanics Flow
---

<style>
    /* Add some specific styles for the calculators */
    .calculator-card {
        background-color: #ffffff;
        border-radius: 8px;
        padding: 24px;
        margin-bottom: 24px;
        box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        border: 1px solid #e2e8f0;
    }
    .calculator-card h3 {
        margin-top: 0;
        color: #1e3a8a; /* A deep blue */
    }
    .calculator-card .formula {
        background-color: #f8fafc;
        padding: 15px;
        border-radius: 5px;
        margin: 15px 0;
        text-align: center;
        overflow-x: auto;
    }
    .form-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
        gap: 16px;
        margin-bottom: 16px;
    }
    .form-group {
        display: flex;
        flex-direction: column;
    }
    .form-group label {
        font-size: 0.9em;
        margin-bottom: 4px;
        color: #4a5568;
    }
    .form-group input, .form-group select {
        padding: 8px;
        border: 1px solid #cbd5e0;
        border-radius: 4px;
        font-size: 1em;
    }
    .btn-calculate {
        background-color: #2563eb;
        color: white;
        border: none;
        padding: 10px 15px;
        border-radius: 5px;
        cursor: pointer;
        font-size: 1em;
        transition: background-color 0.2s;
    }
    .btn-calculate:hover {
        background-color: #1d4ed8;
    }
    .output {
        margin-top: 16px;
        font-size: 1.1em;
        font-weight: bold;
        color: #1e3a8a;
    }
</style>

<div class="container">

<div class="calculator-card" id="reynolds-card">
    <h3>Reynolds Number Calculator</h3>
    <p>The Reynolds number ($Re$) is a dimensionless quantity used to predict fluid flow patterns. It helps determine whether a flow is laminar (smooth) or turbulent (chaotic).</p>
    <div class="formula">
        $$ Re = \frac{\rho V L}{\mu} $$
    </div>
    <div class="form-grid">
        <div class="form-group">
            <label for="re-fluid">Fluid</label>
            <select id="re-fluid" class="fluid-selector">
                <option value="air">Air (STP)</option>
                <option value="water">Water (20°C)</option>
                <option value="glycerin">Glycerin (20°C)</option>
            </select>
        </div>
        <div class="form-group">
            <label for="re-density">Density ($\rho$) [kg/m³]</label>
            <input type="number" id="re-density" value="1.225">
        </div>
        <div class="form-group">
            <label for="re-viscosity">Dynamic Viscosity ($\mu$) [Pa·s]</label>
            <input type="number" id="re-viscosity" value="1.81e-5">
        </div>
        <div class="form-group">
            <label for="re-velocity">Velocity ($V$) [m/s]</label>
            <input type="number" id="re-velocity" placeholder="e.g., 20">
        </div>
        <div class="form-group">
            <label for="re-length">Characteristic Length ($L$) [m]</label>
            <input type="number" id="re-length" placeholder="e.g., 0.5">
        </div>
    </div>
    <button id="calc-re" class="btn-calculate">Calculate</button>
    <div id="re-output" class="output"></div>
</div>

<div class="calculator-card" id="mach-card">
    <h3>Mach Number & Flow Regime Calculator</h3>
    <p>The Mach number ($M$) is the ratio of flow velocity to the local speed of sound. It quantifies the compressibility of a fluid flow.</p>
    <div class="formula">
        $$ M = \frac{V}{a} \quad \text{where for ideal gases,} \quad a = \sqrt{\gamma R T} $$
    </div>
    <div class="form-grid">
        <div class="form-group">
            <label for="mach-fluid">Fluid</label>
            <select id="mach-fluid" class="fluid-selector">
                <option value="air">Air</option>
                <option value="water">Water</option>
            </select>
        </div>
        <div class="form-group">
            <label for="mach-velocity">Flow Velocity ($V$) [m/s]</label>
            <input type="number" id="mach-velocity" placeholder="e.g., 300">
        </div>
        <div class="form-group" id="mach-temp-group">
            <label for="mach-temp">Temperature [°C]</label>
            <input type="number" id="mach-temp" value="15">
        </div>
    </div>
    <button id="calc-mach" class="btn-calculate">Calculate</button>
    <div id="mach-output" class="output"></div>
</div>

<div class="calculator-card" id="dp-card">
    <h3>Dynamic Pressure & Flow Rate Calculator</h3>
    <p>Calculate dynamic pressure ($q$), the kinetic energy per unit volume of a fluid, along with volumetric ($Q$) and mass ($\dot{m}$) flow rates.</p>
    <div class="formula">
        $$ q = \frac{1}{2}\rho V^2 \quad | \quad Q = A \cdot V \quad | \quad \dot{m} = \rho \cdot Q $$
    </div>
    <div class="form-grid">
        <div class="form-group">
            <label for="dp-fluid">Fluid</label>
            <select id="dp-fluid" class="fluid-selector">
                <option value="air">Air (STP)</option>
                <option value="water">Water (20°C)</option>
                <option value="glycerin">Glycerin (20°C)</option>
            </select>
        </div>
        <div class="form-group">
            <label for="dp-density">Density ($\rho$) [kg/m³]</label>
            <input type="number" id="dp-density" value="1.225">
        </div>
         <div class="form-group">
            <label for="dp-velocity">Velocity ($V$) [m/s]</label>
            <input type="number" id="dp-velocity" placeholder="e.g., 50">
        </div>
        <div class="form-group">
            <label for="dp-area">Area ($A$) [m²]</label>
            <input type="number" id="dp-area" placeholder="e.g., 0.1">
        </div>
    </div>
    <button id="calc-dp" class="btn-calculate">Calculate</button>
    <div id="dp-output" class="output"></div>
</div>

<div class="calculator-card" id="continuity-card">
    <h3>Continuity Equation Calculator</h3>
    <p>For an incompressible, steady flow, the continuity equation states that the mass flow rate is constant. This tool solves for the velocity at a second point in a duct.</p>
    <div class="formula">
        $$ A_1 V_1 = A_2 V_2 $$
    </div>
    <div class="form-grid">
        <div class="form-group">
            <label for="cont-a1">Area at Point 1 ($A_1$) [m²]</label>
            <input type="number" id="cont-a1" placeholder="e.g., 0.2">
        </div>
        <div class="form-group">
            <label for="cont-v1">Velocity at Point 1 ($V_1$) [m/s]</label>
            <input type="number" id="cont-v1" placeholder="e.g., 10">
        </div>
        <div class="form-group">
            <label for="cont-a2">Area at Point 2 ($A_2$) [m²]</label>
            <input type="number" id="cont-a2" placeholder="e.g., 0.1">
        </div>
    </div>
    <button id="calc-cont" class="btn-calculate">Calculate</button>
    <div id="cont-output" class="output"></div>
</div>

</div>

<script>
document.addEventListener('DOMContentLoaded', function () {
    const fluidProperties = {
        'air': { rho: 1.225, mu: 1.81e-5, gamma: 1.4, R: 287 },
        'water': { rho: 998, mu: 1.002e-3, a: 1480 },
        'glycerin': { rho: 1261, mu: 1.412 }
    };

    // --- Fluid Selector Logic ---
    const fluidSelectors = document.querySelectorAll('.fluid-selector');
    fluidSelectors.forEach(selector => {
        selector.addEventListener('change', function(event) {
            const selectedCard = event.target.closest('.calculator-card');
            const selectedFluid = event.target.value;
            const properties = fluidProperties[selectedFluid];

            const densityInput = selectedCard.querySelector('input[id*="-density"]');
            const viscosityInput = selectedCard.querySelector('input[id*="-viscosity"]');
            
            if (densityInput && properties.rho) {
                densityInput.value = properties.rho;
            }
            if (viscosityInput && properties.mu) {
                viscosityInput.value = properties.mu;
            }

            // Special handling for Mach calculator temperature input
            if (selectedCard.id === 'mach-card') {
                const tempGroup = selectedCard.querySelector('#mach-temp-group');
                tempGroup.style.display = (selectedFluid === 'air') ? 'flex' : 'none';
            }
        });
    });
    // Trigger change on Mach card to set initial state
    document.getElementById('mach-fluid').dispatchEvent(new Event('change'));


    // --- Reynolds Number Calculation ---
    document.getElementById('calc-re').addEventListener('click', function() {
        const rho = parseFloat(document.getElementById('re-density').value);
        const V = parseFloat(document.getElementById('re-velocity').value);
        const L = parseFloat(document.getElementById('re-length').value);
        const mu = parseFloat(document.getElementById('re-viscosity').value);
        const outputEl = document.getElementById('re-output');

        if ([rho, V, L, mu].some(isNaN)) {
            outputEl.innerHTML = "Please enter valid numbers in all fields.";
            return;
        }

        const re = (rho * V * L) / mu;
        let regime = '';
        // Typical thresholds for external flow (e.g., over a plate)
        if (re < 5e5) {
            regime = 'Laminar';
        } else if (re >= 5e5 && re <= 1e7) {
            regime = 'Transitional';
        } else {
            regime = 'Turbulent';
        }

        outputEl.innerHTML = `Reynolds Number (Re) = ${re.toExponential(4)}<br>Flow Regime: ${regime}`;
    });

    // --- Mach Number Calculation ---
    document.getElementById('calc-mach').addEventListener('click', function() {
        const V = parseFloat(document.getElementById('mach-velocity').value);
        const fluid = document.getElementById('mach-fluid').value;
        const outputEl = document.getElementById('mach-output');

        if (isNaN(V)) {
            outputEl.innerHTML = "Please enter a valid velocity.";
            return;
        }

        let a; // Speed of sound
        const props = fluidProperties[fluid];

        if (fluid === 'air') {
            const tempC = parseFloat(document.getElementById('mach-temp').value);
            if (isNaN(tempC)) {
                outputEl.innerHTML = "Please enter a valid temperature.";
                return;
            }
            const tempK = tempC + 273.15;
            a = Math.sqrt(props.gamma * props.R * tempK);
        } else {
            a = props.a; // Use constant speed of sound for water
        }

        const mach = V / a;
        let regime = '';
        if (mach < 0.8) {
            regime = 'Subsonic';
        } else if (mach >= 0.8 && mach < 1.2) {
            regime = 'Transonic';
        } else if (mach >= 1.2 && mach < 5) {
            regime = 'Supersonic';
        } else {
            regime = 'Hypersonic';
        }

        outputEl.innerHTML = `Speed of Sound (a) = ${a.toFixed(2)} m/s<br>Mach Number (M) = ${mach.toFixed(4)}<br>Flow Regime: ${regime}`;
    });

    // --- Dynamic Pressure Calculation ---
    document.getElementById('calc-dp').addEventListener('click', function() {
        const rho = parseFloat(document.getElementById('dp-density').value);
        const V = parseFloat(document.getElementById('dp-velocity').value);
        const A = parseFloat(document.getElementById('dp-area').value);
        const outputEl = document.getElementById('dp-output');

        if ([rho, V, A].some(isNaN)) {
            outputEl.innerHTML = "Please enter valid numbers in all fields.";
            return;
        }

        const q = 0.5 * rho * V * V;
        const Q = A * V;
        const m_dot = rho * Q;

        outputEl.innerHTML = `Dynamic Pressure (q) = ${q.toExponential(4)} Pa<br>
                              Volumetric Flow Rate (Q) = ${Q.toFixed(4)} m³/s<br>
                              Mass Flow Rate (ṁ) = ${m_dot.toFixed(4)} kg/s`;
    });

    // --- Continuity Equation Calculation ---
    document.getElementById('calc-cont').addEventListener('click', function() {
        const a1 = parseFloat(document.getElementById('cont-a1').value);
        const v1 = parseFloat(document.getElementById('cont-v1').value);
        const a2 = parseFloat(document.getElementById('cont-a2').value);
        const outputEl = document.getElementById('cont-output');

        if ([a1, v1, a2].some(isNaN) || a2 === 0) {
            outputEl.innerHTML = "Please enter valid, non-zero numbers.";
            return;
        }

        const v2 = (a1 * v1) / a2;
        outputEl.innerHTML = `Velocity at Point 2 (V₂) = ${v2.toFixed(4)} m/s`;
    });
});
</script>
