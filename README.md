# Elementis

A luxury wellness brand website built with Next.js 15 — focused on advanced web animation, performant rendering patterns, and modern UI engineering.

---

## Overview

Elementis is a premium wellness platform centered around **Wellness • Innovation • Nature • Community**. The site delivers a high-end digital experience through smooth scroll, immersive animations, and a carefully crafted component architecture.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | [Next.js 15](https://nextjs.org) (App Router) |
| Language | TypeScript 5 |
| UI | React 19 |
| Styling | [Tailwind CSS v4](https://tailwindcss.com) |
| Animation | [Motion (Framer Motion v12)](https://motion.dev) |
| Smooth Scroll | [Lenis](https://lenis.darkroom.engineering/) |
| Utilities | clsx + tailwind-merge |
| Linting | ESLint 9 + eslint-config-next |
| Formatting | Prettier + prettier-plugin-tailwindcss |

---

## Project Structure

```
elementis/
├── app/                        # Next.js App Router root
│   ├── layout.tsx              # Root layout: fonts, Lenis, WindowSizeProvider
│   ├── page.tsx                # Home page — composes all sections
│   ├── globals.css             # Global styles
│   ├── providers.tsx           # WindowSize context provider
│   └── fonts/                  # Self-hosted BasisGrotesquePro (Light/Regular/Medium)
│
├── sections/                   # Full-page sections (Server + Client split)
│   ├── Hero/                   # Full-screen hero with animated marquee and mask text
│   ├── Introduction/           # Brand introduction with image reveal
│   ├── WellnessSanctuary/      # Wellness section with clip image card
│   ├── ElementisStory/         # Brand story section
│   ├── SustainalbeRetreat/     # Sustainable retreat narrative
│   ├── Form/                   # Contact/waitlist form
│   └── Footer/                 # Site footer
│
├── components/
│   ├── Client/                 # Interactive client components
│   │   ├── NavBar.tsx          # Navigation bar (opacity-reactive in Innovation section)
│   │   ├── Cursor.tsx          # Custom cursor (hidden on mobile < 768px)
│   │   ├── Innovation.tsx      # Innovation section with cursor suppression
│   │   ├── ParallaxContainer.tsx # Parallax scroll container
│   │   ├── ClipImageCard.tsx   # Clip-path reveal image card
│   │   ├── ClipImageContainer.tsx
│   │   ├── Marquee.tsx         # Base marquee component
│   │   ├── ResponsiveMarquee.tsx # Marquee with mobile/desktop speed config
│   │   ├── MaskTextClient.tsx  # Client-side animated mask text
│   │   ├── ResponsiveMaskTextVariant.tsx
│   │   ├── SustainableRetreat.tsx
│   │   ├── Loader.tsx          # Page load animation
│   │   └── ...                 # Other interactive components
│   │
│   ├── Server/                 # Static server components
│   │   ├── MaskText.tsx        # Reveal-on-enter text animation wrapper
│   │   ├── SectionTitle.tsx    # Reusable section heading
│   │   ├── Br.tsx              # Responsive break utility
│   │   ├── Input.tsx / Label.tsx / Select.tsx / Checkbox.tsx
│   │   ├── StyledLink.tsx / DashedLink.tsx / CustomLink.tsx
│   │   ├── ContactUs.tsx / StayConnected.tsx
│   │   └── BorderedButton.tsx
│   │
│   ├── SVGComponents/          # Inline SVG icons
│   └── VideoPlayer/            # Video playback component
│
├── hooks/                      # Custom React hooks
│   ├── useCursor.ts            # Custom cursor position + entry/exit state
│   ├── useImageReveal.ts       # Scroll-triggered image reveal animation
│   └── useMaskImage.ts         # Canvas/CSS mask-image animation
│
├── utils/
│   ├── cn.ts                   # clsx + tailwind-merge utility
│   └── lenis.ts                # Lenis smooth scroll React wrapper
│
├── public/                     # Static assets
│   ├── Introduction.png
│   ├── WellnessSanctuaryImage.png
│   └── FormImage.png
│
└── dump/                       # Archived/experimental hooks
    ├── useParallax.ts
    └── useBackgroundImage.ts
```

---

## Key Features & Techniques

### Server / Client Component Split
Every section follows Next.js best practices — static markup and SEO content live in `Server.tsx` files (zero JS shipped to the client), while animations and interactivity are isolated in Client Components.

### Mask Text Animation
Words and lines animate in with a clip/mask reveal using `MaskText` (server) and `MaskTextClient` (client). Driven by Framer Motion's `staggerChildren` with configurable delay per section.

### Custom Cursor
A fully custom cursor (`useCursor.ts`) tracks pointer position with smooth lerp interpolation. It detects element entry/exit and morphs shape accordingly. Hidden entirely on mobile (< 768px) and inside the Innovation section.

### Smooth Scroll — Lenis
Lenis replaces native scroll for buttery inertia. Wrapped in a React context so any component can subscribe to scroll events without extra dependencies.

### Parallax Container
`ParallaxContainer` maps scroll position to a CSS transform offset. The implementation accounts for window size to prevent visual overflow at specific breakpoints.

### Image Reveal on Scroll
`useImageReveal.ts` animates images in using a clip-path / mask-image technique triggered by scroll progress.

### Responsive Marquee
`ResponsiveMarquee` accepts separate `mobile` and `desktop` animation configs (speed + max translate) so the infinite scroll text performs correctly across all screen sizes.

### Typography
Self-hosted **Basis Grotesque Pro** (Light 300, Regular 400, Medium 500) loaded via `next/font/local` for zero layout shift and no third-party font requests.

---

## Getting Started

### Prerequisites
- Node.js 18+
- npm / yarn / pnpm

### Installation

```bash
git clone https://github.com/Adebayodamilola20/elementis-sotd.git
cd elementis-sotd
npm install
```

### Development

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Build

```bash
npm run build
npm start
```

---

## Roadmap

- [ ] `ParallaxContainer` offset refinement at 1200×800 viewport
- [ ] Core Web Vitals optimization pass
- [ ] Form server action → Notion as database
- [x] Cursor entry/exit animation — **Fixed**
- [ ] NavBar opacity handling in Innovation section (Redux to prevent full re-render)

---

## License

MIT
