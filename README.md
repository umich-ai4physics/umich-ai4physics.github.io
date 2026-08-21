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
bundle install && bundle exec jekyll serve --baseurl ""
```

Then open <http://localhost:4000/>.

The `--baseurl ""` override serves the site at the server root, so the local URL
is short and there is no `/umich-ai4physics` prefix to remember. To preview
exactly as production serves it — under the repo prefix, which is worth doing
once before a release to catch any hard-coded `/path` links — drop the override
and open <http://localhost:4000/umich-ai4physics/>. Note that WEBrick, unlike
GitHub Pages, does not redirect the prefix without its trailing slash.

## Deployment

Pushing to `main` triggers [`.github/workflows/pages.yml`](.github/workflows/pages.yml),
which builds the site and publishes it to GitHub Pages.

Both `…/umich-ai4physics` and `…/umich-ai4physics/` reach the site: GitHub Pages
answers the prefix without a trailing slash with a 301 to the canonical
trailing-slash form, so there is nothing to configure for that.

One-time setup: in **Settings → Pages**, set **Source** to **GitHub Actions**,
and replace the placeholder `url:` in `_config.yml` with the org/user URL
(`baseurl` should stay `/umich-ai4physics` unless the repo is renamed).
