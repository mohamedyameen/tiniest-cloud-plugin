# Designing an app — something people sign in to and use

> If the person has design standards of their own — a design system, components, a brand guide, an app or site to match — follow those, and use this playbook only for what they leave open. If they gave none, follow it all.

A tracker, a CRM, an inventory, a booking tool: people come back to it, often daily, to do the
same few things. It should feel fast, calm and obvious; the design serves the task.

## Layout — screen by screen, for what it holds

The starter's frame (a header over one content area) is a placeholder. Choose each screen's
layout from what is on it:

- **Several areas to move between** (a CRM, an admin, the "manage" side of anything): a
  sidebar with the areas and the content beside it using the width. shadcn's sidebar
  (`npx shadcn@latest add sidebar`) collapses to a sheet on a phone.
- **Things people browse by how they look** (recipes, products, photos, boards, courses): a
  grid of cards that fills the row — `grid gap-4 grid-cols-[repeat(auto-fill,minmax(16rem,1fr))]`
  — each card led by its image or its most telling detail, not a title over three grey lines.
- **Records compared by their fields** (contacts, orders, expenses, bookings): a table with
  sortable columns on a laptop, the same rows as a list on a phone.
- **A queue worked through** (requests, tickets, submissions, an inbox): the list with the
  selected item's detail beside it on a wide screen (`lg:grid-cols-[22rem_1fr]`), the detail
  its own screen on a phone.
- **Stages** (a pipeline, tasks by status): columns side by side that scroll sideways.
- **One focused task** (answering a question, a checkout step, a long form, reading): a
  centred column (`mx-auto max-w-xl`) — the one place a narrow column is right.

One app mixes them: a quiz is played in a centred column and managed in a wide workspace with
a table of players. On a laptop use the width — content up to about 1280–1440px — and keep a
phone-width column for the screens that are one task; anywhere else it reads as unfinished.

## Shape

- **Open on the work.** The first screen is the thing people do most — the list with a way to
  add to it — not a welcome page. An empty state explains the first step and offers the button.
- **Navigation that fits the size.** Two or three areas: tabs in the header. Four or more: a
  sidebar on desktop that becomes a bottom bar (five items at most) on a phone. Keep the app's
  name or logo, the theme switch and the account at the edges.
- **Lists are the heart.** A row per item: the main text strong, a secondary line muted,
  status as a small consistent badge, meta (date, amount) right-aligned in tabular figures.
  Search, filters and sort sit above the list and run on the server (`where`, `order`, `limit`);
  more rows come with "Load more" or a cursor, never by loading everything.
- **Adding and editing.** A short form (up to about five fields) in a dialog — a bottom sheet
  on a phone; anything longer on its own page. Save shows progress and then the result in place.
- **Detail.** A header with the title, status and actions; the content; then activity — who
  created it and when (`created_by`, `mine`, `created_at`), shown as "You · 2 hours ago".
- **Deleting.** Reversible actions get an Undo in a toast instead of a confirmation; only what
  cannot be undone asks first, in words that name the thing.

## Feel

- Optimistic and live: show the change at once, then confirm; `tiny.db.watch` keeps every open
  screen current, and items entering or leaving a list animate their height and opacity.
- Feedback for everything: a pressed state, a spinner inside the button while saving, a toast
  for the outcome (shadcn's Sonner), an inline message when something fails with how to retry.
- Density that matches use: an internal tool can be compact (32–36px rows); a personal app
  breathes more (44–56px). Either way, one spacing scale.
- Keyboard: Enter submits, Escape closes, focus lands in the first field of a dialog and
  returns where it was when it closes; power tools can add shortcuts, shown in tooltips.

## Checks

- A new user understands what to do within five seconds of signing in.
- The main action is always one tap away, including on a phone (a sticky button if needed).
- Signed out, signing in, loading, empty, error and "no access" each look intentional.
- Status colours mean the same thing everywhere; nothing relies on colour alone.
- Then the general checklist, "Before you call it done".
