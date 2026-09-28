---
name: tiny-design
description: How apps, websites, dashboards, presentations and forms built for Tiniest Cloud should look and feel — a direction chosen for the product and its industry, palette and type, layout and balance, motion, light and dark, and the checks before calling it done. Use when designing, building or restyling anything to deploy on Tiniest Cloud. Where the person has design standards of their own (a design system, components, a brand guide, an app to match), those come first and this fills only what they leave open; with none, follow it all.
---

# Designing for Tiniest Cloud

## Design — make it look made for its job

**Their standards come first.** When the person has design standards of their own — a design
system, a folder of components, a brand guide, a Figma file, an app or site to match — those
decide, and this section and the design playbooks only fill what theirs leave open. Don't
restyle their components to taste, swap their fonts or colours for ones suggested here, or
"fix" a choice of theirs that this section would call a giveaway (their brand may well use
Inter, or a gradient). Where something of theirs would hurt the people using the app — text too
faint to read, a control too small to tap — build it as specified and tell them, rather than
quietly changing it. When they give nothing of their own ("build me an app for…"), all of the
rest applies.

An app that works but looks like every other starter is not finished. Before the first screen,
decide what this one should feel like — and write it down: a short `DESIGN.md` at the project
root with who it is for, the feel in three words, the palette, the type and how much motion (or,
with their standards, where those live and what they settle).
Hold every screen to it, and read it first when you change the app later (for an app built on
Tiniest Cloud it is kept with the source `get_app_source` returns).

**Start from what it is and who uses it.** Read the request for its scope (a tool used every
day, a page read once, a dashboard glanced at), its audience and its field, and follow that
field's conventions:

- Money, health, legal, B2B: calm and trustworthy — quiet neutrals, one confident accent,
  dense data that lines up, tabular numbers.
- Food, shops, hospitality, events: warm and inviting — richer colour, big imagery, softer shapes.
- Creative, personal, community: expressive — a bolder palette or a display typeface, more motion.
- Kids, games, fitness: energetic — saturated colour, large targets, playful feedback.
- Internal and admin tools: quiet and fast — compact, keyboard-friendly, colour only for status.

A brand, colours or an example the person names always win over these.

**Give it its own palette — theirs if they have one, never the default grey.** Set the theme once, in the CSS
variables (the app starter's `src/index.css`, `:root` and `.dark`): `--primary` is the one
accent (main actions, links, selection), `--muted` and `--accent` are quiet surfaces, plus
`--destructive`, `--ring`, `--chart-1`…`--chart-5` and `--radius`, in both themes. Components
read those tokens; never hard-code a hex colour or `bg-blue-500` in a component, or the dark
theme breaks and the palette stops being one decision. Use colour on purpose: most of a screen
is neutral, and colour marks what to do (the primary action), what is selected, status
(success, warning, error) and the one number that matters — roughly 60% background, 30%
surfaces and text, 10% accent. Keep contrast: 4.5:1 for body text, 3:1 for large text and icons,
in both themes.

**What gives generated UI away — don't** (unless their standards ask for it): the same default font for everything (Inter, system
UI) instead of one chosen for the job; purple-to-blue gradients, glassy cards and glowing blobs
as decoration; a card around everything, cards inside cards; an icon in a rounded square above
every heading, emoji standing in for icons; grey text on a coloured background, pure black and
untinted greys; every section centred, every screen a narrow column in the middle of a wide
display, and every list the same three-card grid; bouncy or slow animation and everything
fading in on load.

**Type and spacing do most of the work.** One typeface family for an app, chosen for its
character and self-hosted with its `@fontsource` package (a display face for headings suits a
site); a clear scale — page title, section heading, body, small and muted —
where size and weight carry the hierarchy, not colour. Numbers in columns use `tabular-nums`.
Space on one scale (Tailwind's 4px steps): related things close together, groups clearly apart,
generous padding at the page edge. Lines of text around 60–75 characters. Align everything to
the same few edges.

**Lay out each screen for what it holds.** A narrow centred column is right for one focused
task — answering a question, a checkout step, a long form, an article — and wrong for most other
screens, where it leaves a laptop mostly empty. Several areas to move between: a sidebar, with
the content beside it using the width. Things people browse by how they look (recipes,
products, photos, boards): a grid of cards that fills the row. Records compared by their fields
(contacts, orders, expenses): a table that becomes a list on a phone. A queue worked through
one at a time: the list with the selected item's detail beside it. Stages: columns side by
side. One app can mix them — a quiz is played in a centred column and managed in a wide
workspace. Cap the width where it stops being readable (about 1280–1440px for an app, 65–75
characters for prose), not at the width of a phone. The starters' frame is a placeholder.

**Balance every screen.** One primary action per screen, visually the strongest; secondary ones
quieter (outline, ghost); destructive ones red and confirmed. Put what matters most where the eye
lands first. Don't box everything — a card inside a card and a border on every section is noise;
group with space and a subtle background instead. Design the states too: empty (what to do
first), loading (skeletons shaped like the content), error (what happened and what to do next),
and long (search, paging).

**shadcn/ui is where you start, not how it must look.** The components in
`src/components/ui` are the app's own code: change radius, padding, sizes, shadows and variants
there so buttons, inputs and cards fit the app's character, and add a variant rather than
overriding classes at every use. Compose them into the app's own pieces (a stat tile, an item
row). Don't add a component because it exists — use the simplest thing that does the job.

