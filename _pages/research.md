---
layout: page
permalink: /research/
title: research
description: ""
nav: true
nav_order: 3
---


<!-- =========================================================
     ACMG INTERACTIVE MICROSTRUCTURE
     ========================================================= -->

<section class="acmg-microstructure-header">

  <canvas id="acmg-microstructure"></canvas>

  <div class="acmg-microstructure-content">

    <h1>Research</h1>

    <p>Computational Mechanics of Materials</p>

  </div>

</section>


<style>

/* =========================================================
   HEADER
   ========================================================= */

.acmg-microstructure-header {

  position: relative;

  width: 100vw;

  left: 50%;

  transform: translateX(-50%);

  height: 360px;

  display: flex;

  align-items: center;

  justify-content: center;

  overflow: hidden;

  background: #ffffff;

  margin-bottom: 40px;

}


/* =========================================================
   CANVAS
   ========================================================= */

#acmg-microstructure {

  position: absolute;

  inset: 0;

  width: 100%;

  height: 100%;

  z-index: 0;

}


/* =========================================================
   TEXT
   ========================================================= */

.acmg-microstructure-content {

  position: relative;

  z-index: 2;

  text-align: center;

  padding: 30px;

}


.acmg-microstructure-content h1 {

  margin: 0 0 12px;

  font-size: 2.8rem;

  font-weight: 400;

  letter-spacing: -0.015em;

}


.acmg-microstructure-content p {

  margin: 0;

  font-size: 1.1rem;

}


/* =========================================================
   MOBILE
   ========================================================= */

@media (max-width: 600px) {

  .acmg-microstructure-header {

    height: 300px;

  }

  .acmg-microstructure-content h1 {

    font-size: 2rem;

  }

}


/* =========================================================
   REDUCED MOTION
   ========================================================= */

@media (prefers-reduced-motion: reduce) {

  #acmg-microstructure {

    display: none;

  }

}

</style>


<script>

