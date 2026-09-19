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

<!-- ==================================================
     ACMG HERO HEADER
     ================================================== -->

<section class="acmg-header">
  <div class="acmg-microstructure-container">
    <canvas id="acmg-microstructure"></canvas>
  </div>

  <div class="acmg-header-content">
    <h1>Applied Computational Mechanics Group</h1>

    <h2>
      <a href="https://meche.iiti.ac.in/" target="_blank" rel="noopener">
        Department of Mechanical Engineering
      </a>
    </h2>

    <h2>
      <a href="https://www.iiti.ac.in/" target="_blank" rel="noopener">
        Indian Institute of Technology Indore
      </a>
    </h2>
  </div>
</section>

<!-- ==================================================
     GROUP PHOTOGRAPH / RESEARCH HIGHLIGHTS IMAGE
     ================================================== -->

<div style="text-align: center; margin: 20px 0 40px;">
  <img src="{{ '/assets/img/6.jpg' | relative_url }}"
       style="width: 100%; max-width: 1100px; border-radius: 6px;"
       alt="Applied Computational Mechanics Group">
</div>
---

<!-- ==================================================
     WELCOME MESSAGE
     ================================================== -->

<p class="acmg-welcome">
  Welcome to the Applied Computational Mechanics Group (ACMG)
  at the Indian Institute of Technology Indore.
</p>
---

<!-- ==================================================
     WHAT WE DO AT ACMG
     ================================================== -->

<h2>What We Do at ACMG</h2>

<p>
  Materials respond differently when they are stretched, compressed, heated,
  loaded quickly, or subjected to complex conditions. Understanding these
  responses helps us predict when and how materials will deform, become
  damaged, or eventually fail.
</p>

<p>
  At ACMG, we use mechanics, mathematics, and computational methods to study
  these behaviours. We look at what happens inside materials at small scales
  and how these mechanisms influence their overall response. Our work covers
  deformation, plasticity, damage, fracture, and failure, including behaviour
  under dynamic loading and in advanced materials and energy-storage systems.
</p>

<p>
  In simple terms, we try to understand
  <strong>why materials behave the way they do—and use that understanding
  to predict what happens next.</strong>
</p>

<p>
  For a more detailed description of our research directions, please visit
  the <a href="{{ '/research/' | relative_url }}">Research</a> page.
</p>
---

<!-- ==================================================
     NEWS & HIGHLIGHTS
     ================================================== -->

<h2 class="acmg-section-title">News &amp; Highlights</h2>

<div class="acmg-news-home">
  {% assign recent_news = site.news | sort: "date" | reverse %}
  {% for item in recent_news limit:4 %}
    <div class="acmg-news-item">
      {% if item.image and item.image != "" %}
        <div class="acmg-news-image">
          <img src="{{ item.image | relative_url }}"
               alt="{{ item.title }}">
        </div>
      {% endif %}

      <div class="acmg-news-content">
        <div class="acmg-news-meta">
          {{ item.date | date: "%d %B %Y" }}
          {% if item.category %}
            <span class="acmg-news-category">
              {{ item.category }}
            </span>
          {% endif %}
        </div>

        <h3>{{ item.title }}</h3>

        <div class="acmg-news-description">
          {{ item.content }}
        </div>
      </div>
    </div>
  {% endfor %}
</div>

<p class="acmg-news-more">
  <a href="{{ '/news/' | relative_url }}">
    View all news →
  </a>
</p>

<!-- ==================================================
     ALL ACMG HOMEPAGE CSS
     ================================================== -->

<style>

/* --------------------------------------------------
   General page
   -------------------------------------------------- */

.post-title {
  display: none !important;
}

/* --------------------------------------------------
   ACMG Hero Header
   -------------------------------------------------- */

.acmg-header {
  position: relative;
  width: 100vw;
  left: 50%;
  transform: translateX(-50%);
  height: 430px;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: -20px;
  margin-bottom: 0;
}

/* --------------------------------------------------
   Microstructure animation container
   -------------------------------------------------- */

