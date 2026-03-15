# Kişisel Website Yeniden Tasarımı - Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Mevcut kişisel website'yi canlı renkler, yeni bölümler ve gelişmiş işlevsellik ile yeniden tasarlamak.

**Architecture:** Tek sayfa (single-page) yapısı korunacak. Vanilla HTML/CSS/JS ile modern, performanslı bir site. CSS custom properties ile theme desteği. Bölümler sırayla eklenecek - önce temel yapı, sonra içerik bölümleri.

**Tech Stack:** Vanilla HTML5, CSS3, JavaScript (ES6+), Google Fonts (Lora, DM Sans, DM Mono)

---

## Dosya Yapısı

- Modify: `index.html` - Ana sayfa (tüm içerik tek dosyada kalacak)
- Create: `img/projects/` - Proje görselleri için (opsiyonel)
- Create: `blog/` - Blog yazıları için dizin (opsiyonel)

---

## Chunk 1: Temel Görsel Yenileme (CSS & Tema)

### Task 1: CSS Değişkenleri ve Renk Sistemi

**Files:**
- Modify: `index.html:9-104` (style tag)

- [ ] **Step 1: Mevcut CSS değişkenlerini canlı renklerle güncelle**

```css
:root {
  /* Light Theme - Canlı Renkler */
  --primary: #06b6d4;    /* Akvamarin */
  --secondary: #f97316;  /* Mercan */
  --accent: #ec4899;     /* Fuşya */
  --bg: #f8fafc;
  --bg-alt: #f1f5f9;
  --text: #0f172a;
  --text-muted: #64748b;
  --border: #e2e8f0;

  /* Gradient tanımları */
  --gradient-hero: linear-gradient(135deg, var(--primary), var(--accent));
  --gradient-btn: linear-gradient(135deg, var(--primary), var(--secondary));
}

[data-theme="dark"] {
  --bg: #0f172a;
  --bg-alt: #1e293b;
  --text: #f8fafc;
  --text-muted: #94a3b8;
  --border: #334155;
}
```

- [ ] **Step 2: Commit**

```bash
git add index.html
git commit -m "feat: add CSS custom properties for live colors and dark theme"
```

---

### Task 2: Theme Toggle JavaScript

**Files:**
- Modify: `index.html:277-285` (script tag)

- [ ] **Step 1: Theme toggle fonksiyonu ekle**

```javascript
// Theme toggle
const themeToggle = document.getElementById('theme-toggle');
const html = document.documentElement;

// Load saved theme
const savedTheme = localStorage.getItem('theme') || 'light';
html.setAttribute('data-theme', savedTheme);
updateThemeIcon(savedTheme);

themeToggle?.addEventListener('click', () => {
  const current = html.getAttribute('data-theme');
  const next = current === 'dark' ? 'light' : 'dark';
  html.setAttribute('data-theme', next);
  localStorage.setItem('theme', next);
  updateThemeIcon(next);
});

function updateThemeIcon(theme) {
  if (!themeToggle) return;
  themeToggle.innerHTML = theme === 'dark'
    ? '<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="5"/><path d="M12 1v2M12 21v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M1 12h2M21 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"/></svg>'
    : '<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"/></svg>';
}
```

- [ ] **Step 2: Commit**

```bash
git add index.html
git commit -m "feat: add theme toggle functionality with localStorage"
```

---

### Task 3: Navbar Güncelleme (Theme Toggle Icon + Social Icons)

**Files:**
- Modify: `index.html:108-115` (nav elementi)

- [ ] **Step 1: Navbar'a theme toggle ve social icons ekle**

```html
<nav id="nav">
  <a class="nav-name" href="#">İlker Halil Türer</a>
  <div class="nav-right">
    <ul class="nav-links">
      <li><a href="#projects">Projects</a></li>
      <li><a href="#blog">Blog</a></li>
      <li><a href="#skills">Skills</a></li>
      <li><a href="#experience">Experience</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
    <a id="theme-toggle" class="theme-btn" aria-label="Toggle theme"></a>
    <div class="social-icons">
      <a href="https://github.com/ilkerhalil" target="_blank" aria-label="GitHub">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
      </a>
      <a href="https://linkedin.com/in/ilker-halil-turer" target="_blank" aria-label="LinkedIn">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/></svg>
      </a>
      <a href="https://twitter.com/ilkerhalil" target="_blank" aria-label="Twitter">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/></svg>
      </a>
    </div>
  </div>
</nav>
```

