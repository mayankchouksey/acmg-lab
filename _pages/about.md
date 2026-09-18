---
layout: about
title: "ACMG"
permalink: /
subtitle: ""
selected_papers: false
social: false
announcements:
  enabled: false
latest_posts:
  enabled: false
---

<section class="acmg-header">

  <div class="acmg-microstructure-container">
    <canvas id="acmg-microstructure"></canvas>
  </div>

  <div class="acmg-header-content">

    <h1>Applied Computational Mechanics Group</h1>

    <h2>
      <a href="https://meche.iiti.ac.in/" target="_blank" rel="noopener">
        Department of Mechanical Engineering
      </a>
    </h2>

    <h2>
      <a href="https://www.iiti.ac.in/" target="_blank" rel="noopener">
        Indian Institute of Technology Indore
      </a>
    </h2>

  </div>

</section>

<style>

.acmg-header {
  position: relative;
  width: 100vw;
  left: 50%;
  transform: translateX(-50%);
  height: 430px;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: -20px;
  margin-bottom: 0;
}

/* --------------------------------------------------
   Microstructure animation
   -------------------------------------------------- */

.acmg-microstructure-container {
  position: absolute;
  z-index: 0;

  top: -140px;
  left: 0;

  width: 100%;
  height: calc(100% + 220px);

  overflow: hidden;

  -webkit-mask-image:
    linear-gradient(
      to bottom,
      transparent 0%,
      rgba(0,0,0,0.10) 7%,
      black 19%,
      black 82%,
      rgba(0,0,0,0.55) 93%,
      transparent 100%
    );

  mask-image:
    linear-gradient(
      to bottom,
      transparent 0%,
      rgba(0,0,0,0.10) 7%,
      black 19%,
      black 82%,
      rgba(0,0,0,0.55) 93%,
      transparent 100%
    );
}

#acmg-microstructure {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}

/* --------------------------------------------------
   Header text
   -------------------------------------------------- */

.acmg-header-content {
  position: relative;
  z-index: 2;
  text-align: center;
  background: rgba(255, 255, 255, 0.20);
  padding: 28px 45px 25px;
  border-radius: 4px;
  width: fit-content;
  max-width: 90%;

  margin: 0 auto;

  backdrop-filter: blur(1.5px);
  -webkit-backdrop-filter: blur(1.5px);
}

/* Group name */

.acmg-header-content h1 {
  margin: 0 0 18px 0;

  font-size: 2.8rem;
  font-weight: 350;
  line-height: 1.2;

  letter-spacing: -0.015em;

  color: rgba(20, 20, 20, 0.95);
}

/* Department + Institute */
/* <h2 style="font-size: 1.6rem; margin: 4px 0 25px; font-weight: 400;"> */

  
.acmg-header-content h2 {
  margin: 8px 0;

  font-size: 1.8rem;
  font-weight: 375;
  line-height: 1.4;

  color: rgba(35, 35, 35, 0.90);
}

/* Hyperlinks */

.acmg-header-content h2 a {
  color: inherit;
  text-decoration: none;
}

.acmg-header-content h2 a:hover {
  text-decoration: underline;
  text-underline-offset: 4px;
}

/* --------------------------------------------------
   Mobile
   -------------------------------------------------- */

@media (max-width: 600px) {

  .acmg-header {
    height: 350px;
  }

  .acmg-header-content {
    padding: 22px 25px 20px;
    max-width: 92%;
  }

  .acmg-header-content h1 {
    font-size: 2rem;
    margin-bottom: 14px;
  }

  .acmg-header-content h2 {
    font-size: 1.1rem;
    margin: 6px 0;
  }

}

</style>


<script>

