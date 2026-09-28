# Designing a presentation — slides

> If the person has design standards of their own — a design system, components, a brand guide, an app or site to match — follow those, and use this playbook only for what they leave open. If they gave none, follow it all.

First decide what the person wants:

- **A file** — a .pptx, a PDF, a Keynote to send or present from their own laptop: make it
  with your own tools (your presentation or document skill), filling it from the app's data
  with `summarize_app_data` and `read_app_data`. Deploy nothing.
- **A link** — a deck to share, open on any device, or keep current from an app's data: build
  a web deck and deploy it. The skeleton below is a single HTML file that needs no build; put it
  in its own app (or as a page of the app whose data it shows), and "Save as PDF" in the browser
  still gives one slide per page.

## Slides that work

- One idea per slide, and the headline states the point ("Churn fell 18% after the redesign"),
  not the topic ("Churn").
- Few words: around 25 on a slide; the detail goes in what the speaker says (notes).
- Big type: headlines around 72–110px and body at least 36–40px on a 1920×1080 slide.
- One grid and one margin for the whole deck; one accent colour, used for the thing to look at.
- A chart shows one comparison with the point highlighted, labelled directly; a number that
  matters can be the whole slide.
- Images full-bleed or on the grid, never floating.
- A story: title → the problem → what we found → what we propose → proof → the ask; about one
  slide per minute; a closing slide with the ask and how to reach you.
- The deck's palette and fonts follow the same brief as everything else (see the design guide).

## Web deck skeleton

Keyboard (arrows, space, Page Up/Down, Home/End), click either half, swipe on a phone; `#3`
in the address opens slide three; F for full screen; fits any window; one slide per page when
printed. Change the variables at the top for the palette and font, and add sections.

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Deck title</title>
<style>
  :root { --bg: #f6f5f1; --ink: #1d1c1a; --muted: #6a665e; --accent: #2e6a5b; --font: system-ui, sans-serif; }
  * { box-sizing: border-box; margin: 0; }
  html, body { height: 100%; background: #111; overflow: hidden; }
  body { font-family: var(--font); }
  .deck { position: absolute; left: 50%; top: 50%; width: 1920px; height: 1080px; background: var(--bg);
          transform: translate(-50%, -50%) scale(var(--scale, 1)); }
  .slide { position: absolute; inset: 0; padding: 120px 150px; display: flex; flex-direction: column;
           justify-content: center; gap: 40px; background: var(--bg); color: var(--ink);
           opacity: 0; visibility: hidden; transition: opacity 250ms ease-out, visibility 250ms; }
  .slide.current { opacity: 1; visibility: visible; }
  .slide h1 { font-size: 112px; line-height: 1.04; letter-spacing: -0.02em; text-wrap: balance; }
  .slide h2 { font-size: 76px; line-height: 1.08; letter-spacing: -0.01em; text-wrap: balance; }
  .slide p, .slide li { font-size: 40px; line-height: 1.4; color: var(--muted); max-width: 34ch; }
  .slide ul { padding-left: 1.1em; display: grid; gap: 16px; }
  .slide .accent { color: var(--accent); }
  .count { position: fixed; right: 20px; bottom: 14px; color: #9a9a9a; font: 14px/1 system-ui, sans-serif; }
  @media (prefers-reduced-motion: reduce) { .slide { transition: none; } }
  @media print {
    @page { size: 1920px 1080px; margin: 0; }
    html, body { height: auto; overflow: visible; background: none; }
    .deck { position: static; transform: none; height: auto; }
    .slide { position: relative; height: 1080px; opacity: 1; visibility: visible; break-after: page; }
    .count { display: none; }
  }
</style>
</head>
<body>
<main class="deck">
  <section class="slide"><h1>The headline says the point, not the topic</h1><p>Speaker · Date</p></section>
  <section class="slide"><h2>One idea per slide</h2><ul><li>A few words each</li><li>The detail belongs in what you say</li></ul></section>
  <section class="slide"><h2><span class="accent">3×</span> faster when the number is the slide</h2></section>
</main>
<div class="count" aria-hidden="true"></div>
<script>
  const deck = document.querySelector(".deck");
  const slides = [...document.querySelectorAll(".slide")];
  const count = document.querySelector(".count");
  const clamp = (n) => Math.min(Math.max(n, 0), slides.length - 1);
  let current = 0;
  function fit() { deck.style.setProperty("--scale", Math.min(innerWidth / 1920, innerHeight / 1080)); }
  function show(n) {
    current = clamp(n);
    slides.forEach((s, k) => { s.classList.toggle("current", k === current); s.inert = k !== current; });
    count.textContent = `${current + 1} / ${slides.length}`;
    history.replaceState(null, "", `#${current + 1}`);
  }
  const fromHash = () => clamp((parseInt(location.hash.slice(1), 10) || 1) - 1);
  addEventListener("keydown", (e) => {
    if (["ArrowRight", "ArrowDown", "PageDown", " ", "Enter"].includes(e.key)) show(current + 1);
    else if (["ArrowLeft", "ArrowUp", "PageUp", "Backspace"].includes(e.key)) show(current - 1);
    else if (e.key === "Home") show(0);
    else if (e.key === "End") show(slides.length - 1);
    else if (e.key === "f") document.documentElement.requestFullscreen?.();
    else return;
    e.preventDefault();
  });
  addEventListener("click", (e) => {
    if (e.target.closest("a, button, input, select, textarea, video")) return;
    show(e.clientX > innerWidth / 2 ? current + 1 : current - 1);
  });
  let startX = null;
  addEventListener("touchstart", (e) => { startX = e.touches[0].clientX; }, { passive: true });
  addEventListener("touchend", (e) => {
    const dx = startX === null ? 0 : e.changedTouches[0].clientX - startX;
    if (Math.abs(dx) > 40) show(dx < 0 ? current + 1 : current - 1);
    startX = null;
  });
  addEventListener("resize", fit);
  addEventListener("hashchange", () => show(fromHash()));
  fit();
  show(fromHash());
</script>
</body>
</html>
```

For numbers that stay current, make the deck a page of the app that holds the data and fill
the slides from `tiny.db` (`sumBy`, `countBy`) when it opens.

## Checks

- Each slide can be understood in the three seconds it is on screen.
- The headlines alone tell the story.
- It reads from the back of a room: nothing under 36px on a 1920px slide.
- Printed or saved as PDF, every slide is one page and nothing is cut off.
