# Daniel App House Style

Use this guide for web apps and local tools built under `/Users/dpradilla/dev`.

## Source Of Truth

- Primary visual basis: `/Users/dpradilla/dev/classification-visualization/`
- Secondary component inventory: `/Users/dpradilla/dev/echotree/public/style-guide.html`
- Canonical rendered reference: `/Users/dpradilla/dev/danielpradilla-app-style/index.html`

## Visual Direction

- Use a light editorial interface: `rgb(255, 253, 249)` page background, black primary text, muted gray support text, and hairline borders.
- Prefer system sans typography with light weights. Keep letter spacing at `0`, except uppercase metadata labels.
- Keep controls, panels, cards, and table shells square edged. Avoid pill-shaped buttons and rounded cards unless an external framework requires it.
- Use no decorative shadows in normal surfaces. Use borders and spacing for hierarchy.
- Use `--blue` and `--blue-soft` for selected or primary interaction. Use green, warning, and danger only for semantic status.
- Keep screens dense but calm. The first view should be the working app, dashboard, game, or tool, not a landing page.

## Required Component Coverage

Every substantial app should define or consciously omit these pieces:

- Typography: page title, section heading, panel heading, body copy, labels, metadata, inline code.
- Color tokens: page, paper, soft paper, ink, muted, secondary, rule, selected, success, warning, danger.
- Controls: button, primary button, danger/destructive button, text input, select, textarea, range, checkbox, radio, segmented control.
- Feedback: focus-visible, hover, disabled, loading, empty state, warning note, error note, toast or inline confirmation.
- Data display: metric cards, summary blocks, tables, list rows, badges/status pills, pagination when lists can grow.
- Layout: topbar, constrained shell, control/sidebar panel, main workspace, explanation panel, responsive collapse.
- Domain views: real examples using the app's vocabulary, not generic placeholder UI.

## CSS Rules

- Start with the token set from `index.html` and add domain tokens sparingly.
- Keep cards for individual repeated items or framed tools. Do not put page sections inside decorative cards.
- Use `border: 1px solid var(--rule)` and `border-radius: 0` for default surfaces.
- Keep form controls at roughly `40px` minimum height.
- Tables use uppercase metadata headers, hairline row dividers, and no zebra striping unless needed for scanning.
- State badges are compact, uppercase, and bordered.
- Chart containers and fixed-format workspaces need stable dimensions with `aspect-ratio`, grid tracks, or min/max constraints.

## Header And Footer Navigation

**Scope: webpages only.** This section applies to published, browsable project pages reachable from `/projects/` — the kind of thing a visitor lands on from a link or a search result. It does not apply to webapps (tools, dashboards, utilities meant to be used rather than browsed) or iOS apps. If a task is explicitly a webapp or an iOS app, skip this section entirely; the rest of this guide (tokens, typography, controls) still applies.

**Exception: the `/projects/` hub page itself.** That page's header is not `.dp-navbar` — it's a byte-for-byte visual match of the live blog header (uppercase wordmark, tagline, the blog's actual nav menu). See `danielpradilla-projects/projects/AGENTS.md`. The `.dp-navbar` two-row pattern below is for the individual project pages the hub links to.

Every project *page* under danielpradilla.info uses the same shell so a visitor can always identify the site and reach the hub, without the header competing with the project itself for vertical space.

### Header: two rows

**Row 1 — site bar** (`.dp-navbar`), small and constant across every project:

- Left: a small uppercase "DANIEL PRADILLA" text wordmark, linking to `/projects/`. No tagline here — the tagline belongs only on the `/projects/` hub page itself.
- Right, in one `nav`, left to right: this project's own intra-project tabs (Explore, Methodology, Play, whatever the project has) first, then `Blog` (`/blog/`), then `GitHub` (the project's own repo, not the profile, when linking from inside a project).
- Omit the intra-project tabs entirely when the project has only one view; do not add a nav for a single page.
- Below 600px, the row 1 `nav` collapses into a hamburger menu. See "Compact site-bar implementation requirements" below for the exact markup and CSS — do not improvise this part, the naive approach breaks in a way that isn't obvious from a desktop screenshot.

**Row 2 — project header** (`.dp-project-header`):

- One `h1` with the project name and, if useful, a single-line tagline directly under it.
- No lede paragraph, no multi-paragraph intro, no dates or period ranges in the header. That content belongs in the page body, not the header. (This is the thing to fix in `choplifter` and `stylometric-analysis` today — see Known Gaps below.)
- A primary control (search box, zoom select) may sit on the right of this row when the project already has one, matching `uk-music-cities` and `european-monarchies-timeline`.

Reference markup and CSS: the "Site Header and Footer" demo in `index.html`, classes `.dp-navbar`, `.dp-project-header`.

### Compact site-bar implementation requirements

For public project pages, implement the site bar as a compact, visually stable first header row.

