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
generous padding at the page edge — at least 20px on a phone (`px-5`), 32px or more on a
laptop — and bars that run edge to edge pad their content by the same amount. Lines of text
around 60–75 characters. Align everything to the same few edges.

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
group with space and a subtle background instead. Cards side by side are built alike: the same
parts in the same places — if one has an icon, a chart or a caption, they all do — so their
labels, numbers and bottoms line up and none looks emptier than its neighbour. Design the states
too: empty (what to do first), loading (skeletons shaped like the content), error (what happened
and what to do next), and long (search, paging).

**The header stays put.** The header — name or logo, navigation, theme switch, account — stays
at the top while the page scrolls, so people can always move around without scrolling back up:
`sticky top-0 z-40` on the `<header>`, a solid page background (`bg-background`, never
see-through over the content) and its bottom border. Keep it short — about 56–64px, one row
on a phone, where an app's screens move to the bottom bar — so it doesn't eat the screen. A
sidebar stays put the same way (`sticky top-0 h-svh`), and a detail pane beside a long list
scrolls on its own.
A website's header may shrink as you scroll, but stays reachable. A long list's search and
filters stick just below the header the same way, so people can search without scrolling back
up — on a phone, at least the search. Measure the header (a `ResizeObserver` writing
`--header-h` on the root) and stick below it with `top-(--header-h)`, rather than guessing
its height; a sticky element only sticks within its parent, so give it one as tall as the list.

**shadcn/ui is where you start, not how it must look.** The components in
`src/components/ui` are the app's own code: change radius, padding, sizes, shadows and variants
there so buttons, inputs and cards fit the app's character, and add a variant rather than
overriding classes at every use. Compose them into the app's own pieces (a stat tile, an item
row). Don't add a component because it exists — use the simplest thing that does the job.

**Never the browser's own controls.** What the browser draws itself ignores the theme and looks
the same in every app, so build it from the app's components, styled to its palette and radius:

- A date: the calendar in a popover (`calendar` + `popover`); a time: the app's own choices
  (chips or a list). Never `type="date"`, `type="time"` or `datetime-local`.
- A dropdown: the `select` component or a combobox, never a bare `<select>`.
- A hint on hover or focus: the `tooltip` component, never a `title` attribute.
- A question or warning: `alert-dialog` or `dialog`; a message: a toast. Never `alert()`,
  `confirm()` or `prompt()`.
- Checkboxes, radios, switches, sliders and file pickers: styled ones (a visually hidden native
  input under the styled one keeps the keyboard and screen readers working).

`type="email"`, `tel`, `inputmode` and `autocomplete` stay — they only choose the keyboard
and autofill. Restyle the calendar, popover and tooltip like every other component: the accent
for the selected day, the app's radius and type, both themes.

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

**Make motion say where things are.** Movement should match the layout, so people feel where
they went:

- **Indicators glide.** The selected pill of tabs, segmented controls, filters and the bottom
  navigation slides to the option picked rather than jumping (`motion`'s shared `layoutId` on
  the pill), and a softer pill follows the pointer across the options on hover.
- **Screens move the way the navigation runs.** Going forward (to a tab further right, deeper
  into a list) enters from the right; going back enters from the left. A short slide with a
  fade (about 24px, 200 ms in, a little faster out).
- **Things come from where they live.** A detail opened from a list slides in from the side it
  sits on, a menu or popover grows from its trigger, a bottom sheet rises from the bottom, and
  a success replaces the form with a brief scale-in.
- **A theme change crossfades.** Light to dark fades smoothly across the whole page
  (`document.startViewTransition` around the class change, about 250 ms ease-out on
  `::view-transition-old(root)` and `-new(root)`), never a hard flash; instant under reduced
  motion or where the browser has no view transitions.

Keep one easing and duration for the whole app, defined once (a small `motion.ts`), so every
movement feels like the same hand made it.

**An app doesn't bounce.** Turn off the page's rubber-band overscroll (`overscroll-behavior:
none` on `html` and `body`), so pulling past the top or bottom doesn't drag the header and
bars with it; a website reading like a document may keep it.

**Light and dark, both designed** — unless their standards settle it otherwise. Give people a
light / dark / match-device switch, somewhere visible and styled to fit: the app starter includes one (`src/components/theme-toggle.tsx`,
remembered on the device in a cookie); if the project has none, add one the same way — a cookie,
not localStorage, which a deploy flags. Check both
themes: shadows barely show in dark, so lift surfaces with a slightly lighter background
instead; pure black and pure white are harsh — use the palette's near-black and off-white.

**Phone first.** Most people open a link on a phone: touch targets at least 44px, one column
on a phone that becomes the screen's real layout on a wider one (the sidebar, the grid, the
detail beside its list), nothing reachable only by hover, inputs that bring up the right
keyboard (`type="email"`, `inputmode="numeric"`). Every control is laid out for the phone
too, not just squeezed: a row of three or more icon buttons in the header (a theme switch, view
toggles) becomes one button with a small menu that marks the current choice; segmented options
and filter tabs are each as wide as their words (never equal columns, which squeeze the longest
label), and when they no longer fit they scroll sideways or become a select; a toolbar's
secondary actions fold into a "more" menu. Check each control at 375px, not only the layout.

