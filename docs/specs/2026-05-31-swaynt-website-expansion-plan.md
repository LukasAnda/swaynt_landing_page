# Swaynt Website Expansion Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Expand Swaynt from a single-page landing site to a 5-page website (Home, About, Services, Contact, Privacy) to meet Apple Developer Program enrollment requirements.

**Architecture:** Static HTML/CSS site for GitHub Pages. Extract shared CSS to a stylesheet, create consistent nav/footer across all pages, maintain existing dark theme aesthetic with DM Serif Display + Outfit typography.

**Tech Stack:** HTML5, CSS3, vanilla JavaScript (email obfuscation only)

---

## File Structure

```
styles.css      → Shared stylesheet (extracted from index.html)
index.html      → Home (update nav, services grid, footer)
about.html      → About page (new)
services.html   → Services page (new)
contact.html    → Contact page (new)
privacy.html    → Privacy Policy page (new)
```

---

### Task 1: Extract Shared CSS to Stylesheet

**Files:**
- Create: `styles.css`
- Modify: `index.html`

- [ ] **Step 1: Create styles.css with all shared styles**

Create `styles.css` with the full CSS from index.html, plus new styles for page-specific elements:

```css
*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --bg: #080808;
  --text: #ffffff;
  --muted: #777777;
  --subtle: #4a4a4a;
  --dim: #2a2a2a;
  --border: #171717;
  --accent-bg: #ffffff;
  --accent-text: #000000;
  --font-display: 'DM Serif Display', Georgia, 'Times New Roman', serif;
  --font-body: 'Outfit', -apple-system, BlinkMacSystemFont, system-ui, sans-serif;
}

html {
  scroll-behavior: smooth;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-body);
  font-weight: 400;
  overflow-x: hidden;
}

body::after {
  content: '';
  position: fixed;
  inset: 0;
  z-index: 9999;
  pointer-events: none;
  opacity: 0.03;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  background-repeat: repeat;
  background-size: 256px 256px;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding-left: 64px;
  padding-right: 64px;
}

/* Animations */
@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translateY(24px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes lineReveal {
  from { transform: scaleX(0); }
  to { transform: scaleX(1); }
}

.animate-up {
  opacity: 0;
  animation: fadeUp 0.8s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}

.animate-fade {
  opacity: 0;
  animation: fadeIn 0.6s ease forwards;
}

/* Navigation */
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 40px;
  padding-bottom: 40px;
}

.logo {
  font-family: var(--font-body);
  font-size: 15px;
  font-weight: 600;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: var(--text);
  text-decoration: none;
  animation: fadeIn 0.6s ease 0.1s both;
}

.nav-links {
  display: flex;
  gap: 32px;
  animation: fadeIn 0.6s ease 0.2s both;
}

.nav-link {
  font-family: var(--font-body);
  font-size: 13px;
  font-weight: 400;
  color: var(--muted);
  text-decoration: none;
  letter-spacing: 0.5px;
  transition: color 0.3s ease;
}

.nav-link:hover,
.nav-link.active {
  color: var(--text);
}

/* Hero */
.hero {
  padding-top: 100px;
  padding-bottom: 160px;
  position: relative;
}

.hero h1 {
  font-family: var(--font-display);
  font-size: clamp(40px, 6vw, 76px);
  font-weight: 400;
  line-height: 1.1;
  letter-spacing: -1px;
  max-width: 720px;
  animation-delay: 0.15s;
}

.hero p {
  font-size: 17px;
  font-weight: 300;
  color: var(--muted);
  line-height: 1.75;
  max-width: 440px;
  margin-top: 36px;
  animation-delay: 0.3s;
}

.hero-cta {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  margin-top: 52px;
  padding: 15px 32px;
  background: var(--accent-bg);
  color: var(--accent-text);
  font-family: var(--font-body);
  font-size: 14px;
  font-weight: 500;
  text-decoration: none;
  border-radius: 100px;
  letter-spacing: 0.3px;
  transition: transform 0.3s cubic-bezier(0.22, 1, 0.36, 1),
              box-shadow 0.3s ease;
  animation-delay: 0.45s;
}

.hero-cta:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 40px rgba(255, 255, 255, 0.08);
}

.hero-cta::after {
  content: '→';
  font-size: 16px;
  transition: transform 0.3s ease;
}

.hero-cta:hover::after {
  transform: translateX(3px);
}

/* Page Header (for inner pages) */
.page-header {
  padding-top: 100px;
  padding-bottom: 80px;
}

.page-header h1 {
  font-family: var(--font-display);
  font-size: clamp(36px, 5vw, 56px);
  font-weight: 400;
  line-height: 1.15;
  letter-spacing: -0.5px;
  max-width: 600px;
  animation-delay: 0.15s;
}

.page-header p {
  font-size: 17px;
  font-weight: 300;
  color: var(--muted);
  line-height: 1.75;
  max-width: 540px;
  margin-top: 24px;
  animation-delay: 0.3s;
}

/* Page Content */
.page-content {
  padding-bottom: 120px;
}

.page-content p {
  font-size: 16px;
  font-weight: 300;
  color: var(--muted);
  line-height: 1.8;
  max-width: 600px;
  margin-bottom: 24px;
}

.page-content h2 {
  font-family: var(--font-display);
  font-size: 28px;
  font-weight: 400;
  margin-top: 64px;
  margin-bottom: 24px;
  letter-spacing: -0.3px;
}

.page-content h3 {
  font-family: var(--font-body);
  font-size: 14px;
  font-weight: 500;
  color: var(--text);
  margin-top: 48px;
  margin-bottom: 16px;
  letter-spacing: 0.5px;
}

.page-content ul {
  list-style: none;
  padding: 0;
  margin: 0 0 24px 0;
}

.page-content li {
  font-size: 15px;
  font-weight: 300;
  color: var(--muted);
  line-height: 1.8;
  padding-left: 20px;
  position: relative;
  margin-bottom: 8px;
}

.page-content li::before {
  content: '—';
  position: absolute;
  left: 0;
  color: var(--subtle);
}

/* Divider */
.divider {
  height: 1px;
  background: var(--border);
  transform-origin: left center;
  animation: lineReveal 1s cubic-bezier(0.22, 1, 0.36, 1) 0.5s both;
}

.divider-delayed {
  animation-delay: 1.2s;
}

/* Services Grid */
.services {
  padding-top: 100px;
  padding-bottom: 120px;
}

.services-label {
  font-family: var(--font-body);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--subtle);
  margin-bottom: 72px;
  animation-delay: 0.6s;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 48px;
}

.service-item {
  opacity: 0;
  animation: fadeUp 0.7s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}

.service-item:nth-child(1) { animation-delay: 0.7s; }
.service-item:nth-child(2) { animation-delay: 0.82s; }
.service-item:nth-child(3) { animation-delay: 0.94s; }
.service-item:nth-child(4) { animation-delay: 1.06s; }

.service-number {
  font-family: var(--font-body);
  font-size: 12px;
  font-weight: 400;
  color: var(--dim);
  margin-bottom: 20px;
  letter-spacing: 1px;
}

.service-item h3 {
  font-family: var(--font-display);
  font-size: 22px;
  font-weight: 400;
  margin-bottom: 14px;
  letter-spacing: -0.2px;
}

.service-item p {
  font-size: 14px;
  font-weight: 300;
  color: var(--muted);
  line-height: 1.75;
}

/* Services Page Detailed Cards */
.service-detail {
  padding: 48px 0;
  border-bottom: 1px solid var(--border);
}

.service-detail:last-child {
  border-bottom: none;
}

.service-detail h2 {
  font-family: var(--font-display);
  font-size: 32px;
  font-weight: 400;
  margin-bottom: 20px;
  letter-spacing: -0.3px;
}

.service-detail p {
  font-size: 16px;
  font-weight: 300;
  color: var(--muted);
  line-height: 1.8;
  max-width: 600px;
  margin-bottom: 16px;
}

/* Contact Info */
.contact-info {
  padding-top: 40px;
}

.contact-block {
  margin-bottom: 48px;
}

.contact-label {
  font-family: var(--font-body);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--subtle);
  margin-bottom: 16px;
}

.contact-value {
  font-size: 18px;
  font-weight: 400;
  color: var(--text);
  line-height: 1.6;
}

.contact-value a {
  color: var(--text);
  text-decoration: none;
  transition: color 0.3s ease;
}

.contact-value a:hover {
  color: var(--muted);
}

/* Footer */
footer {
  padding-top: 64px;
  padding-bottom: 48px;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}

.footer-left {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.footer-right {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 8px;
}

.footer-copy,
.footer-address {
  font-size: 13px;
  font-weight: 300;
  color: var(--subtle);
  letter-spacing: 0.3px;
}

.footer-link {
  font-size: 13px;
  font-weight: 400;
  color: var(--muted);
  text-decoration: none;
  letter-spacing: 0.3px;
  transition: color 0.3s ease;
}

.footer-link:hover {
  color: var(--text);
}

/* Responsive: Tablet */
@media (max-width: 768px) {
  .container {
    padding-left: 32px;
    padding-right: 32px;
  }

  nav {
    padding-top: 28px;
    padding-bottom: 28px;
  }

  .nav-links {
    gap: 24px;
  }

  .hero {
    padding-top: 72px;
    padding-bottom: 100px;
  }

  .hero p {
    font-size: 16px;
  }

  .page-header {
    padding-top: 72px;
    padding-bottom: 60px;
  }

  .services {
    padding-top: 72px;
    padding-bottom: 80px;
  }

  .services-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 48px 40px;
  }

  footer {
    flex-direction: column;
    align-items: flex-start;
    gap: 24px;
    padding-top: 48px;
    padding-bottom: 36px;
  }

  .footer-right {
    align-items: flex-start;
  }
}

/* Responsive: Mobile */
@media (max-width: 480px) {
  .container {
    padding-left: 24px;
    padding-right: 24px;
  }

  .nav-links {
    gap: 16px;
  }

  .nav-link {
    font-size: 12px;
  }

  .hero {
    padding-top: 56px;
    padding-bottom: 80px;
  }

  .services-grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }

  .services-label {
    margin-bottom: 48px;
  }
}
```

