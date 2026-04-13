---
layout: default
title: Santhosh Kumar Sankar | Aerospace Engineer
---

<script src="https://cdn.tailwindcss.com"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">

<script>
  document.documentElement.classList.add('dark')
  tailwind.config = {
    content: [],
    theme: {
      extend: {
        colors: {
          neon: '#00f5ff',
          deep: '#0a1428'
        }
      }
    }
  }
</script>

<div class="min-h-screen bg-gradient-to-br from-[#0a1428] via-[#001122] to-black text-white font-sans">

  <!-- Navbar -->
  <nav class="border-b border-white/10 backdrop-blur-lg bg-black/70 fixed w-full z-50">
    <div class="max-w-7xl mx-auto px-8 py-5 flex items-center justify-between">
      <a href="/" class="text-2xl font-bold tracking-tighter flex items-center gap-2">
        <span class="text-[#00f5ff]">SANTHOSH</span><span class="text-white">AERO</span>
      </a>
      <div class="flex items-center gap-8 text-sm uppercase tracking-widest">
        <a href="/" class="hover:text-[#00f5ff] transition">ABOUT</a>
        <a href="/aerodynamic-analysis" class="hover:text-[#00f5ff] transition">AERODYNAMICS</a>
        <a href="/tools" class="hover:text-[#00f5ff] transition">ENGINEERING TOOLS</a>
        <a href="https://www.linkedin.com/in/yourprofile" target="_blank" class="bg-[#00f5ff] text-black px-6 py-2 rounded-full font-bold hover:bg-white transition">CONNECT</a>
      </div>
    </div>
  </nav>

  <!-- Hero -->
  <div class="pt-28 pb-20 max-w-7xl mx-auto px-8">
    <div class="grid md:grid-cols-2 gap-12 items-center">
      <div>
        <h1 class="text-6xl md:text-7xl font-bold leading-none tracking-tighter">
          SANTHOSH KUMAR SANKAR
        </h1>
        <p class="mt-4 text-2xl text-[#00f5ff]">Aerospace Engineer • CFD & Aerodynamics Specialist</p>
        <p class="mt-6 text-lg max-w-md opacity-90">
          7+ years international R&amp;D | Reduced experimental setup time by <strong>60%</strong> with automation | 
          eVTOL ducts, microchannel flows, plasma jets
        </p>
        <div class="mt-10 flex gap-4">
          <a href="/Santhosh_CV.pdf" class="px-8 py-4 bg-[#00f5ff] text-black font-bold rounded-2xl hover:scale-105 transition flex items-center gap-2">
            <i class="fas fa-download"></i> DOWNLOAD CV
          </a>
          <a href="/aerodynamic-analysis" class="px-8 py-4 border border-white/30 rounded-2xl hover:border-[#00f5ff] hover:text-[#00f5ff] transition">EXPLORE WORK →</a>
        </div>
      </div>
      <div class="hidden md:block">
        <div class="bg-white/5 backdrop-blur-xl border border-white/10 rounded-3xl p-8 shadow-2xl">
          <p class="text-sm uppercase tracking-widest text-[#00f5ff]">Currently seeking</p>
          <p class="text-3xl font-light">Aerospace • Mechanical Design • R&amp;D roles in Sydney</p>
          <div class="mt-8 text-xs grid grid-cols-2 gap-4 opacity-75">
            <div>Full Unrestricted Work Rights</div>
            <div>NSW Driver Licence</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Quick Expertise -->
  <div class="max-w-7xl mx-auto px-8 py-16 border-t border-white/10">
    <h2 class="text-center text-[#00f5ff] text-sm tracking-[3px] mb-8">EXPERTISE</h2>
    <div class="grid md:grid-cols-4 gap-6 text-center">
      <div class="bg-white/5 p-6 rounded-3xl">External &amp; Internal Aerodynamics</div>
      <div class="bg-white/5 p-6 rounded-3xl">CFD (Ansys Fluent • OpenFOAM)</div>
      <div class="bg-white/5 p-6 rounded-3xl">Automated Experimental Systems</div>
      <div class="bg-white/5 p-6 rounded-3xl">eVTOL • UAV • Plasma Flows</div>
    </div>
  </div>

</div>
