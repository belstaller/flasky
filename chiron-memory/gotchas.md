# gotcha

A non-obvious pitfall or trap, learned the hard way.

## The auth blueprint's `before_app_request` hook redirects any authenticated-but-unconfirme…

What: The auth blueprint's `before_app_request` hook redirects any authenticated-but-unconfirmed user to `/auth/unconfirmed` for every non-auth page, before any per-view logic runs. · Why: This caused the new landing-page redirect test to unexpectedly get a 302 to `/auth/unconfirmed` instead of the expected feed redirect. · Where: app/auth/views.py (before_app_request handler). · Learned: Any test that logs a user in and expects to reach a normal (non-auth) route must also confirm the user first (as the existing `test_register_and_login` test already does), or the confirm-account redirect intercepts the request first. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-1 -->
