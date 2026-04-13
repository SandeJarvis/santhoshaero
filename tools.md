---
layout: default
title: Engineering Tools
---

<script src="https://cdn.tailwindcss.com"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf-lib/1.17.1/pdf-lib.min.js"></script>

<div class="min-h-screen bg-gradient-to-br from-[#0a1428] to-black text-white p-8">
  <div class="max-w-7xl mx-auto">
    <h1 class="text-5xl font-bold mb-8">Engineering Tools</h1>

    <div class="flex border-b border-white/20 mb-8">
      <button onclick="showToolTab(0)" id="toolTab0" class="px-8 py-4 border-b-4 border-[#00f5ff]">CALCULATORS</button>
      <button onclick="showToolTab(1)" id="toolTab1" class="px-8 py-4">PDF TOOLS</button>
    </div>

    <!-- Calculators Tab -->
    <div id="toolContent0">
      <div class="grid md:grid-cols-3 gap-8">
        <!-- Add your lift/drag/etc calculators with JS here – I can expand this if you want -->
        <div class="bg-white/5 p-8 rounded-3xl">Lift &amp; Drag Calculator (coming in next step)</div>
      </div>
    </div>

    <!-- PDF Tools Tab -->
    <div id="toolContent1" class="hidden">
      <h2 class="text-3xl mb-6">PDF Tools (All work in your browser – no upload to server)</h2>
      <input type="file" id="pdfFiles" multiple accept=".pdf" class="block mb-6">
      <button onclick="mergePDFs()" class="px-10 py-4 bg-[#00f5ff] text-black rounded-3xl font-bold">Merge Selected PDFs</button>
      <div id="pdfResult" class="mt-8"></div>
    </div>
  </div>
</div>

<script>
function showToolTab(n) {
  document.getElementById('toolContent0').classList.add('hidden')
  document.getElementById('toolContent1').classList.add('hidden')
  document.getElementById('toolContent' + n).classList.remove('hidden')
  // tab styling...
}

async function mergePDFs() {
  const files = document.getElementById('pdfFiles').files
  if (files.length < 2) { alert("Select at least 2 PDFs"); return; }
  const pdfDoc = await PDFLib.PDFDocument.create()
  for (let file of files) {
    const arrayBuffer = await file.arrayBuffer()
    const pdf = await PDFLib.PDFDocument.load(arrayBuffer)
    const copiedPages = await pdfDoc.copyPages(pdf, pdf.getPageIndices())
    copiedPages.forEach(page => pdfDoc.addPage(page))
  }
  const mergedPdfBytes = await pdfDoc.save()
  const blob = new Blob([mergedPdfBytes], { type: 'application/pdf' })
  const url = URL.createObjectURL(blob)
  document.getElementById('pdfResult').innerHTML = `<a href="${url}" download="merged.pdf" class="text-[#00f5ff]">✅ Download Merged PDF</a>`
}
</script>
