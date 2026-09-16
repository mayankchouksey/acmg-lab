---
layout: page
permalink: /research-output/
title: research output
description: ""
nav: true
nav_order: 5
---

<div class="page-header-clean">
  <h1>Research Output</h1>
  <p>
    Selected research contributions (publications, conference 
     participation, and invited talks) from the
    Applied Computational Mechanics Group.
  </p>
</div>

<div class="page-header-line"></div>


<!-- ========================================================= -->
<!-- JOURNAL PUBLICATIONS                                      -->
<!-- ========================================================= -->

<h2>Journal Publications</h2>


<div class="publications">
  {% bibliography --file papers %}
</div>


<!-- ========================================================= -->
<!-- CONFERENCE PARTICIPATION                                  -->
<!-- ========================================================= -->

<h2>Conference Participation</h2>

<div class="publications">
  {% bibliography --file conferences %}
</div>


<!-- ========================================================= -->
<!-- INVITED TALKS                                             -->
<!-- ========================================================= -->

<h2>Invited Talks</h2>

<div class="publications">
  {% bibliography --file talks %}
</div>


<style>

.post-title {
  display: none;
}


/* --------------------------------------------------------- */
/* Page Header                                               */
/* --------------------------------------------------------- */

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


/* --------------------------------------------------------- */
/* Section Headings                                          */
/* --------------------------------------------------------- */

.post-content h2 {
  margin-top: 42px;
  margin-bottom: 20px;
}


/* --------------------------------------------------------- */
/* Bibliography Sections                                     */
/* --------------------------------------------------------- */

.publications {
  margin-bottom: 35px;
}


/* --------------------------------------------------------- */
/* Mobile                                                    */
/* --------------------------------------------------------- */

@media (max-width: 600px) {

  .page-header-clean h1 {
    font-size: 2rem;
  }

  .page-header-clean p {
    font-size: 1rem;
  }

}

</style>

