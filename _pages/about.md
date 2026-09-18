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
     ACMG HEADER WITH INTERACTIVE MESH
     ========================================================= -->

<section class="acmg-header">

  <canvas id="acmg-mesh"></canvas>

  <div class="acmg-header-content">

    <h1>Applied Computational Mechanics Group</h1>

    <h2>
      Department of Mechanical Engineering
    </h2>

    <h2>
      Indian Institute of Technology Indore
    </h2>

  </div>

</section>


<style>

/* =========================================================
   ACMG HEADER
   ========================================================= */

.acmg-header {
  position: relative;

  width: 100%;
  min-height: 300px;

  display: flex;
  align-items: center;
  justify-content: center;

  overflow: hidden;

  background: #ffffff;

  margin-bottom: 20px;
}


/* =========================================================
   CANVAS
   ========================================================= */

#acmg-mesh {
  position: absolute;

  top: 0;
  left: 0;

  width: 100%;
  height: 100%;

  z-index: 0;

  pointer-events: none;
}


/* =========================================================
   HEADER TEXT
   ========================================================= */

.acmg-header-content {
  position: relative;

  z-index: 2;

  width: 100%;

  padding: 55px 20px;

  text-align: center;
}


.acmg-header-content h1 {
  margin: 0 0 8px 0;

  font-size: 2.4rem;

  font-weight: 400;

  line-height: 1.2;
}


.acmg-header-content h2 {
  margin: 4px 0;

  font-size: 1.6rem;

  font-weight: 400;

  line-height: 1.35;
}


/* =========================================================
   MOBILE
   ========================================================= */

@media (max-width: 600px) {

  .acmg-header {
    min-height: 260px;
  }

  .acmg-header-content {
    padding: 45px 15px;
  }

  .acmg-header-content h1 {
    font-size: 1.9rem;
  }

  .acmg-header-content h2 {
    font-size: 1.15rem;
  }

}


/* =========================================================
   REDUCED MOTION
   ========================================================= */

@media (prefers-reduced-motion: reduce) {

  #acmg-mesh {
    display: none;
  }

}

</style>


<script>

(function () {

  const canvas =
    document.getElementById("acmg-mesh");

  if (!canvas) return;

  const ctx =
    canvas.getContext("2d");


  let width = 0;
  let height = 0;

  let points = [];

  let columns = 0;
  let rows = 0;


  /*
   * ========================================================
   * MESH PARAMETERS
   * ========================================================
   *
   * These are the values you selected.
   */

  const settings = {

    spacing: 45,

    influenceRadius: 180,

    deformation: 55,

    relaxation: 0.065,

    lineColor:
      "rgba(110, 110, 110, 0.20)",

    pointColor:
      "rgba(110, 110, 110, 0.18)",

    lineWidth: 0.7

  };


  /*
   * Mouse
   */

  const mouse = {

    x: -1000,

    y: -1000,

    active: false

  };


  /*
   * ========================================================
   * CREATE MESH
   * ========================================================
   */

  function createMesh() {

    points = [];

    columns =
      Math.ceil(width / settings.spacing) + 1;

    rows =
      Math.ceil(height / settings.spacing) + 1;


    for (let j = 0; j < rows; j++) {

      for (let i = 0; i < columns; i++) {

        const x =
          i * settings.spacing;

        const y =
          j * settings.spacing;


        points.push({

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


    createMesh();

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
        event.clientX - rect.left;

      mouse.y =
        event.clientY - rect.top;

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
   * DEFORM POINT
   * ========================================================
   */

  function deformPoint(point) {

    let targetX =
      point.ox;

    let targetY =
      point.oy;


    if (mouse.active) {

      const dx =
        point.ox - mouse.x;

      const dy =
        point.oy - mouse.y;


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


    /*
     * Return smoothly to
     * undeformed configuration.
     */

    point.x +=
      (targetX - point.x) *
      settings.relaxation;


    point.y +=
      (targetY - point.y) *
      settings.relaxation;

  }


  /*
   * ========================================================
   * DRAW MESH
   * ========================================================
   */

  function drawMesh() {

    ctx.clearRect(
      0,
      0,
      width,
      height
    );


    /*
     * Update points
     */

    for (
      let i = 0;
      i < points.length;
      i++
    ) {

      deformPoint(
        points[i]
      );

    }


    /*
     * Line appearance
     */

    ctx.lineWidth =
      settings.lineWidth;

    ctx.strokeStyle =
      settings.lineColor;


    /*
     * Horizontal lines
     */

    for (
      let j = 0;
      j < rows;
      j++
    ) {

      ctx.beginPath();


      for (
        let i = 0;
        i < columns;
        i++
      ) {

        const index =
          j * columns + i;


        const point =
          points[index];


        if (i === 0) {

          ctx.moveTo(
            point.x,
            point.y
          );

        } else {

          ctx.lineTo(
            point.x,
            point.y
          );

        }

      }


      ctx.stroke();

    }


    /*
     * Vertical lines
     */

    for (
      let i = 0;
      i < columns;
      i++
    ) {

      ctx.beginPath();


      for (
        let j = 0;
        j < rows;
        j++
      ) {

        const index =
          j * columns + i;


        const point =
          points[index];


        if (j === 0) {

          ctx.moveTo(
            point.x,
            point.y
          );

        } else {

          ctx.lineTo(
            point.x,
            point.y
          );

        }

      }


      ctx.stroke();

    }


    /*
     * Nodes
     */

    ctx.fillStyle =
      settings.pointColor;


    for (
      let i = 0;
      i < points.length;
      i++
    ) {

      const point =
        points[i];


      ctx.beginPath();


      ctx.arc(
        point.x,
        point.y,
        1.1,
        0,
        Math.PI * 2
      );


      ctx.fill();

    }


    requestAnimationFrame(
      drawMesh
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

  drawMesh();


})();

</script>












<div style="text-align: center; margin-bottom: 30px;">

<h1 style="margin-bottom: 8px;">Applied Computational Mechanics Group</h1>

<h2 style="font-size: 1.6rem; margin: 4px 0; font-weight: 400;">
Department of Mechanical Engineering
</h2>

<h2 style="font-size: 1.6rem; margin: 4px 0 25px; font-weight: 400;">
Indian Institute of Technology Indore
</h2>

</div>

<div style="text-align: center; margin: 20px 0 40px;">

<img src="{{ '/assets/img/6.jpg' | relative_url }}"
     style="width: 100%; max-width: 1100px; border-radius: 6px;"
     alt="Applied Computational Mechanics Group">

</div>

<p style="text-align: center; font-size: 1.15rem; margin: 0 0 35px 0;">
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