- [ ] **Step 2: Nav CSS güncelleme**

```css
nav { /* ... mevcut stiller ... */ }
.nav-right { display: flex; align-items: center; gap: 1.5rem; }
.social-icons { display: flex; gap: 0.75rem; }
.social-icons a { color: var(--text-muted); transition: color .2s; }
.social-icons a:hover { color: var(--primary); }
.theme-btn { background: none; border: none; cursor: pointer; color: var(--text-muted); padding: 0.25rem; display: flex; align-items: center; justify-content: center; transition: color .2s; }
.theme-btn:hover { color: var(--primary); }

/* Mobile */
@media (max-width: 768px) {
  .nav-right { gap: 1rem; }
  .social-icons { display: none; } /* Mobile'da gizle */
}
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add theme toggle and social icons to navbar"
```

---

## Chunk 2: Hero Section Güncelleme

### Task 4: Hero Section Görsel İyileştirme

**Files:**
- Modify: `index.html:117-135` (hero section)

- [ ] **Step 1: Hero section CSS güncelle - canlı renk vurguları**

```css
.hero-greeting { /* mevcut */ }
.hero-greeting::before { background: var(--primary); } /* Akvamarin */

.hero-name { /* mevcut */ }
.hero-name em { color: var(--secondary); } /* Mercan vurgu */

.hero-bio strong { color: var(--primary); }

/* CTA Butonları - Gradient */
.btn-solid {
  background: var(--gradient-btn);
  border: none;
}
.btn-solid:hover {
  filter: brightness(1.1);
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(6, 182, 212, 0.3);
}

/* Hero sayıları - canlı renk */
.num-val { color: var(--primary); }
```

- [ ] **Step 2: Commit**

```bash
git add index.html
git commit -m "feat: update hero section with vibrant colors and gradients"
```

---

## Chunk 3: Skills Section Güncelleme

### Task 5: Skills Section Renk Güncelleme

**Files:**
- Modify: `index.html:137-187` (skills section)

- [ ] **Step 1: Skills CSS güncelle**

```css
.sg-title { /* mevcut */ border-bottom-color: var(--border); }
.pill { border-color: var(--border); }
.pill:hover, .pill.hi {
  background: linear-gradient(135deg, rgba(6,182,212,0.15), rgba(249,115,22,0.15));
  border-color: var(--primary);
  color: var(--primary);
}
```

- [ ] **Step 2: Commit**

```bash
git add index.html
git commit -m "feat: update skills section with vibrant color highlights"
```

---

## Chunk 4: Projects Section (YENİ)

### Task 6: Projects Section HTML & CSS

**Files:**
- Modify: `index.html` - Add new section after Skills

- [ ] **Step 1: Projects section HTML ekle**

