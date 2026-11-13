# CLAUDE.md

This repo is the professional homepage of Agnieszka Międlar, published at https://amiedlar.github.io.
It is a Jekyll site based on the AcademicPages template (GitHub Pages).

## Reference design

The site's structure should follow https://smithrgh.github.io (source: https://github.com/smithrgh/smithrgh.github.io, also an AcademicPages fork):
- Main menu (`_data/navigation.yml`): Research, Publications, Teaching, Presentations and Talks (`/talks/`), Software, CV
  (order and the "Presentations and Talks" label set at her request; they differ from the reference on purpose).
- Publications page: grouped by category, numbered within each category, title linking to the publication page,
  an authors/citation line, then link pills (BibTeX pop-up, Preprint, Code, ...). No excerpts in the list.

## Rules

- Do not change the site's content (bio, publication data, etc.) unless explicitly asked; structural/layout changes only.
- Removing leftover AcademicPages sample content is welcome, but ask before deleting anything that might be real content.
- Don't commit or push unless asked.

## Current state (Nov 2026)

- Menu matches the reference and is in the header of every page, homepage included (`_includes/masthead.html`).
  All items have the `persist` class so they never collapse into the ☰ button; the first item's label is
  `masthead_title` ("Home") in `_config.yml`.
- Research (`_pages/research.md`) and Software (`_pages/software.html`) are empty stubs;
  Talks (`/talks/`, titled "Presentations and Talks"), Teaching and CV (`_pages/cv.md`) are empty and waiting for real content.
- Template sample entries in `_talks/`, `_teaching/` and the sample publication were removed.
- Still left from the template: sample attachments in `files/` (`paper1–3.pdf`, `slides1–3.pdf`, `bibtex1.bib`; nothing links to them),
  and unused sample pages/collections not in the menu (portfolio, blog posts in `_posts/`, `_pages/markdown.md`, etc.).
- `_pages/about.md` (home page) holds the bio; author sidebar info is under `author:` in `_config.yml`.
- Sidebar shows the name, then one block: title (`bio`: "Associate Professor") with `affiliation` lines right under it,
  then a "Mail address:" heading with the `address` lines, then "**Office:**" + `office` — all under `author:` in `_config.yml`
  (multi-line fields: one line per line), rendered in `_includes/author-profile.html` (shown on all screen sizes).

## Layout and phones

- Colours: the theme's own light greyscale look (white header, light grey footer). The reference's navy
  header/footer/side edges were tried and rejected — don't reintroduce them.
- `_sass/layout/_frame.scss` (ported from the reference): content uses the full width next to the sidebar, and the phone/tablet rules
  (menu is one swipeable row, no ☰; sidebar shows photo + links without "Follow"; homepage photo `.about__photo` moves above the text).
  The sidebar photo keeps the theme size (max 175px, round): `images/Miedlar.jpg` is portrait, so filling the sidebar made it huge.
- Keep every change phone-friendly; check at ~375px width as well as desktop.

## News (homepage)

- Items live in `_data/news.yml` (`date: YYYY-MM-DD`, `text:` Markdown allowed); order in the file doesn't matter, they're sorted newest first.
- `_includes/news.html`, included under the "News" heading in `_pages/about.md`, shows the 10 most recent;
  older ones are under a "More news" toggle (`<details>`, no JS). Change the count with `{% include news.html limit=N %}`.
  Styles in `_sass/layout/_news.scss`.

## Building

- Local preview uses Homebrew `ruby@3.3` (keg-only; the system Ruby 2.6 is too old). Gems are in `vendor/bundle` (git-ignored).
  ```
  export PATH=/opt/homebrew/opt/ruby@3.3/bin:$PATH
  bundle exec jekyll serve --livereload     # http://127.0.0.1:4000
  ```
  Restart the server after editing `_config.yml` (it isn't reloaded automatically).
- If `bundle install` fails on `eventmachine` with "'iostream' file not found", the fix (already set in `.bundle/config`) is:
  `bundle config set --local build.eventmachine "--with-cxxflags=-I$(xcrun --show-sdk-path)/usr/include/c++/v1"`.
- Sass deprecation warnings during the build are from the theme and harmless.

## Publications

- One file per publication in `_publications/`; `category` must be a key of `publication_category` in `_config.yml`
  (`submitted`, `manuscripts`, `books`, `conferences`, `preprints`, shown in that order), otherwise it does not appear on the page
  (this is why the preprints were missing before `preprints` was added).
- Section order on the page follows the order of `publication_category` in `_config.yml`; entries within a section are newest first (by `date`).
- Every entry has `bibtex: |` (BibTeX pop-up). DOIs/BibTeX came from Crossref (published versions, cleaned: her name as
  "Międlar", `--` page ranges, unique keys `<FirstAuthor><Year><firstword>`), arXiv for preprints, or were written from the
  citation when no DOI exists (Oberwolfach reports, Snowmass LoI, IPAM white paper).
- Buttons: BibTeX; Paper = `https://doi.org/<doi>` if `doi` is set, else `paperurl` unless it equals the preprint link; Preprint = `preprint`.
  When adding a paper, look up its DOI on Crossref and add `doi` and `bibtex` too.
- List rendering is in `_includes/archive-single.html` (publications branch) and styled by `_sass/layout/_publications.scss`.
- Existing entries use `citation`, `paperurl`, `preprint`, `slidesurl`, `bibtexurl`. The list splits a citation of the form
  `Authors (Year). "Title." Venue. Preprint: <a ...>arXiv</a>.` into an authors line (her name "Międlar, A." in bold)
  and a "Venue, Year." line (title and inline Preprint link dropped, since the title and the Preprint button show them).
  Keep new citations in that exact form; anything else is shown as the full citation. The reference site's fields are also supported:
  `authors`, `status`, `arxiv_id`, `doi`, `arxiv`, `code`, and `bibtex` (inline BibTeX shown in a pop-up via `assets/js/bibtex.js`).
