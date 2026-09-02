# gotcha

A non-obvious pitfall or trap, learned the hard way.

## `auth.before_app_request` in app/auth/views.py redirects any authenticated-but-unconfirme…

What: `auth.before_app_request` in app/auth/views.py redirects any authenticated-but-unconfirmed user to `/auth/unconfirmed` before any other view executes, including newly added routes. · Why: This is easy to miss when writing a test that logs a user in and then hits an arbitrary route — the request never reaches the view under test, it 302s to the confirm-account page instead. · Where: app/auth/views.py (before_app_request hook); tests must confirm the user first, following the pattern in the existing `test_register_and_login` test. · Learned: any new test that checks behavior for a logged-in user must confirm the account first or the assertion will fail against the wrong response. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-2 -->

## Existing tests reference routes via hardcoded path strings (e.g

What: Existing tests reference routes via hardcoded path strings (e.g. `self.client.get('/')` in tests/test_client.py, `'http://localhost:5000/'` in tests/test_selenium.py) rather than via `url_for`, unlike the app/template code which always uses `url_for('main.index')`/`url_for('.index')`. · Why: This means a route path change is *not* fully safe just because a grep of `app/` and templates for `url_for` calls comes up clean — the test suite has its own, separate set of hardcoded path references that must be found and updated independently. · Where: tests/test_client.py, tests/test_selenium.py. · Learned: when changing a route's path, grep tests/ specifically for hardcoded path/URL strings (e.g. `client.get('/...')`) in addition to grepping app/ for url_for usage. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-7 -->