.acmg-microstructure-container {
  position: absolute;
  z-index: 0;
  top: -140px;
  left: 0;
  width: 100%;
  height: calc(100% + 220px);
  overflow: hidden;
  -webkit-mask-image: linear-gradient(
    to bottom,
    transparent 0%,
    rgba(0,0,0,0.10) 7%,
    black 19%,
    black 82%,
    rgba(0,0,0,0.55) 93%,
    transparent 100%
  );
  mask-image: linear-gradient(
    to bottom,
    transparent 0%,
    rgba(0,0,0,0.10) 7%,
    black 19%,
    black 82%,
    rgba(0,0,0,0.55) 93%,
    transparent 100%
  );
}

#acmg-microstructure {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}

/* --------------------------------------------------
   Hero text
   -------------------------------------------------- */

.acmg-header-content {
  position: relative;
  z-index: 2;
  text-align: center;
  background: rgba(255, 255, 255, 0.10);
  padding: 28px 45px 25px;
  border-radius: 4px;
  width: fit-content;
  max-width: 90%;
  margin: 0 auto;
  backdrop-filter: blur(1.5px);
  -webkit-backdrop-filter: blur(1.5px);
}

/* Group name */

.acmg-header-content h1 {
  margin: 0 0 18px 0;
  font-size: 2.8rem;
  font-weight: 350;
  line-height: 1.2;
  letter-spacing: -0.015em;
  color: rgba(20, 20, 20, 0.95);
}

/* Department and Institute */

.acmg-header-content h2 {
  margin: 8px 0;
  font-size: 1.8rem;
  font-weight: 375;
  line-height: 1.4;
  color: rgba(35, 35, 35, 0.90);
}

/* Department and Institute links */

.acmg-header-content h2 a {
  color: inherit;
  text-decoration: none;
}

.acmg-header-content h2 a:hover {
  text-decoration: underline;
  text-underline-offset: 4px;
}

/* --------------------------------------------------
   Welcome message
   -------------------------------------------------- */

.acmg-welcome {
  text-align: center;
  font-size: 1.45rem;
  line-height: 1.6;
  margin: 5px auto 40px;
  max-width: 950px;
}

/* --------------------------------------------------
   News and Highlights
   -------------------------------------------------- */

.acmg-section-title {
  margin-top: 45px;
  margin-bottom: 25px;
  font-size: 1.8rem;
  font-weight: 500;
}

.acmg-news-home {
  max-width: 900px;
  margin: 0 auto;
}

.acmg-news-item {
  display: flex;
  gap: 24px;
  padding: 20px 0;
  border-bottom: 1px solid rgba(100, 100, 100, 0.20);
}

.acmg-news-item:first-child {
  padding-top: 0;
}

.acmg-news-image {
  flex: 0 0 180px;
}

.acmg-news-image img {
  width: 180px;
  height: 115px;
  object-fit: cover;
  border-radius: 4px;
}

.acmg-news-content {
  flex: 1;
}

.acmg-news-meta {
  font-size: 0.85rem;
  color: rgba(80, 80, 80, 0.75);
  margin-bottom: 5px;
}

.acmg-news-category {
  margin-left: 12px;
  padding-left: 12px;
  border-left: 1px solid rgba(80, 80, 80, 0.35);
}

.acmg-news-content h3 {
  margin: 0 0 7px 0;
  font-size: 1.15rem;
  font-weight: 500;
}

.acmg-news-description {
  font-size: 0.95rem;
  line-height: 1.55;
}

.acmg-news-description p {
  margin: 0;
}

.acmg-news-more {
  text-align: center;
  margin-top: 22px;
}

.acmg-news-more a {
  text-decoration: none;
  font-weight: 500;
}

.acmg-news-more a:hover {
  text-decoration: underline;
}

/* --------------------------------------------------
   Mobile layout
   -------------------------------------------------- */

@media (max-width: 600px) {
  .acmg-header {
    height: 350px;
  }

  .acmg-header-content {
    padding: 22px 25px 20px;
    max-width: 92%;
  }

  .acmg-header-content h1 {
    font-size: 2rem;
    margin-bottom: 14px;
  }

  .acmg-header-content h2 {
    font-size: 1.1rem;
    margin: 6px 0;
  }

  .acmg-news-item {
    gap: 15px;
  }

  .acmg-news-image {
    flex: 0 0 110px;
  }

  .acmg-news-image img {
    width: 110px;
    height: 85px;
  }

  .acmg-news-content h3 {
    font-size: 1.05rem;
  }

  .acmg-news-description {
    font-size: 0.9rem;
  }
}

