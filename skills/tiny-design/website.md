# Designing a website — pages people read

> If the person has design standards of their own — a design system, components, a brand guide, an app or site to match — follow those, and use this playbook only for what they leave open. If they gave none, follow it all.

A landing page, a portfolio, a small business, an event, docs or a blog: people arrive from a
link, decide in seconds whether it is for them, read, and maybe act once. Build it on the site
starter (Astro), so every page arrives as finished HTML that search engines and link previews
can read.

## Shape by purpose

- **Landing page:** a hero that says what it is and for whom → proof (logos, numbers, a quote)
  → how it works in three steps → what you get → questions → one clear final call to action.
- **Small business:** what, where and when first — hours, location, the menu or services, how
  to book or call — then the story and the photos.
- **Portfolio:** the work first, big; a short line about the person; each project with the
  problem, the result and the images.
- **Event:** name, date, place and the register button above the fold; schedule, speakers,
  getting there, questions.
- **Docs or blog:** a reading layout — a narrow column (about 65 characters), a table of
  contents, clear headings, code and images that fit the column.

## The hero

Open with the most characteristic thing in the subject's world: the product in use, the dish,
the building, the work itself — not a gradient with three statistics. A headline under about
ten words that says what it is and for whom; one primary action and at most one secondary.

## Craft

- Rhythm: generous vertical space between sections (80px or more on desktop), content width
  capped (around 1100–1200px), prose narrower. Vary section treatments sparingly — a band of
  colour, a full-bleed image — so the page has a beat without looking like a template.
- Type can be more expressive than in an app: a display face for headlines, a calm text face
  at 17–19px with a line height around 1.6; `text-wrap: balance` on headings.
- Images: real photographs or screenshots with one consistent treatment; width and height set,
  lazy below the fold, compressed (WebP or AVIF), alt text that says what is shown.
- Motion: one orchestrated entrance for the hero, at most a gentle reveal as sections scroll
  in. Never hijack scrolling.
- Navigation: a header that stays out of the way (it may shrink as you scroll), a real menu on
  a phone, a footer with contact and the essentials.
- Every page has its own title and description, one `h1`, headings in order, and an image for
  link previews.
- One form (a sign-up, a booking request) follows the form playbook; the site adds the SDK tag
  only for it.

## Checks

- In five seconds a stranger can say what this is, who it is for and what to do next.
- It reads well on a phone first; tap targets are big enough and nothing scrolls sideways.
- The page loads fast: self-hosted fonts, sized images, little JavaScript.
- Then the general checklist in the design guide.