- [ ] **Step 2: Update index.html to use external stylesheet**

Replace the `<style>` block in index.html with a link to the stylesheet. In the `<head>` section, after the Google Fonts link, add:

```html
<link rel="stylesheet" href="styles.css">
```

Remove the entire `<style>...</style>` block (lines 16-356 in the original file).

- [ ] **Step 3: Verify the page still renders correctly**

Open `index.html` in a browser and verify:
- All styles are applied correctly
- Animations work
- Responsive breakpoints work (resize window)

- [ ] **Step 4: Commit**

```bash
git add styles.css index.html
git commit -m "refactor: extract CSS to shared stylesheet"
```

---

### Task 2: Update Home Page Navigation and Footer

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Update navigation with links**

Replace the current nav section:

```html
<div class="container">
  <nav>
    <div class="logo">Swaynt</div>
    <a href="#contact" class="nav-link">Get in touch</a>
  </nav>
</div>
```

With:

```html
<div class="container">
  <nav>
    <a href="index.html" class="logo">Swaynt</a>
    <div class="nav-links">
      <a href="about.html" class="nav-link">About</a>
      <a href="services.html" class="nav-link">Services</a>
      <a href="contact.html" class="nav-link">Contact</a>
    </div>
  </nav>
</div>
```

- [ ] **Step 2: Update services grid content**