(function () {

  const canvas =
    document.getElementById(
      "acmg-microstructure"
    );

  if (!canvas) return;

  const ctx =
    canvas.getContext("2d");


  let width = 0;
  let height = 0;

  let particles = [];


  const mouse = {

    x: -1000,

    y: -1000,

    active: false

  };


  /*
   * ========================================================
   * SETTINGS
   * ========================================================
   */

  const settings = {

    /*
     * Distance between material particles.
     */
    spacing: 48,

    /*
     * Randomness of microstructure.
     */
    irregularity: 14,

    /*
     * Cursor influence.
     */
    influenceRadius: 170,

    /*
     * Deformation.
     */
    deformation: 45,

    /*
     * Relaxation.
     */
    relaxation: 0.055,

    /*
     * Particle size.
     */
    particleRadius: 2.0,

    /*
     * Particle visibility.
     */
    particleColor:
      "rgba(100, 100, 100, 0.30)",

    /*
     * Grain connection visibility.
     */
    connectionColor:
      "rgba(100, 100, 100, 0.12)",

    lineWidth: 0.6

  };


  /*
   * ========================================================
   * CREATE MICROSTRUCTURE
   * ========================================================
   */

  function createParticles() {

    particles = [];


    const cols =
      Math.ceil(
        width /
        settings.spacing
      ) + 1;


    const rows =
      Math.ceil(
        height /
        settings.spacing
      ) + 1;


    for (
      let j = 0;
      j < rows;
      j++
    ) {

      for (
        let i = 0;
        i < cols;
        i++
      ) {

        /*
         * Slightly randomize
         * the material positions.
         */

        const x =
          i *
          settings.spacing +
          (Math.random() - 0.5) *
          settings.irregularity;


        const y =
          j *
          settings.spacing +
          (Math.random() - 0.5) *
          settings.irregularity;


        particles.push({

          ox: x,
          oy: y,

          x: x,
          y: y

        });

      }

    }

  }


  /*
   * ========================================================
   * RESIZE
   * ========================================================
   */

  function resizeCanvas() {

    width =
      canvas.clientWidth;

    height =
      canvas.clientHeight;


    const dpr =
      Math.min(
        window.devicePixelRatio || 1,
        2
      );


    canvas.width =
      width * dpr;

    canvas.height =
      height * dpr;


    ctx.setTransform(
      dpr,
      0,
      0,
      dpr,
      0,
      0
    );


    createParticles();

  }


  /*
   * ========================================================
   * MOUSE
   * ========================================================
   */

  canvas.parentElement.addEventListener(
    "mousemove",
    function (event) {

      const rect =
        canvas.getBoundingClientRect();


      mouse.x =
        event.clientX -
        rect.left;

      mouse.y =
        event.clientY -
        rect.top;


      mouse.active =
        true;

    }
  );


  canvas.parentElement.addEventListener(
    "mouseleave",
    function () {

      mouse.active =
        false;

    }
  );


  /*
   * ========================================================
   * DEFORM PARTICLE
   * ========================================================
   */

  function deformParticle(
    particle
  ) {

    let targetX =
      particle.ox;

    let targetY =
      particle.oy;


    if (mouse.active) {

      const dx =
        particle.ox -
        mouse.x;


      const dy =
        particle.oy -
        mouse.y;


      const distance =
        Math.sqrt(
          dx * dx +
          dy * dy
        );


      if (
        distance <
        settings.influenceRadius
      ) {

        const normalized =
          1 -
          distance /
          settings.influenceRadius;


        const influence =
          normalized *
          normalized *
          normalized;


        if (distance > 0) {

          targetX +=
            (dx / distance) *
            settings.deformation *
            influence;


          targetY +=
            (dy / distance) *
            settings.deformation *
            influence;

        }

      }

    }


    particle.x +=
      (targetX - particle.x) *
      settings.relaxation;


    particle.y +=
      (targetY - particle.y) *
      settings.relaxation;

  }


  /*
   * ========================================================
   * DRAW
   * ========================================================
   */

  function drawMicrostructure() {

    ctx.clearRect(
      0,
      0,
      width,
      height
    );


    /*
     * Update particles.
     */

    for (
      let i = 0;
      i < particles.length;
      i++
    ) {

      deformParticle(
        particles[i]
      );

    }


    /*
     * ======================================================
     * CONNECTIONS
     * ======================================================
     */

    ctx.strokeStyle =
      settings.connectionColor;

    ctx.lineWidth =
      settings.lineWidth;


    for (
      let i = 0;
      i < particles.length;
      i++
    ) {

      const p =
        particles[i];


      for (
        let j = i + 1;
        j < particles.length;
        j++
      ) {

        const q =
          particles[j];


        const dx =
          p.x - q.x;

        const dy =
          p.y - q.y;


        const distance =
          Math.sqrt(
            dx * dx +
            dy * dy
          );


        /*
         * Connect only nearby
         * particles.
         */

        if (
          distance <
          settings.spacing * 1.35
        ) {

          ctx.beginPath();

          ctx.moveTo(
            p.x,
            p.y
          );

          ctx.lineTo(
            q.x,
            q.y
          );

          ctx.stroke();

        }

      }

    }


    /*
     * ======================================================
     * PARTICLES
     * ======================================================
     */

    ctx.fillStyle =
      settings.particleColor;


    for (
      let i = 0;
      i < particles.length;
      i++
    ) {

      const p =
        particles[i];


      ctx.beginPath();


      ctx.arc(
        p.x,
        p.y,
        settings.particleRadius,
        0,
        Math.PI * 2
      );


      ctx.fill();

    }


    requestAnimationFrame(
      drawMicrostructure
    );

  }


  /*
   * START
   */

  window.addEventListener(
    "resize",
    resizeCanvas
  );


  resizeCanvas();

  drawMicrostructure();


})();

</script>