**On a phone, an app's screens live in a bottom bar.** Below the `sm` breakpoint, an app with
two to five main screens moves them out of the header into a navigation bar fixed to the
bottom, in reach of a thumb: an icon over a short label for each, the current one clearly
marked (the accent behind its icon), a solid background, a border on top and the phone's safe
area below. The header becomes one row — name or logo, theme switch, account. Publish the
bar's height (`--nav-h`, 0 from `sm` up) so the page pads its bottom by it and anything else
pinned to the bottom (a form's submit bar, a detail's actions, toasts) sits above it, never
under it. More than five screens: four in the bar and "More". A website keeps a menu in its
header instead. A detail screen on a phone (one item opened from a list) keeps its way back
pinned just under the header while it scrolls — a slim bar reading "← ‹the list's name›" — and
its actions in a bar of their own pinned at the bottom, above the navigation, never scrolled out
of reach.

**Words are part of the design.** Short, plain, active; a button says what it does ("Save
expense", not "Submit"); an error says what to do next; an empty state invites the first action.
When people choose between options, every option shows what the choice turns on — how many
are left, what it costs, how long it takes — not only the last few. Numbers, money and dates go
through `Intl.NumberFormat` and `Intl.DateTimeFormat`, in the reader's locale.

**Every field gets a placeholder, written for this app.** A friendly prompt or a sample answer,
in the app's own voice and about its own subject: a short question the field answers, or a
realistic example of what goes there. Where the format matters, a sample in that format (a phone
number in the reader's local format, "name@company.com"); in a search box, a real term from the
app's own data to try ("Try '‹a name or status that exists›'").
Never the label again ("Enter your name", "Email"), never generic filler ("Type here…"), and
never in place of the label, which stays visible above the field. Placeholder text uses the
muted text colour at full strength, so it is readable but clearly not an answer.

**Only content can be selected.** In an app, a drag or a double-click shouldn't paint the
interface: the header, navigation, buttons, tabs, chips, badges, labels, hints, stat tiles and
screen titles get `select-none` (one rule in the base CSS covers most of them). What people
actually copy stays selectable: names, phone numbers, emails, addresses, notes, messages,
codes and amounts — and anything typed into a field (give `input` and `textarea`
`select-text`, so an unselectable form never stops typing). Never block copying everywhere;
a website's reading text stays selectable throughout.

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
- A form's submit button is never a scroll away (a bar pinned to the bottom on a long form).
- Cards in a row have the same parts and line up; stat tiles carry an icon and a small visual
  drawn from the data.
- Each screen is laid out for what it holds — a sidebar, a grid, a table, a list beside its
  detail — with a narrow centred column only for one focused task; a laptop's width is used.
- Empty, loading, error and very long states all designed; long names truncate (`truncate`,
  `line-clamp-*`, `min-w-0` on flex children) instead of breaking the layout.
- Every option people choose between shows what helps them choose (what's left, the price,
  how long).
- Every input has a visible label, a friendly placeholder written for this app, the right
  `type`, `autocomplete` and `inputmode`; errors sit next to their field.
- Every clickable thing has hover, pressed and visible focus states; icon-only buttons have an
  `aria-label`; a link navigates, a button acts.
- Select-all highlights only content (names, contacts, notes, typed text), never the
  header, controls, labels or titles.
- Motion is quick (150–250 ms; up to about 500 ms only for an earned moment in a playful app),
  on transform and opacity only, and off under reduced motion.
- Selected pills glide between options, screens slide in the direction of the navigation, a
  theme change crossfades, and an app has no rubber-band overscroll.
- Images have width and height, alt text, and load lazily below the fold.
- Filters, tabs and pages live in the URL, so a link opens the same view.
- It works at 375px wide with 44px touch targets and no sideways scroll; at least 20px of
  padding at the phone's edges; an app's screens in a bottom navigation bar on a phone, with
  every other bottom bar above it; a detail screen keeps its way back and its actions pinned.
- The header stays at the top while the page scrolls, on a laptop and a phone, with a solid
  background; a long list's search (and filters, where there's room) stays pinned under it.
- No control the browser draws: dates use the calendar, dropdowns the select, hints the tooltip,
  questions a dialog — all styled to the theme.
- None of the giveaways (the design guide's "What gives generated UI away").
- You looked at it: preview_app, light and dark, at a laptop's width and a phone's.

## Playbooks

Read the one for what you are building before its first screen:

- [app](app.md) — something people sign in to and use
- [website](website.md) — pages people read
- [dashboard](dashboard.md) — numbers, charts and reports
- [presentation](presentation.md) — slides, as a file or a shareable web deck
- [form](form.md) — sign-ups, surveys, bookings and requests
