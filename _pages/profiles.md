---
layout: page
permalink: /people/
title: "team"
description: ""
nav: true
nav_order: 2
---

<!-- =========================================================
     ACMG STRESS / STRAIN FIELD
     ========================================================= -->

<section class="acmg-field-header">

  <canvas id="acmg-stress-field"></canvas>

  <div class="acmg-field-content">

    <h1>Our Team</h1>

    <p>
       Our group brings together researchers and students working on computational mechanics and the mechanics of materials, with a focus on understanding and predicting material behavior.
    </p>

  </div>

</section>


<style>

/* =========================================================
   HEADER
   ========================================================= */

.acmg-field-header {

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

#acmg-stress-field {

  position: absolute;

  inset: 0;

  width: 100%;

  height: 100%;

  z-index: 0;

}


/* =========================================================
   TEXT
   ========================================================= */

.acmg-field-content {

  position: relative;

  z-index: 2;

  text-align: center;

  padding: 30px;

}


.acmg-field-content h1 {

  margin: 0 0 12px;

  font-size: 2.8rem;

  font-weight: 400;

  letter-spacing: -0.015em;

}


.acmg-field-content p {

  margin: 0;

  font-size: 1.1rem;

  line-height: 1.6;

}


/* =========================================================
   MOBILE
   ========================================================= */

@media (max-width: 600px) {

  .acmg-field-header {

    height: 300px;

  }

  .acmg-field-content h1 {

    font-size: 2rem;

  }

  .acmg-field-content p {

    font-size: 1rem;

  }

}


/* =========================================================
   REDUCED MOTION
   ========================================================= */

@media (prefers-reduced-motion: reduce) {

  #acmg-stress-field {

    display: none;

  }

}

</style>


<script>

(function () {

  const canvas =
    document.getElementById("acmg-stress-field");

  if (!canvas) return;

  const ctx =
    canvas.getContext("2d");


  let width = 0;
  let height = 0;


  const mouse = {

    x: -1000,

    y: -1000,

    active: false

  };


  /*
   * ========================================================
   * FIELD SETTINGS
   * ========================================================
   */

  const settings = {

    /*
     * Number of contour lines.
     */
    lines: 18,

    /*
     * Vertical separation.
     */
    spacing: 22,

    /*
     * Cursor influence.
     */
    influenceRadius: 220,

    /*
     * Deformation magnitude.
     */
    deformation: 65,

    /*
     * Smoothness of return.
     */
    relaxation: 0.045,

    /*
     * Subtle gray contour lines.
     */
    lineColor:
      "rgba(100, 100, 100, 0.20)",

    lineWidth: 0.75

  };


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

      mouse.active = true;

    }
  );


  canvas.parentElement.addEventListener(
    "mouseleave",
    function () {

      mouse.active = false;

    }
  );


  /*
   * ========================================================
   * FIELD DEFORMATION
   * ========================================================
   */

  function displacement(x, y) {

    if (!mouse.active) {

      return {
        x: 0,
        y: 0
      };

    }


    const dx =
      x - mouse.x;

    const dy =
      y - mouse.y;


    const distance =
      Math.sqrt(
        dx * dx +
        dy * dy
      );


    if (
      distance >
      settings.influenceRadius
    ) {

      return {
        x: 0,
        y: 0
      };

    }


    const normalized =
      1 -
      distance /
      settings.influenceRadius;


    const influence =
      normalized *
      normalized *
      normalized;


    if (distance === 0) {

      return {
        x: 0,
        y: 0
      };

    }


    return {

      x:
        (dx / distance) *
        settings.deformation *
        influence,

      y:
        (dy / distance) *
        settings.deformation *
        influence

    };

  }


  /*
   * ========================================================
   * DRAW FIELD
   * ========================================================
   */

  function drawField() {

    ctx.clearRect(
      0,
      0,
      width,
      height
    );


    ctx.strokeStyle =
      settings.lineColor;

    ctx.lineWidth =
      settings.lineWidth;


    /*
     * Draw curved contour lines.
     */

    for (
      let l = 0;
      l < settings.lines;
      l++
    ) {

      const baseY =
        35 +
        l * settings.spacing;


      ctx.beginPath();


      for (
        let x = -20;
        x <= width + 20;
        x += 8
      ) {

        /*
         * Smooth sinusoidal
         * background field.
         */

        const wave =
          Math.sin(
            x * 0.008 +
            l * 0.35
          ) * 8;


        const y =
          baseY +
          wave;


        const d =
          displacement(
            x,
            y
          );


        const finalX =
          x + d.x;

        const finalY =
          y + d.y;


        if (x === -20) {

          ctx.moveTo(
            finalX,
            finalY
          );

        } else {

          ctx.lineTo(
            finalX,
            finalY
          );

        }

      }


      ctx.stroke();

    }


    requestAnimationFrame(
      drawField
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

  drawField();

})();

