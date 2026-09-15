---
layout: page
permalink: /teaching/
title: teaching
description: ""
nav: true
nav_order: 6
---

<!-- ============================================================
     PAGE HEADER
     ============================================================ -->

<div class="page-header-clean">

  <h1>Teaching</h1>

  <p>
    Courses taught by Dr. Mayank Chouksey in mechanics, plasticity,
    and mechanics of materials.
  </p>

</div>

<div class="page-header-line"></div>


<!-- ============================================================
     UNDERGRADUATE COURSES
     ============================================================ -->

<h2>Undergraduate Courses</h2>

<div class="course-list">

  <div class="course-item">
    <span class="course-name">Engineering Mechanics</span>
    <span class="course-code">ME101</span>
  </div>

  <div class="course-item">
    <span class="course-name">Strength of Materials</span>
    <span class="course-code">ME201</span>
  </div>

  <div class="course-item">
    <span class="course-name">Mechanics of Materials</span>
    <span class="course-code">ME202</span>
  </div>

</div>


<!-- ============================================================
     GRADUATE COURSES
     ============================================================ -->

<h2>Graduate Courses</h2>

<div class="course-list">

  <div class="course-item">
    <span class="course-name">Theory of Elasticity</span>
    <span class="course-code">ME730</span>
  </div>

  <div class="course-item">
    <span class="course-name">Theory of Plasticity</span>
    <span class="course-code">ME466 / ME666</span>
  </div>

  <div class="course-item">
    <span class="course-name">Fracture Mechanics</span>
    <span class="course-code">—</span>
  </div>

</div>


<!-- ============================================================
     PAGE STYLING
     ============================================================ -->

<style>

  /* ------------------------------------------------------------
     Hide automatic al-folio page title
     ------------------------------------------------------------ */

  .post-title {
    display: none;
  }


  /* ------------------------------------------------------------
     Clean page header
     ------------------------------------------------------------ */

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


  /* ------------------------------------------------------------
     Divider
     ------------------------------------------------------------ */

  .page-header-line {
    border-bottom: 2px solid var(--global-text-color);
    margin-bottom: 42px;
  }


  /* ------------------------------------------------------------
     Section headings
     ------------------------------------------------------------ */

  .post-content h2 {
    margin-top: 38px;
    margin-bottom: 18px;
  }


  /* ------------------------------------------------------------
     Course list
     ------------------------------------------------------------ */

  .course-list {
    max-width: 850px;
  }

  .course-item {
    display: flex;
    justify-content: space-between;
    align-items: center;

    padding: 13px 5px;

    border-bottom: 1px solid var(--global-divider-color);
  }

  .course-name {
    font-size: 1.05rem;
  }

  .course-code {
    font-size: 0.95rem;
    opacity: 0.75;
    white-space: nowrap;
    margin-left: 20px;
  }


  /* ------------------------------------------------------------
     Mobile
     ------------------------------------------------------------ */

  @media (max-width: 600px) {

    .course-item {
      align-items: flex-start;
    }

    .course-name {
      font-size: 1rem;
    }

    .course-code {
      font-size: 0.9rem;
    }

  }

</style>
