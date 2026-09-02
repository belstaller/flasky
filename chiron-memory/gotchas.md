# gotcha

A non-obvious pitfall or trap, learned the hard way.

## `tests/test_client.py::test_landing_page` asserted the step-1 placeholder text, not real conte…

What: The `test_landing_page` test written when the `/` route was scaffolded asserted the literal placeholder string `'Welcome to Flasky'` from `landing.html`, so it broke the moment the real hero/features/how-it-works copy replaced that placeholder. · Why: A landing page built across multiple sequential work orders (scaffold route+template, then fill in content, then style) will have earlier steps' tests pinned to placeholder text that later steps are explicitly meant to replace. · Where: tests/test_client.py (`test_landing_page`), app/templates/landing.html. · Learned: when a work order says to replace placeholder/scaffold content, grep tests for the placeholder string before finishing — the fix is to update the assertion to check for stable markers of the new content (e.g. CTA button text, `url_for`-rendered link paths like `/auth/register`), not to treat the failure as a regression.

## The auth blueprint's `before_app_request` hook redirects any authenticated-but-unconfirme…

What: The auth blueprint's `before_app_request` hook redirects any authenticated-but-unconfirmed user to `/auth/unconfirmed` for every non-auth page, before any per-view logic runs. · Why: This caused the new landing-page redirect test to unexpectedly get a 302 to `/auth/unconfirmed` instead of the expected feed redirect. · Where: app/auth/views.py (before_app_request handler). · Learned: Any test that logs a user in and expects to reach a normal (non-auth) route must also confirm the user first (as the existing `test_register_and_login` test already does), or the confirm-account redirect intercepts the request first. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-1 -->

## Existing tests reference routes via hardcoded path strings (e.g

What: Existing tests reference routes via hardcoded path strings (e.g. `self.client.get('/')` in tests/test_client.py, `'http://localhost:5000/'` in tests/test_selenium.py) rather than via `url_for`, unlike the app/template code which always uses `url_for('main.index')`/`url_for('.index')`. · Why: This means a route path change is *not* fully safe just because a grep of `app/` and templates for `url_for` calls comes up clean — the test suite has its own, separate set of hardcoded path references that must be found and updated independently. · Where: tests/test_client.py, tests/test_selenium.py. · Learned: when changing a route's path, grep tests/ specifically for hardcoded path/URL strings (e.g. `client.get('/...')`) in addition to grepping app/ for url_for usage. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-7 -->

## tests/test_client.py::test_landing_page asserted the literal step-1 placeholder text ('We…

What: tests/test_client.py::test_landing_page asserted the literal step-1 placeholder text ('Welcome to Flasky') from landing.html. · Why: In multi-step page-building work, tests pinned to placeholder copy pass silently until a later step replaces that copy with real content, then break even though the change is correct. · Where: tests/test_client.py, app/templates/landing.html. · Learned: Before replacing placeholder content added by an earlier step, grep the test suite for the placeholder string and update assertions to check stable markers (CTA text, url_for-rendered link targets) instead of literal copy. <!-- id: dd874d2b-9dc3-427c-8427-e8dae9ba2b15-1 -->
