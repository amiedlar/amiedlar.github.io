# CLAUDE.md

This repo is the professional homepage of Agnieszka Międlar, published at https://amiedlar.github.io.
It is a Jekyll site based on the AcademicPages template (GitHub Pages).

## Reference design

The site's structure should follow https://smithrgh.github.io (source: https://github.com/smithrgh/smithrgh.github.io, also an AcademicPages fork):
- Main menu (`_data/navigation.yml`): Research, Publications, People, Teaching, Talks and Media (`/talks/`), CV.
  Software is commented out (hidden) until `_pages/software.html` has content
  (order and the "Talks and Media" label set at her request; they differ from the reference on purpose).
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
- Software (`_pages/software.html`) is an empty stub;
  CV (`_pages/cv.md`, title "Curriculum Vitae", menu label stays "CV"): name line, then sections "Education"
  (`_data/education.yml`), "Employment History" (`_data/employment.yml`) and "Invited Research Stays" (`_data/research_stays.yml`; canceled visits left out), newest first.
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

## Teaching

- Same structure as https://smithrgh.github.io/teaching/: one row per file in `_teaching/`, newest `date` first, rendered by
  `_includes/rs-cvrow.html` (styles `_sass/layout/_cvrow.scss`): bold `heading` + `dates` on the right, `detail` + `location`
  on the right, then the `items` bullet list.
- Rows: one per level and institution, e.g. `_teaching/virginia-tech-undergraduate.md` (heading "Undergraduate Courses",
  detail "Virginia Tech"), `virginia-tech-graduate.md` ("Graduate Courses"). Courses are `items` like
  "MATH 2114H: Introduction to Linear Algebra (Spring 2027)", newest first; update `dates` (range) and `date` (most recent term).
  `summer-winter-schools.md` ("Summer and Winter Schools", kept last via an old `date`) is ready for entries.
  University of Kansas rows: add files the same way when there are courses.
- The teaching collection has no pages of its own (`output: false`).

## Research page

- Starts with "Research Interests" (intro paragraph + five bullet areas), text approved by her; edit only on request.
- `_pages/research.md`, section "Honors and Awards": rows from `_data/awards.yml` (newest first; `heading`, `dates`, `detail`,
  `location`), rendered with the same row include as Teaching. Only research fellowships/awards go here; student-mentoring
  awards (KU Undergraduate Research Awards, Graduate Research Consultant Award) were left out on purpose.
- Section "Funding" (first on the page), subsection "External Funding": rows from `_data/funding.yml` (`heading` = project, `dates` = grant period, `detail` = role,
  funder, award number, notes) plus `end` (YYYY-MM-DD; both funding lists are sorted by it, newest end date first).
  Never show dollar amounts on the site.
- Subsection "Internal Funding" (after External): rows from `_data/internal_funding.yml`, same fields plus `location` =
  university (right column).

## Talks and Media (`/talks/`; talks, presentations, press releases)

- `_pages/talks.html` renders sections from `_data/presentations.yml` ("Invited Research Presentations", "General Public Presentations"
  — arts/outreach for a public audience — and "Other Presentations" — student, departmental, seminars), newest first,
  as rows like the reference: `heading` = event, `dates`, `role` + `talk_title` (quoted; `paper` links a publication page),
  `location`. Each section shows its first `shown` (5) entries; the rest are behind a "More ..." `<details>` toggle.
- The old `_talks` collection / talkmap are not used.
- Canceled talks and talks postponed to a date that is already listed (e.g. Householder XXI 2020 -> 2022, Acta Numerica
  2021 -> 2022) are left out; only talks that took place are listed.

## People (`/people/`, research group)

- `_pages/people.html` renders `_data/people.yml`: sections Postdoctoral Researchers, Graduate Students
  (PhD and Master's; `role` says which), Undergraduate Students (members as cards: photo or initials, name linked to `url`, role, dates, topic, co-advisor, "Homepage · CV" links from `url`/`cv`) and Alumni
  (rows: name, degree + year, thesis, next position). Headings show even when empty. Photos go in `images/people/`.
  Field list is at the top of `_data/people.yml`. Styles: `_sass/layout/_people.scss`.

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
