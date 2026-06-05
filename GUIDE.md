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