Replace the current services grid content with mobile-focused items:

```html
<div class="services-grid">
  <div class="service-item">
    <div class="service-number">01</div>
    <h3>iOS & Android</h3>
    <p>Native apps for both platforms, built to feel right on each device.</p>
  </div>
  <div class="service-item">
    <div class="service-number">02</div>
    <h3>Kotlin Multiplatform</h3>
    <p>One codebase, native performance on both platforms. No compromises.</p>
  </div>
  <div class="service-item">
    <div class="service-number">03</div>
    <h3>Quality First</h3>
    <p>Clean code, thoroughly tested, built to last and easy to maintain.</p>
  </div>
  <div class="service-item">
    <div class="service-number">04</div>
    <h3>Full Lifecycle</h3>
    <p>From concept to App Store submission, we handle the entire journey.</p>
  </div>
</div>
```

- [ ] **Step 3: Update footer**

Replace the current footer:

```html
<div class="container">
  <footer id="contact">
    <div class="footer-copy">&copy; 2026 Swaynt</div>
    <a href="#" class="footer-email" onclick="return false;">
      <span id="e"></span>
    </a>
  </footer>
</div>
```

With:

```html
<div class="container">
  <div class="divider"></div>
</div>

<div class="container">
  <footer>
    <div class="footer-left">
      <div class="footer-copy">&copy; 2026 Swaynt LLC</div>
      <div class="footer-address">75 E 3rd St, Sheridan, WY 82801</div>
    </div>
    <div class="footer-right">
      <a href="privacy.html" class="footer-link">Privacy Policy</a>
      <a href="#" class="footer-link" onclick="return false;"><span id="e"></span></a>
    </div>
  </footer>
</div>
```

