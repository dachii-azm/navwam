# NavWAM Project Page

Project page for **NavWAM: A Navigation World Action Model for Goal-Conditioned Visual Navigation**.

A static site built on the [Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template)
(adopted from the [Nerfies](https://nerfies.github.io) project page). All content lives in `index.html`.

## Structure

- `index.html` — all page content (hero, teaser, overview, method, results, real-world, qualitative, BibTeX).
- `static/css/`, `static/js/` — Bulma / carousel / slider assets from the template.
- `static/figures/navwam/` — figures exported from the paper (PNG).
- `static/videos/navwam/` — real-robot rollout videos for the qualitative carousel.

## TODO before publishing

- Fill in the **Paper** and **Code** links (currently `#` placeholders) and the arXiv id in the BibTeX block.
- Add real-robot rollout videos to `static/videos/navwam/` as `rollout1.mp4` … `rollout4.mp4`.
- Replace `favicon.ico` if desired.

## Local preview

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```