```html
<section id="projects">
  <div class="container">
    <div class="reveal">
      <div class="eyebrow">Portfolio</div>
      <h2>Featured Projects</h2>
    </div>
    <div class="projects-grid reveal">
      <!-- Project 1 -->
      <article class="project-card">
        <div class="project-content">
          <h3>Project Name</h3>
          <p>Project description goes here. Brief overview of what was built and the impact.</p>
          <div class="project-tags">
            <span class="etag">.NET Core</span><span class="etag">AWS</span><span class="etag">Kubernetes</span>
          </div>
        </div>
        <a href="#" class="project-link">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6M15 3h6v6M10 14L21 3"/></svg>
        </a>
      </article>

      <!-- Project 2 -->
      <article class="project-card">
        <div class="project-content">
          <h3>Project Name</h3>
          <p>Project description goes here. Brief overview of what was built and the impact.</p>
          <div class="project-tags">
            <span class="etag">Python</span><span class="etag">FastAPI</span><span class="etag">ML</span>
          </div>
        </div>
        <a href="#" class="project-link">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6M15 3h6v6M10 14L21 3"/></svg>
        </a>
      </article>

      <!-- Project 3 -->
      <article class="project-card">
        <div class="project-content">
          <h3>Project Name</h3>
          <p>Project description goes here. Brief overview of what was built and the impact.</p>
          <div class="project-tags">
            <span class="etag">React</span><span class="etag">TypeScript</span><span class="etag">Node.js</span>
          </div>
        </div>
        <a href="#" class="project-link">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6M15 3h6v6M10 14L21 3"/></svg>
        </a>
      </article>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Projects CSS ekle**

```css
#projects { padding: 7rem 0; background: var(--bg-alt); }
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
}
.project-card {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  transition: all .3s ease;
  position: relative;
  overflow: hidden;
}
.project-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 4px;
  height: 100%;
  background: var(--gradient-hero);
  opacity: 0;
  transition: opacity .3s;
}
.project-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 40px rgba(6, 182, 212, 0.15);
  border-color: var(--primary);
}
.project-card:hover::before { opacity: 1; }
.project-card h3 {
  font-family: 'Lora', serif;
  font-size: 1.25rem;
  color: var(--text);
  margin-bottom: 0.75rem;
}
.project-card p {
  font-size: .9rem;
  color: var(--text-muted);
  line-height: 1.6;
  margin-bottom: 1rem;
}
.project-tags { display: flex; flex-wrap: wrap; gap: 0.4rem; }
.project-link {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  color: var(--text-muted);
  transition: color .2s, transform .2s;
}
.project-link:hover {
  color: var(--primary);
  transform: translate(3px, -3px);
}
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add projects section with card layout"
```

---

## Chunk 5: Blog Section (YENİ)

### Task 7: Blog Section HTML & CSS

**Files:**
- Modify: `index.html` - Add new section after Projects

- [ ] **Step 1: Blog section HTML ekle**

```html
<section id="blog">
  <div class="container">
    <div class="reveal">
      <div class="eyebrow">Writing</div>
      <h2>Latest Articles</h2>
    </div>
    <div class="blog-list reveal">
      <!-- Blog Post 1 -->
      <article class="blog-item">
        <span class="blog-date">March 2026</span>
        <h3><a href="#">Building Scalable Systems with Modern Architecture</a></h3>
        <p>Exploring the key principles of designing systems that can scale...</p>
        <div class="blog-meta">
          <span class="blog-read">8 min read</span>
          <span class="blog-tag">Architecture</span>
        </div>
      </article>

      <!-- Blog Post 2 -->
      <article class="blog-item">
        <span class="blog-date">February 2026</span>
        <h3><a href="#">AI Integration in Enterprise Applications</a></h3>
        <p>Practical guide to integrating LLMs into existing software...</p>
        <div class="blog-meta">
          <span class="blog-read">12 min read</span>
          <span class="blog-tag">AI/ML</span>
        </div>
      </article>

      <!-- Blog Post 3 -->
      <article class="blog-item">
        <span class="blog-date">January 2026</span>
        <h3><a href="#">Kubernetes Best Practices for Production</a></h3>
        <p>Lessons learned from managing EKS clusters at scale...</p>
        <div class="blog-meta">
          <span class="blog-read">10 min read</span>
          <span class="blog-tag">DevOps</span>
        </div>
      </article>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Blog CSS ekle**

```css
#blog { padding: 7rem 0; }
.blog-list { display: flex; flex-direction: column; gap: 2rem; }
.blog-item {
  padding: 1.5rem 0;
  border-bottom: 1px solid var(--border);
  transition: padding-left .3s;
}
.blog-item:hover { padding-left: 1rem; }
.blog-item:last-child { border-bottom: none; }
.blog-date {
  font-family: 'DM Mono', monospace;
  font-size: .65rem;
  color: var(--text-muted);
  letter-spacing: .08em;
  text-transform: uppercase;
}
.blog-item h3 {
  font-family: 'Lora', serif;
  font-size: 1.4rem;
  font-weight: 400;
  margin: 0.5rem 0;
}
.blog-item h3 a {
  color: var(--text);
  text-decoration: none;
  transition: color .2s;
}
.blog-item h3 a:hover { color: var(--primary); }
.blog-item p {
  font-size: .95rem;
  color: var(--text-muted);
  line-height: 1.6;
  margin-bottom: 0.75rem;
}
.blog-meta {
  display: flex;
  gap: 1rem;
  font-family: 'DM Mono', monospace;
  font-size: .6rem;
  letter-spacing: .05em;
  text-transform: uppercase;
}
.blog-read, .blog-tag { color: var(--text-muted); }
.blog-tag {
  background: var(--bg-alt);
  padding: 0.2rem 0.5rem;
  border-radius: 4px;
}
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add blog section with article list"
```

---

## Chunk 6: Testimonials Section (YENİ)

