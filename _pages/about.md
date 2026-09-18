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
     ACMG INTERACTIVE COMPUTATIONAL MECHANICS BACKGROUND
     ========================================================= -->

<canvas id="acmg-mesh-background"></canvas>

<style>

#acmg-mesh-background {
  position: fixed;
  top: 0;
  left: 0;

  width: 100vw;
  height: 100vh;

  z-index: 0;

  pointer-events: none;

  background: transparent;
}


/*
 * Keep the actual webpage content above
 * the animated mesh.
 */

main,
.page,
.post,
.post-content,
.container {
  position: relative;
  z-index: 1;
}


/*
 * Very subtle mesh.
 */

#acmg-mesh-background {
  opacity: 0.75;
}


/*
 * Disable animation for users who
 * prefer reduced motion.
 */

@media (prefers-reduced-motion: reduce) {

  #acmg-mesh-background {
    display: none;
  }

}

</style>


<script>

(function () {

  const canvas =
    document.getElementById("acmg-mesh-background");

  if (!canvas) return;

  const ctx =
    canvas.getContext("2d");

  let width = 0;
  let height = 0;

  let points = [];

  let columns = 0;
  let rows = 0;

  let spacing = 60;


  /*
   * Mouse position
   */

  const mouse = {

    x: -1000,
    y: -1000,

    active: false

  };


  /*
   * Animation parameters
   */

  const settings = {

    /*
     * Distance between mesh nodes.
     *
     * Increase to make mesh less dense.
     */
    spacing: 45,


    /*
     * Radius around cursor
     * affected by deformation.
     */
    influenceRadius: 180,


    /*
     * Maximum displacement.
     */
    deformation: 55,


    /*
     * How quickly the mesh
     * returns to its original position.
     */
    relaxation: 0.065,


    /*
     * Very light gray lines.
     */
    lineColor:
      "rgba(110, 110, 110, 0.20)",


    /*
     * Extremely subtle nodes.
     */
    pointColor:
      "rgba(110, 110, 110, 0.18)",


    /*
     * Thin lines.
     */
    lineWidth: 0.65

  };


  /*
   * ========================================================
   * CREATE MESH
   * ========================================================
   */

  function createMesh() {

    points = [];

    spacing = settings.spacing;

    columns =
      Math.ceil(width / spacing) + 1;

    rows =
      Math.ceil(height / spacing) + 1;


    for (let j = 0; j < rows; j++) {

      for (let i = 0; i < columns; i++) {

        const x = i * spacing;
        const y = j * spacing;


        points.push({

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


  /*
   * ========================================================
   * RESIZE
   * ========================================================
   */

  function resizeCanvas() {

    width =
      window.innerWidth;

    height =
      window.innerHeight;


    const dpr =
      Math.min(
        window.devicePixelRatio || 1,
        2
      );


    canvas.width =
      width * dpr;

    canvas.height =
      height * dpr;


    canvas.style.width =
      width + "px";

    canvas.style.height =
      height + "px";


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
   * TRACK MOUSE
   * ========================================================
   */

  document.addEventListener(
    "mousemove",
    function (event) {

      mouse.x =
        event.clientX;

      mouse.y =
        event.clientY;

      mouse.active =
        true;

    }
  );


  /*
   * Stop deformation when
   * pointer leaves the browser.
   */

  document.addEventListener(
    "mouseleave",
    function () {

      mouse.active =
        false;

    }
  );


  /*
   * ========================================================
   * DEFORM EACH NODE
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

        /*
         * Smooth influence:
         *
         * 1.0 near cursor
         * 0.0 at influence boundary
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
           * Push the material
           * away from cursor.
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
     * Smooth relaxation.
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
     * Update points.
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
     * Line settings.
     */

    ctx.lineWidth =
      settings.lineWidth;

    ctx.strokeStyle =
      settings.lineColor;


    /*
     * ======================================================
     * HORIZONTAL LINES
     * ======================================================
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
     * ======================================================
     * VERTICAL LINES
     * ======================================================
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
     * ======================================================
     * SUBTLE NODES
     * ======================================================
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


    /*
     * Continue animation.
     */

    requestAnimationFrame(
      drawMesh
    );

  }


  /*
   * ========================================================
   * START
   * ========================================================
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
