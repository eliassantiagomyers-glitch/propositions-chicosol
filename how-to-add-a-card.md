# Adding a new proposition card

All the cards are generated from one JavaScript array near the bottom of
`prop-tracker.html`, called `PROPOSITIONS`. You never touch the HTML or CSS to
add a card — you just add one object to that array, and the grid grows to fit it.

## Where to look

Open `prop-tracker.html` and find this block inside the `<script>` tag:

```js
const PROPOSITIONS = [
  {
    id: "prop-5",
    number: "Prop 5",
    title: "Recall reform",
    summary: "Delay replacing recalled state officials",
    details: "Placeholder — replace with 2–3 sentences...",
    isNew: true
  },
  ...
];
```

## Adding a card

Copy one of the existing objects, paste it as a new entry (don't forget the
comma between entries), and fill in the six fields:

| Field | What it is | Notes |
|---|---|---|
| `id` | A short unique slug for this card | Lowercase, hyphens only, no spaces (e.g. `"prop-42"`). Must be different from every other card's `id` — it's used internally to link the button to its detail panel. |
| `number` | The proposition label | Shown in bold, e.g. `"Prop 42"`. |
| `title` | The short name of the measure | Shown next to the number after a `\|`, e.g. `"Property taxes"`. Keep it to 2–4 words so it doesn't wrap awkwardly. |
| `summary` | The one-line description | Always visible under the title, e.g. `"Ban new taxes on personal property"`. One sentence, no period needed. |
| `details` | The 2–3 sentence write-up | This is what appears when someone taps the card open. Write it the way you'd write a nut graf — what it does, who's behind it, what it means if it passes. |
| `isNew` | Whether the "New" tag shows | Set to `true` when you first file the measure, then flip it to `false` once it's been up for a while (a few days to a week is reasonable — there's no automatic expiration). |

Example — adding Prop 42 from the reference screenshot:

```js
{
  id: "prop-42",
  number: "Prop 42",
  title: "Property taxes",
  summary: "Ban new taxes on personal property",
  details: "This measure would bar the state and local governments from creating new taxes on personal property. Backers say it protects residents from surprise levies; opponents warn it could squeeze future city and county budgets.",
  isNew: true
}
```

Save the file and reload it — the new card appears in the grid automatically.

## Layout behavior (nothing to configure)

- The grid is fixed at **two cards per row** on desktop and tablet, and drops
  to **one per row** on screens narrower than 640px. This is set once in the
  CSS (`.prop-grid` and the `@media (max-width: 640px)` block) and applies to
  every card automatically — you don't need to touch it as you add more.
- Cards fill left-to-right, top-to-bottom in the order they appear in the
  array. Put newer or higher-priority measures first if you want them to show
  up first.
- Each card's detail panel is independent — readers can have more than one
  open at once.

## Changing colors or fonts later

The three brand colors are defined once at the top of the `<style>` block:

```css
--primary: #a0312a;   /* Prop number, title accents, left border */
--secondary: #f8b135; /* "New" badge */
--tertiary: #e75a1f;  /* chevron button */
```

Change a value here and it updates everywhere it's used — you don't need to
hunt through the rest of the CSS.

## Embedding on chicosol.org

The file is self-contained (HTML + CSS + JS in one place), so you have two
options:

1. **Standalone page:** upload `prop-tracker.html` as-is if you want it at its
   own URL.
2. **Embed in a post/page:** in the WordPress editor, add a **Custom HTML**
   block and paste in everything between (and including) the `<div class="prop-tracker">`
   and the closing `</script>` tag — skip the `<!DOCTYPE>`, `<head>`, and `<body>`
   wrapper tags, since the WordPress page already provides those.

## A note on the fonts and exact colors

I couldn't pull chicosol.org's live stylesheet to match it pixel-for-pixel, so
this uses Fraunces (headlines) and Work Sans (body text) as a close, readable
pairing, plus the three hex colors you gave me. If you want it to match
exactly, send me the site's actual font names and any additional colors
(link color, body text color) and I'll swap them in.