### Task 8: Testimonials Section HTML & CSS

**Files:**
- Modify: `index.html` - Add new section after Blog

- [ ] **Step 1: Testimonials section HTML ekle**

```html
<section id="testimonials">
  <div class="container">
    <div class="reveal">
      <div class="eyebrow">References</div>
      <h2>What People Say</h2>
    </div>
    <div class="testimonials-grid reveal">
      <!-- Testimonial 1 -->
      <blockquote class="testimonial-card">
        <p>"İlker is one of those rare architects who can explain complex systems in simple terms. His leadership on our migration project was invaluable."</p>
        <footer>
          <div class="testimonial-author">
            <div class="author-avatar">AK</div>
            <div>
              <cite>Ayşe Kaya</cite>
              <span class="author-title">CTO, Intertech</span>
            </div>
          </div>
        </footer>
      </blockquote>

      <!-- Testimonial 2 -->
      <blockquote class="testimonial-card">
        <p>"Working with İlker transformed our team's approach to cloud infrastructure. His mentorship has been crucial to our growth."</p>
        <footer>
          <div class="testimonial-author">
            <div class="author-avatar">ME</div>
            <div>
              <cite>Mehmet Demir</cite>
              <span class="author-title">Lead Developer, TechCorp</span>
            </div>
          </div>
        </footer>
      </blockquote>

      <!-- Testimonial 3 -->
      <blockquote class="testimonial-card">
        <p>"İlker's ability to bridge business requirements with technical solutions is exceptional. A true engineering leader."</p>
        <footer>
          <div class="testimonial-author">
            <div class="author-avatar">SZ</div>
            <div>
              <cite>Zeynep Soylu</cite>
              <span class="author-title">Product Manager, InnovateTech</span>
            </div>
          </div>
        </footer>
      </blockquote>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Testimonials CSS ekle**

```css
#testimonials { padding: 7rem 0; background: var(--bg-alt); }
.testimonials-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
}
.testimonial-card {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 1.75rem;
  margin: 0;
  transition: all .3s ease;
}
.testimonial-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 40px rgba(249, 115, 22, 0.1);
  border-color: var(--secondary);
}
.testimonial-card p {
  font-size: .95rem;
  color: var(--text);
  line-height: 1.7;
  font-style: italic;
  margin-bottom: 1.5rem;
}
.testimonial-card footer { border: none; padding: 0; margin: 0; }
.testimonial-author {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}
.author-avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: var(--gradient-hero);
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-family: 'DM Sans', sans-serif;
  font-size: .8rem;
  font-weight: 600;
}
.testimonial-author cite {
  display: block;
  font-style: normal;
  font-weight: 600;
  color: var(--text);
  font-size: .9rem;
}
.author-title {
  display: block;
  font-size: .75rem;
  color: var(--text-muted);
}
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add testimonials section"
```

---

## Chunk 7: Speaking Section (YENİ)

### Task 9: Speaking Section HTML & CSS

**Files:**
- Modify: `index.html` - Add new section after Testimonials

- [ ] **Step 1: Speaking section HTML ekle**

```html
<section id="speaking">
  <div class="container">
    <div class="reveal">
      <div class="eyebrow">Speaking</div>
      <h2>Talks & Presentations</h2>
    </div>
    <div class="speaking-timeline reveal">
      <!-- Talk 1 -->
      <div class="talk-item">
        <div class="talk-year">2025</div>
        <div class="talk-content">
          <span class="talk-event">TechConf İzmir</span>
          <h3>Modernizing Legacy Systems for the Cloud Age</h3>
          <p>İzmir, Turkey</p>
        </div>
      </div>

      <!-- Talk 2 -->
      <div class="talk-item">
        <div class="talk-year">2024</div>
        <div class="talk-content">
          <span class="talk-event">AWS User Group Istanbul</span>
          <h3>Kubernetes at Scale: Lessons from Production</h3>
          <p>Istanbul, Turkey</p>
        </div>
      </div>

      <!-- Talk 3 -->
      <div class="talk-item">
        <div class="talk-year">2023</div>
        <div class="talk-content">
          <span class="talk-event">DevOps Days Ankara</span>
          <h3>Building a Culture of Continuous Learning</h3>
          <p>Ankara, Turkey</p>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Speaking CSS ekle**

