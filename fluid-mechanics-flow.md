---
layout: default
title: Fluid Mechanics Flow
---

<script>
window.MathJax = {
  tex: { inlineMath: [['$','$'],['\\(','\\)']], displayMath: [['$$','$$'],['\\[','\\]']] },
  svg: { fontCache: 'global' }
};
</script>
<script async id="MathJax-script" src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js"></script>

<style>
    /* Defining CSS variables to match the new style */
    :root {
        --brand: #2563eb; /* A nice blue */
        --brand-hover: #1d4ed8; /* Darker blue for hover */
        --ring: #cbd5e0; /* A neutral gray for borders */
        --card-bg: #ffffff;
        --card-shadow: rgba(0,0,0,0.1);
        --text-color: #4a5568;
        --title-color: #1e3a8a;
    }

    /* Core card layout from reference */
    .card {
        background-color: var(--card-bg);
        border-radius: 8px;
        padding: 24px;
        margin-bottom: 24px;
        box-shadow: 0 4px 8px var(--card-shadow);
        border: 1px solid #e2e8f0;
    }
    .card h2 {
        margin-top: 0;
        color: var(--title-color);
    }
    .card p {
        color: var(--text-color);
        line-height: 1.6;
    }
    .pill {
        display: inline-block;
        background-color: #e0e7ff;
        color: #3730a3;
        padding: 4px 12px;
        border-radius: 9999px;
        font-size: 0.85em;
        font-weight: 600;
        margin-bottom: 16px;
    }

    /* Input and form styling from reference */
    .input-group {
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;
        margin-top: .6rem;
        align-items: flex-end; /* Aligns items to the bottom */
    }
    .input-box {
        padding: 8px;
        border-radius: 6px;
        border: 1px solid var(--ring);
        font-size: 1em;
    }
    .input-group label {
        font-size: 0.9em;
        margin-bottom: 4px;
        color: var(--text-color);
        display: block; /* Makes label take its own line */
    }
    .btn-calculate {
        background-color: var(--brand);
        color: white;
        border: none;
        padding: 9px 15px;
        border-radius: 6px;
        cursor: pointer;
        font-size: 1em;
        transition: background-color 0.2s;
    }
    .btn-calculate:hover {
        background-color: var(--brand-hover);
    }
    
    /* General styles */
    .formula {
        background-color: #f8fafc;
        padding: 15px;
        border-radius: 5px;
        margin: 20px 0;
        text-align: center;
        overflow-x: auto;
    }
    .output {
        margin-top: 20px;
        font-size: 1.1em;
        font-weight: bold;
        color: var(--title-color);
        background-color: #f0f4fa;
        padding: 15px;
        border-radius: 6px;
    }
</style>

<div class="container">

<div class="card" id="reynolds-card">
    <div class="pill">Flow Regime</div>
    <h2>Reynolds Number Calculator</h2>
    <p>The Reynolds number ($Re$) is a dimensionless quantity used to predict fluid flow patterns. It helps determine whether a flow is laminar, transitional, or turbulent.</p>
    <div class="formula">$$ Re = \frac{\rho V D_h}{\mu} $$</div>

    <div class="input-group">
        <div>
            <label for="re-fluid">Fluid</label>
            <select id="re-fluid" class="input-box fluid-selector">
                <option value="air">Air (20°C)</option>
                <option value="water">Water (20°C)</option>
                <option value="argon">Argon (20°C)</option>
                <option value="nitrogen">Nitrogen (20°C)</option>
                <option value="oxygen">Oxygen (20°C)</option>
            </select>
        </div>
        <div>
            <label>Density ($\rho$) [kg/m³]</label>
            <input type="number" id="re-density" class="input-box" style="width:120px;" value="1.204">
        </div>
        <div>
            <label>Dyn. Viscosity ($\mu$) [Pa·s]</label>
            <input type="number" id="re-viscosity" class="input-box" style="width:120px;" value="1.81e-5">
        </div>
        <div>
            <label>Velocity ($V$) [m/s]</label>
            <input type="number" id="re-velocity" placeholder="e.g., 20" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Hydraulic Diameter ($D_h$) [m]</label>
            <input type="number" id="re-length" placeholder="e.g., 0.1" class="input-box" style="width:120px;">
        </div>
        <div>
            <button id="calc-re" class="btn-calculate">Calculate</button>
        </div>
    </div>
    <div id="re-output" class="output" style="display:none;"></div>
