---
layout: project_page
permalink: /

title: "PRISM: Latent Composition Consistency for Single-Image Reflection Removal"
authors: [
  "<a href='https://junsung6140.github.io/'>Junseong Shin<sup>1</sup></a>",
  "<a href='https://sites.google.com/view/lliger9/'>Tae Hyun Kim<sup>1,2</sup></a>"
]
affiliations:
    "<sup>1</sup>Hanyang University &nbsp;&nbsp; <sup>2</sup>VILAB"
conference: "<span style='font-weight:600;'>ECCV 2026</span>"

arxiv: "https://arxiv.org/abs/2606.31513"
paper: "https://arxiv.org/pdf/2606.31513"
code: "https://github.com/junsung6140/PRISM-SIRR"
---


<!-- ═══════════════════════════════════════════════════
     HERO: DAI vs PRISM comparison (JuxtaposeJS)
     ═══════════════════════════════════════════════════ -->

<div class="comparison-section">

  <!-- Thumbnail selector -->
  <div class="thumb-row">
    <img class="thumb active" src="./static/image/real/roma_input.jpg" data-idx="0" alt="Portrait">
    <img class="thumb" src="./static/image/real/chef_input.jpg" data-idx="1" alt="Chef">
    <img class="thumb" src="./static/image/real/lights_input.jpg" data-idx="2" alt="Lights">
  </div>

  <!-- Single Juxtapose container (rebuilt on thumbnail click) -->
  <div id="jx-wrap">
    <div id="jx-slider"></div>
  </div>

  <p class="comparison-caption">
    Drag the slider to compare <strong>DAI</strong> (left) vs <strong>PRISM (Ours)</strong> (right) on challenging in-the-wild images.
    <br>Click thumbnails above to switch images.
  </p>

</div>

<!-- Input → Transmission + Reflection triplets -->
<div class="result-gallery fade-in">
  <h3 style="text-align:center; margin-bottom:1rem;">PRISM decomposes each image into transmission and reflection</h3>
  <div class="result-triplet">
    <div class="result-img"><img src="./static/image/real/roma_input.jpg" alt="Input"><div class="result-label">Input</div></div>
    <div class="result-img"><img src="./static/image/real/roma_trans.jpg" alt="Transmission"><div class="result-label">Transmission</div></div>
    <div class="result-img"><img src="./static/image/real/roma_refl.jpg" alt="Reflection"><div class="result-label">Reflection</div></div>
  </div>
  <div class="result-triplet">
    <div class="result-img"><img src="./static/image/real/chef_input.jpg" alt="Input"><div class="result-label">Input</div></div>
    <div class="result-img"><img src="./static/image/real/chef_trans.jpg" alt="Transmission"><div class="result-label">Transmission</div></div>
    <div class="result-img"><img src="./static/image/real/chef_refl.jpg" alt="Reflection"><div class="result-label">Reflection</div></div>
  </div>
  <div class="result-triplet">
    <div class="result-img"><img src="./static/image/real/lights_input.jpg" alt="Input"><div class="result-label">Input</div></div>
    <div class="result-img"><img src="./static/image/real/lights_trans.jpg" alt="Transmission"><div class="result-label">Transmission</div></div>
    <div class="result-img"><img src="./static/image/real/lights_refl.jpg" alt="Reflection"><div class="result-label">Reflection</div></div>
  </div>
</div>

---

<!-- ═══════════════════════════════════════════════════
     ABSTRACT
     ═══════════════════════════════════════════════════ -->
<div class="columns is-centered has-text-centered">
    <div class="column is-four-fifths">
        <h2>Abstract</h2>
        <div class="content has-text-justified">
Single-image reflection removal (SIRR) seeks to recover the transmission layer from a mixture corrupted by reflections — a severely ill-posed problem. Existing methods operate in pixel space, where the nonlinear sRGB formation model entangles the two layers and limits generalization. We observe that pretrained VAE latent spaces exhibit substantially lower coherence between image layers compared to pixel space, providing a more favorable working space for decomposition. Building on this finding, we propose <strong>PRISM</strong> (<em>Pretrained-latent Reflection Image Separation Model</em>), which reinterprets SIRR as a latent linear separation problem. Under an approximate additive formulation in latent space, PRISM learns a flow matching velocity field on a pretrained FLUX backbone that recovers both transmission and reflection in a single forward pass. To enforce robust disentanglement, we introduce a <strong>Latent Composition Consistency (LCC)</strong> strategy that constructs synthetic mixtures by swapping reflection latents across samples and enforces consistent decomposition via a cycle loss. We further propose a <strong>Layer Contrastive Separation (LCS)</strong> loss that promotes semantic separation between layers through patch-level contrastive learning, without requiring explicit reflection targets. Experiments on six benchmarks demonstrate that PRISM consistently outperforms state-of-the-art methods by significant margins, with strong generalization to in-the-wild images.
        </div>
    </div>