```css
#speaking { padding: 7rem 0; }
.speaking-timeline {
  display: flex;
  flex-direction: column;
  gap: 0;
}
.talk-item {
  display: grid;
  grid-template-columns: 80px 1fr;
  gap: 2rem;
  padding: 1.5rem 0;
  border-bottom: 1px solid var(--border);
  transition: background .3s, padding-left .3s;
}
.talk-item:first-child { border-top: 1px solid var(--border); }
.talk-item:hover {
  background: var(--bg-alt);
  padding-left: 1rem;
}
.talk-year {
  font-family: 'DM Mono', monospace;
  font-size: .8rem;
  color: var(--primary);
  font-weight: 600;
}
.talk-event {
  font-family: 'DM Mono', monospace;
  font-size: .65rem;
  letter-spacing: .08em;
  text-transform: uppercase;
  color: var(--secondary);
  display: block;
  margin-bottom: 0.25rem;
}
.talk-content h3 {
  font-family: 'Lora', serif;
  font-size: 1.15rem;
  color: var(--text);
  margin-bottom: 0.25rem;
}
.talk-content p {
  font-size: .85rem;
  color: var(--text-muted);
}

@media (max-width: 600px) {
  .talk-item { grid-template-columns: 1fr; gap: 0.5rem; }
}
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add speaking section with timeline layout"
```

---

## Chunk 8: GitHub Section (YENİ)

### Task 10: GitHub Section HTML & CSS

**Files:**
- Modify: `index.html` - Add new section after Speaking

- [ ] **Step 1: GitHub section HTML ekle**

```html
<section id="github">
  <div class="container">
    <div class="reveal">
      <div class="eyebrow">Open Source</div>
      <h2>GitHub Activity</h2>
    </div>
    <div class="github-stats reveal">
      <div class="stat-card">
        <span class="stat-value">150+</span>
        <span class="stat-label">Contributions</span>
      </div>
      <div class="stat-card">
        <span class="stat-value">25+</span>
        <span class="stat-label">Repositories</span>
      </div>
      <div class="stat-card">
        <span class="stat-value">500+</span>
        <span class="stat-label">Stars Earned</span>
      </div>
    </div>
    <div class="repo-grid reveal">
      <!-- Repo 1 -->
      <a href="https://github.com/ilkerhalil/project1" target="_blank" class="repo-card">
        <h4>project-name</h4>
        <p>Project description goes here.</p>
        <div class="repo-stats">
          <span><span class="repo-dot">●</span> 128</span>
          <span><svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0l-2.464 2.889 2.464.889-2.464 2.889 2.464.889-2.464 2.889L12 12l2.464-2.889-2.464-.889 2.464-2.889-2.464-.889L12 0zm0 18.222l-2.464 2.889 2.464.889-2.464 2.889 2.464.889-2.464 2.889L12 24l2.464-2.889-2.464-.889 2.464-2.889-2.464-.889L12 18.222z"/></svg> 64</span>
        </div>
      </a>
      <!-- Repo 2 -->
      <a href="https://github.com/ilkerhalil/project2" target="_blank" class="repo-card">
        <h4>another-project</h4>
        <p>Description for another project.</p>
        <div class="repo-stats">
          <span><span class="repo-dot" style="color:var(--secondary)">●</span> 89</span>
          <span><svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0l-2.464 2.889 2.464.889-2.464 2.889 2.464.889-2.464 2.889L12 12l2.464-2.889-2.464-.889 2.464-2.889-2.464-.889L12 0zm0 18.222l-2.464 2.889 2.464.889-2.464 2.889 2.464.889-2.464 2.889L12 24l2.464-2.889-2.464-.889 2.464-2.889-2.464-.889L12 18.222z"/></svg> 32</span>
        </div>
      </a>
      <!-- Repo 3 -->
      <a href="https://github.com/ilkerhalil/project3" target="_blank" class="repo-card">
        <h4>useful-tool</h4>
        <p>A useful tool for developers.</p>
        <div class="repo-stats">
          <span><span class="repo-dot" style="color:var(--accent)">●</span> 256</span>
          <span><svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0l-2.464 2.889 2.464.889-2.464 2.889 2.464.889-2.464 2.889L12 12l2.464-2.889-2.464-.889 2.464-2.889-2.464-.889L12 0zm0 18.222l-2.464 2.889 2.464.889-2.464 2.889 2.464.889-2.464 2.889L12 24l2.464-2.889-2.464-.889 2.464-2.889-2.464-.889L12 18.222z"/></svg> 128</span>
        </div>
      </a>
    </div>
  </div>
</section>
```

