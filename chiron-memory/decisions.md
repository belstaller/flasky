# decision

A choice made and the reasoning behind it — the path taken over the alternatives.

## Main feed moved from `/` to `/feed`; `/` is now the marketing landing page

**What**: `app/main/views.py` — the `index()` view (the authenticated post feed)
is now registered at `/feed` instead of `/`. A new `landing()` view, with no
`@login_required`, is registered at `/`: it renders `app/templates/landing.html`
for anonymous visitors and redirects authenticated users to `main.index`
(`/feed`). The endpoint name `index` was kept unchanged, so every
`url_for('main.index')` / `url_for('.index')` call site kept working without
edits.

**Why**: The work order required `/` to serve a public landing page for
anonymous users while authenticated users get redirected to the main feed.
Flask/Werkzeug can't cleanly dispatch two different endpoints on the exact
same static URL rule, so the feed had to move off `/`. `/feed` was chosen
because the work order itself calls the destination "the main feed".

**Where**: `app/main/views.py` (`landing()` and `index()`), `app/templates/landing.html`,
`tests/test_client.py`, `tests/test_selenium.py`.

**Learned**: `auth.before_app_request` (in `app/auth/views.py`) redirects any
authenticated-but-unconfirmed user to `auth.unconfirmed` for *any* non-auth,
non-static endpoint — including the new `/` landing route — before that
route's own view code runs. A test that logs in a freshly registered user and
then expects a redirect to the feed must confirm the account first
(`user.confirm(token)`), otherwise the observed redirect target is
`/auth/unconfirmed`, not `/feed`.