</style>

<!-- ==================================================
     ACMG MICROSTRUCTURE INTERACTION
     ================================================== -->

<script>
(function () {
  const canvas = document.getElementById("acmg-microstructure");
  if (!canvas) return;
  const ctx = canvas.getContext("2d");
  let width;
  let height;
  let particles = [];
  const spacing = 45;
  const influenceRadius = 200;
  const deformation = 55;
  const relaxation = 0.045;
  const particleRadius = 1.8;
  const particleColor = "rgba(95, 95, 95, 0.28)";
  const connectionColor = "rgba(95, 95, 95, 0.13)";
  const lineWidth = 0.6;
  let mouse = {
    x: null,
    y: null
  };

  function resize() {
    const rect = canvas.getBoundingClientRect();
    width = rect.width;
    height = rect.height;
    const dpr = window.devicePixelRatio || 1;
    canvas.width = width * dpr;
    canvas.height = height * dpr;
    ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
    createMicrostructure();
  }

  function createMicrostructure() {
    particles = [];
    const cols = Math.ceil(width / spacing) + 2;
    const rows = Math.ceil(height / spacing) + 2;

    for (let i = 0; i < cols; i++) {
      for (let j = 0; j < rows; j++) {
        const x =
          i * spacing -
          spacing +
          (Math.random() - 0.5) * spacing * 0.35;
        const y =
          j * spacing -
          spacing +
          (Math.random() - 0.5) * spacing * 0.35;

        particles.push({
          x: x,
          y: y,
          baseX: x,
          baseY: y,
          vx: 0,
          vy: 0
        });
      }
    }
  }

  function update() {
    particles.forEach(p => {
      let targetX = p.baseX;
      let targetY = p.baseY;

      if (mouse.x !== null) {
        const dx = p.baseX - mouse.x;
        const dy = p.baseY - mouse.y;
        const distance = Math.sqrt(dx * dx + dy * dy);

        if (distance < influenceRadius) {
          const influence = 1 - distance / influenceRadius;
          const force = influence * influence * deformation;
          const angle = Math.atan2(dy, dx);
          targetX += Math.cos(angle) * force;
          targetY += Math.sin(angle) * force;
        }
      }

      p.vx += (targetX - p.x) * relaxation;
      p.vy += (targetY - p.y) * relaxation;
      p.vx *= 0.88;
      p.vy *= 0.88;
      p.x += p.vx;
      p.y += p.vy;
    });
  }

  function draw() {
    ctx.clearRect(0, 0, width, height);

    /* Mesh connections */

    ctx.strokeStyle = connectionColor;
    ctx.lineWidth = lineWidth;

    for (let i = 0; i < particles.length; i++) {
      const p = particles[i];

      for (let j = i + 1; j < particles.length; j++) {
        const q = particles[j];
        const dx = p.x - q.x;
        const dy = p.y - q.y;
        const distance = Math.sqrt(dx * dx + dy * dy);

        if (distance < spacing * 1.45) {
          ctx.beginPath();
          ctx.moveTo(p.x, p.y);
          ctx.lineTo(q.x, q.y);
          ctx.stroke();
        }
      }
    }

    /* Mesh particles */

    ctx.fillStyle = particleColor;

    particles.forEach(p => {
      ctx.beginPath();
      ctx.arc(
        p.x,
        p.y,
        particleRadius,
        0,
        Math.PI * 2
      );
      ctx.fill();
    });
  }

  function animate() {
    update();
    draw();
    requestAnimationFrame(animate);
  }

  /* Mouse interaction over the entire header */

  const header = document.querySelector(".acmg-header");

  header.addEventListener("mousemove", function (event) {
    const rect = canvas.getBoundingClientRect();
    mouse.x = event.clientX - rect.left;
    mouse.y = event.clientY - rect.top;
  });

  header.addEventListener("mouseleave", function () {
    mouse.x = null;
    mouse.y = null;
  });

  window.addEventListener("resize", resize);
  resize();
  animate();
})();
</script>