- [ ] **Step 2: GitHub CSS ekle**

```css
#github { padding: 7rem 0; background: var(--bg-alt); }
.github-stats {
  display: flex;
  gap: 2rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
}
.stat-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1.5rem 2.5rem;
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 12px;
  transition: all .3s;
}
.stat-card:hover {
  border-color: var(--primary);
  transform: translateY(-2px);
}
.stat-value {
  font-family: 'Lora', serif;
  font-size: 2.5rem;
  color: var(--primary);
}
.stat-label {
  font-family: 'DM Mono', monospace;
  font-size: .7rem;
  letter-spacing: .1em;
  text-transform: uppercase;
  color: var(--text-muted);
}
.repo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
}
.repo-card {
  background: var(--bg);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 1.25rem;
  text-decoration: none;
  transition: all .3s;
}
.repo-card:hover {
  border-color: var(--primary);
  transform: translateY(-2px);
  box-shadow: 0 8px 24px rgba(6, 182, 212, 0.1);
}
.repo-card h4 {
  font-family: 'DM Mono', monospace;
  font-size: .9rem;
  color: var(--primary);
  margin-bottom: 0.5rem;
}
.repo-card p {
  font-size: .8rem;
  color: var(--text-muted);
  margin-bottom: 0.75rem;
  line-height: 1.4;
}
.repo-stats {
  display: flex;
  gap: 1rem;
  font-family: 'DM Mono', monospace;
  font-size: .7rem;
  color: var(--text-muted);
}
.repo-stats svg { vertical-align: middle; margin-left: 3px; }
.repo-dot { margin-right: 3px; }
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add github section with stats and repos"
```

---

## Chunk 9: Experience & Contact Güncelleme + Footer

### Task 11: Experience Section Güncelleme

**Files:**
- Modify: `index.html:189-237` (experience section)

- [ ] **Step 1: Experience CSS güncelleme**

```css
#experience { padding: 7rem 0; background: var(--bg-alt); }
.exp-co { color: var(--secondary); } /* Mercan vurgu */
.exp-tags .etag:hover {
  background: var(--bg);
  border-color: var(--primary);
  color: var(--primary);
}
```

- [ ] **Step 2: Commit**

```bash
git add index.html
git commit -m "feat: update experience section colors"
```

---

### Task 12: Contact Section Güncelleme + Social Icons

**Files:**
- Modify: `index.html:239-270` (contact section)

- [ ] **Step 1: Contact section'a social icons ekle**

```html
<section id="contact">
  <div class="container">
    <div class="reveal">
      <div class="eyebrow">Contact</div>
      <h2>Let's work together</h2>
    </div>
    <div class="contact-layout reveal">
      <div>
        <p class="contact-tagline">"Feel free to reach out about a new project, an opportunity, or just to say hello."</p>
        <div class="clinks">
          <a href="mailto:ilkerhalil@gmail.com" class="clink">
            <span class="clink-label">email</span>ilkerhalil@gmail.com
          </a>
          <a href="https://linkedin.com/in/ilker-halil-turer" target="_blank" class="clink">
            <span class="clink-label">linkedin</span>ilker-halil-turer
          </a>
          <a href="https://github.com/ilkerhalil" target="_blank" class="clink">
            <span class="clink-label">github</span>ilkerhalil
          </a>
        </div>
        <div class="contact-socials">
          <a href="https://github.com/ilkerhalil" target="_blank" aria-label="GitHub" class="social-btn">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
          </a>
          <a href="https://linkedin.com/in/ilker-halil-turer" target="_blank" aria-label="LinkedIn" class="social-btn">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/></svg>
          </a>
          <a href="https://twitter.com/ilkerhalil" target="_blank" aria-label="Twitter" class="social-btn">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/></svg>
          </a>
        </div>
      </div>
      <div>
        <div class="info-table">
          <div class="info-row"><span class="info-k">Location</span><span class="info-v">İzmir / Istanbul</span></div>
          <div class="info-row"><span class="info-k">Work style</span><span class="info-v">Remote · Hybrid</span></div>
          <div class="info-row"><span class="info-k">Status</span><span class="info-v ok">Open to new opportunities</span></div>
          <div class="info-row"><span class="info-k">Languages</span><span class="info-v">Turkish · English</span></div>
        </div>
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Contact CSS güncelleme**

```css
.contact-tagline { color: var(--text-muted); }
.info-v.ok { color: var(--primary); } /* Açık yeşil - müsait */