</div>

<div class="card" id="mach-card">
    <div class="pill">Compressibility</div>
    <h2>Mach Number & Flow Regime</h2>
    <p>The Mach number ($M$) is the ratio of flow velocity to the local speed of sound. It quantifies the compressibility of a fluid flow.</p>
    <div class="formula">$$ M = \frac{V}{a} \quad \text{where for ideal gases,} \quad a = \sqrt{\gamma R T} $$</div>
    <div class="input-group">
        <div>
            <label for="mach-fluid">Fluid</label>
            <select id="mach-fluid" class="input-box fluid-selector">
                <option value="air">Air</option>
                <option value="water">Water</option>
                <option value="argon">Argon</option>
                <option value="nitrogen">Nitrogen</option>
                <option value="oxygen">Oxygen</option>
            </select>
        </div>
        <div>
            <label>Flow Velocity ($V$) [m/s]</label>
            <input type="number" id="mach-velocity" placeholder="e.g., 300" class="input-box" style="width:140px;">
        </div>
        <div id="mach-temp-group">
            <label>Temperature [°C]</label>
            <input type="number" id="mach-temp" value="15" class="input-box" style="width:100px;">
        </div>
        <div>
            <button id="calc-mach" class="btn-calculate">Calculate</button>
        </div>
    </div>
    <div id="mach-output" class="output" style="display:none;"></div>
</div>

<div class="card" id="continuity-card">
    <div class="pill">Conservation of Mass</div>
    <h2>Continuity Equation Solver</h2>
    <p>For an incompressible, steady flow, the continuity equation ($A_1 V_1 = A_2 V_2$) states that the mass flow rate is constant. Select which variable you wish to solve for.</p>
    <div class="formula">$$ A_1 V_1 = A_2 V_2 $$</div>
    <div class="input-group">
         <div>
            <label>Calculate for:</label>
            <select id="cont-solve-for" class="input-box">
                <option value="v2">Velocity at Point 2 (V₂)</option>
                <option value="a2">Area at Point 2 (A₂)</option>
                <option value="v1">Velocity at Point 1 (V₁)</option>
                <option value="a1">Area at Point 1 (A₁)</option>
            </select>
        </div>
        <div>
            <label>Area 1 ($A_1$) [m²]</label>
            <input type="number" id="cont-a1" placeholder="e.g., 0.2" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Velocity 1 ($V_1$) [m/s]</label>
            <input type="number" id="cont-v1" placeholder="e.g., 10" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Area 2 ($A_2$) [m²]</label>
            <input type="number" id="cont-a2" placeholder="e.g., 0.1" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Velocity 2 ($V_2$) [m/s]</label>
            <input type="number" id="cont-v2" class="input-box" style="width:120px;" disabled>
        </div>
         <div>
            <button id="calc-cont" class="btn-calculate">Calculate</button>
        </div>
    </div>
    <div id="cont-output" class="output" style="display:none;"></div>
</div>