- [ ] **Step 4: Update hero CTA link**

Change the hero CTA from `#contact` to `contact.html`:

```html
<a href="contact.html" class="hero-cta animate-up">Get in touch</a>
```

- [ ] **Step 5: Verify in browser**

Open index.html and check:
- Navigation links are visible and styled
- Services grid shows mobile-focused content
- Footer shows address and privacy link
- Email obfuscation still works

- [ ] **Step 6: Commit**

```bash
git add index.html
git commit -m "feat: update home page with new nav, services, and footer"
```

---

### Task 3: Create About Page

**Files:**
- Create: `about.html`

- [ ] **Step 1: Create about.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>About — Swaynt</title>
  <meta name="description" content="Swaynt is an independent software studio founded in 2026. We craft mobile apps and games with a focus on quality over quantity.">
  <meta property="og:title" content="About — Swaynt">
  <meta property="og:description" content="An independent software studio focused on craft.">
  <meta property="og:type" content="website">
  <meta property="og:url" content="https://swaynt.com/about">
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><circle cx='50' cy='50' r='50' fill='%230a0a0a'/><text x='50' y='68' font-family='Georgia,serif' font-size='52' font-weight='bold' fill='white' text-anchor='middle'>S</text></svg>">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=Outfit:wght@300;400;500;600&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <div class="container">
    <nav>
      <a href="index.html" class="logo">Swaynt</a>
      <div class="nav-links">
        <a href="about.html" class="nav-link active">About</a>
        <a href="services.html" class="nav-link">Services</a>
        <a href="contact.html" class="nav-link">Contact</a>
      </div>
    </nav>
  </div>

  <div class="container">
    <section class="page-header">
      <h1 class="animate-up">Building software<br>with intention.</h1>
    </section>
  </div>

  <div class="container">
    <div class="divider"></div>
  </div>

  <div class="container">
    <section class="page-content">
      <p class="animate-up" style="animation-delay: 0.3s;">Swaynt is an independent software studio founded in 2026. We craft mobile apps and games with a focus on quality over quantity.</p>
      <p class="animate-up" style="animation-delay: 0.45s;">We believe great software comes from small teams with clear vision. Every project gets our full attention — no assembly lines, no shortcuts.</p>
    </section>
  </div>

  <div class="container">
    <div class="divider"></div>
  </div>

  <div class="container">
    <footer>
      <div class="footer-left">
        <div class="footer-copy">&copy; 2026 Swaynt LLC</div>
        <div class="footer-address">75 E 3rd St, Sheridan, WY 82801</div>
      </div>
      <div class="footer-right">
        <a href="privacy.html" class="footer-link">Privacy Policy</a>
        <a href="#" class="footer-link" onclick="return false;"><span id="e"></span></a>
      </div>
    </footer>
  </div>

  <script>
    (function(){
      var p=['s','u','p','p','o','r','t'];
      var d=String.fromCharCode(64);
      var h=['s','w','a','y','n','t'];
      var t=['.','c','o','m'];
      var r=p.join('')+d+h.join('')+t.join('');
      var el=document.getElementById('e');
      el.textContent=r;
      el.parentElement.href='mai'+'lto:'+r;
      el.parentElement.onclick=null;
    })();
  </script>

