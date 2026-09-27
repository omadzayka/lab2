# Box Styles — Single HTML, Two Stylesheets

A single-page site built with **only HTML and CSS** (no JavaScript, no
external libraries) that renders two completely different layouts of
the same six boxes, depending on which stylesheet is linked.

## Files

| File          | Purpose                                                        |
|---------------|-----------------------------------------------------------------|
| `index.html`  | The one HTML document — markup never changes between versions   |
| `styleA.css`  | Produces **Version A**: six boxes stacked vertically and centered |
| `styleB.css`  | Produces **Version B**: five boxes in a row + one pinned corner box |

## How it works

`index.html` contains six boxes (`A`–`F`) and links to a single
stylesheet in its `<head>`:

```html
<link rel="stylesheet" href="styleA.css">
```

Swapping that `href` to `styleB.css` (and reloading the page) switches
the entire look of the page — the HTML itself is never touched.

```html
<link rel="stylesheet" href="styleB.css">
```

## Version A — vertical, evenly spaced

- Six 100×100px boxes stacked in a single column, centered horizontally.
- Boxes are spread evenly from the top to the bottom of the window using
  a flexbox column with `justify-content: space-between`. Resizing the
  window changes the *gaps* between boxes, never their size.
- Boxes A–E alternate background colors (`#dfe1e7` / `#eeeff2`) and have
  a 1px top border (`#687291`).
- Box F has a distinct background (`#687291`), a 4px black border, and
  its text is centered vertically (unlike A–E, whose text sits near the top).
- Font: Tahoma, 40px.

**Notable technique:** boxes A–E live inside a `.container` div in the
markup, but `styleA.css` sets `display: contents` on it. That removes
the wrapper from the visual layout (without removing its children),
letting all six boxes act as siblings in one flex layout — which is
what makes the "equally spaced across the whole page" effect work
cleanly.

## Version B — horizontal, pinned corners

- Boxes A–E form a horizontal row pinned to the top-left corner and
  never wrap, even if the window is narrower than the row itself.
- Each box is 100×150px (`#eeeff2`) with a 10px dotted left border
  (`#D0D0FF`), separated by 10px of spacing, with 10px of padding
  between the letter and the box edges.
- Box F is pinned to the bottom-right corner independently of A–E and
  stays there regardless of window size.
- Hovering any box shows a pointer cursor and swaps its background to
  `yellow` with `goldenrod` text.
- Font: Tahoma, 40px.

## Viewing it

Just open `index.html` in a browser — no build step or server
required. To see the other version, edit the `<link>` tag's `href` in
`index.html` (or serve both and toggle manually).

## Constraints followed

- Pure HTML/CSS only — no JavaScript, no external stylesheets/libraries.
- Uses CSS Flexbox for layout in both versions.
- All spacing/behavior not explicitly specified (e.g. page margins,
  default text color) was chosen to be visually reasonable.