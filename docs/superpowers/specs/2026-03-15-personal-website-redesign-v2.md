# Personal Website Redesign - Design Specification

**Version:** 2.0
**Date:** 2026-03-15
**Author:** Claude

## Overview

Complete redesign of ilkerhalil.github.io with a "Smart Minimal" aesthetic combining terminal/code editor visual language with professional corporate polish. The site showcases a senior software architect's profile with 14+ years of experience.

---

## Design Direction

### Aesthetic

- **Style:** Smart Minimal - Terminal/Code Editor aesthetic meets Professional Corporate
- **Mood:** Technical yet approachable, distinctive but not flashy

### Color Palette

| Role | Color | Usage |
|------|-------|-------|
| Background | `#0d0d12` (dark charcoal) | Main body, hero |
| Surface | `#16161e` | Cards, code blocks |
| Surface Light | `#1e1e28` | Hover states |
| Text Primary | `#e8e6e3` | Headings, important text |
| Text Secondary | `#9a9a9a` | Body text, descriptions |
| Accent | `#d4a574` (warm gold) | Links, highlights, buttons |
| Accent Hover | `#e6b885` | Hover states |
| Border | `#2a2a35` | Separators, code block borders |
| Code Syntax | `#7aa2f7` (blue), `#bb9af7` (purple), `#9ece6a` (green) | Syntax highlighting |

### Typography

- **Headings:** "JetBrains Mono" or "Fira Code" - monospace, tech feel
- **Body:** "DM Sans" or "Inter" - clean, readable
- **Code/Accent:** "JetBrains Mono" - terminal aesthetic

Font sizes scaled with clamp() for responsive design.

---

## Page Sections

### 1. Navigation

- Fixed top navbar, transparent initially, solid on scroll
- Logo/Name on left (monospace font)
- Links: Skills, Experience, Contact
- Minimal, clean - no hamburger menu on desktop

### 2. Hero Section

**Visual:** Terminal prompt aesthetic
```
ilker@portfolio ~ $
```

**Content:**
- Terminal-style greeting with prompt animation
- Name as main heading (large, prominent)
- Role/title below
- Short bio (2-3 lines)
- CTA buttons: "Get in touch", "View Experience"
- Stats row: Years, Mentored, Cost Reduction

**Animation:**
- Typing effect for the terminal prompt
- Fade-in for content blocks

### 3. Skills Section

**Visual:** Code editor / IDE aesthetic
- Skill categories as "import" statements
- Pills displayed as code syntax (e.g., `const skills = [.NET, Python]`)

```
Backend & Languages
─────────────────────────────────
> const backend = ["C#", ".NET Core", "Python", "FastAPI"];

Cloud & Infrastructure
─────────────────────────────────
> const cloud = ["AWS", "Kubernetes", "Docker", "Terraform"];

AI & Machine Learning
─────────────────────────────────
> const ai = ["Ollama", "MCP Protocol", "RAG", "CatBoost"];
```

### 4. Experience Section

**Visual:** Detailed, professional, CV-style

Each position includes:
- Company name + dates (terminal prompt style: `> 2020 - Present`)
- Job title (heading)
- Detailed bullet points describing achievements
- Technology tags (as code comments)

```
> Intertech — 2020 - Present
─────────────────────────────────
## Senior Software Architect

• Architected enterprise-scale cloud infrastructure on AWS EKS
• Achieved 40% infrastructure cost reduction through legacy modernization
• Led team of 20+ developers with mentoring and code reviews
• Spearheaded AI/ML integration initiatives

// Tags: [.NET Core] [AWS EKS] [Kubernetes] [Python] [AI/ML]
```

### 5. Contact Section

**Visual:** Terminal chat / prompt interface

```
~ $ contact --init
```

- Tagline as terminal output
- Contact links as terminal commands
- Info table styled as JSON or config

```json
{
  "email": "ilkerhalil@gmail.com",
  "linkedin": "linkedin.com/in/ilker-halil-turer",
  "github": "github.com/ilkerhalil",
  "status": "open_to_work",
  "location": "Izmir, Turkey"
}
```

---

## Animations & Interactions

1. **Page Load:**
   - Terminal typing effect for prompts (100ms per character)
   - Staggered fade-in for content sections

2. **Scroll:**
   - Elements reveal with subtle slide-up + fade
   - Navbar becomes solid after scrolling 40px

3. **Hover:**
   - Buttons: slight scale + color shift
   - Links: accent color underline animation
   - Skill tags: subtle glow effect

4. **Code Blocks:**
   - Subtle scanline or gradient overlay (optional)
   - Syntax colors remain static

---

## Responsive Breakpoints

| Breakpoint | Width | Adjustments |
|------------|-------|-------------|
| Desktop | > 1024px | Full layout, multi-column |
| Tablet | 768px - 1024px | Reduced padding, single column |
| Mobile | < 768px | Stacked layout, simplified nav |

---

## Content Updates (from CV)

### Updated Bio
Current: "I've been working on software architecture and cloud infrastructure for 14 years..."

New (based on CV):
- Add AWS Certified Solutions Architect mention
- Add CKA (Certified Kubernetes Administrator)
- Emphasize AI/ML work more strongly

### Experience Updates
Based on CV details:
- Intertech: Add specific achievements (AWS migration, cost reduction, team leadership)
- Add more detail to earlier roles if available

---

## Acceptance Criteria

1. ✅ Terminal/code editor aesthetic is clearly visible
2. ✅ Color scheme is consistent (dark with gold accents)
3. ✅ Hero has typing animation
4. ✅ Skills displayed in code-syntax style
5. ✅ Experience section is detailed with bullet points
6. ✅ Contact uses terminal/chat interface
7. ✅ Fully responsive on mobile
8. ✅ Animations are smooth (60fps)
9. ✅ Accessible (contrast ratios, keyboard navigation)

---

## Technical Implementation

- Single HTML file with embedded CSS/JS
- No external frameworks (vanilla JS)
- Google Fonts: JetBrains Mono, DM Sans
- CSS custom properties for theming
- Intersection Observer for scroll animations
- Minimal JS (typing effect, navbar scroll, reveal animations)