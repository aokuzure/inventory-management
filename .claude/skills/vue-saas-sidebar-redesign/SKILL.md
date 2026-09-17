---
name: vue-saas-sidebar-redesign
description: >
  Redesigns a Vue 3 application's navigation shell into a modern, clean-minimal
  SaaS interface — replacing a horizontal top nav bar with a fixed-width
  vertical left sidebar, adding a slim top utility bar for account/search/
  language controls, and introducing a consistent spacing/radius/shadow
  design-token system. Use this whenever the user asks to "redesign the UI,"
  "add a sidebar," "give this a dashboard/SaaS feel," "make this look more
  professional or modern," or references products like Linear, Notion, or
  Stripe as a visual target for a Vue app — even if they don't say "skill,"
  "sidebar," or name Vue explicitly and just describe an app that currently
  has tabs or a top nav. Only applies to Vue 3 codebases (Options API or
  Composition API, with or without vue-router); do not use for other
  frameworks or for narrow single-element style tweaks like "change this
  button's color" that don't involve restructuring navigation.
---

# Vue 3 SaaS Sidebar Redesign

## What this skill does

This skill turns a Vue 3 app's horizontal top navigation into a clean, minimal
left sidebar — the kind of shell you'd see in Linear, Notion, or a modern
Stripe-adjacent SaaS dashboard. It touches the layout shell (usually
`App.vue`) and the global/shared stylesheet only. It does not rewrite
individual view or page files — those keep whatever internal spacing and
markup they already have. Think of this as replacing the frame around the
picture, not repainting the picture itself.

Read this whole file before touching any code. It's short by design; the
bundled `references/icons.md` is the only file you should need to open
mid-task.

## Step 0: Check house rules first

Before editing anything, look for a `CLAUDE.md` (root and any nested ones
near the frontend) and read it. Repos sometimes have specific conventions
that override generic best practice — a required subagent for `.vue` file
edits, a "no emojis in UI" rule, a specific component library, a naming
convention for CSS classes. Whatever you find, follow it without being asked
twice. If the repo requires delegating `.vue` edits to a specific subagent
(this is common), delegate the actual file writes for the layout component to
that subagent rather than editing it yourself, while you retain the overall
plan and design decisions.

## Step 1: Discover the current shell

You're working on an arbitrary app, so don't assume file names — verify them:

- **Root layout file**: usually `src/App.vue`, but confirm by checking what
  the app's entry file (`main.js`/`main.ts`) mounts. This is the file that
  currently renders the top nav and wraps `<router-view />` (or, in apps
  without vue-router, wraps whatever conditional-rendering/tab-switching
  logic drives the "pages").
- **Router config**: look for `src/router.js`, `src/router/index.js`, or
  inline `createRouter(...)` in `main.js`. Record every route's `path` and
  the label used to link to it — this list is your source of truth for what
  the sidebar must contain, and later for verifying nothing broke. If there's
  no vue-router (some small apps just toggle a `currentView` ref), find that
  state variable and the list of view names instead; the sidebar items will
  set that state on click rather than use `<router-link>`.
- **Existing nav markup**: find the element(s) currently rendering nav
  destinations — a `<nav>`, a `<header>`, a row of `<router-link>` or
  `<button>` elements. Note whether the app is Options API (`data()`,
  `methods`) or Composition API (`<script setup>`, `ref`/`computed`) — your
  edits need to match the existing style so the file stays consistent with
  the rest of the codebase.