</div>

---

## Key Idea

<div class="columns is-centered" style="align-items:center; gap:2rem;">
  <div class="column is-half">
    <div class="figure-wrapper fade-in">
      <img src="./static/image/cosine_scatter_paper.png" alt="Cosine similarity comparison between pixel space and latent space">
    </div>
  </div>
  <div class="column is-half">
    <div class="key-insight">
      <div class="key-insight-label">Why Latent Space?</div>
      In pixel space, transmission and reflection are highly entangled (avg. cos = <strong>0.74</strong>). In <strong>FLUX VAE latent space</strong>, this drops to <strong>0.07</strong> — broad decorrelation that makes linear separation feasible.
    </div>
  </div>
</div>

---

## Method

<div class="figure-wrapper fade-in">
  <img src="./static/image/overview2.png" alt="PRISM overview: flow matching on a pretrained FLUX backbone with LCC and LCS losses">
</div>

<div class="method-cards">
  <div class="method-card">
    <div class="method-card-title">Latent Composition Consistency (LCC)</div>
    <div class="method-card-desc">Constructs synthetic mixtures by <em>swapping reflection latents</em> across samples and enforces consistent decomposition via a cycle loss.</div>
  </div>
  <div class="method-card">
    <div class="method-card-title">Layer Contrastive Separation (LCS)</div>
    <div class="method-card-desc">Promotes semantic separation between layers through <em>patch-level contrastive learning</em>, without requiring explicit reflection targets.</div>
  </div>
</div>

---

## Benchmark Results

### Qualitative Comparison

<div class="figure-wrapper fade-in">
  <img src="./static/image/visual_comparison.png" alt="Qualitative comparison on six benchmarks">
</div>

### Reflection Recovery

<div class="figure-wrapper fade-in">
  <img src="./static/image/reflection_comparison.png" alt="Reflection recovery and in-the-wild generalization">
</div>

---

## Citation

<div class="citation-block">
<button class="copy-btn" onclick="copyBibtex()">
  <i class="fas fa-copy"></i> Copy BibTeX
</button>
<pre><code id="bibtex">@inproceedings{shin2026prism,
    title={PRISM: Latent Composition Consistency for Single-Image Reflection Removal},
    author={Junseong Shin and Tae Hyun Kim},
    booktitle={European Conference on Computer Vision (ECCV)},
    year={2026}
}</code></pre>
</div>

<script>
function copyBibtex() {
  var text = document.getElementById('bibtex').innerText;
  navigator.clipboard.writeText(text).then(function() {
    var btn = document.querySelector('.copy-btn');
    btn.innerHTML = '<i class="fas fa-check"></i> Copied!';
    setTimeout(function() {
      btn.innerHTML = '<i class="fas fa-copy"></i> Copy BibTeX';
    }, 2000);
  });
}

// ── JuxtaposeJS: build sliders and handle thumbnail switching ──
document.addEventListener('DOMContentLoaded', function() {

  var pairs = [
    { dai: './static/image/real/roma_dai.jpg',   ours: './static/image/real/roma_trans.jpg' },
    { dai: './static/image/real/chef_dai.jpg',   ours: './static/image/real/chef_trans.jpg' },
    { dai: './static/image/real/lights_dai.jpg', ours: './static/image/real/lights_trans.jpg' }
  ];

  // Build slider for a given index
  function buildSlider(idx) {
    var container = document.getElementById('jx-slider');
    // Clear previous slider
    container.innerHTML = '';
    var p = pairs[idx];
    new juxtapose.JXSlider('#jx-slider', [
      { src: p.dai,  label: 'DAI' },
      { src: p.ours, label: 'PRISM (Ours)' }
    ], {
      animate: true,
      showLabels: true,
      showCredits: false,
      startingPosition: '50%',
      makeResponsive: true
    });
  }

  // Initialize first slider
  buildSlider(0);

  // Thumbnail click → destroy & rebuild slider
  document.querySelectorAll('.thumb').forEach(function(thumb) {
    thumb.addEventListener('click', function() {
      var idx = parseInt(this.getAttribute('data-idx'));
      document.querySelectorAll('.thumb').forEach(function(t) { t.classList.remove('active'); });
      this.classList.add('active');
      buildSlider(idx);
    });
  });

  // ── Scroll fade-in ──
  var observer = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, { threshold: 0.1 });
  document.querySelectorAll('.fade-in').forEach(function(el) {
    observer.observe(el);
  });
});
</script>
