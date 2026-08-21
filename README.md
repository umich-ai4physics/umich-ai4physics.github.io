# AI for Physics Seminar — UMich

Source for the seminar website: a single-page, no-JavaScript Jekyll site built
and deployed by GitHub Actions.

## Editing the site

Almost everything lives in two files — you should rarely need to touch HTML.

**`_config.yml`** — title, tagline, term, meeting time and place, contact
address, and the organizer list.

**`_data/speakers.yml`** — one entry per seminar. Entries are sorted by `date`
automatically, and talks whose date has passed are dimmed in the table:

```yaml
- date: 2026-09-10          # required, YYYY-MM-DD
  name: Jane Doe            # required (unless using `note`)
  url: https://…            # optional — links the speaker's name
  affiliation: MIT          # optional
  title: "Talk title"       # optional — renders as "TBD" when omitted
  abstract_url: https://…   # optional — links the title

- date: 2026-10-08
  note: "No seminar — fall break"   # a full-width row instead of a talk
```

The "About" blurb is prose in [`index.html`](index.html); edit it there.
Colors, type, and spacing are in [`assets/css/style.css`](assets/css/style.css).

## Local preview

```bash
bundle install && bundle exec jekyll serve
```

Then open <http://localhost:4000/>, which matches how production serves the
site: `baseurl` is empty, so there is no path prefix in either place.

## Deployment

Pushing to `main` triggers [`.github/workflows/pages.yml`](.github/workflows/pages.yml),
which builds the site and publishes it to GitHub Pages.

This requires **Settings → Pages → Source** to be set to **GitHub Actions**
(already done for this repo); without it the `configure-pages` step fails with
*Get Pages site failed*.

Because the repo is named `umich-ai4physics.github.io`, it is an organization
site and is published at https://umich-ai4physics.github.io/ — the domain root,
with no repo path. That is why `baseurl` in `_config.yml` is empty; renaming the
repo to anything else would make it a project site again and `baseurl` would
have to become `/<repo-name>`.