</script>







<!-- ============================================================
     PAGE HEADER
     ============================================================ -->
<!--
<div class="page-header-clean">
  <h1>Our Team</h1>
  <p>
    Our group brings together researchers and students working on computational mechanics and the mechanics of materials, with a focus on understanding and predicting material behavior.
  </p>
</div>
<div class="page-header-line"></div>
-->

<!-- ============================================================
     GROUP LEADER
     ============================================================ -->

<div class="pi-profile">

  <!-- PI PHOTO -->
  <div class="pi-photo">
    <img src="{{ '/assets/img/6.jpg' | relative_url }}"
         alt="Dr. Mayank Chouksey">
  </div>

  <!-- PI INFORMATION -->
  <div class="pi-info">

    <h2>Dr. Mayank Chouksey</h2>

    <p class="pi-position">
      Assistant Professor
    </p>

    <p class="pi-affiliation">
      Department of Mechanical Engineering<br>
      Indian Institute of Technology Indore
    </p>

    <div class="pi-bio">

      <p>
        Dr. Mayank Chouksey is an Assistant Professor in the Department of
        Mechanical Engineering at the Indian Institute of Technology Indore.
        His research focuses on computational mechanics and the mechanics
        of materials, with emphasis on physically motivated modelling and
        numerical methods.
      </p>

      <p>
        His research interests include micromechanics and homogenization,
        plasticity and constitutive modelling, damage and fracture mechanics,
        dynamic and extreme loading, crystal plasticity, and
        electro-chemo-mechanical modelling of materials.
      </p>

    </div>


    <!-- ========================================================
         SOCIAL / RESEARCH ICONS
         Same icon style as al-folio
         ======================================================== -->

    <div class="pi-socials">

      <!-- Google Scholar -->
      <a href="https://scholar.google.com/citations?user=Tt0enWsAAAAJ&hl=en&oi=ao"
         target="_blank"
         rel="noopener"
         aria-label="Google Scholar"
         title="Google Scholar">
        <i class="ai ai-google-scholar"></i>
      </a>

      <!-- LinkedIn -->
      <a href="https://www.linkedin.com/in/mayank-chouksey-24529844/"
         target="_blank"
         rel="noopener"
         aria-label="LinkedIn"
         title="LinkedIn">
        <i class="fab fa-linkedin"></i>
      </a>

      <!-- ResearchGate -->
      <a href="https://www.researchgate.net/profile/Mayank-Chouksey-2?ev=hdr_xprf"
         target="_blank"
         rel="noopener"
         aria-label="ResearchGate"
         title="ResearchGate">
        <i class="ai ai-researchgate"></i>
      </a>

      <!-- ORCID -->
      <a href="https://orcid.org/my-orcid?orcid=0000-0001-6479-4944"
         target="_blank"
         rel="noopener"
         aria-label="ORCID"
         title="ORCID">
        <i class="ai ai-orcid"></i>
      </a>

      <!-- GitHub -->
      <a href="https://github.com/mayankchouksey"
         target="_blank"
         rel="noopener"
         aria-label="GitHub"
         title="GitHub">
        <i class="fab fa-github"></i>
      </a>

      <!-- Email -->
      <a href="mailto:mayank@iiti.ac.in"
         aria-label="Email"
         title="Email">
        <i class="fas fa-envelope"></i>
      </a>

      <a href="{{ '/cv/' | relative_url }}" title="Curriculum Vitae">
        <i class="fas fa-file-lines"></i>
      </a>

    </div>

  </div>

</div>


<!-- ============================================================
     PHD STUDENTS
     ============================================================ -->

<h2 class="people-section-title">PhD Students</h2>

