# Shopwithus

A modern, static e‑commerce landing page built with HTML, CSS, and vanilla JavaScript. It’s responsive, fast, and easy to customize. Highlights include full-bleed video banners, SVG poster fallbacks, sequential “How To Use” overlay steps that reveal quickly and stay visible, and a unified footer with accessible contact links.

## Table of Contents
- Overview
- Features
- Tech Stack
- Project Structure
- Getting Started
- Development Workflow
- Customization
- JavaScript Behavior
- Assets & Media
- Accessibility & SEO
- Performance Tips
- Deployment
- Troubleshooting
- Changelog
- Credits

## Overview
Shopwithus is a single-page, static site intended as a storefront/landing. It uses minimal dependencies and is designed to run on any static host. Styling is centralized in `assets/css/style.css` and interactions are implemented in `assets/js/script.js` using data attributes.

## Features
- Video banners with `autoplay`, `muted`, `loop`, `playsinline` and SVG poster fallbacks (`banner-1.svg`, `banner-2.svg`).
- Sequential “How To Use” overlay steps that reveal quickly and remain visible; interval configurable per banner.
- Unified footer with contact links (Phone, Email, WhatsApp, TikTok, Instagram) and blended logo.
- Sticky header on scroll and a back‑to‑top button.
- Scroll reveal animations to activate sections as they enter the viewport.
- Mobile bottom navigation for quick access on small screens; hidden on larger screens.
- Responsive layout across breakpoints with simple, tokenized design.

## Tech Stack
- HTML5
- CSS3
- Vanilla JavaScript
- Ionicons (icon set via CDN)

## Project Structure
```
Shopwithus/
├── index.html
├── assets/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── script.js
│   └── images/
│       ├── video1.mp4, video2.mp4, video3.mp4
│       ├── banner-1.svg, banner-2.svg       # video poster fallbacks
│       ├── banner.jpg, banner.svg           # banner.svg wraps banner.jpg
│       ├── logo.svg, pay.png
│       └── product/blog images
├── favicon.svg
├── icon.jpg
├── style-guide.md
└── README.md
```

## Getting Started
- Open `index.html` directly in your browser, or serve locally:
  - Node (Windows PowerShell): `npx serve -p 8000 .` → visit `http://localhost:8000/`
  - Python: `python -m http.server 8000` → visit `http://localhost:8000/`

## Development Workflow
- Edit HTML: `index.html`
- Edit styles: `assets/css/style.css`
- Edit scripts: `assets/js/script.js`
- Assets: `assets/images/`
- No build step required; refresh your browser after changes.

## Customization
- Colors and tokens (defined in `:root` within `assets/css/style.css`):
  - `--site-bg` (site background, currently `#FFE9EF`)
  - Greens: `--hoockers-green`, `--hoockers-green_20`
  - Grays: `--spanish-gray`, `--light-gray`, `--gray-web`
  - Utility colors: `--white`, `--black`, various alpha blends
  - Gradients: `--gradient`
  - Typography: `--ff-urbanist`, font sizes `--fs-1` … `--fs-9`, weights `--fw-400` … `--fw-800`
  - Spacing: `--section-padding`
  - Shadow: `--shadow-1`, `--shadow-2`
  - Radius: `--radius-3`
  - Transitions and cubic beziers
- Footer logo blend (subtle watermark effect):
  ```css
  .footer .logo img {
    opacity: 0.35;
    mix-blend-mode: multiply;
  }
  ```
  Increase/decrease `opacity` for a stronger/weaker tint.
- Banner step reveal interval per list:
  ```html
  <ul class="card-steps" data-reveal-interval="700"> … </ul>
  ```
  Fallback: supports `data-rotate-interval` if present.
- Mobile bottom navigation styling:
  ```css
  @media (max-width: 991px) {
    body { padding-bottom: 68px; }
    .back-top-btn { bottom: 88px; }
  }
  ```
  Adjust `.mobile-bottom-nav` colors, spacing, and icon sizes in `assets/css/style.css`.
- Section padding per breakpoint is managed in media queries; adjust `--section-padding` and responsive rules as needed.

## JavaScript Behavior (`assets/js/script.js`)
- Navbar toggle via `[data-nav-toggler]`, `[data-navbar]`, `[data-overlay]`.
- Header sticky + back‑to‑top activation when `window.scrollY > 150` (`[data-header]`, `[data-back-top-btn]`).
- Scroll reveal: sections with `[data-section]` receive `active` class when entering viewport.
- Banner overlay steps: reveal `.card-step` elements sequentially inside `.banner-card .card-steps`; speed configurable with `data-reveal-interval` (default `700ms`; falls back to `data-rotate-interval` when present).
- Mobile bottom nav uses anchor links for section jumps; no extra JS required; nav items include `[data-nav-link]` for consistent behavior.

## Assets & Media
- Video files: `video1.mp4`, `video2.mp4`, `video3.mp4`.
- Posters: `banner-1.svg`, `banner-2.svg` (each wraps corresponding JPG via `<image href="...">`).
- Banner image wrapper: `banner.svg` embeds `banner.jpg` to allow `.svg` references.
- Logo files: `logo.svg` and a raster `Bottom.png` (used in footer as needed).

## Accessibility & SEO
- Use descriptive `alt` text on images and meaningful link labels.
- Videos are muted and set to play inline to avoid intrusive audio and improve autoplay reliability.
- Keep headings semantic and content grouped into sections.
- Bottom nav provides text labels alongside icons; ensure sufficient contrast and touch targets (~44px).

## Performance Tips
- Keep videos lightweight; consider shorter loops and moderate resolutions.
- Provide `poster` images for videos to avoid blank frames prior to playback.
- Use preload hints in `<head>` for large assets if needed.
- Optimize images in `assets/images` (compression/resizing).

## Deployment
- Any static host works (GitHub Pages, Netlify, Vercel, Firebase Hosting, etc.).
- GitHub Pages:
  - Push the repo to GitHub.
  - Enable Pages for the `main` branch (root).
  - Visit the published URL and verify assets load.
- Netlify/Vercel:
  - Drag‑and‑drop or connect repo.
  - Configure as a static site with root as the publish directory.

## Troubleshooting
- Videos don’t autoplay on mobile:
  - Ensure `<video>` tags include `muted playsinline`.
  - Verify file paths like `assets/images/video1.mp4`.
- Icons not visible:
  - Ensure Ionicons CDN is included in `index.html`.
- Unexpected space after footer:
  - `body { margin: 0; }` is applied to remove default margins.
- Footer logo too strong/too faint:
  - Adjust `.footer .logo img { opacity: … }` or try `mix-blend-mode: screen` for dark backgrounds.
- Bottom nav overlaps content on small screens:
  - Confirm `body { padding-bottom: 68px; }` and `.back-top-btn { bottom: 88px; }` within the mobile media query.

## Changelog (Recent)
- Changed: “How To Use” steps now reveal sequentially and remain visible; CSS stacks steps vertically.
- Added mobile bottom navigation with responsive spacing; adjusted back-to-top on mobile.
- Converted `banner.jpg` to an SVG wrapper (`assets/images/banner.svg`).
- Switched video posters to `banner-1.svg` and `banner-2.svg`.
- Removed feature section images; preserved titles and copy.
- Blended footer logo with background using `mix-blend-mode`.
- Eliminated extra page spacing with `body { margin: 0; }`.

## Credits
- Author: dubemjesse
- Icons: Ionicons
- Assets: `assets/images/`
- Original design base: `codewithsadee` (CSS structure inspiration)