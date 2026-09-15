<div align="center">

# `taseen.dev`
### Personal Portfolio · Technical Blog · Life in Progress

<br/>

<a href="https://taseenkabir.vercel.app">
  <img src="https://readme-typing-svg.demolab.com?font=Space+Mono&weight=700&size=16&duration=3500&pause=1000&color=22D3EE&center=true&vCenter=true&width=620&height=50&lines=Cybersecurity+Enthusiast+%C2%B7+AI+Explorer+%C2%B7+Web+Developer;Pre-university+student+building+production-grade+software." alt="Typing SVG" />
</a>

<br/><br/>

[![Live Site](https://img.shields.io/badge/🌐_Live_Site-taseenkabir.vercel.app-22d3ee?style=for-the-badge&labelColor=0a0a0f)](https://taseenkabir.vercel.app)
![Status](https://img.shields.io/badge/Status-Actively_Maintained-34d399?style=for-the-badge&labelColor=0a0a0f)
![Version](https://img.shields.io/badge/Version-2.0-a78bfa?style=for-the-badge&labelColor=0a0a0f)

<br/>

![Next.js](https://img.shields.io/badge/Next.js-16.1.1-white?style=flat-square&logo=next.js&logoColor=white&labelColor=0a0a0f)
![React](https://img.shields.io/badge/React-19.2.3-61DAFB?style=flat-square&logo=react&labelColor=0a0a0f)
![Three.js](https://img.shields.io/badge/Three.js-r128-white?style=flat-square&logo=three.js&labelColor=0a0a0f)
![Framer Motion](https://img.shields.io/badge/Framer_Motion-12.x-ff0055?style=flat-square&logo=framer&labelColor=0a0a0f)
![Vercel](https://img.shields.io/badge/Deployed_on-Vercel-white?style=flat-square&logo=vercel&labelColor=0a0a0f)

</div>

---

## About This Project

This is the source code of my personal portfolio website — a full-stack web application I designed and built independently as a pre-university student in Dhaka, Bangladesh.

The project began as a simple static portfolio but evolved into a more ambitious undertaking: a complete platform with a content system, dynamic routing, 3D animations, and a component architecture I designed from scratch. I used this project to teach myself production-level frontend engineering — not from a course, but by reading documentation, studying open-source codebases, and iterating on real problems.

I am currently in my final year of secondary education (Class 12, Science stream) at Civil Aviation School & College, Dhaka. My long-term academic goal is to pursue a B.Sc. in Computer Science or Cybersecurity Engineering at a research-focused university. This project is part of my effort to demonstrate technical aptitude and self-directed learning beyond the classroom.

---

## Live Demo

**[`https://taseenkabir.vercel.app`](https://taseenkabir.vercel.app)**

| Route | Content |
|-------|---------|
| `/` | Home — hero, latest articles, skills, projects, contact |
| `/about` | Background, values, quick facts |
| `/blog` | Articles on security, AI, and technology |
| `/journey` | Personal timeline from 2008 to present |
| `/photography` | Nature photography gallery |
| `/404` | Custom error page |

---

## Why I Built This

A GitHub profile with no context tells very little. I wanted to create a space that reflects not just *what* I know, but *how* I think — how I approach problems, what I find interesting, and what I am still learning.

The secondary goal was practical: building this forced me to work through real engineering decisions under real constraints. No instructor to ask. No prescribed architecture. Every choice — from state management to animation performance to SEO — had to be researched, justified, and implemented independently.

This project is, in many ways, a more honest record of my current capability than any certificate.

---

## Technical Stack

| Layer | Technology | Reason for Choice |
|-------|-----------|-------------------|
| Framework | Next.js 16 (Pages Router) | Stable SSG/SSR, explicit data-fetching via `getStaticProps` |
| UI | React 19 | Component architecture, hooks-based state management |
| Animation | Framer Motion 12 | Declarative API, `AnimatePresence` for route transitions |
| 3D | Three.js r128 | Lightweight, no WebGPU dependency, broad browser support |
| Styling | CSS Custom Properties | Zero-dependency theming, runtime dark/light switching |
| Deployment | Vercel | Edge CDN, automatic preview deployments on `git push` |

---

## Engineering Decisions

These are the deliberate trade-offs I made and the reasoning behind each one.

**1. Pages Router over App Router**
Next.js 13+ introduced the App Router with React Server Components. I chose the Pages Router because `getStaticProps` and `getStaticPaths` give explicit, predictable control over static generation. The App Router's streaming model introduced complexity I did not yet fully understand — and I prefer not to use tools I cannot debug confidently.

**2. No external CSS framework**
I considered Tailwind CSS but decided against it. The design system relies heavily on CSS custom properties (`--cyan`, `--bg`, `--surface`, etc.) for runtime theme switching. Tailwind's utility-first approach would have required extensive override configuration. Inline styles with CSS variables gave complete control without build-time overhead.

**3. Three.js loaded with dynamic import**
The 3D background is a heavy asset (~500KB parsed). I load it with `next/dynamic` and `ssr: false` so it never blocks the initial server render. Users see the page immediately; Three.js hydrates on the client after first paint. Without this, initial render time on mobile increased by over 800ms.

**4. Canvas API for particle effects**
The hero section's particle network is drawn on an HTML5 Canvas element rather than as DOM nodes. At 45+ particles with connection-line logic, DOM-based rendering caused visible jank due to layout thrashing. Canvas rendering runs entirely in a `requestAnimationFrame` loop with zero DOM interaction.

**5. File-based content over a CMS**
Blog content currently lives in `data/blog-posts.js`. This was a deliberate starting point — zero external dependencies, instant build times, and full version control over content. Migration to Sanity.io is planned as a future iteration, but I did not want to introduce that complexity before fully understanding the content requirements.

---

## Performance

Measured outcomes, not aspirational claims.

| Metric | Result | Approach |
|--------|--------|----------|
| Lighthouse Performance | 90+ | Dynamic imports, code splitting |
| Lighthouse SEO | 100 | Meta tags, Open Graph, Twitter Card |
| Lighthouse Accessibility | 95+ | Semantic HTML, keyboard navigation, ARIA |
| Core Web Vitals — LCP | < 2.5s | Image optimization, deferred heavy assets |
| Core Web Vitals — CLS | < 0.1 | Reserved layout space for dynamic elements |
| Three.js Bundle | Deferred | Client-side only, loaded after first paint |

---

## Project Structure

```
taseen-website/
│
├── components/
│   ├── Header.js             # Fixed navbar with cross-page anchor navigation
│   ├── Footer.js             # Minimal footer
│   ├── Hero.js               # Canvas-based interactive particle system
│   ├── Skills.js             # Progress bars with scroll-triggered animation
│   ├── Projects.js           # GitHub-linked project cards
│   ├── LatestBlogs.js        # 3D floating blog card previews
│   ├── Reviews.js            # Testimonials with star rating component
│   ├── EmailSubscription.js  # Newsletter signup form
│   ├── Contact.js            # Social platform links with hover effects
│   ├── Journey.js            # Life timeline (alternating left-right layout)
│   ├── LoadingScreen.js      # Cinematic intro animation
│   ├── CustomCursor.js       # Cursor replacement (desktop only)
│   ├── ThreeBackground.js    # Three.js scene (SSR-disabled via dynamic import)
│   ├── PageTransition.js     # Route-change animation wrapper
│   ├── ReadingProgress.js    # Scroll-based reading progress tracker
│   ├── BackToTop.js          # Circular progress scroll button
│   ├── EasterEgg.js          # Hidden keyboard sequence interaction
│   └── ThreeDCard.js         # Reusable 3D tilt card utility
│
├── pages/
│   ├── _app.js               # Global layout, theme state, providers
│   ├── _document.js          # HTML head, SEO meta tags, Open Graph
│   ├── index.js              # Homepage (7 content sections)
│   ├── about.js              # About page
│   ├── journey.js            # Life timeline page
│   ├── photography.js        # Photo gallery with category filter
│   ├── 404.js                # Custom error page
│   └── blog/
│       ├── index.js          # Article listing (client-side search + tag filter)
│       └── [slug].js         # Dynamic article page via getStaticPaths
│
├── data/
│   ├── blog-posts.js         # Article content, metadata, tags
│   └── journey.js            # Timeline events (2008–2026)
│
├── styles/
│   └── globals.css           # Design tokens (CSS custom properties), resets
│
└── public/
    └── photos/               # Photography gallery assets
```

---

## What I Learned

I want to be honest about where my knowledge was before this project and what it taught me.

**Before this project**, I had built simple React applications following tutorials. I understood component state and props, but had no experience with SSG, dynamic routing, or production deployment pipelines.

**Through this project**, I learned:
- How `getStaticPaths` generates pages at build time versus `getServerSideProps` at request time — and when each is appropriate
- How to structure a CSS design system with custom properties so theming works without any JavaScript overhead
- Why `requestAnimationFrame` exists and how the browser rendering pipeline actually works — this came from debugging a canvas animation performance issue
- The difference between layout, paint, and composite operations — and why `transform` is a cheaper property to animate than `top` or `left`
- How Vercel's build pipeline works, what edge functions are, and how to read and interpret build logs

**What I am still learning:**
- TypeScript — I am working through the type system. The project has a `tsconfig.json` but most components are still `.js`
- Testing — I have not written unit or integration tests for this codebase. This is a gap I am aware of and plan to address
- Backend architecture — the email subscription form currently has no server-side implementation. I understand conceptually what the API route needs to do; I have not yet built one in production

I include this section because honesty about the boundary between what I know and what I am still learning is more useful to anyone reading this than a list of claimed competencies.

---

## Academic Interests

My interest in cybersecurity grew from a broader curiosity about how complex systems fail — and how they can be made more resilient. I am particularly drawn to:

- **Secure system design** — how security properties are formally specified and enforced at the architecture level
- **Applied cryptography** — the engineering of cryptographic protocols, not only their mathematical foundations
- **AI safety and robustness** — how machine learning systems behave outside their training distribution, and how to reason about that formally
- **Privacy-preserving computation** — the practical tradeoffs in differential privacy and federated learning

I am currently building [Project Cypher](https://github.com/smtaseenkabir) — a portable, locally-executed secure computing environment using Fedora Silverblue, LUKS2 encryption, and local AI inference via llama.cpp — as a way to explore these topics through direct systems work.

---

## Planned Improvements

- [ ] Migrate blog content to Sanity.io headless CMS
- [ ] Implement email subscription backend (Resend API)
- [ ] Add TypeScript across all components
- [ ] Write unit and integration tests (Jest + React Testing Library)
- [ ] Set up Lighthouse CI in GitHub Actions pipeline
- [ ] Progressive Web App support (service worker, offline capability)

---

## Running Locally

**Requirements**
```
Node.js  >= 18.0.0
npm      >= 9.0.0
```

**Setup**
```bash
git clone https://github.com/smtaseenkabir/taseen-website.git
cd taseen-website
npm install
npm run dev
```

Open `http://localhost:3000`.

**Available scripts**
```bash
npm run dev      # Development server with Turbopack (hot reload)
npm run build    # Production build with static optimization
npm run start    # Serve production build locally
npm run lint     # ESLint code quality check
```

---

## Connect

| | |
|--|--|
| Website | [taseenkabir.vercel.app](https://taseenkabir.vercel.app) |
| GitHub | [@smtaseenkabir](https://github.com/smtaseenkabir) |
| Email | [s.m.taseenkabir8960@gmail.com](mailto:s.m.taseenkabir8960@gmail.com) |
| Telegram | [@smtaseenkabir](https://t.me/smtaseenkabir) |

---

## License

MIT License © 2026 S.M. Taseen Kabir

The code architecture and component patterns in this repository are available for reference under the MIT License. Personal content — biography, photographs, project descriptions — is not licensed for reproduction.

---

<div align="center">

<br/>

*Built by [S.M. Taseen Kabir](https://taseenkabir.vercel.app) — Dhaka, Bangladesh*

*"Engineering resilient systems, exploring intelligent algorithms, and building software that serves a purpose."*

<br/>

![](https://img.shields.io/badge/Made_in-Dhaka,_Bangladesh-22d3ee?style=flat-square&labelColor=0a0a0f)
![](https://img.shields.io/badge/Class-12_Science-a78bfa?style=flat-square&labelColor=0a0a0f)
![](https://img.shields.io/badge/Goal-CS_Engineering_Abroad-f472b6?style=flat-square&labelColor=0a0a0f)

</div>
