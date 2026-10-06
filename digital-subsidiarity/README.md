# Digital Subsidiarity: Stewardship as a Vocation

An interactive, scroll-driven essay in the style of [Humanity 3026](https://superada.ai/3026), adapting the *Digital Subsidiarity Network* augmentation "Stewardship as Vocation" into fourteen chapters, each with its own live canvas visualisation.

No build step and no dependencies: plain HTML, CSS, and JavaScript.

## Run locally

```bash
cd digital-subsidiarity
python3 -m http.server 8000
# open http://localhost:8000
```

Opening `index.html` directly from disk also works.

## Files

- `index.html`: page shell (HUD clock, chapter nav, progress bar, film atmosphere)
- `styles.css`: typography and cinematic layout
- `story.js`: the story text, its parser, the scroll engine, and the visualisations
- `STORY.md`: the full text, generated from `story.js`

## Editing the story

The text lives in the `STORY` string at the top of `story.js`. Each chapter is a `##` heading followed by a directive:

```
## II. The Fifty-Year Test
<!-- viz: fade | year: 5 | until: 50 | era: The Long Test | status: Drifting | accent: #d79a52 -->
```

- `viz` picks the background visualisation (`mesh`, `roll`, `fade`, `communion`, `steward`, `bloom`, `primitives`, `keystone`, `ecosystem`, `ladder`, `school`, `exit`, `compass`, `field`, `generations`, `dawn`, `credits`)
- `year` / `until` drive the "Year N" clock, counting from `year` to `until` across the chapter
- `era`, `status`, and `accent` set the HUD labels and the chapter colour

Blocks are separated by blank lines: plain paragraphs become cards, `>` and `>>` become pull quotes, `>>>` is a large centred statement, and `::: stats` ... `:::` with `Term | description` rows becomes a definition list.

After editing, regenerate `STORY.md`:

```bash
python3 -c "import re;s=open('story.js').read();open('STORY.md','w').write(re.search(r'const STORY = \x60(.*?)\x60;',s,re.S).group(1))"
```

## Deploying

Any static host works. On Vercel, set the project root to `digital-subsidiarity`. On GitHub Pages, publish this folder.