.contact-socials {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
  padding-top: 2rem;
  border-top: 1px solid var(--border);
}
.social-btn {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  background: var(--bg-alt);
  border: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text-muted);
  transition: all .3s;
}
.social-btn:hover {
  background: var(--primary);
  border-color: var(--primary);
  color: white;
  transform: translateY(-3px);
}
```

- [ ] **Step 3: Footer güncelleme**

```css
footer {
  padding: 2rem 3rem;
  border-top: 1px solid var(--border);
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: 'DM Mono', monospace;
  font-size: .68rem;
  color: var(--text-muted);
  letter-spacing: .05em;
  background: var(--bg);
}
footer .social-footer {
  display: flex;
  gap: 1rem;
}
footer .social-footer a {
  color: var(--text-muted);
  transition: color .2s;
}
footer .social-footer a:hover { color: var(--primary); }

@media (max-width: 600px) {
  footer { flex-direction: column; gap: 1rem; text-align: center; }
}
```

- [ ] **Step 4: Footer HTML güncelleme**

```html
<footer>
  <span>İlker Halil Türer</span>
  <div class="social-footer">
    <a href="https://github.com/ilkerhalil" target="_blank">GitHub</a>
    <a href="https://linkedin.com/in/ilker-halil-turer" target="_blank">LinkedIn</a>
    <a href="https://twitter.com/ilkerhalil" target="_blank">Twitter</a>
  </div>
  <span>© 2026</span>
</footer>
```

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: update contact section and footer with social links"
```

---

## Chunk 10: Animasyonlar ve Performans

### Task 13: Enhanced Animasyonlar

**Files:**
- Modify: `index.html:93-95` (reveal CSS) ve script section

- [ ] **Step 1: Daha zengin reveal animasyonları**

```css
.reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity .7s ease, transform .7s ease;
}
.reveal.in {
  opacity: 1;
  transform: none;
}

/* Staggered delays for children */
.reveal:nth-child(1) { transition-delay: 0s; }
.reveal:nth-child(2) { transition-delay: 0.1s; }
.reveal:nth-child(3) { transition-delay: 0.2s; }
.reveal:nth-child(4) { transition-delay: 0.3s; }
.reveal:nth-child(5) { transition-delay: 0.4s; }
.reveal:nth-child(6) { transition-delay: 0.5s; }

/* Smooth scrolling */
html { scroll-behavior: smooth; }
```

- [ ] **Step 2: Script'te parallax ve daha smooth animasyon**

```javascript
// Enhanced scroll animations with parallax
window.addEventListener('scroll', () => {
  const scrolled = window.scrollY;
  const nav = document.getElementById('nav');

  // Nav background
  if (scrolled > 40) {
    nav.classList.add('scrolled');
  } else {
    nav.classList.remove('scrolled');
  }

  // Subtle parallax on hero
  const hero = document.querySelector('.hero-name');
  if (hero) {
    hero.style.transform = `translateY(${scrolled * 0.15}px)`;
    hero.style.opacity = 1 - (scrolled * 0.002);
  }
});

// Intersection Observer with more options
const obsOptions = {
  root: null,
  rootMargin: '0px',
  threshold: 0.1
};

const obs = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('in');
      // Optionally unobserve after reveal
      // obs.unobserve(entry.target);
    }
  });
}, obsOptions);

document.querySelectorAll('.reveal').forEach(el => obs.observe(el));
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add enhanced scroll animations and parallax effects"
```

---

### Task 14: Performans Optimizasyonları

**Files:**
- Modify: `index.html` - head section

- [ ] **Step 1: Performans için head optimizasyonları**

```html
<head>
  <!-- Mevcut meta tags... -->

  <!-- Preconnect for performance -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link rel="preconnect" href="https://github.com">

  <!-- Font display swap -->
  <link href="https://fonts.googleapis.com/css2?family=Lora:ital,wght@0,400;0,500;1,400&family=DM+Sans:wght@300;400;500&family=DM+Mono:wght@300;400&display=swap" rel="stylesheet">

  <!-- Critical CSS inline (move some styles here) -->
  <style>
    body { opacity: 0; } /* Prevent FOUC */
    body.loaded { opacity: 1; transition: opacity 0.3s; }
  </style>

  <!-- Mevcut style tag... -->
</head>
```

