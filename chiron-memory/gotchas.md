# gotcha

A non-obvious pitfall or trap, learned the hard way.

## `auth.before_app_request` in app/auth/views.py redirects any authenticated-but-unconfirme…

What: `auth.before_app_request` in app/auth/views.py redirects any authenticated-but-unconfirmed user to `/auth/unconfirmed` before any other view executes, including newly added routes. · Why: This is easy to miss when writing a test that logs a user in and then hits an arbitrary route — the request never reaches the view under test, it 302s to the confirm-account page instead. · Where: app/auth/views.py (before_app_request hook); tests must confirm the user first, following the pattern in the existing `test_register_and_login` test. · Learned: any new test that checks behavior for a logged-in user must confirm the account first or the assertion will fail against the wrong response. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-2 -->

## `tests/test_client.py::test_landing_page` asserted the step-1 placeholder text, not real conte…

What: The `test_landing_page` test written when the `/` route was scaffolded asserted the literal placeholder string `'Welcome to Flasky'` from `landing.html`, so it broke the moment the real hero/features/how-it-works copy replaced that placeholder. · Why: A landing page built across multiple sequential work orders (scaffold route+template, then fill in content, then style) will have earlier steps' tests pinned to placeholder text that later steps are explicitly meant to replace. · Where: tests/test_client.py (`test_landing_page`), app/templates/landing.html. · Learned: when a work order says to replace placeholder/scaffold content, grep tests for the placeholder string before finishing — the fix is to update the assertion to check for stable markers of the new content (e.g. CTA button text, `url_for`-rendered link paths like `/auth/register`), not to treat the failure as a regression.

## Existing tests reference routes via hardcoded path strings (e.g

What: Existing tests reference routes via hardcoded path strings (e.g. `self.client.get('/')` in tests/test_client.py, `'http://localhost:5000/'` in tests/test_selenium.py) rather than via `url_for`, unlike the app/template code which always uses `url_for('main.index')`/`url_for('.index')`. · Why: This means a route path change is *not* fully safe just because a grep of `app/` and templates for `url_for` calls comes up clean — the test suite has its own, separate set of hardcoded path references that must be found and updated independently. · Where: tests/test_client.py, tests/test_selenium.py. · Learned: when changing a route's path, grep tests/ specifically for hardcoded path/URL strings (e.g. `client.get('/...')`) in addition to grepping app/ for url_for usage. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-7 -->