<div class="card" id="bernoulli-card">
    <div class="pill">Conservation of Energy</div>
    <h2>Bernoulli's Equation Solver</h2>
    <p>For an inviscid flow, Bernoulli's principle relates pressure, velocity, and height. This solves for a property at a second point. (Assumes constant density).</p>
    <div class="formula">$$ p_1 + \frac{1}{2}\rho V_1^2 + \rho g h_1 = p_2 + \frac{1}{2}\rho V_2^2 + \rho g h_2 $$</div>
    <div class="input-group">
        <div>
            <label>Fluid Density ($\rho$) [kg/m³]</label>
            <input type="number" id="bern-rho" value="998" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Pressure 1 ($p_1$) [Pa]</label>
            <input type="number" id="bern-p1" placeholder="e.g., 101325" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Velocity 1 ($V_1$) [m/s]</label>
            <input type="number" id="bern-v1" placeholder="e.g., 2" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Height 1 ($h_1$) [m]</label>
            <input type="number" id="bern-h1" value="0" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Pressure 2 ($p_2$) [Pa]</label>
            <input type="number" id="bern-p2" placeholder="e.g., 90000" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Velocity 2 ($V_2$) [m/s]</label>
            <input type="number" id="bern-v2" placeholder="e.g., 10" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Height 2 ($h_2$) [m]</label>
            <input type="number" id="bern-h2" placeholder="e.g., 5" class="input-box" style="width:120px;">
        </div>
        <div>
            <button id="calc-bern" class="btn-calculate">Calculate Unknown</button>
        </div>
    </div>
    <p style="font-size:0.9em; margin-top:1rem;"><em>Instruction: Leave the field you want to calculate empty and fill in all others.</em></p>
    <div id="bern-output" class="output" style="display:none;"></div>
</div>

<div class="card" id="pipe-loss-card">
    <div class="pill">Internal Flow</div>
    <h2>Pipe Friction Head Loss</h2>
    <p>The Darcy-Weisbach equation calculates the pressure drop ($\Delta p$) or head loss ($h_L$) in a pipe due to friction.</p>
    <div class="formula">$$ \Delta p = f \frac{L}{D} \frac{\rho V^2}{2} \quad | \quad h_L = \frac{\Delta p}{\rho g} $$</div>
    <div class="input-group">
        <div>
            <label>Friction Factor ($f$)</label>
            <input type="number" id="loss-f" value="0.02" class="input-box" style="width:100px;">
        </div>
        <div>
            <label>Pipe Length ($L$) [m]</label>
            <input type="number" id="loss-l" placeholder="e.g., 100" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Pipe Diameter ($D$) [m]</label>
            <input type="number" id="loss-d" placeholder="e.g., 0.1" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Fluid Density ($\rho$) [kg/m³]</label>
            <input type="number" id="loss-rho" value="998" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Velocity ($V$) [m/s]</label>
            <input type="number" id="loss-v" placeholder="e.g., 2" class="input-box" style="width:120px;">
        </div>
        <div>
            <button id="calc-loss" class="btn-calculate">Calculate</button>
        </div>
    </div>
    <div id="loss-output" class="output" style="display:none;"></div>
</div>

<div class="card" id="lift-drag-card">
    <div class="pill">Aerodynamics</div>
    <h2>Lift & Drag Force Calculator</h2>
    <p>Calculates the aerodynamic lift and drag forces acting on a body. Dynamic pressure ($q$) is calculated first.</p>
    <div class="formula">$$ q = \frac{1}{2}\rho V^2 \quad | \quad L = C_L \cdot q \cdot A \quad | \quad D = C_D \cdot q \cdot A $$</div>
    <div class="input-group">
        <div>
            <label>Fluid Density ($\rho$) [kg/m³]</label>
            <input type="number" id="ld-rho" value="1.225" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Velocity ($V$) [m/s]</label>
            <input type="number" id="ld-v" placeholder="e.g., 80" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Ref. Area ($A$) [m²]</label>
            <input type="number" id="ld-a" placeholder="e.g., 15" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Lift Coeff. ($C_L$)</label>
            <input type="number" id="ld-cl" value="0.5" class="input-box" style="width:120px;">
        </div>
        <div>
            <label>Drag Coeff. ($C_D$)</label>
            <input type="number" id="ld-cd" value="0.05" class="input-box" style="width:120px;">
        </div>
        <div>
            <button id="calc-ld" class="btn-calculate">Calculate</button>
        </div>
    </div>
    <div id="ld-output" class="output" style="display:none;"></div>
</div>