**When the person points at their own work, that is the design.** "Use the components in
../design-system", "follow the brand in ./brand", "make it look like our other app", a style
guide, a Figma export, a screenshot: read it before writing any screen, and build from it
rather than from the starter's defaults.

- **Their components.** Reuse them, with their names and props. React + Tailwind components go
  into `src/components` as they are (bring their dependencies into package.json); anything
  else is rebuilt faithfully on the starter's stack. Use theirs wherever one exists and
  shadcn/ui only for what they lack, restyled to match — never two looks on one screen.
- **Their brand.** Take its colours into the theme variables (`--primary`, surfaces, radius) for
  the themes it defines — only light if they define only light, unless they ask for dark. Fonts: files into
  `public/fonts` with `@font-face`, or the matching `@fontsource` package. Logo and images
  into `public/` and use them in the header, the sign-in state and the page title. Keep the
  voice of their copy too.
- **Copy, never link.** Only what is inside the deployed folder ships: a path on the person's
  computer or a sibling folder does not exist once the app is live. Copy the files in; keep
  brand tokens in one place (the theme variables) so the next app can reuse them.
- **Can't reach the folder?** In a chat with no access to their files, ask them to attach the
  files, a screenshot, or the colours, fonts and logo — don't guess a brand.

**Motion: smooth, quick and for a reason.** Animate to explain a change — an item arriving in a
list, a panel opening, a number updating — never to decorate. 150–250 ms, ease-out for things
entering, ease-in for things leaving. Everything clickable has hover and pressed states
(`transition-colors`, a slight scale on press); dialogs and sheets fade and slide in (the
starter's tw-animate-css: `animate-in fade-in slide-in-from-bottom-2`); a list that changes live
animates its items (add `motion` from npm for layout animation). Respect reduced motion
(`motion-safe:` / `motion-reduce:`). Animate only `transform` and `opacity`, name the
properties (never `transition-all`), and prefer one orchestrated entrance to every element
fading in on its own. No bouncing, no long delays, nothing that animates on every render.
One exception: a moment the person earned — a right answer, a finished goal, a win in a game —
may celebrate for up to about 500 ms, with a small overshoot or a burst, where the app's feel is
playful (games, kids, fitness, a team event). Keep it to that moment, never in the way of the
next action, and off under reduced motion like the rest.

**Light and dark, both designed** — unless their standards settle it otherwise. Give people a
light / dark / match-device switch, somewhere visible and styled to fit: the app starter includes one (`src/components/theme-toggle.tsx`,
remembered on the device in a cookie); if the project has none, add one the same way — a cookie,
not localStorage, which a deploy flags. Check both
themes: shadows barely show in dark, so lift surfaces with a slightly lighter background
instead; pure black and pure white are harsh — use the palette's near-black and off-white.

**Phone first.** Most people open a link on a phone: touch targets at least 44px, one column
on a phone that becomes the screen's real layout on a wider one (the sidebar, the grid, the
detail beside its list), nothing reachable only by hover, inputs that bring up the right
keyboard (`type="email"`, `inputmode="numeric"`).