<div class="students-grid">


  <!-- ========================================================
       STUDENT 1
       ======================================================== -->

  <div class="student-card">

    <div class="student-photo">
      <img src="{{ '/assets/img/2.jpg' | relative_url }}"
           alt="Shradhha Gublake">
    </div>

    <div class="student-info">

      <h3>Shradhha Gublake</h3>

      <p class="student-degree">
        PhD Student
      </p>

      <p>
        <strong>Research:</strong>
        Research area to be added
      </p>

    </div>

  </div>


  <!-- ========================================================
       STUDENT 2
       ======================================================== -->

  <div class="student-card">

    <div class="student-photo">
      <img src="{{ '/assets/img/2.jpg' | relative_url }}"
           alt="Ashesh Parmar">
    </div>

    <div class="student-info">

      <h3>Parmar Ashesh Lalitkumar</h3>

      <p class="student-degree">
        PhD Student
      </p>

      <p>
        <strong>Research:</strong>
        Research area to be added
      </p>

    </div>

  </div>

</div>


<!-- ============================================================
     MS / MTECH STUDENTS
     ============================================================ -->

<h2 class="people-section-title">MS / MTech Students</h2>
<div class="students-grid">


  <!-- Student 1 -->
  <div class="student-card">
    <div class="student-photo">
      <img src="{{ '/assets/img/4.jpg' | relative_url }}"
           alt="Pranali Rao">
    </div>

    <div class="student-info">
      <h3>Pranali Rao</h3>
      <p class="student-degree">
        MS Student
      </p>

      <p>
        <strong>Research:</strong>
        Effect of void distribution on ductile failure
      </p>
    </div>
  </div>
  
  <!-- Student 2 -->
  <div class="student-card">
    <div class="student-photo">
      <img src="{{ '/assets/img/3.jpg' | relative_url }}"
           alt="Utkarsh Dubey">
    </div>

    <div class="student-info">
      <h3>Utkarsh Dubey</h3>
      <p class="student-degree">
        MTech Student
      </p>

      <p>
        <strong>Research:</strong>
        Homogenized constitutive framework using a data-driven framework
      </p>
    </div>
  </div>

  <!-- Student 3 -->
  <div class="student-card">
    <div class="student-photo">
      <img src="{{ '/assets/img/3.jpg' | relative_url }}"
           alt="Anshuman Singh">
    </div>

    <div class="student-info">
      <h3>Anshuman Singh</h3>
      <p class="student-degree">
        MTech Student
      </p>

      <p>
        <strong>Research:</strong>
        Unit cell calculations accounting for micro-inertia effect
      </p>
    </div>
  </div>


</div>



<!-- ============================================================
     Project Staf
     ============================================================ -->

<h2 class="people-section-title">Project Staf</h2>
<div class="students-grid">


  <!-- Student 1 -->
  <div class="student-card">
    <div class="student-photo">
      <img src="{{ '/assets/img/5.jpg' | relative_url }}"
           alt="Shivam Kumar Vishwakarma">
    </div>

    <div class="student-info">
      <h3>Shivam Kumar Vishwakarma</h3>
      <p class="student-degree">
        Junior Research Fellow
      </p>

      <p>
        <strong>Research:</strong>
        Effect of void distribution on ductile failure
      </p>
    </div>
  </div>
  

</div>




<!-- ============================================================
     ALUMNI
     ============================================================ -->

<h2 class="people-section-title">Alumni</h2>

<div class="alumni-list">

<!-- =1st Alumni Student = -->
  <div class="alumni-row">
    <div class="alumni-name">
      Devesh Agrawal
    </div>

    <div class="alumni-degree">
      M.Tech, 2025
    </div>

    <div class="alumni-position">
      Research Engineering, XXXXXXXXX
    </div>
  </div>

<!-- =2nd Alumni Student = -->
  <div class="alumni-row">
    <div class="alumni-name">
      Chandra Pratap Singh
    </div>

    <div class="alumni-degree">
      M.Tech, 2025
    </div>

    <div class="alumni-position">
      Engineer, ONGC
    </div>
  </div>

<!-- =3rd Alumni Student = -->
  <div class="alumni-row">
    <div class="alumni-name">
      Anant Kumar
    </div>

    <div class="alumni-degree">
      M.Tech., 2026
    </div>

    <div class="alumni-position">
      Research Engineer, XXXXXXXX
    </div>
  </div>

  
</div>


<!-- ============================================================
     STYLING
     ============================================================ -->