- Use the uppercase wordmark `DANIEL PRADILLA` on the left, linked to `/projects/`.
- Keep the project title in a separate second row (`.dp-project-header`). The site bar must never replace the project title.
- The site bar contains, in order: page-local project links, `Blog` (`/blog/`), then the project repository's `GitHub` link.
- Use a native `<details>/<summary>` hamburger menu below `600px`; do not add JavaScript.
- Do not rely on a closed `<details>` element to provide the desktop navigation. Browsers hide closed details content even when CSS attempts to lay it out. Render:
  1. an inline desktop `<nav class="dp-navbar-links">` visible at `600px` and above, and
  2. a duplicate `<nav>` inside `.dp-navbar-menu` visible only through the native mobile disclosure below `600px`.
  Only one nav may be visible at a time.

#### Vertical alignment

The site bar must retain the same height across the desktop/mobile breakpoint. Do not let the hamburger make the project title jump vertically.

```css
.dp-navbar {
  height: 53px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0;
  border-bottom: 1px solid var(--rule);
}

.dp-navbar-menu {
  display: none;
}

@media (max-width: 600px) {
  .dp-navbar .dp-navbar-links {
    display: none;
  }

  .dp-navbar-brand,
  .dp-navbar-menu {
    transform: translateY(-5px);
  }

  .dp-navbar-menu {
    position: relative;
    display: block;
  }

  .dp-navbar-menu summary {
    width: 36px;
    height: 32px;
    display: flex;
    align-items: center;
    justify-content: center;
    list-style: none;
    cursor: pointer;
    border: 1px solid var(--rule);
  }

  .dp-navbar-menu summary::-webkit-details-marker {
    display: none;
  }

  .dp-navbar-menu nav {
    position: absolute;
    z-index: 1;
    top: calc(100% + 4px);
    right: 0;
    display: flex;
    flex-direction: column;
    gap: 10px;
    min-width: 160px;
    padding: 12px 16px;
    background: var(--paper);
    border: 1px solid var(--rule);
  }
}
```

Before delivery, visually inspect both a desktop viewport and a viewport below 600px. Confirm:

1. the site bar has the same height at both widths;
2. the wordmark and hamburger are visually aligned;
3. the project title does not move when the hamburger replaces the inline nav;
4. the menu opens above page content and does not cause horizontal overflow.

### Footer: one row, plus optional project content above it

- `.dp-footer` is always present and always has the same shape: `© {year} Daniel Pradilla` on the left, a `nav` on the right with `Projects` (`/projects/`), `Blog` (`/blog/`), `GitHub`.
- Project-specific footer content (data sources, license text, freshness timestamps, as in `uk-music-cities` and `european-monarchies-timeline`) goes in its own block placed above the `.dp-footer` row inside the same `<footer>` element. It never replaces the common nav row.

### Known gaps (audited 2026-09-20)

None of the following currently match this pattern; treat this section as the target, not the current state, until each project is migrated. `flipasio` (immersive calculator) and `stylometric-analysis` (password-protected tool) are borderline webapp cases per the scope note above — confirm with Daniel before adding site nav to those two rather than assuming they qualify.

- `swiss-commutes`: slim single-row masthead is the right shape, but it brands as "Swiss Commutes" instead of "Daniel Pradilla" and has no Blog/GitHub links anywhere.
- `choplifter`: closest structurally (site bar + project header + footer nav already exist), but the project header is a tall multi-paragraph intro with dates; trim it to the row-2 spec above.
- `uk-music-cities`: intra-project nav (Explore/Play/Read) exists but "Read" points at one blog post instead of `/blog/`; no GitHub link anywhere, no site wordmark.
- `european-monarchies-timeline`: has the best intra-project tab row (Explore/Methodology/Essay/Data quality); missing the Daniel Pradilla wordmark and a Blog link.
- `classification-visualization`, `stylometric-analysis`, `leboncoin`, `flipasio`: no Blog/GitHub links, no wordmark, no `/projects/` link; `stylometric-analysis`, `leboncoin`, and `flipasio` have no footer nav at all.
- `d3clock`, `echotree`: not present in the local checkout at audit time; re-check against the deployed site before migrating.

## Implementation Workflow

1. Inspect the target app's existing CSS and component structure.
2. Apply this style only where it does not fight established domain requirements.
3. Copy the token names and component patterns from `/Users/dpradilla/dev/danielpradilla-app-style/styles.css`.
4. Build real app screens first. Add or update a local style guide page when the component set expands.
5. Verify desktop and mobile viewports. Check that controls do not overflow, text does not overlap, and focus states are visible.

## Completeness Review From The Source Apps

`classification-visualization` already covered the core look: typography, color, buttons, selects, ranges, segmented controls, summary metrics, cards, explanation panels, and chart marks.

`echotree` added useful missing patterns: text inputs, textarea, checkbox/radio, tables, empty states, badges/status pills, alert notes, reader/list rows, side navigation, code snippets, and dense content layouts.

The canonical guide also adds common future needs that neither source fully covered: destructive buttons, toast/dialog examples, loading state, pagination, disabled/feedback guidance, and responsive workspace rules.