**Words are part of the design.** Short, plain, active; a button says what it does ("Save
expense", not "Submit"); an error says what to do next; an empty state invites the first action.
Numbers, money and dates go through `Intl.NumberFormat` and `Intl.DateTimeFormat`, in the
reader's locale.

**Accessible is part of looking good.** Visible focus rings, a label on every input and icon
button, never colour alone to carry meaning, headings in order.

**Look before you call it done.** After deploying, open it with preview_app in light and dark
and at a phone's width, and fix what is off: edges that don't line up, cramped spacing, colour
that means nothing, an empty state that says nothing.

**Each kind of build has its own playbook** — app, website, dashboard, presentation, form — with
its layouts, patterns and checks. Read the one for what you are building before its first
screen: `tiny_guide` with its `topic` returns it together with the directions by industry and
the final checklist, and where the design skill is installed it is the file beside this one.

## Directions by kind of product

Only for an app whose person gave no brand or standards of their own — theirs always win.
Starting points, not answers. Pick the direction that fits the brief, then make it this app's
own — shift the hue, tint the neutrals toward the accent, choose the weights — so two finance
apps never come out the same. Every font here is on npm as `@fontsource/<name>` (or
`@fontsource-variable/<name>`); self-host it rather than linking a font service.

| Kind | Direction | Palette | Type |
|---|---|---|---|
| Money, accounting, fintech | Ledger: precise, trusted | ink and cool greys, one emerald or teal accent for gains and actions | IBM Plex Sans + IBM Plex Mono for figures |
| | Modern bank: warm, calm | warm off-white, deep plum or petrol accent | Manrope |
| | Personal tracker: light, friendly | soft greys, one clear sky or coral accent | Figtree |
| Health, wellbeing, care | Calm clinic | white, blue-green accent, high contrast | Atkinson Hyperlegible |
| | Gentle | sage or eucalyptus, warm white, rounded shapes | Nunito |
| | Mindful | sand and muted lavender, lots of air | Newsreader headings + DM Sans |
| Food, cafés, restaurants | Market | deep green with a mustard or tomato accent | Bricolage Grotesque |
| | Bistro | black, white and one bold red | Playfair Display + Work Sans |
| | Photo-led | neutral frame, the food carries the colour | Fraunces + Figtree |
| Shops, products, e-commerce | Editorial | big imagery, quiet neutrals, accent only on price and buy | Cormorant Garamond + Instrument Sans |
| | Bold brand | one saturated brand colour used generously | Archivo |
| | Minimal | monochrome, accent on the buy button alone | Geist |
| Learning, kids | Playful | bright primaries, large targets, rounded | Fredoka or Baloo 2 |
| | Study | calm blue, highlighter yellow for what matters | Lexend |
| Creative, portfolio, personal | Typographic | oversized headings, one accent, the work as the image | Syne or Bricolage Grotesque |
| | Gallery | near-white, the work first, thin rules | Instrument Serif + Instrument Sans |
| | Studio at night | deep charcoal, one warm accent (not acid green) | Space Grotesk |
| Internal tools, B2B | Quiet productivity | neutral, one blue or indigo accent (no gradients) | Onest or Geist |
| | Dense operations | compact slate, colour only for status | IBM Plex Sans |
| Community, events, social | Energetic | coral or orange accent, lively type | Outfit |
| | Warm community | sunflower with deep blue | Figtree |
| | Night event | dark ground, one vivid duotone | Sora |
| Travel, stays, real estate | Photo-led | sand and ocean, generous imagery | Newsreader + DM Sans |
| | Quiet luxury | ivory and near-black, a restrained metallic accent | Cormorant Garamond + Manrope |
| Developer tools, docs | Technical | dark-first, mono for code and labels | Geist + JetBrains Mono |
| | Readable docs | white, a serif for long reading | Source Serif 4 + Public Sans |
| Public service, non-profit | Plain and accessible | high contrast, one trustworthy blue or green | Public Sans or Atkinson Hyperlegible |
| Fitness, sport | High energy | dark-friendly, electric orange or lime | Barlow Condensed + Archivo |

## Before you call it done

- The person's own standards, where they gave any, are followed on every screen, and nothing
  from these guides overrode them.
- The brief is written (`DESIGN.md`) and the screens match it.
- The palette is theirs or this app's own, in the theme variables, in light and dark; no hex colours in components.
- Colour marks actions, selection, status and the key number, and nothing else.
- Contrast: body text 4.5:1, large text and icons 3:1, both themes.
- One primary action per screen; destructive actions confirmed or undoable.
- Each screen is laid out for what it holds — a sidebar, a grid, a table, a list beside its
  detail — with a narrow centred column only for one focused task; a laptop's width is used.
- Empty, loading, error and very long states all designed; long names truncate (`truncate`,
  `line-clamp-*`, `min-w-0` on flex children) instead of breaking the layout.
- Every input has a visible label, the right `type`, `autocomplete` and `inputmode`; errors
  sit next to their field.
- Every clickable thing has hover, pressed and visible focus states; icon-only buttons have an
  `aria-label`; a link navigates, a button acts.
- Motion is quick (150–250 ms; up to about 500 ms only for an earned moment in a playful app),
  on transform and opacity only, and off under reduced motion.
- Images have width and height, alt text, and load lazily below the fold.
- Filters, tabs and pages live in the URL, so a link opens the same view.
- It works at 375px wide with 44px touch targets and no sideways scroll.
- None of the giveaways (the design guide's "What gives generated UI away").
- You looked at it: preview_app, light and dark, at a laptop's width and a phone's.

## Playbooks

Read the one for what you are building before its first screen:

- [app](app.md) — something people sign in to and use
- [website](website.md) — pages people read
- [dashboard](dashboard.md) — numbers, charts and reports
- [presentation](presentation.md) — slides, as a file or a shareable web deck
- [form](form.md) — sign-ups, surveys, bookings and requests
