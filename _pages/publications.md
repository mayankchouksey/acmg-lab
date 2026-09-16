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


<!-- ==================== PUBLICATIONS ==================== -->

<h2>Publications</h2>

<p class="output-description">
  Peer-reviewed journal articles.
</p>

<div class="publications compact-publications">
  {% bibliography --file papers %}
</div>


<!-- ==================== CONFERENCES ==================== -->

<!--  ~~~~~~~~~COMMENTED

<h2>Conferences</h2>
<p class="output-description">
  Conference presentations and participation.
</p>
<div class="publications compact-publications">
  {% bibliography --file conferences %}
</div>
~~~~~COMMENTED -->

<!-- ==================== TALKS ==================== -->

<!--  ~~~~~~~~~COMMENTED

<h2>Talks</h2>
<p class="output-description">
  Invited academic talks and seminars.
</p>
<div class="publications compact-publications">
  {% bibliography --file talks %}
</div>
~~~~~COMMENTED -->


<style>

/* ---------- Page Header ---------- */

.post-title {
  display: none;
}

.page-header-clean {
  text-align: center;
  margin-top: 5px;
  margin-bottom: 22px;
}

.page-header-clean h1 {
  font-size: 2.4rem;
  font-weight: 400;
  margin-bottom: 8px;
}

.page-header-clean p {
  max-width: 720px;
  margin: 0 auto;
  font-size: 1.05rem;
  line-height: 1.5;
}

.page-header-line {
  border-bottom: 2px solid var(--global-text-color);
  margin-bottom: 30px;
}


/* ---------- Section Headings ---------- */

.post-content h2 {
  margin-top: 30px;
  margin-bottom: 4px;
  font-size: 1.55rem;
  font-weight: 500;
}

.output-description {
  margin-top: 0;
  margin-bottom: 14px;
  font-size: 0.92rem;
  font-style: italic;
  line-height: 1.4;
}


/* ---------- Compact Bibliography ---------- */

.compact-publications {
  margin-bottom: 20px;
}

/* Reduce spacing between bibliography entries */
.compact-publications ol.bibliography {
  margin-top: 0;
  margin-bottom: 0;
}

.compact-publications ol.bibliography li {
  margin-bottom: 12px;
  padding-bottom: 0;
  line-height: 1.45;
}


/* Remove excessive paragraph spacing */
.compact-publications p {
  margin-top: 0;
  margin-bottom: 4px;
}


/* Reduce space around links/buttons */
.compact-publications .links {
  margin-top: 4px;
  margin-bottom: 0;
}


/* ---------- Mobile ---------- */

@media (max-width: 600px) {

  .page-header-clean h1 {
    font-size: 2rem;
  }

  .page-header-clean p {
    font-size: 1rem;
  }

  .post-content h2 {
    font-size: 1.35rem;
    margin-top: 26px;
  }

  .compact-publications ol.bibliography li {
    margin-bottom: 10px;
  }

}

</style>
