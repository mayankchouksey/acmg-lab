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

<!-- =========================================================
     ACMG HOMEPAGE MICROSTRUCTURE HEADER
     ========================================================= -->

<section class="acmg-header">

  <div class="acmg-microstructure-container">

    <canvas id="acmg-microstructure"></canvas>

  </div>


  <div class="acmg-header-content">

    <h1>
      Applied Computational Mechanics Group
    </h1>

  <h2>
    <a href="https://me.iiti.ac.in/" target="_blank" rel="noopener">
      Department of Mechanical Engineering
    </a>
  </h2>

  <h2>
    <a href="https://www.iiti.ac.in/" target="_blank" rel="noopener">
      Indian Institute of Technology Indore
    </a>
  </h2>
    <div class="acmg-header-line"></div>

  </div>

</section>


<style>

/* =========================================================
   ACMG HEADER
   ========================================================= */

.acmg-header {

  position: relative;

  width: 100vw;

  /*
   * Extend the header to the complete
   * browser width instead of the normal
   * al-folio content width.
   */
  left: 50%;

  transform: translateX(-50%);

  /*
   * Header height.
   */
  height: 430px;

  display: flex;

  align-items: center;

  justify-content: center;

  background: #ffffff;

  margin: 0;

  /*
   * Allows the microstructure to extend
   * beyond the header boundaries.
   */
  overflow: visible;

  z-index: 1;

}


/* =========================================================
   MICROSTRUCTURE CONTAINER
   ========================================================= */

.acmg-microstructure-container {

  position: absolute;

  left: 0;

  /*
   * Extend upward behind the navbar.
   */
  top: -140px;

  /*
   * Extend downward into the photograph.
   */
  width: 100%;

  height: calc(100% + 220px);

  overflow: hidden;

  pointer-events: none;

  z-index: 0;


  /*
   * Gradual disappearance at the top
   * and bottom.
   */
  -webkit-mask-image:
    linear-gradient(
      to bottom,
      transparent 0%,
      rgba(0, 0, 0, 0.10) 7%,
      black 19%,
      black 82%,
      rgba(0, 0, 0, 0.55) 93%,
      transparent 100%
    );

  mask-image:
    linear-gradient(
      to bottom,
      transparent 0%,
      rgba(0, 0, 0, 0.10) 7%,
      black 19%,
      black 82%,
      rgba(0, 0, 0, 0.55) 93%,
      transparent 100%
    );

}


/* =========================================================
   CANVAS
   ========================================================= */

#acmg-microstructure {

  position: absolute;

  top: 0;

  left: 0;

  width: 100%;

  height: 100%;

  display: block;

}


/* =========================================================
   HEADER TEXT
   ========================================================= */

.acmg-header-content {

  position: relative;

  z-index: 2;

  width: 100%;

  padding: 40px 20px;

  text-align: center;

}


/*
 * ACMG name
 */

.acmg-header-content h1 {

  margin: 0 0 18px 0;

  font-size: 2.8rem;

  font-weight: 350;

  line-height: 1.2;

  letter-spacing: -0.015em;

}


/*
 * Department and institute
 */

.acmg-header-content h2 {

  margin: 6px 0;

  font-size: 1.45rem;

  font-weight: 350;

  line-height: 1.35;

}


/* =========================================================
   HORIZONTAL LINE
   ========================================================= */

.acmg-header-line {

  width: 280px;

  max-width: 45%;

  margin: 22px auto 0;

  border-top:
    1px solid
    rgba(80, 80, 80, 0.45);

}


/* =========================================================
   MOBILE
   ========================================================= */

@media (max-width: 600px) {

  .acmg-header {

    height: 350px;

  }


  .acmg-header-content {

    padding: 30px 15px;

  }


  .acmg-header-content h1 {

    font-size: 2rem;

    letter-spacing: -0.01em;

  }


  .acmg-header-content h2 {

    font-size: 1.15rem;

  }


  .acmg-header-line {

    width: 200px;

    max-width: 55%;

    margin-top: 18px;

  }

}


/* =========================================================
   REDUCED MOTION
   ========================================================= */

