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
     REAL-WORLD DEMO — first thing visitors see
     ═══════════════════════════════════════════════════ -->

## See It In Action

<p style="text-align:center; color:#64748B; margin-bottom:1.5rem;">
Drag the slider to compare. All images are <strong>challenging in-the-wild photos</strong> — no model has seen them during training.
</p>

<!-- Slider 1: Cat -->
<div class="ba-slider" data-label-left="Input (with reflection)" data-label-right="PRISM output">
  <img src="./static/image/real/cat_input.jpg" alt="Input" class="ba-before">
  <img src="./static/image/real/cat_trans.jpg" alt="PRISM transmission output" class="ba-after">
  <div class="ba-handle">
    <div class="ba-handle-line"></div>
    <div class="ba-handle-circle"><span>&lsaquo; &rsaquo;</span></div>
    <div class="ba-handle-line"></div>
  </div>
</div>

<!-- Slider 2: Market -->
<div class="ba-slider" data-label-left="Input" data-label-right="Transmission">
  <img src="./static/image/real/market_input.jpg" alt="Input" class="ba-before">
  <img src="./static/image/real/market_trans.jpg" alt="PRISM transmission output" class="ba-after">
  <div class="ba-handle">
    <div class="ba-handle-line"></div>
    <div class="ba-handle-circle"><span>&lsaquo; &rsaquo;</span></div>
    <div class="ba-handle-line"></div>
  </div>
</div>

<!-- Gallery: more examples as triplets -->
<div class="result-gallery fade-in">
  <div class="result-triplet">
    <div class="result-img"><img src="./static/image/real/lights_input.jpg" alt="Input"><div class="result-label">Input</div></div>
    <div class="result-img"><img src="./static/image/real/lights_trans.jpg" alt="Transmission"><div class="result-label">Transmission</div></div>
    <div class="result-img"><img src="./static/image/real/lights_refl.jpg" alt="Reflection"><div class="result-label">Reflection</div></div>
  </div>
  <div class="result-triplet">
    <div class="result-img"><img src="./static/image/real/cafe_input.jpg" alt="Input"><div class="result-label">Input</div></div>
    <div class="result-img"><img src="./static/image/real/cafe_trans.jpg" alt="Transmission"><div class="result-label">Transmission</div></div>
    <div class="result-img"><img src="./static/image/real/cafe_refl.jpg" alt="Reflection"><div class="result-label">Reflection</div></div>
  </div>
  <div class="result-triplet">
    <div class="result-img"><img src="./static/image/real/street_input.jpg" alt="Input"><div class="result-label">Input</div></div>
    <div class="result-img"><img src="./static/image/real/street_trans.jpg" alt="Transmission"><div class="result-label">Transmission</div></div>
    <div class="result-img"><img src="./static/image/real/street_refl.jpg" alt="Reflection"><div class="result-label">Reflection</div></div>
  </div>
</div>

---

<!-- ═══════════════════════════════════════════════════
     ABSTRACT (collapsed, clean)
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

<!-- ═══════════════════════════════════════════════════
     KEY IDEA (brief)
     ═══════════════════════════════════════════════════ -->

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

// ── Before / After Slider ──
document.addEventListener('DOMContentLoaded', function() {
  document.querySelectorAll('.ba-slider').forEach(function(slider) {
    var before = slider.querySelector('.ba-before');
    var handle = slider.querySelector('.ba-handle');
    var isDragging = false;

    function setPosition(x) {
      var rect = slider.getBoundingClientRect();
      var pos = Math.max(0, Math.min(x - rect.left, rect.width));
      var pct = (pos / rect.width) * 100;
      before.style.clipPath = 'inset(0 ' + (100 - pct) + '% 0 0)';
      handle.style.left = pct + '%';
    }

    // Initialize at 50%
    before.style.clipPath = 'inset(0 50% 0 0)';
    handle.style.left = '50%';

    slider.addEventListener('mousedown', function(e) {
      isDragging = true;
      setPosition(e.clientX);
      e.preventDefault();
    });
    window.addEventListener('mousemove', function(e) {
      if (isDragging) setPosition(e.clientX);
    });
    window.addEventListener('mouseup', function() {
      isDragging = false;
    });

    // Touch support
    slider.addEventListener('touchstart', function(e) {
      isDragging = true;
      setPosition(e.touches[0].clientX);
    });
    window.addEventListener('touchmove', function(e) {
      if (isDragging) setPosition(e.touches[0].clientX);
    });
    window.addEventListener('touchend', function() {
      isDragging = false;
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
