---
layout: page
permalink: /people/
title: people
description: Members of the Applied Computational Mechanics Group
nav: true
nav_order: 7
---

<!-- ============================================================
     GROUP LEADER
     ============================================================ -->

<div class="pi-profile">

  <!-- PI PHOTO -->
  <div class="pi-photo">
    <img src="{{ '/assets/img/prof_pic.jpg' | relative_url }}"
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
      <a href="YOUR_GOOGLE_SCHOLAR_LINK"
         target="_blank"
         rel="noopener"
         aria-label="Google Scholar"
         title="Google Scholar">
        <i class="ai ai-google-scholar"></i>
      </a>

      <!-- LinkedIn -->
      <a href="YOUR_LINKEDIN_LINK"
         target="_blank"
         rel="noopener"
         aria-label="LinkedIn"
         title="LinkedIn">
        <i class="fab fa-linkedin"></i>
      </a>

      <!-- ResearchGate -->
      <a href="YOUR_RESEARCHGATE_LINK"
         target="_blank"
         rel="noopener"
         aria-label="ResearchGate"
         title="ResearchGate">
        <i class="ai ai-researchgate"></i>
      </a>

      <!-- ORCID -->
      <a href="YOUR_ORCID_LINK"
         target="_blank"
         rel="noopener"
         aria-label="ORCID"
         title="ORCID">
        <i class="ai ai-orcid"></i>
      </a>

      <!-- GitHub -->
      <a href="YOUR_GITHUB_LINK"
         target="_blank"
         rel="noopener"
         aria-label="GitHub"
         title="GitHub">
        <i class="fab fa-github"></i>
      </a>

      <!-- Email -->
      <a href="mailto:YOUR_EMAIL_ADDRESS"
         aria-label="Email"
         title="Email">
        <i class="fas fa-envelope"></i>
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

      <h3>Ashesh Parmar</h3>

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

  <!-- Add MS / MTech students here -->

</div>


<!-- ============================================================
     ALUMNI
     ============================================================ -->

<h2 class="people-section-title">Alumni</h2>

<div class="students-grid">

  <!-- Add alumni here -->

</div>


<!-- ============================================================
     STYLING
     ============================================================ -->

<style>

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