</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Open about.html and check:
- Navigation shows "About" as active
- Content displays correctly
- Footer is consistent with home page
- Responsive at all breakpoints

- [ ] **Step 3: Commit**

```bash
git add about.html
git commit -m "feat: add about page"
```

---

### Task 4: Create Services Page

**Files:**
- Create: `services.html`

- [ ] **Step 1: Create services.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Services — Swaynt</title>
  <meta name="description" content="Mobile app development with Kotlin Multiplatform. Native iOS and Android apps from a single codebase.">
  <meta property="og:title" content="Services — Swaynt">
  <meta property="og:description" content="Mobile app development with Kotlin Multiplatform.">
  <meta property="og:type" content="website">
  <meta property="og:url" content="https://swaynt.com/services">
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><circle cx='50' cy='50' r='50' fill='%230a0a0a'/><text x='50' y='68' font-family='Georgia,serif' font-size='52' font-weight='bold' fill='white' text-anchor='middle'>S</text></svg>">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=Outfit:wght@300;400;500;600&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <div class="container">
    <nav>
      <a href="index.html" class="logo">Swaynt</a>
      <div class="nav-links">
        <a href="about.html" class="nav-link">About</a>
        <a href="services.html" class="nav-link active">Services</a>
        <a href="contact.html" class="nav-link">Contact</a>
      </div>
    </nav>
  </div>

  <div class="container">
    <section class="page-header">
      <h1 class="animate-up">Mobile Development</h1>
      <p class="animate-up">Native iOS and Android apps built with Kotlin Multiplatform — one codebase, no compromises on performance or user experience.</p>
    </section>
  </div>

  <div class="container">
    <div class="divider"></div>
  </div>

  <div class="container">
    <section class="page-content">
      <div class="service-detail animate-up" style="animation-delay: 0.3s;">
        <h2>Why Kotlin Multiplatform</h2>
        <p>Kotlin Multiplatform lets us share business logic across iOS and Android while keeping the UI fully native. You get the efficiency of shared code without sacrificing the polish users expect from a native app.</p>
        <p>Unlike cross-platform frameworks that wrap everything in a compatibility layer, KMP compiles directly to native code. The result is apps that perform like they were built specifically for each platform — because the parts that matter are.</p>
      </div>

      <div class="service-detail animate-up" style="animation-delay: 0.45s;">
        <h2>Our Process</h2>
        <p>Every project starts with understanding what you're building and why. We work closely with you to define scope, prioritize features, and set realistic timelines.</p>
        <p>Development happens in short cycles with regular builds you can test. No disappearing for months — you see progress as it happens and can course-correct early.</p>
      </div>

      <div class="service-detail animate-up" style="animation-delay: 0.6s;">
        <h2>What You Get</h2>
        <ul>
          <li>Native iOS and Android apps from a single codebase</li>
          <li>Clean, maintainable code with comprehensive documentation</li>
          <li>App Store and Play Store submission support</li>
          <li>Source code ownership — it's yours</li>
        </ul>
      </div>
    </section>
  </div>

  <div class="container">
    <div class="divider"></div>
  </div>

  <div class="container">
    <footer>
      <div class="footer-left">
        <div class="footer-copy">&copy; 2026 Swaynt LLC</div>
        <div class="footer-address">75 E 3rd St, Sheridan, WY 82801</div>
      </div>
      <div class="footer-right">
        <a href="privacy.html" class="footer-link">Privacy Policy</a>
        <a href="#" class="footer-link" onclick="return false;"><span id="e"></span></a>
      </div>
    </footer>
  </div>

  <script>
    (function(){
      var p=['s','u','p','p','o','r','t'];
      var d=String.fromCharCode(64);
      var h=['s','w','a','y','n','t'];
      var t=['.','c','o','m'];
      var r=p.join('')+d+h.join('')+t.join('');
      var el=document.getElementById('e');
      el.textContent=r;
      el.parentElement.href='mai'+'lto:'+r;
      el.parentElement.onclick=null;
    })();
  </script>

