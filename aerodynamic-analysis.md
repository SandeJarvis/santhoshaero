---
layout: default
title: Aerodynamics
---

<script src="https://cdn.tailwindcss.com"></script>
<div class="min-h-screen bg-gradient-to-br from-[#0a1428] to-black text-white p-8">
  <div class="max-w-7xl mx-auto">
    <h1 class="text-5xl font-bold mb-8">Aerodynamics</h1>

    <div class="flex border-b border-white/20 mb-8">
      <button onclick="showTab(0)" id="tab0" class="px-8 py-4 border-b-4 border-[#00f5ff] text-[#00f5ff]">EXTERNAL AERODYNAMICS</button>
      <button onclick="showTab(1)" id="tab1" class="px-8 py-4">INTERNAL FLUID DYNAMICS</button>
    </div>

    <div id="content0">
      <h2 class="text-3xl">External Aerodynamics</h2>
      <p class="text-xl mt-4">UAV / eVTOL ducts, blades, fuselage, unsteady flows, flexible flaps, superhydrophobic surfaces.</p>
      <!-- Add your existing external content here -->
    </div>

    <div id="content1" class="hidden">
      <h2 class="text-3xl">Internal Fluid Dynamics</h2>
      <p class="text-xl mt-4">Microchannel gas flows, plasma jet research, CAPPJ/kINPen, free-jet studies.</p>
      <!-- Add your existing internal content here -->
    </div>
  </div>
</div>

<script>
function showTab(n) {
  document.getElementById('content0').classList.add('hidden')
  document.getElementById('content1').classList.add('hidden')
  document.getElementById('content' + n).classList.remove('hidden')
  document.querySelectorAll('button').forEach(b => b.classList.remove('border-b-4', 'border-[#00f5ff]', 'text-[#00f5ff]'))
  document.getElementById('tab' + n).classList.add('border-b-4', 'border-[#00f5ff]', 'text-[#00f5ff]')
}
</script>
