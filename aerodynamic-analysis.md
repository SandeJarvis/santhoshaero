---
layout: default
title: Aerodynamic Analysis — Aerodynamics with Santhosh
---

<div class="card">
  <div class="pill">Category</div>
  <h1>Aerodynamic Analysis</h1>
  <p>External aerodynamics, unsteady flow behavior, and performance assessment for UAV/eVTOL and related systems.</p>
</div>

<div class="card" style="margin-top:1rem">
  <div class="pill">Find a Tool</div>
  <input id="search-aa" type="search" placeholder="Search tools (e.g., lift, drag, unsteady)…" style="width:100%;padding:.6rem;border-radius:10px;border:1px solid var(--ring);">
</div>

<div class="card" style="margin-top:1rem">
  <div class="pill">Tools</div>
  <div id="tools-aa" class="tools-grid" style="display:grid;grid-template-columns:repeat(auto-fill,minmax(240px,1fr));gap:12px;">
    <!-- Example placeholders (edit/replace later) -->
    <a class="tool-card" href="{{ '/tools/aerodynamics/lift' | relative_url }}" data-keywords="lift cl airfoil wing area dynamic pressure unsteady">
      <strong>Lift Calculator</strong><br><small>CL, L = ½ρV²SCL</small>
    </a>
    <a class="tool-card" href="{{ '/tools/aerodynamics/drag' | relative_url }}" data-keywords="drag cd parasite induced reynolds">
      <strong>Drag Calculator</strong><br><small>CD, Drag breakdown</small>
    </a>
    <a class="tool-card" href="{{ '/tools/aerodynamics/mach-compressibility' | relative_url }}" data-keywords="mach compressibility prandtl glauert wave">
      <strong>Mach &amp; Compressibility</strong><br><small>Subsonic corrections</small>
    </a>
  </div>
</div>

<div class="card" style="margin-top:1rem">
  <div class="pill">Data &amp; References</div>
  <p>Standard atmosphere, reference air properties, and validation snapshots will appear here.</p>
</div>

<div class="card" style="margin-top:1rem">
  <div class="pill">Notes</div>
  <p>Use this area for short derivations, assumptions, and quick references tied to the tools above.</p>
</div>

<script>
(function(){
  const q = document.getElementById('search-aa');
  const list = document.getElementById('tools-aa');
  if(!q || !list) return;
  const items = Array.from(list.querySelectorAll('.tool-card'));
  q.addEventListener('input', () => {
    const s = q.value.trim().toLowerCase();
    items.forEach(el => {
      const hay = (el.textContent + ' ' + (el.dataset.keywords||'')).toLowerCase();
      el.style.display = hay.includes(s) ? '' : 'none';
    });
  });
})();
</script>