- **Global stylesheet / token location**: some apps keep global styles in a
  single `<style>` block inside `App.vue` (no separate CSS file at all);
  others have `src/assets/main.css`, `src/styles/`, or a `:root` block
  somewhere already. Find wherever global, non-scoped CSS currently lives —
  that's where design tokens go. If styles are inline in `App.vue`'s
  `<style>` block and there's no dedicated global CSS file, it's fine to add
  the token `:root` block there; don't invent a new file structure the repo
  doesn't already use unless the app clearly has no global style location at
  all, in which case a new `src/assets/tokens.css` (or similar, matching the
  repo's naming conventions) imported once from `main.js` is reasonable.
- **i18n**: if nav labels come from a `useI18n()`/`t(...)` call or an
  `$t(...)` global, or from a Vuex/Pinia store rather than hardcoded strings,
  keep using that call — the sidebar just relocates the label, it doesn't
  change how the label is produced. Never touch locale files.

## Step 2: Classify the old top bar's contents

Every element currently in the header divides into three buckets. Getting
this classification right is the difference between a redesign and a
regression — nothing should quietly disappear.

1. **Primary navigation** — the actual `<router-link>`s / tab buttons that
   switch the main view (Dashboard, Inventory, Orders, Settings, etc.).
   These become the sidebar's nav item list.
2. **Logo / branding** — app name, logo image, tagline/subtitle text. This
   becomes the sidebar header, above the nav list.
3. **Everything else** — search inputs, a language/locale switcher, a
   profile/account menu, notification bells, help links, a "new item" button,
   whatever doesn't fit the first two buckets. This is not primary
   navigation and doesn't belong in a vertical nav list — it moves into a new
   slim top utility bar that spans the width of the content area (to the
   right of the sidebar, not full page width). Nothing in this bucket gets
   deleted; if you're unsure whether something is primary nav or a utility
   control, ask yourself whether clicking it changes "which page you're on"
   (→ nav) or adjusts context/account/settings without changing the page
   (→ utility bar).

Any pre-existing filter bar or page-level toolbar (e.g. a component that
renders global filters above the router-view) is neither of these — leave it
exactly where it is functionally, just beneath the new top utility bar
instead of beneath the old header. Don't merge it into the utility bar or
redesign it; it's out of scope.

## Step 3: Establish design tokens

Add these CSS custom properties to the global stylesheet location you found
in Step 1. This is a starting point, not a rigid spec — adjust names to match
any existing convention in the repo (e.g. if the app already prefixes
variables like `--app-*`, follow that), but keep the underlying scale.

```css
:root {
  /* Spacing — 4px grid, generous by default (Linear/Notion lean airy) */
  --space-1: 4px;
  --space-2: 8px;
  --space-3: 12px;
  --space-4: 16px;
  --space-5: 24px;
  --space-6: 32px;
  --space-7: 48px;
  --space-8: 64px;

  /* Radius — soft but not bubbly */
  --radius-sm: 6px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-full: 999px;

  /* Shadow — restrained; borders do most of the work, shadows are a light lift */
  --shadow-sm: 0 1px 2px rgba(15, 23, 42, 0.04);
  --shadow-md: 0 2px 8px rgba(15, 23, 42, 0.06);
  --shadow-lg: 0 8px 24px rgba(15, 23, 42, 0.08);

  /* Borders — thin, neutral, not heavy dividers */
  --border-color: #e5e7eb;
  --border-width: 1px;

  /* Neutral text/background scale */
  --color-bg: #ffffff;
  --color-bg-subtle: #f9fafb;
  --color-bg-sidebar: #fafafa;
  --color-text: #111827;
  --color-text-muted: #6b7280;
  --color-text-faint: #9ca3af;

  /* Layout */
  --sidebar-width: 240px;
  --topbar-height: 56px;

  /* Accent — see detection logic below */
  --color-accent: #4f46e5;        /* fallback: indigo-600 */
  --color-accent-bg: #eef2ff;     /* tinted background for active states */
  --color-accent-text: #4338ca;   /* slightly deeper, for text-on-tint contrast */
}
```

**Accent color detection**: before falling back to the indigo default above,
look for an existing accent color the app already uses consistently — check
active-nav-link styling, primary button backgrounds, focus rings, and link
colors in the current global stylesheet. If you find one clear, consistently
used non-gray color (e.g. a specific hex used for `.active`, `.btn-primary`,
etc.), reuse that exact value for `--color-accent` and derive
`--color-accent-bg` as a light tint of it (roughly 90-95% lightened, or a
pre-existing lighter variant if the app already has one) and
`--color-accent-text` as a slightly deeper shade for use on light tinted
backgrounds. Only fall back to the indigo default if no color is used
consistently enough to count as "the" accent (e.g. multiple unrelated colors,
or only status colors like green/red/yellow, which are semantic, not brand).
Preserving an app's existing identity matters more than imposing a house
style.

The same "preserve what's already there" principle applies to the neutral
scale, not just the accent: the border/background/text-gray hex values above
are a reasonable starting point for an app with no existing design system,
but if the app already has its own neutral palette in consistent use (e.g. a
documented set of grays in its own CLAUDE.md, or the same handful of gray
hex values reused across borders/text/backgrounds throughout the current
stylesheet), reuse those values for `--border-color`/`--color-text`/etc.
instead of introducing a second, competing gray scale. The goal is one
coherent palette, not the skill's specific numbers.

## Step 4: Build the sidebar + content shell

Restructure the root layout into a two-column shell:

```
<div class="app-shell">
  <aside class="sidebar">           <!-- fixed width: var(--sidebar-width) -->
    <div class="sidebar-header">…logo/branding…</div>
    <nav class="sidebar-nav">…nav items…</nav>
    <!-- sidebar-footer is OPTIONAL: only add it if something from Step 2's
         classification actually belongs there (e.g. the old top bar had a
         logout button or version string). Don't invent placeholder content
         just because the shape has room for it. -->
  </aside>
  <div class="content-area">        <!-- flex: 1, min-width: 0 -->
    <header class="topbar">…utility bar contents…</header>
    <!-- pre-existing filter/toolbar component, unchanged, goes here -->
    <main class="main-content">
      <router-view /> <!-- or existing view-switching logic -->
    </main>
  </div>
</div>
```

Use flexbox for the outer shell (`display: flex` on `.app-shell`, sidebar at
a fixed `width: var(--sidebar-width); flex-shrink: 0`, content area
`flex: 1; min-width: 0` so long content doesn't blow out the layout). This is
the only sidebar mode to support — fixed width, always expanded. Don't build
a collapse/expand toggle or a hover-to-widen interaction; that's explicitly
out of scope and adds failure surface for no requested benefit.

**Sidebar visual details** (clean-minimal, not dense-dark-admin):
- The sidebar must stay visible while the page content scrolls — that's the
  entire point of moving navigation out of a page-level header. Give
  `.sidebar` `position: sticky; top: 0; height: 100vh` (or `position: fixed`
  with matching layout offsets, whichever fits the app's existing layout
  approach better) so it behaves at least as well as whatever sticky/fixed
  positioning the old top nav had — check the old header's CSS for
  `position: sticky`/`fixed` before you remove it, since apps that already
  bothered to keep their nav visible while scrolling will regress badly if
  the new sidebar just scrolls away on any view taller than one screen. Give
  `.topbar` the same `position: sticky; top: 0` treatment within the content
  area so utility controls (search, profile menu) stay reachable too.
- Light background (`--color-bg-sidebar`), not a dark/navy panel.
- A single `1px solid var(--border-color)` right border — no drop shadow
  separating sidebar from content.
- Generous vertical rhythm between nav items (`--space-2` to `--space-3`
  padding), not a cramped list.
- Nav item = icon (20x20, see Step 6) + label, `--radius-md` corners,
  `padding: var(--space-2) var(--space-3)`.
- **Active state**: because this is a vertical list, don't reuse a top-nav
  underline pattern — it reads wrong here. Use a tinted background
  (`--color-accent-bg`) with accent-colored text and icon
  (`--color-accent-text`), optionally with a thin (2-3px) accent-colored bar
  on the item's left edge for extra scannability. Inactive items get neutral
  text (`--color-text-muted`) with a plain hover state (subtle gray
  background, no accent color) so the active item stays visually distinct.
- Sidebar header holds the logo/branding bucket from Step 2, with modest
  padding and a bottom border separating it from the nav list.

## Step 5: Build the top utility bar

The utility bar is a slim (`--topbar-height`, ~56px) horizontal strip at the
top of the content area only — it does not span behind the sidebar, and it
sits above any pre-existing filter bar or page toolbar, which stays
functionally unchanged directly beneath it. Left side of the utility bar can
hold a page title if one isn't already rendered by the current view — check
this by looking at a couple of view/page files for an existing `<h1>`/`<h2>`
page heading (most apps that had a top nav also give each page its own
title in the page body) rather than guessing; if every view already titles
itself, leave the topbar's left side empty. Right
side holds everything from classification bucket (c) in Step 2 — search
input, language switcher, notification bell, profile/account menu, etc., in
whatever order they appeared before. Keep these as the same components
(`<LanguageSwitcher />`, `<ProfileMenu />`, or equivalent) — you're relocating
them, not reimplementing them. Style the utility bar with a bottom
`1px solid var(--border-color)` and `--color-bg` background, consistent with
the sidebar's restrained-border aesthetic rather than a shadow-heavy app-bar
look.

## Step 6: Icons

Most Vue apps you'll encounter don't have an icon library installed, and
this skill should never add an npm dependency or pull from a CDN icon font
just to get a few nav icons — that's a heavyweight, network-dependent
solution to a small problem. First check whether the target app already uses
an icon library (look for imports like `@heroicons/vue`, `lucide-vue-next`,
`vue-feather`, FontAwesome classes, or a local `icons/` component folder). If
one is already in use, use it for consistency instead of the bundled set
below.

If there's no existing icon pattern, use `references/icons.md`, bundled with
this skill — a small set of inline SVG line icons (stroke-based, currentColor,
20x20 viewBox, thin stroke, Linear/Notion in spirit) covering common nav
concepts. For each nav item, pick the icon whose concept best matches the
route's label/purpose (e.g. "Inventory" → box icon, "Orders" → cart icon,
"Finance"/"Spending" → dollar icon, "Reports"/"Analytics" → chart icon). If
nothing in the set is a good semantic match for a given label, use the
generic fallback icon (dot/bookmark) rather than forcing a poor match — a
neutral icon reads better than a confusing one. If two nav items would
naturally reach for the same icon (e.g. both "Reports" and "Demand Forecast"
read as chart-shaped), don't reuse one icon for both — scannability is the
whole point of adding icons in the first place. Give one of them the closest
alternative in the set instead (a documents icon reads fine for "Reports"
since a report is a document, leaving the chart icon for the one that's more
literally about trends/analytics).

## Step 7: Verify nothing broke

This is a structural refactor of navigation, so the verification bar is
"every destination and every piece of functionality that existed before
still exists and still works" — not just "does it look nice."

- **Route parity**: compare the list of route paths (or view-switch targets)
  you recorded in Step 1 against what the new sidebar links to. Every route
  must be reachable from the new sidebar, and no route path should have
  changed.
- **Nav stays reachable on long pages**: if the old header used
  `position: sticky`/`fixed`, confirm the new `.sidebar`/`.topbar` got
  equivalent treatment (see Step 4) — otherwise navigation and account
  controls silently scroll out of reach on any view taller than the
  viewport, which is a real regression even though nothing "broke" in a
  build-error sense.
- **Compiles/runs**: start (or confirm running) the dev server and check
  there are no build errors. If a browser automation tool is available,
  navigate to each route and take a look — otherwise at minimum confirm the
  build/compile step is clean. If a dev server is already running on the
  project's usual ports (check before binding), don't start a second one —
  run a portless build/compile check instead (e.g. `vite build`) to avoid
  port collisions.
- **Console errors**: if you have a browser tool available, check the
  console for new errors or warnings after the change (missing component
  registration, broken prop, etc.) — don't assume silence, check.
- **i18n untouched**: confirm you didn't edit any locale/translation files —
  labels should still be produced by the same `t(...)`/`$t(...)` calls,
  just rendered in new markup.
- **Utility elements present**: confirm every component/element you sorted
  into bucket (c) in Step 2 is still rendered somewhere in the new layout —
  grep the new layout file for each one by name if it's easy to lose track
  (e.g. `grep -c "ProfileMenu" App.vue` should be ≥1 both before and after).

## Step 8: Report back

Summarize what changed: which file(s) were edited, what moved where (nav →
sidebar, logo → sidebar header, utility controls → top bar), and what the new
design tokens are. Explicitly note that this skill intentionally does not
touch individual view/page files — so per-view internal spacing, card
layouts, or table density may now look visually inconsistent with the new
shell's spacing scale even though nothing is broken. Call this out as a
natural, optional follow-up ("apply the new spacing tokens inside individual
views for full visual consistency") rather than something the skill failed
to do — it was out of scope by design.