@media (prefers-reduced-motion: reduce) {

  .acmg-microstructure-container {

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


  /* =======================================================
     MOUSE
     ======================================================= */

  const mouse = {

    x: -1000,

    y: -1000,

    active: false

  };


  /* =======================================================
     MICROSTRUCTURE SETTINGS
     ======================================================= */

  const settings = {

    /*
     * Distance between material particles.
     *
     * 45 gives the relatively dense
     * microstructure you selected.
     */
    spacing: 45,


    /*
     * Randomness of particle positions.
     *
     * Larger = more irregular material.
     */
    irregularity: 14,


    /*
     * Radius of cursor influence.
     */
    influenceRadius: 200,


    /*
     * Maximum deformation.
     */
    deformation: 55,


    /*
     * Return speed.
     */
    relaxation: 0.045,


    /*
     * Particle size.
     */
    particleRadius: 1.8,


    /*
     * Particle visibility.
     */
    particleColor:
      "rgba(95, 95, 95, 0.28)",


    /*
     * Very subtle material connections.
     */
    connectionColor:
      "rgba(95, 95, 95, 0.13)",


    /*
     * Connection thickness.
     */
    lineWidth: 0.6

  };


  /* =======================================================
     CREATE MICROSTRUCTURE
     ======================================================= */

  function createParticles() {

    particles = [];


    const columns =
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
        i < columns;
        i++
      ) {

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

          /*
           * Original position
           */
          ox: x,

          oy: y,


          /*
           * Current position
           */
          x: x,

          y: y

        });

      }

    }

  }


  /* =======================================================
     RESIZE
     ======================================================= */

  function resizeCanvas() {

    const rect =
      canvas.getBoundingClientRect();


    width =
      rect.width;

    height =
      rect.height;


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


  /* =======================================================
     MOUSE MOVEMENT
     ======================================================= */

  document.addEventListener(
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


      mouse.active = true;

    }
  );


  /*
   * Stop deformation when the
   * cursor leaves the browser.
   */

  document.addEventListener(
    "mouseleave",
    function () {

      mouse.active = false;

    }
  );


  /* =======================================================
     DEFORM PARTICLE
     ======================================================= */

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

        /*
         * Smooth influence.
         */
        const normalized =
          1 -
          distance /
          settings.influenceRadius;


        const influence =
          normalized *
          normalized *
          normalized;


        if (distance > 0) {

          /*
           * Push material away
           * from cursor.
           */

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


    /*
     * Smooth return to the
     * undeformed configuration.
     */

    particle.x +=
      (targetX - particle.x) *
      settings.relaxation;


    particle.y +=
      (targetY - particle.y) *
      settings.relaxation;

  }


  /* =======================================================
     DRAW MICROSTRUCTURE
     ======================================================= */

  function drawMicrostructure() {

    ctx.clearRect(
      0,
      0,
      width,
      height
    );


    /*
     * Update all material particles.
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


    /* =====================================================
       DRAW CONNECTIONS
       ===================================================== */

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
         * Connect nearby particles.
         */

        if (
          distance <
          settings.spacing * 1.28
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


    /* =====================================================
       DRAW PARTICLES
       ===================================================== */

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


    /*
     * Continue animation.
     */

    requestAnimationFrame(
      drawMicrostructure
    );

  }


  /* =======================================================
     START
     ======================================================= */

  window.addEventListener(
    "resize",
    resizeCanvas
  );


  resizeCanvas();
  drawMicrostructure();


})();

</script>





<div style="text-align: center; margin: 20px 0 40px;">
<img src="{{ '/assets/img/6.jpg' | relative_url }}"
     style="width: 100%; max-width: 1100px; border-radius: 6px;"
     alt="Applied Computational Mechanics Group">
</div>

<p style="
  text-align: center; 
  font-size: 1.35rem;
  line-height: 1.6;
  margin: 5px auto 40px;
  max-width: 950px;
  ">
  Welcome to the Applied Computational Mechanics Group (ACMG)
  at the Indian Institute of Technology Indore.
</p>

---


### Computational Mechanics of Materials

The **Applied Computational Mechanics Group (ACMG)** at the Department of Mechanical Engineering, Indian Institute of Technology Indore, focuses on understanding and predicting the mechanical response of materials through computational mechanics, micromechanics, and numerical modelling.

Our research spans **deformation, plasticity, damage, fracture, and failure of materials** under a wide range of loading and environmental conditions.

---

## Research Areas

- **Micromechanics and Homogenization**
- **Plasticity and Constitutive Modelling**
- **Damage and Fracture Mechanics**
- **Dynamic and Extreme Loading**
- **Crystal Plasticity and Deformation Mechanisms**
- **Electro-chemo-mechanical Modelling of Materials**

---

## Research Philosophy

We develop computational frameworks that connect **material behaviour across length and time scales**, from microscale mechanisms to macroscopic response, with emphasis on physically motivated modelling and robust numerical methods.

---


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

<!--
## Group Leader

**Dr. Mayank Chouksey**  
Assistant Professor  
Department of Mechanical Engineering  
Indian Institute of Technology Indore
-->



<style>
.post-title {
  display: none !important;
}
</style>