<div class="page-header-clean">
  <h1>Research</h1>
  <p>
    Computational Mechanics of Materials
  </p>
</div>

<div class="page-header-line"></div>

<p class="research-intro">
  The Applied Computational Mechanics Group (ACMG) develops computational
  and theoretical approaches to understand, model, and predict the
  mechanical behaviour of materials across length and time scales.
  Our research combines mechanics, numerical methods, and material
  modelling to investigate deformation, damage, and failure under
  complex loading conditions.
</p>

<h2>Research Areas</h2>

<div class="research-area">

  <h3>Micromechanics &amp; Homogenization</h3>

  <p>
    Development of computational and theoretical approaches for
    understanding the effective mechanical response of heterogeneous
    materials. Research focuses on microstructure–property relationships,
    homogenization, and multiscale descriptions of material behaviour.
  </p>

</div>

<div class="research-area">

  <h3>Plasticity &amp; Constitutive Modelling</h3>

  <p>
    Development of constitutive models for plastic deformation under
    complex loading conditions. Particular emphasis is placed on
    non-proportional loading, loading-path effects, rate dependence,
    and the evolution of material behaviour.
  </p>

</div>

<div class="research-area">

  <h3>Damage &amp; Fracture Mechanics</h3>

  <p>
    Computational investigation of damage initiation, evolution,
    void growth, coalescence, and fracture. The research aims to
    connect microscale mechanisms of material degradation with
    macroscopic failure behaviour.
  </p>

</div>

<div class="research-area">

  <h3>Dynamic &amp; Extreme Loading</h3>

  <p>
    Investigation of material behaviour under high strain rates and
    dynamic loading conditions. Research considers the roles of
    inertia, rate sensitivity, thermal effects, and loading history
    in deformation and failure.
  </p>

</div>

<div class="research-area">

  <h3>Crystal Plasticity &amp; Deformation Mechanisms</h3>

  <p>
    Computational study of deformation mechanisms in crystalline
    materials, including crystallographic slip, anisotropy, and
    microstructure-driven deformation. The research seeks to relate
    crystal-scale mechanisms to the macroscopic mechanical response.
  </p>

</div>

<div class="research-area">

  <h3>Electro-chemo-mechanical Modelling</h3>

  <p>
    Development of multiphysics approaches for studying the coupled
    mechanical, electrochemical, and transport behaviour of energy
    storage materials. Particular interest lies in understanding
    deformation, damage, and failure in battery electrodes.
  </p>

</div>

<h2>Research Approach</h2>

<p>
  Our research integrates continuum mechanics, computational
  modelling, numerical methods, and micromechanical approaches.
  Depending on the problem, these methods are combined with
  experimental observations to develop physically informed models
  capable of describing material behaviour under realistic loading
  conditions.
</p>

<style>
.post-title {
  display: none;
}

.page-header-clean {
  text-align: center;
  margin-top: 5px;
  margin-bottom: 28px;
}

.page-header-clean h1 {
  font-size: 2.4rem;
  font-weight: 400;
  margin-bottom: 12px;
}

.page-header-clean p {
  max-width: 720px;
  margin: 0 auto;
  font-size: 1.05rem;
  line-height: 1.6;
}

.page-header-line {
  border-bottom: 2px solid var(--global-text-color);
  margin-bottom: 38px;
}

.research-intro {
  max-width: 900px;
  margin-bottom: 38px;
  line-height: 1.7;
}

.post-content h2 {
  margin-top: 38px;
  margin-bottom: 20px;
}

.research-area {
  max-width: 900px;
  margin-bottom: 28px;
}

.research-area h3 {
  margin-bottom: 8px;
  font-size: 1.25rem;
  font-weight: 500;
}

.research-area p {
  margin-top: 0;
  line-height: 1.7;
}

@media (max-width: 600px) {
  .page-header-clean h1 {
    font-size: 2rem;
  }

  .research-area h3 {
    font-size: 1.15rem;
  }
}
</style>