- [ ] **Step 2: Script'te FOUC önleme**

```javascript
// Add loaded class after DOM ready
document.addEventListener('DOMContentLoaded', () => {
  document.body.classList.add('loaded');
});
```

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "perf: add performance optimizations (preconnect, font-display, FOUC prevention)"
```

---

## Chunk 11: Final Touches ve Test

### Task 15: Responsive Hamburger Menu (Mobile)

**Files:**
- Modify: `index.html` - nav section ve CSS

- [ ] **Step 1: Mobile hamburger menu**

```html
<!-- Nav'da hamburger button ekle -->
<button class="mobile-menu-btn" id="mobile-menu-btn" aria-label="Toggle menu">
  <span></span>
  <span></span>
  <span></span>
</button>
```

```css
.mobile-menu-btn {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 4px;
}

.mobile-menu-btn span {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--text);
  transition: all .3s;
}

.mobile-menu-btn.active span:nth-child(1) {
  transform: rotate(45deg) translate(5px, 5px);
}
.mobile-menu-btn.active span:nth-child(2) { opacity: 0; }
.mobile-menu-btn.active span:nth-child(3) {
  transform: rotate(-45deg) translate(5px, -5px);
}

@media (max-width: 768px) {
  .mobile-menu-btn { display: flex; }
  .nav-links {
    position: fixed;
    top: 60px;
    left: 0;
    right: 0;
    background: var(--bg);
    flex-direction: column;
    padding: 1rem;
    gap: 0;
    border-bottom: 1px solid var(--border);
    display: none;
  }
  .nav-links.active { display: flex; }
  .nav-links li { border-bottom: 1px solid var(--border); }
  .nav-links a { display: block; padding: 1rem; }
}
```

```javascript
// Mobile menu toggle
const mobileMenuBtn = document.getElementById('mobile-menu-btn');
const navLinks = document.querySelector('.nav-links');

mobileMenuBtn?.addEventListener('click', () => {
  mobileMenuBtn.classList.toggle('active');
  navLinks.classList.toggle('active');
});

// Close menu when clicking a link
document.querySelectorAll('.nav-links a').forEach(link => {
  link.addEventListener('click', () => {
    mobileMenuBtn.classList.remove('active');
    navLinks.classList.remove('active');
  });
});
```

- [ ] **Step 2: Commit**

```bash
git add index.html
git commit -m "feat: add responsive hamburger menu for mobile"
```

---

### Task 16: Final Test ve Kontrol

**Files:**
- Test: Manual browser test

- [ ] **Step 1: Tüm bölümlerin görünürlüğünü kontrol et**
  - Hero, Skills, Projects, Blog, Testimonials, Speaking, GitHub, Experience, Contact

- [ ] **Step 2: Theme toggle çalışıyor mu?**
  - Açık/koyu mod geçişi
  - localStorage'a kaydediliyor mu?

- [ ] **Step 3: Responsive tasarım**
  - Mobile, tablet, desktop görünümler

- [ ] **Step 4: Animasyonlar**
  - Scroll-triggered reveal
  - Hover efektleri

- [ ] **Step 5: Final commit**

```bash
git add .
git commit -m "feat: complete website redesign - all sections, theme toggle, animations

- Visual: Live colors (cyan, coral, magenta), gradient buttons
- Sections: Projects, Blog, Testimonials, Speaking, GitHub
- Features: Theme toggle, social icons, enhanced animations
- Performance: Preconnect, font-display swap, FOUC prevention
- Mobile: Hamburger menu, responsive grid"

git push origin main
```

---

## Özet

Bu plan toplam **16 task** içeriyor, her biri küçük ve yönetilebilir adımlara ayrılmış:

1. CSS Variables & Colors
2. Theme Toggle JS
3. Navbar Update
4. Hero Section
5. Skills Section
6. Projects Section (NEW)
7. Blog Section (NEW)
8. Testimonials (NEW)
9. Speaking (NEW)
10. GitHub Section (NEW)
11. Experience Update
12. Contact + Footer Update
13. Enhanced Animations
14. Performance
15. Mobile Menu
16. Final Test

Her task commit ile sonlanır - böylece ilerlemenin geri alınması kolaydır.