</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Open services.html and check:
- Navigation shows "Services" as active
- All three sections display correctly
- List items render with dashes
- Footer is consistent

- [ ] **Step 3: Commit**

```bash
git add services.html
git commit -m "feat: add services page with KMP focus"
```

---

### Task 5: Create Contact Page

**Files:**
- Create: `contact.html`

- [ ] **Step 1: Create contact.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact — Swaynt</title>
  <meta name="description" content="Get in touch with Swaynt. Email us at support@swaynt.com.">
  <meta property="og:title" content="Contact — Swaynt">
  <meta property="og:description" content="Get in touch with Swaynt.">
  <meta property="og:type" content="website">
  <meta property="og:url" content="https://swaynt.com/contact">
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><circle cx='50' cy='50' r='50' fill='%230a0a0a'/><text x='50' y='68' font-family='Georgia,serif' font-size='52' font-weight='bold' fill='white' text-anchor='middle'>S</text></svg>">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=Outfit:wght@300;400;500;600&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <div class="container">
    <nav>
      <a href="index.html" class="logo">Swaynt</a>
      <div class="nav-links">
        <a href="about.html" class="nav-link">About</a>
        <a href="services.html" class="nav-link">Services</a>
        <a href="contact.html" class="nav-link active">Contact</a>
      </div>
    </nav>
  </div>

  <div class="container">
    <section class="page-header">
      <h1 class="animate-up">Get in touch</h1>
    </section>
  </div>

  <div class="container">
    <div class="divider"></div>
  </div>

  <div class="container">
    <section class="contact-info page-content">
      <div class="contact-block animate-up" style="animation-delay: 0.3s;">
        <div class="contact-label">Email</div>
        <div class="contact-value">
          <a href="#" onclick="return false;"><span id="e"></span></a>
        </div>
      </div>

      <div class="contact-block animate-up" style="animation-delay: 0.45s;">
        <div class="contact-label">Address</div>
        <div class="contact-value">
          75 E 3rd St<br>
          Sheridan, WY 82801<br>
          USA
        </div>
      </div>
    </section>
  </div>

  <div class="container">
    <div class="divider"></div>
  </div>

  <div class="container">
    <footer>
      <div class="footer-left">
        <div class="footer-copy">&copy; 2026 Swaynt LLC</div>
        <div class="footer-address">75 E 3rd St, Sheridan, WY 82801</div>
      </div>
      <div class="footer-right">
        <a href="privacy.html" class="footer-link">Privacy Policy</a>
        <a href="#" class="footer-link" onclick="return false;"><span id="e2"></span></a>
      </div>
    </footer>
  </div>

  <script>
    (function(){
      var p=['s','u','p','p','o','r','t'];
      var d=String.fromCharCode(64);
      var h=['s','w','a','y','n','t'];
      var t=['.','c','o','m'];
      var r=p.join('')+d+h.join('')+t.join('');
      
      var el=document.getElementById('e');
      el.textContent=r;
      el.parentElement.href='mai'+'lto:'+r;
      el.parentElement.onclick=null;
      
      var el2=document.getElementById('e2');
      if(el2){
        el2.textContent=r;
        el2.parentElement.href='mai'+'lto:'+r;
        el2.parentElement.onclick=null;
      }
    })();
  </script>

</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Open contact.html and check:
- Navigation shows "Contact" as active
- Email and address display correctly
- Email obfuscation works (click opens mailto)
- Footer is consistent

- [ ] **Step 3: Commit**

```bash
git add contact.html
git commit -m "feat: add contact page"
```

---

### Task 6: Create Privacy Policy Page

**Files:**
- Create: `privacy.html`

