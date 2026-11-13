# CLAUDE.md

This repo is the professional homepage of Agnieszka Międlar, published at https://amiedlar.github.io.
It is a Jekyll site based on the AcademicPages template (GitHub Pages).

## Reference design

The site's structure should follow https://smithrgh.github.io (source: https://github.com/smithrgh/smithrgh.github.io, also an AcademicPages fork):
- Main menu (`_data/navigation.yml`): Research, Publications, Software, Conference contributions (`/talks/`), Teaching, CV.
- Publications page: grouped by category, numbered within each category, title linking to the publication page,
  an authors/citation line, then link pills (BibTeX pop-up, Preprint, Code, ...). No excerpts in the list.

## Rules

- Do not change the site's content (bio, publication data, etc.) unless explicitly asked; structural/layout changes only.
- Removing leftover AcademicPages sample content is welcome, but ask before deleting anything that might be real content.
- Don't commit or push unless asked.

## Current state (Nov 2026)

- Menu matches the reference. Research (`_pages/research.md`) and Software (`_pages/software.html`) are empty stubs;
  Talks (`/talks/`, titled "Conference contributions"), Teaching and CV (`_pages/cv.md`) are empty and waiting for real content.
- Template sample entries in `_talks/`, `_teaching/` and the sample publication were removed.
- Still left from the template: sample attachments in `files/` (`paper1–3.pdf`, `slides1–3.pdf`, `bibtex1.bib`; nothing links to them),
  and unused sample pages/collections not in the menu (portfolio, blog posts in `_posts/`, `_pages/markdown.md`, etc.).
- `_pages/about.md` (home page) holds the bio; author sidebar info is under `author:` in `_config.yml`.

## Building

- Local build was not possible on this Mac: only system Ruby 2.6 (too old for the Gemfile) and no Docker.
  Changes are verified by pushing to GitHub Pages, or install a newer Ruby (e.g. Homebrew) and run `bundle exec jekyll serve`.

## Publications

- One file per publication in `_publications/`; `category` must be a key of `publication_category` in `_config.yml`
  (`manuscripts`, `books`, `conferences`, `preprints`), otherwise it does not appear on the page
  (this is why the preprints were missing before `preprints` was added).
- Section order on the page follows the order of `publication_category` in `_config.yml`; entries within a section are newest first (by `date`).
- List rendering is in `_includes/archive-single.html` (publications branch) and styled by `_sass/layout/_publications.scss`.
- Existing entries use `citation`, `paperurl`, `preprint`, `slidesurl`, `bibtexurl`. The reference site's fields are also supported:
  `authors`, `status`, `arxiv_id`, `doi`, `arxiv`, `code`, and `bibtex` (inline BibTeX shown in a pop-up via `assets/js/bibtex.js`).