(function () {

  const canvas = document.getElementById("acmg-microstructure");

  if (!canvas) return;

  const ctx = canvas.getContext("2d");

  let width;
  let height;

  let particles = [];

  const spacing = 45;
  const influenceRadius = 200;
  const deformation = 55;
  const relaxation = 0.045;

  const particleRadius = 1.8;

  const particleColor = "rgba(95, 95, 95, 0.28)";
  const connectionColor = "rgba(95, 95, 95, 0.13)";

  const lineWidth = 0.6;

  let mouse = {
    x: null,
    y: null
  };


  function resize() {

    const rect = canvas.getBoundingClientRect();

    width = rect.width;
    height = rect.height;

    const dpr = window.devicePixelRatio || 1;

    canvas.width = width * dpr;
    canvas.height = height * dpr;

    ctx.setTransform(dpr, 0, 0, dpr, 0, 0);

    createMicrostructure();
  }


  function createMicrostructure() {

    particles = [];

    const cols = Math.ceil(width / spacing) + 2;
    const rows = Math.ceil(height / spacing) + 2;

    for (let i = 0; i < cols; i++) {

      for (let j = 0; j < rows; j++) {

        const x =
          i * spacing -
          spacing +
          (Math.random() - 0.5) * spacing * 0.35;

        const y =
          j * spacing -
          spacing +
          (Math.random() - 0.5) * spacing * 0.35;

        particles.push({
          x: x,
          y: y,
          baseX: x,
          baseY: y,
          vx: 0,
          vy: 0
        });

      }
    }
  }


  function update() {

    particles.forEach(p => {

      let targetX = p.baseX;
      let targetY = p.baseY;

      if (mouse.x !== null) {

        const dx = p.baseX - mouse.x;
        const dy = p.baseY - mouse.y;

        const distance = Math.sqrt(dx * dx + dy * dy);

        if (distance < influenceRadius) {

          const influence =
            1 - distance / influenceRadius;

          const force =
            influence * influence * deformation;

          const angle =
            Math.atan2(dy, dx);

          targetX +=
            Math.cos(angle) * force;

          targetY +=
            Math.sin(angle) * force;

        }
      }

      p.vx +=
        (targetX - p.x) *
        relaxation;

      p.vy +=
        (targetY - p.y) *
        relaxation;

      p.vx *= 0.88;
      p.vy *= 0.88;

      p.x += p.vx;
      p.y += p.vy;

    });

  }


  function draw() {

    ctx.clearRect(0, 0, width, height);

    /* connections */

    ctx.strokeStyle = connectionColor;
    ctx.lineWidth = lineWidth;

    for (let i = 0; i < particles.length; i++) {

      const p = particles[i];

      for (let j = i + 1; j < particles.length; j++) {

        const q = particles[j];

        const dx = p.x - q.x;
        const dy = p.y - q.y;

        const distance =
          Math.sqrt(dx * dx + dy * dy);

        if (distance < spacing * 1.45) {

          ctx.beginPath();

          ctx.moveTo(p.x, p.y);
          ctx.lineTo(q.x, q.y);

          ctx.stroke();

        }

      }

    }


    /* particles */

    ctx.fillStyle = particleColor;

    particles.forEach(p => {

      ctx.beginPath();

      ctx.arc(
        p.x,
        p.y,
        particleRadius,
        0,
        Math.PI * 2
      );

      ctx.fill();

    });

  }


  function animate() {

    update();
    draw();

    requestAnimationFrame(animate);

  }

const header = document.querySelector(".acmg-header");
header.addEventListener("mousemove", function (event) {
  const rect =
    canvas.getBoundingClientRect();
  mouse.x =
    event.clientX - rect.left;
  mouse.y =
    event.clientY - rect.top;
});


header.addEventListener("mouseleave", function () {
  mouse.x = null;
  mouse.y = null;
});


  window.addEventListener("resize", resize);
  resize();
  animate();

})();

</script>







<div style="text-align: center; margin: 20px 0 40px;">
<img src="{{ '/assets/img/6.jpg' | relative_url }}"
     style="width: 100%; max-width: 1100px; border-radius: 6px;"
     alt="Applied Computational Mechanics Group">
</div>

<p style="
  text-align: center; 
  font-size: 1.45rem;
  line-height: 1.6;
  margin: 5px auto 40px;
  max-width: 950px;
  ">
  Welcome to the Applied Computational Mechanics Group (ACMG)
  at the Indian Institute of Technology Indore.
</p>
---



<!--
---
### Computational Mechanics of Materials

The **Applied Computational Mechanics Group (ACMG)** at the Department of Mechanical Engineering, Indian Institute of Technology Indore, focuses on understanding and predicting the mechanical response of materials through computational mechanics, micromechanics, and numerical modeling.

Our research spans **deformation, plasticity, damage, fracture, and failure of materials** under a wide range of loading and environmental conditions.
-->


<h2>What We Do at ACMG</h2>

Materials respond differently when they are stretched, compressed, heated, loaded quickly, or subjected to complex conditions. Understanding these responses helps us predict when and how materials will deform, become damaged, or eventually fail.

At ACMG, we use mechanics, mathematics, and computational methods to study these behaviors. We look at what happens inside materials at small scales and how these mechanisms influence their overall response. Our work covers deformation, plasticity, damage, fracture, and failure, including behavior under dynamic loading and in advanced materials and energy-storage systems.

In simple terms, we try to understand **why materials behave the way they do—and use that understanding to predict what happens next.**

<p>For a more detailed description of our research directions, please visit the <a href="{{ '/research/' | relative_url }}">Research</a> page.
</p>
---

<!--

<div style="text-align: center; margin-bottom: 30px;">
<h1 style="margin-bottom: 8px;">Applied Computational Mechanics Group</h1>
<h2 style="font-size: 1.6rem; margin: 4px 0; font-weight: 400;">
Department of Mechanical Engineering
</h2>
<h2 style="font-size: 1.6rem; margin: 4px 0 25px; font-weight: 400;">
Indian Institute of Technology Indore
</h2>
</div>
---
-->


<style>
.post-title {
  display: none !important;
}
</style>