- [ ] **Step 1: Create privacy.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Privacy Policy — Swaynt</title>
  <meta name="description" content="Privacy Policy for Swaynt LLC website and mobile applications.">
  <meta property="og:title" content="Privacy Policy — Swaynt">
  <meta property="og:description" content="Privacy Policy for Swaynt LLC.">
  <meta property="og:type" content="website">
  <meta property="og:url" content="https://swaynt.com/privacy">
  <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><circle cx='50' cy='50' r='50' fill='%230a0a0a'/><text x='50' y='68' font-family='Georgia,serif' font-size='52' font-weight='bold' fill='white' text-anchor='middle'>S</text></svg>">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=Outfit:wght@300;400;500;600&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <div class="container">
    <nav>
      <a href="index.html" class="logo">Swaynt</a>
      <div class="nav-links">
        <a href="about.html" class="nav-link">About</a>
        <a href="services.html" class="nav-link">Services</a>
        <a href="contact.html" class="nav-link">Contact</a>
      </div>
    </nav>
  </div>

  <div class="container">
    <section class="page-header">
      <h1 class="animate-up">Privacy Policy</h1>
      <p class="animate-up">Last updated: May 31, 2026</p>
    </section>
  </div>

  <div class="container">
    <div class="divider"></div>
  </div>

  <div class="container">
    <section class="page-content">
      
      <h2>Introduction</h2>
      <p>Swaynt LLC ("we," "our," or "us") operates the swaynt.com website and mobile applications. This Privacy Policy explains how we collect, use, and protect your information when you use our services.</p>
      <p>By using our website or applications, you agree to the collection and use of information in accordance with this policy.</p>

      <h2>Information We Collect</h2>
      
      <h3>Website</h3>
      <p>When you visit our website, we may collect:</p>
      <ul>
        <li>Basic analytics data (pages visited, time spent, referral source)</li>
        <li>Device information (browser type, operating system)</li>
        <li>IP address (anonymized)</li>
      </ul>

      <h3>Mobile Applications</h3>
      <p>When you use our mobile apps, we may collect:</p>
      <ul>
        <li>Device information (model, operating system version, unique device identifiers)</li>
        <li>Usage data (app features used, session duration, crash reports)</li>
        <li>Advertising identifiers (for displaying relevant ads)</li>
      </ul>

      <h2>How We Use Your Information</h2>
      <p>We use the collected information to:</p>
      <ul>
        <li>Improve app performance and user experience</li>
        <li>Display relevant advertisements</li>
        <li>Fix bugs and prevent crashes</li>
        <li>Analyze usage patterns to guide development</li>
        <li>Respond to your inquiries</li>
      </ul>
      <p>We do not sell your personal information to third parties.</p>

      <h2>Third-Party Services</h2>
      <p>Our applications may use third-party services that collect information:</p>
      <ul>
        <li><strong>Google AdMob</strong> — for displaying advertisements. <a href="https://policies.google.com/privacy" style="color: var(--muted);">Google Privacy Policy</a></li>
        <li><strong>Firebase Analytics</strong> — for app analytics and crash reporting. <a href="https://firebase.google.com/support/privacy" style="color: var(--muted);">Firebase Privacy</a></li>
      </ul>
      <p>These services have their own privacy policies governing their use of your data.</p>

      <h2>Data Retention</h2>
      <p>We retain collected data only as long as necessary to provide our services and fulfill the purposes described in this policy. Analytics data is typically retained for 26 months, after which it is automatically deleted or anonymized.</p>

      <h2>Your Rights</h2>
      <p>Depending on your location, you may have the right to:</p>
      <ul>
        <li>Access the personal data we hold about you</li>
        <li>Request correction of inaccurate data</li>
        <li>Request deletion of your data</li>
        <li>Opt out of certain data collection</li>
      </ul>
      <p>To exercise these rights, contact us at <a href="#" onclick="return false;" style="color: var(--muted);"><span id="e-privacy"></span></a>.</p>

      <h2>Children's Privacy</h2>
      <p>Our services are not directed to children under 13. We do not knowingly collect personal information from children under 13. If you are a parent or guardian and believe your child has provided us with personal information, please contact us so we can delete it.</p>
      <p>For users between 13 and 18, we encourage parental guidance when using our applications.</p>

      <h2>Changes to This Policy</h2>
      <p>We may update this Privacy Policy from time to time. We will notify you of any changes by posting the new Privacy Policy on this page and updating the "Last updated" date.</p>
      <p>We encourage you to review this Privacy Policy periodically for any changes.</p>

      <h2>Contact Us</h2>
      <p>If you have any questions about this Privacy Policy, please contact us:</p>
      <ul>
        <li>Email: <a href="#" onclick="return false;" style="color: var(--muted);"><span id="e-contact"></span></a></li>
        <li>Address: 75 E 3rd St, Sheridan, WY 82801, USA</li>
      </ul>

    </section>
  </div>

  <div class="container">
    <div class="divider"></div>
  </div>

  <div class="container">
    <footer>
      <div class="footer-left">
        <div class="footer-copy">&copy; 2026 Swaynt LLC</div>
        <div class="footer-address">75 E 3rd St, Sheridan, WY 82801</div>
      </div>
      <div class="footer-right">
        <a href="privacy.html" class="footer-link">Privacy Policy</a>
        <a href="#" class="footer-link" onclick="return false;"><span id="e"></span></a>
      </div>
    </footer>
  </div>

  <script>
    (function(){
      var p=['s','u','p','p','o','r','t'];
      var d=String.fromCharCode(64);
      var h=['s','w','a','y','n','t'];
      var t=['.','c','o','m'];
      var r=p.join('')+d+h.join('')+t.join('');
      
      ['e', 'e-privacy', 'e-contact'].forEach(function(id) {
        var el = document.getElementById(id);
        if (el) {
          el.textContent = r;
          if (el.parentElement.tagName === 'A') {
            el.parentElement.href = 'mai' + 'lto:' + r;
            el.parentElement.onclick = null;
          }
        }
      });
    })();
  </script>

