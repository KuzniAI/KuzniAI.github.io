# AGENTS.md

The static site for the KuźnAI GitHub organization (https://github.com/KuzniAI). It is a single `index.html` with inline CSS and no build step, deployed to GitHub Pages by `.github/workflows/static.yml`.

**Before any visual, layout or copy change, read [DESIGN.md](DESIGN.md).** It records the agreed design and content decisions: palette, fonts, single column, logo treatment, Polish impersonal voice, no animation. Follow it. If a change intentionally departs from it, update DESIGN.md in the same change.

- Copy is in Polish and never addresses the reader directly (no "Ty" or "Państwo").
- Placeholder content is marked `<!-- PRZYKŁAD -->`. Don't present it as real.
- Use the color and spacing tokens in `:root`; don't add new hex values inline.
