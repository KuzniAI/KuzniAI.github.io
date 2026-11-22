# KuźnAI — design decisions

The visual and editorial rules for the KuzniAI.github.io site. These are settled decisions; change them deliberately, and update this file when you do.

## Brand idea

- **Metaphor: "the material is the tool."** In the logo, a hand made of the same flowing material forges on an anvil. Language models are the same: the model that generates answers can also evaluate them, prepare data and build parts of the system.
- **Forge vocabulary is kept.** Section titles and copy use forging terms on purpose: surowiec, kowadło, kowale, kuźnia. The way-of-working steps are the forging stages **Rozgrzanie → Kucie → Hartowanie → Przekazanie**. Hartowanie (tempering) is where evals, edge cases and reliability work belong.
- **Tone: nerdy but serious and grounded.** Engineering credibility first; playful only in small details (mono labels, forge naming).

## Direction: "Forge at night" + Bauhaus

Picked over two alternatives: "Blueprint" (grid paper, line work) and "Workshop paper" (a light background).

- Near-black navy page. The **logo is the only glowing element**: no glow effects, gradients-as-decoration or shadows elsewhere.
- Bauhaus structure: flat color blocks, hard edges, **circle / square / triangle** as markers, thick color rules, no rounded corners.
- **Static: no animation**, no scroll effects, no hover motion. Hover changes color only.

## Layout

- **Single narrow column** on every screen size: `--measure: 40rem` of content plus a `1.25rem` gutter. No multi-column layouts or wide sections.
- Mobile-first; the page must work at 320px with no horizontal scroll.
- Vertical rhythm comes from `--space` (fluid, about 4–7rem) between sections.

## Logo

- Top center, in the masthead, `min(20rem, 78vw)` wide.
- The JPG has its own navy background. It is **blended into the page**: the page background is the logo's navy, and only the outer edges of the square are faded with a linear mask (about 9% horizontally, 5–7% vertically).
- **The wordmark at the bottom of the logo must never be faded.** A radial fade was tried and rejected because it ate the "KuźnAI" letters.
- Served as WebP with a JPG fallback, 512 and 1024 sizes, with `fetchpriority="high"` because it is the largest element on the first screen.

## Color

Sampled from the logo, plus one added warm color. All are defined as tokens in `:root` in `index.html`.

| Token | Hex | Source | Use |
|---|---|---|---|
| `--navy-950` | `#031738` | logo background | page background |
| `--navy-900` | `#052449` | logo background | top glow behind the logo, process step boxes |
| `--navy-800` | `#093762` | logo | button hover |
| `--steel-700` | `#165989` | logo mid-tone | process step side bars |
| `--steel-500` | `#388cb6` | logo mid-tone | circle marker, first color in rotations |
| `--cyan-400` | `#59c5dd` | logo glow | highlighted words in headings, link underlines, square marker |
| `--cyan-200` | `#94eff5` | logo wordmark | links, big numbers |
| `--ember-500` | `#ff7a3d` | **added** ("hot metal") | section numbers, focus ring, triangle marker, testimonial corner, contact block |

- **Ember is a full third color next to navy and cyan, not a rare accent.** The current amount (all `[0x]` labels, the testimonial corner and the solid contact block) was approved as is.
- Colored items cycle in the fixed order **steel → cyan → ember** (services markers, project top rules).
- Dark only (`color-scheme: dark`); there is no light theme.
- Text: `--ink #dbe8ef` for body text, `--ink-muted #9fb6c6` for secondary text, white for headings. Inside the ember block, text is navy.

## Typography

- **Archivo** (variable, width axis) for everything readable. Headings use **Archivo Expanded** (`font-stretch: 125%`), weight 850, uppercase, tight line height. It is the closest match to the heavy geometric wordmark in the logo.
- **IBM Plex Mono** for the "nerdy" layer only: section numbers like `[01]`, tags, project metadata, link rows and buttons. It is never used for body paragraphs.
- Both fonts cover Polish characters (ą ę ł ń ó ś ź ż). Any new font must too.
- Fluid sizes use `clamp()` with rem limits; the maximum stays within 2.5× the minimum so browser zoom keeps working. `font-size-adjust: from-font` limits the layout jump when the web fonts load.
- Inside headings, `<em>` is not italic; it switches the words to cyan (white in the contact block).

## Components

- **Section head:** a mono ember label `[0n] Name`, then an uppercase H2 whose second part is highlighted in `<em>`.
- **Services:** a list with ruled lines between items and a Bauhaus shape (square, circle, triangle, outlined square) as each item's marker.
- **Process:** numbered navy boxes with a steel left bar; the last step's bar is ember.
- **Projects:** a top rule cycling steel/cyan/ember; a mono meta line (`P-0n · type · tech`); a name in expanded type; a description; mono links with ↗.
- **Testimonial:** a box with a 2px cyan border, a solid ember square in the top-right corner, a large semibold quote and a mono attribution.
- **Facts:** a strip of 3 equal cells separated by 1px rule lines.
- **Contact block:** a solid ember block with navy text and a navy mono button.
- **Focus:** a 3px ember outline (navy inside the ember block). Keep the skip link.

## Content

- **Polish only.** `lang="pl"`.
- **Impersonal / "my" voice.** Describe what we do ("Budujemy…", "Pomagamy zespołom…"). **Never address the reader** as "Ty" or "Państwo", and avoid imperatives aimed at them.
- **Collective identity:** no individual names, photos or personal profiles. Use "trzech inżynierów" / "trzech kowali".
- **Contact goes only through the GitHub organization** (https://github.com/KuzniAI) for now; there is no email or booking link yet.
- Section order: Idea → Co robimy → Jak pracujemy → Projekty → testimonial → Kim jesteśmy → Kontakt.

## Open / deferred

- **Copywriting is deferred.** All copy is a draft, including the headline "Materiał jest narzędziem". A dedicated copywriting pass will come later.
- **Placeholders** (marked with `<!-- PRZYKŁAD -->` in the HTML): the testimonial, the facts numbers (e.g. "40+ lat"), and the projects (Kowadło, Miech, Obcęgi: names, descriptions and links).
- Facts strip: deciding between real numbers and removing it is deferred.
- Not decided yet: a link-preview (OG) image, an FAQ section, an English version.

## Tech

- One static `index.html` with inline CSS, no build step and no JavaScript. It is deployed by GitHub Pages (`.github/workflows/static.yml`).
- Google Fonts is the only external dependency.