</body>
</html>
```

- [ ] **Step 2: Verify in browser**

Open privacy.html and check:
- All sections display correctly
- Links to Google/Firebase privacy policies work
- Email obfuscation works in all three places
- Footer is consistent
- Responsive at all breakpoints

- [ ] **Step 3: Commit**

```bash
git add privacy.html
git commit -m "feat: add privacy policy page"
```

---

### Task 7: Final Verification and Cross-Page Testing

**Files:**
- All HTML files

- [ ] **Step 1: Test all navigation links**

Open each page and click every navigation link:
- Home → About ✓
- Home → Services ✓
- Home → Contact ✓
- About → Home (logo) ✓
- About → Services ✓
- About → Contact ✓
- Services → Home (logo) ✓
- Services → About ✓
- Services → Contact ✓
- Contact → Home (logo) ✓
- Contact → About ✓
- Contact → Services ✓
- Privacy → Home (logo) ✓
- Privacy → About ✓
- Privacy → Services ✓
- Privacy → Contact ✓
- All footers → Privacy ✓

- [ ] **Step 2: Test responsive breakpoints**

For each page, resize browser window to verify:
- Desktop (>768px): Full layout
- Tablet (768px): 2-column services grid, stacked footer
- Mobile (480px): Single-column services grid, smaller nav gaps

- [ ] **Step 3: Test email obfuscation**

On each page, verify:
- Email displays as "support@swaynt.com"
- Clicking opens mailto: link

- [ ] **Step 4: Validate HTML**

Run HTML validation on each file (optional but recommended):
```bash
npx html-validate index.html about.html services.html contact.html privacy.html
```

- [ ] **Step 5: Final commit if any fixes needed**

```bash
git add -A
git commit -m "fix: address any issues found in final verification"
```

(Skip if no changes needed)

- [ ] **Step 6: Push to deploy**

```bash
git push origin main
```

Verify the site is live on GitHub Pages.

---

## Summary

| Task | Description | Files |
|------|-------------|-------|
| 1 | Extract shared CSS | styles.css, index.html |
| 2 | Update home page | index.html |
| 3 | Create about page | about.html |
| 4 | Create services page | services.html |
| 5 | Create contact page | contact.html |
| 6 | Create privacy page | privacy.html |
| 7 | Final verification | All files |

Total: 7 tasks, ~6 commits, estimated time: 45-60 minutes.