</div> <script>
document.addEventListener('DOMContentLoaded', function () {
    const G = 9.80665; // Gravity
    
    // Expanded fluid properties database
    const fluidProperties = {
        'air':     { rho: 1.204,   mu: 1.81e-5,  gamma: 1.4,   R: 287.05 },
        'water':   { rho: 998,     mu: 1.002e-3, a: 1480 },
        'argon':   { rho: 1.633,   mu: 2.2e-5,   gamma: 1.667, R: 208.1 },
        'nitrogen':{ rho: 1.165,   mu: 1.76e-5,  gamma: 1.4,   R: 296.8 },
        'oxygen':  { rho: 1.331,   mu: 2.0e-5,   gamma: 1.4,   R: 259.8 }
    };
    
    // --- Helper function to show output
    function showOutput(el, content) {
        el.style.display = 'block';
        el.innerHTML = content;
        // Rerender MathJax if there are formulas in the output
        if (window.MathJax && window.MathJax.typesetPromise) {
            window.MathJax.typesetPromise([el]);
        }
    }

    // --- Fluid Selector Logic ---
    document.querySelectorAll('.fluid-selector').forEach(selector => {
        selector.addEventListener('change', function(event) {
            const selectedCard = event.target.closest('.card');
            const selectedFluid = event.target.value;
            const props = fluidProperties[selectedFluid];

            const densityInput = selectedCard.querySelector('input[id*="-density"]');
            const viscosityInput = selectedCard.querySelector('input[id*="-viscosity"]');
            
            if (densityInput && props.rho) densityInput.value = props.rho;
            if (viscosityInput && props.mu) viscosityInput.value = props.mu;

            // Special handling for Mach calculator temperature input
            if (selectedCard.id === 'mach-card') {
                const tempGroup = selectedCard.querySelector('#mach-temp-group');
                tempGroup.style.display = (selectedFluid !== 'water') ? 'block' : 'none';
            }
        });
    });
    // Trigger change on Mach card to set initial state
    document.getElementById('mach-fluid').dispatchEvent(new Event('change'));

    // --- Reynolds Number ---
    document.getElementById('calc-re').addEventListener('click', function() {
        const rho = parseFloat(document.getElementById('re-density').value);
        const V = parseFloat(document.getElementById('re-velocity').value);
        const L = parseFloat(document.getElementById('re-length').value);
        const mu = parseFloat(document.getElementById('re-viscosity').value);
        const outputEl = document.getElementById('re-output');

        if ([rho, V, L, mu].some(isNaN)) {
            return showOutput(outputEl, "Error: Please enter valid numbers in all fields.");
        }
        const re = (rho * V * L) / mu;
        let regime = (re < 2300) ? 'Laminar' : (re > 4000) ? 'Turbulent' : 'Transitional';
        showOutput(outputEl, `Reynolds Number (Re) = <strong>${re.toExponential(4)}</strong><br>Flow Regime: <strong>${regime}</strong> (Internal Flow)`);
    });

    // --- Mach Number ---
    document.getElementById('calc-mach').addEventListener('click', function() {
        const V = parseFloat(document.getElementById('mach-velocity').value);
        const fluid = document.getElementById('mach-fluid').value;
        const outputEl = document.getElementById('mach-output');

        if (isNaN(V)) {
            return showOutput(outputEl, "Error: Please enter a valid velocity.");
        }
        
        let a; // Speed of sound
        const props = fluidProperties[fluid];
        let soundSpeedDetails = "";

        if (fluid !== 'water') {
            const tempC = parseFloat(document.getElementById('mach-temp').value);
            if (isNaN(tempC)) {
                return showOutput(outputEl, "Error: Please enter a valid temperature.");
            }
            const tempK = tempC + 273.15;
            a = Math.sqrt(props.gamma * props.R * tempK);
            soundSpeedDetails = `Speed of Sound (a) = <strong>${a.toFixed(2)} m/s</strong><br>`;
        } else {
            a = props.a; // Use constant speed of sound for water
            soundSpeedDetails = `Speed of Sound (a) in Water &approx; <strong>${a} m/s</strong><br>`;
        }

        const mach = V / a;
        let regime = 'Subsonic';
        if (mach >= 0.8 && mach < 1.2) regime = 'Transonic';
        else if (mach >= 1.2 && mach < 5) regime = 'Supersonic';
        else if (mach >= 5) regime = 'Hypersonic';

        showOutput(outputEl, `${soundSpeedDetails}Mach Number (M) = <strong>${mach.toFixed(4)}</strong><br>Flow Regime: <strong>${regime}</strong>`);
    });

    // --- Continuity Equation (Flexible) ---
    const contInputs = {
        a1: document.getElementById('cont-a1'),
        v1: document.getElementById('cont-v1'),
        a2: document.getElementById('cont-a2'),
        v2: document.getElementById('cont-v2')
    };

    document.getElementById('cont-solve-for').addEventListener('change', function() {
        Object.values(contInputs).forEach(input => input.disabled = false); // Enable all
        contInputs[this.value].disabled = true; // Disable the one to be calculated
        contInputs[this.value].value = ''; // Clear it
    });

    document.getElementById('calc-cont').addEventListener('click', function() {
        const solveFor = document.getElementById('cont-solve-for').value;
        const outputEl = document.getElementById('cont-output');
        
        const a1 = parseFloat(contInputs.a1.value);
        const v1 = parseFloat(contInputs.v1.value);
        const a2 = parseFloat(contInputs.a2.value);
        const v2 = parseFloat(contInputs.v2.value);
        
        let result, resultVar, resultUnit;
        try {
            switch(solveFor) {
                case 'v2':
                    if ([a1,v1,a2].some(isNaN) || a2 === 0) throw new Error();
                    result = (a1 * v1) / a2; resultVar = 'V₂'; resultUnit = 'm/s';
                    break;
                case 'a2':
                    if ([a1,v1,v2].some(isNaN) || v2 === 0) throw new Error();
                    result = (a1 * v1) / v2; resultVar = 'A₂'; resultUnit = 'm²';
                    break;
                case 'v1':
                    if ([a2,v2,a1].some(isNaN) || a1 === 0) throw new Error();
                    result = (a2 * v2) / a1; resultVar = 'V₁'; resultUnit = 'm/s';
                    break;
                case 'a1':
                    if ([a2,v2,v1].some(isNaN) || v1 === 0) throw new Error();
                    result = (a2 * v2) / v1; resultVar = 'A₁'; resultUnit = 'm²';
                    break;
            }
            showOutput(outputEl, `Calculated Result: <strong>${resultVar} = ${result.toFixed(4)} ${resultUnit}</strong>`);
        } catch (e) {
            showOutput(outputEl, 'Error: Please provide valid inputs. Avoid division by zero.');
        }
    });

    // --- Bernoulli's Equation ---
    document.getElementById('calc-bern').addEventListener('click', function() {
        const rho = parseFloat(document.getElementById('bern-rho').value);
        const p1_val = document.getElementById('bern-p1').value;
        const v1_val = document.getElementById('bern-v1').value;
        const h1_val = document.getElementById('bern-h1').value;
        const p2_val = document.getElementById('bern-p2').value;
        const v2_val = document.getElementById('bern-v2').value;
        const h2_val = document.getElementById('bern-h2').value;
        const outputEl = document.getElementById('bern-output');

        const inputs = [p1_val, v1_val, h1_val, p2_val, v2_val, h2_val];
        const emptyFields = inputs.filter(v => v === '');
        
        if (isNaN(rho) || emptyFields.length !== 1) {
            return showOutput(outputEl, "Error: Please enter a valid density and leave exactly one other field empty to calculate.");
        }
        
        const p1 = parseFloat(p1_val), v1 = parseFloat(v1_val), h1 = parseFloat(h1_val);
        const p2 = parseFloat(p2_val), v2 = parseFloat(v2_val), h2 = parseFloat(h2_val);
        
        let result, resultVar, resultUnit;

        try {
            if (p2_val === '') {
                const term1 = p1 + 0.5 * rho * v1*v1 + rho * G * h1;
                result = term1 - (0.5 * rho * v2*v2 + rho * G * h2);
                resultVar = 'p₂'; resultUnit = 'Pa';
            } else if (v2_val === '') {
                const term1 = p1 + 0.5 * rho * v1*v1 + rho * G * h1;
                const intermediate = (term1 - p2 - rho * G * h2) * 2 / rho;
                if (intermediate < 0) throw new Error("Resulting velocity is imaginary. Check inputs.");
                result = Math.sqrt(intermediate);
                resultVar = 'V₂'; resultUnit = 'm/s';
            } else if (h2_val === '') {
                 const term1 = p1 + 0.5 * rho * v1*v1 + rho * G * h1;
                 result = (term1 - p2 - 0.5 * rho * v2*v2) / (rho * G);
                 resultVar = 'h₂'; resultUnit = 'm';
            } else { // Handle point 1 calculations similarly
                const term2 = p2 + 0.5 * rho * v2*v2 + rho * G * h2;
                if (p1_val === '') {
                    result = term2 - (0.5 * rho * v1*v1 + rho * G * h1);
                    resultVar = 'p₁'; resultUnit = 'Pa';
                } else if (v1_val === '') {
                    const intermediate = (term2 - p1 - rho * G * h1) * 2 / rho;
                    if (intermediate < 0) throw new Error("Resulting velocity is imaginary. Check inputs.");
                    result = Math.sqrt(intermediate);
                    resultVar = 'V₁'; resultUnit = 'm/s';
                } else if (h1_val === '') {
                    result = (term2 - p1 - 0.5 * rho * v1*v1) / (rho * G);
                    resultVar = 'h₁'; resultUnit = 'm';
                }
            }
            showOutput(outputEl, `Calculated Result: <strong>${resultVar} = ${result.toExponential(4)} ${resultUnit}</strong>`);

        } catch (e) {
            showOutput(outputEl, "Error: Invalid inputs provided. " + e.message);
        }
    });
    
    // --- Pipe Friction Head Loss ---
    document.getElementById('calc-loss').addEventListener('click', function() {
        const f = parseFloat(document.getElementById('loss-f').value);
        const L = parseFloat(document.getElementById('loss-l').value);
        const D = parseFloat(document.getElementById('loss-d').value);
        const rho = parseFloat(document.getElementById('loss-rho').value);
        const V = parseFloat(document.getElementById('loss-v').value);
        const outputEl = document.getElementById('loss-output');

        if ([f, L, D, rho, V].some(isNaN)) {
            return showOutput(outputEl, "Error: Please enter valid numbers in all fields.");
        }
        
        const delta_p = f * (L/D) * (rho * V*V / 2);
        const hL = delta_p / (rho * G);
        
        showOutput(outputEl, `Pressure Drop ($\Delta p$) = <strong>${delta_p.toExponential(4)} Pa</strong><br>
                               Head Loss ($h_L$) = <strong>${hL.toFixed(4)} m</strong>`);
    });

    // --- Lift & Drag ---
    document.getElementById('calc-ld').addEventListener('click', function() {
        const rho = parseFloat(document.getElementById('ld-rho').value);
        const V = parseFloat(document.getElementById('ld-v').value);
        const A = parseFloat(document.getElementById('ld-a').value);
        const CL = parseFloat(document.getElementById('ld-cl').value);
        const CD = parseFloat(document.getElementById('ld-cd').value);
        const outputEl = document.getElementById('ld-output');

        if ([rho, V, A, CL, CD].some(isNaN)) {
            return showOutput(outputEl, "Error: Please enter valid numbers in all fields.");
        }
        
        const q = 0.5 * rho * V * V;
        const lift = CL * q * A;
        const drag = CD * q * A;
        
        showOutput(outputEl, `Dynamic Pressure (q) = <strong>${q.toExponential(4)} Pa</strong><br>
                               Lift Force (L) = <strong>${lift.toExponential(4)} N</strong><br>
                               Drag Force (D) = <strong>${drag.toExponential(4)} N</strong>`);
    });

});
</script>
