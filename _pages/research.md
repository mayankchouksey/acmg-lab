---
layout: page
permalink: /research/
title: Research
description: ""
nav: true
nav_order: 3
---

<div class="page-header-clean">
  <h1>Research</h1>
  <p>
    Computational Mechanics of Materials
  </p>
</div>

<div class="page-header-line"></div>

<p class="research-intro">
<!--  Our research focuses on understanding and predicting the mechanical behavior of materials through computational modelling. We investigate specific problems involving deformation, damage and failure, developing numerical formulations that connect material behavior at different length and time scales. -->
  
  Our research focuses on understanding and predicting the mechanical behavior of materials through computational and theoretical approaches. 
  We investigate specific problems combining mechanics, numerical methods, and material modelling to investigate deformation, damage, and failure under complex loading conditions at different length and time scales.  
</p>

<div class="research-area">
  <h3>Micromechanical Modelling of Ductile Failure</h3>

  <p>
    Ductile failure in metals involves the nucleation, growth and coalescence
    of microscopic voids. Predicting this process under complex loading
    conditions requires an understanding of the interaction between plastic
    deformation and evolving microstructure.
  </p>

  <p>
    At ACMG, we investigate ductile failure using
    micromechanical unit-cell calculations, in which the
    deformation of a representative material volume containing a void is
    explicitly modelled. These calculations provide insight into the influence
    of stress triaxiality, Lode parameter and loading history on void evolution
    and material failure.
  </p>

  <p>
    Our computational approach combines:
  </p>

  <ul>
    <li>
      <strong>Micromechanical unit-cell modelling</strong> to investigate void
      growth and coalescence under different stress states.
    </li>
    <li>
      <strong>Computational plasticity</strong> to describe the inelastic
      deformation of the surrounding matrix.
    </li>
    <li>
      <strong>Numerical homogenization</strong> to establish the relationship
      between the macroscopic stress state and the microscopic deformation
      response.
    </li>
<!--
    <li>
      <strong>Instability-based failure criteria</strong> to identify the onset
      of material failure from the micromechanical response.
    </li>
-->    
  </ul>

  <p>
    We also extend these formulations to dynamic loading conditions, accounting
    for material rate sensitivity, inertia and thermal softening. An important
    aspect of this work is understanding how these effects influence the onset
    of ductile failure, particularly under low-triaxiality loading.
  </p>

</div>

<div class="research-area">
  <h3>Coupled Electrochemical–Mechanical Modelling of Batteries</h3>

  <p>
    Lithium-ion batteries undergo significant changes in their mechanical state
    during charging and discharging. Lithium intercalation leads to changes in
    electrode particle volume, while the resulting mechanical stresses can
    influence electrode deformation and degradation.
  </p>

  <p>
    At ACMG, we investigate these phenomena through
    <strong>coupled electrochemical–mechanical modelling</strong>, combining
    homogenized solid mechanics (SOM) formulations with electrochemical models
    such as the Doyle–Fuller–Newman (DFN) model.
  </p>

  <p>
    Our approach involves:
  </p>

  <ul>
    <li>
      <strong>Electrochemical modelling using the DFN framework</strong> to
      describe lithium transport and electrochemical processes within battery
      electrodes.
    </li>
    <li>
      <strong>Homogenized solid mechanics</strong> to represent the macroscopic
      mechanical response of porous electrodes.
    </li>
    <li>
      <strong>Elastoplastic constitutive modelling</strong> to capture the
      mechanical response of electrode materials.
    </li>
    <li>
      <strong>Electrochemical–mechanical coupling</strong> to investigate the
      relationship between lithium concentration, electrode deformation and
      the development of mechanical stresses.
    </li>
  </ul>

  <p>
    The broader objective is to develop computational frameworks that can
    describe the evolution of mechanical stresses and deformation during
    battery operation and help understand the mechanisms associated with
    electrode degradation.
  </p>
</div>



<div class="research-area">
  <h3>Deformation and Failure of Layered MAX Phases</h3>

  <p>
    MAX phases are layered ceramic materials that exhibit a combination of metallic and ceramic characteristics. Their deformation behavior is strongly influenced by their hexagonal crystal structure, anisotropic mechanical response and the availability of different deformation mechanisms.
  </p>

  <p>
    We investigate the deformation and failure of these materials using crystal plasticity finite element modelling (CPFEM). The framework accounts for crystallographic deformation mechanisms and their influence on the macroscopic mechanical response.
  </p>

  <p>
    Our investigations include:
  </p>

  <ul>
    <li>
      <strong>Crystallographic slip</strong> involving basal and non-basal slip systems.
    </li>
    <li>
      <strong>Anisotropic deformation</strong> arising from the layered hexagonal crystal structure.
    </li>
    <li>
      <strong>Kinking and cleavage</strong> as mechanisms contributing to deformation and failure.
    </li>
    <li>
      <strong>Crystal plasticity finite element modelling</strong> to investigate the influence of crystallographic mechanisms on the overall mechanical response.
    </li>
  </ul>

  <p>
    These studies aim to establish a computational understanding of how crystallographic deformation mechanisms govern the mechanical behavior and failure of layered materials.
  </p>
</div>



<div class="research-area">
  <h2>Multiscale Modelling of Lightweight, Damage-Tolerant Structures</h2>

  <p>
    The mechanical response of lightweight cellular and architected materials is governed by their underlying microstructure and the deformation mechanisms activated under external loading. Understanding this relationship is important for predicting their energy absorption and damage tolerance, particularly under dynamic loading.
  </p>

  <p>
    Our work in this area explores computational approaches that connect the response of material constituents and structural architectures to their overall mechanical behavior.
  </p>

  <p>
    The modelling approach involves:
  </p>

  <ul>
    <li>
      <strong>Micromechanical and homogenization-based formulations</strong> to relate structural architecture to effective mechanical properties.
    </li>
    <li>
      <strong>Computational solid mechanics</strong> to investigate deformation under mechanical and dynamic loading.
    </li>
    <li>
      <strong>Damage and failure modelling</strong> to study the evolution of structural integrity under demanding loading conditions.
    </li>
  </ul>

  <p>
    These approaches provide a basis for investigating the design and mechanical performance of lightweight, damage-tolerant structures, including structures intended for dynamic threat mitigation.
  </p>
</div>






<h2>Research Approach</h2>
<p>
  Our research integrates continuum mechanics, computational modelling,
  numerical methods, and micromechanical approaches. Depending on the
  problem, these methods are combined to develop physically informed
  computational frameworks capable of describing material behaviour under
  realistic loading conditions.
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

.research-area ul {
  max-width: 900px;
  margin-top: 8px;
  margin-bottom: 20px;
  line-height: 1.7;
}

.research-area li {
  margin-bottom: 8px;
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