<style>

    /* ==========================================================
     clean title
     ========================================================== */

/* Hide the automatic page title */
.post-title {
  display: none;
}
  
  /* ==========================================================
     TEAM HEADING
     ========================================================== */

.team-heading {
  text-align: center;
  margin-top: 10px;
  margin-bottom: 45px;
}

.team-heading h1 {
  font-size: 2.2rem;
  margin-bottom: 0;
}

/* ============================================================
   CLEAN PAGE HEADER
   ============================================================ */

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
  margin-bottom: 42px;
}
  
  /* ==========================================================
     PI PROFILE
     ========================================================== */

  .pi-profile {
    display: flex;
    align-items: flex-start;
    gap: 40px;
    margin-top: 25px;
    margin-bottom: 50px;
    padding-bottom: 35px;
    border-bottom: 1px solid var(--global-divider-color);
  }

  .pi-photo {
    flex: 0 0 280px;
  }

  .pi-photo img {
    width: 280px;
    height: 280px;
    object-fit: cover;
    border-radius: 6px;
  }

  .pi-info {
    flex: 1;
  }

  .pi-info h2 {
    margin-top: 0;
    margin-bottom: 5px;
    font-size: 2rem;
  }

  .pi-position {
    font-size: 1.15rem;
    margin-top: 0;
    margin-bottom: 6px;
  }

  .pi-affiliation {
    line-height: 1.6;
    margin-bottom: 20px;
  }

  .pi-bio {
    line-height: 1.6;
  }

  .pi-bio p {
    margin-bottom: 12px;
  }


  /* ==========================================================
     SOCIAL ICONS
     ========================================================== */

  .pi-socials {
    display: flex;
    align-items: center;
    gap: 18px;
    margin-top: 22px;
  }

  .pi-socials a {
    font-size: 1.65rem;
    color: var(--global-text-color);
    text-decoration: none;
    transition: color 0.2s ease;
  }

  .pi-socials a:hover {
    color: var(--global-theme-color);
  }


  /* ==========================================================
     SECTION HEADINGS
     ========================================================== */

  .people-section-title {
    font-size: 1.65rem;
    margin-top: 45px;
    margin-bottom: 25px;
    padding-bottom: 8px;
    border-bottom: 1px solid var(--global-divider-color);
  }


  /* ==========================================================
     STUDENT GRID
     ========================================================== */

  .students-grid {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    column-gap: 45px;
    row-gap: 30px;
    margin-bottom: 30px;
  }


  /* ==========================================================
     STUDENT CARD
     ========================================================== */

  .student-card {
    display: flex;
    align-items: flex-start;
    gap: 20px;
  }

  .student-photo {
    flex: 0 0 105px;
  }

  .student-photo img {
    width: 105px;
    height: 105px;
    object-fit: cover;
    border-radius: 6px;
  }

  .student-info {
    flex: 1;
  }

  .student-info h3 {
    margin-top: 0;
    margin-bottom: 5px;
    font-size: 1.2rem;
  }

  .student-degree {
    margin-bottom: 7px;
  }

  .student-info p {
    line-height: 1.45;
    margin-bottom: 5px;
  }


  /* ==========================================================
     ALUMNI CARD
     ========================================================== */


.alumni-list {
  margin-bottom: 40px;
}

.alumni-row {
  display: grid;
  grid-template-columns: 1.4fr 1fr 2fr;
  column-gap: 25px;
  padding: 12px 0;
  border-bottom: 1px solid var(--global-divider-color);
  align-items: center;
}

.alumni-name {
  font-weight: 500;
  font-size: 1.05rem;
}

.alumni-degree {
  font-size: 0.95rem;
}

.alumni-position {
  font-size: 0.95rem;
}

@media (max-width: 768px) {

  .alumni-row {
    grid-template-columns: 1fr;
    row-gap: 4px;
    padding: 15px 0;
  }

  .alumni-degree,
  .alumni-position {
    font-size: 0.9rem;
  }

}


     

  /* ==========================================================
     MOBILE
     ========================================================== */

  @media (max-width: 768px) {

    .pi-profile {
      flex-direction: column;
      gap: 25px;
    }

    .pi-photo {
      flex: none;
    }

    .pi-photo img {
      width: 220px;
      height: 220px;
    }

    .students-grid {
      grid-template-columns: 1fr;
    }

  }

</style>
