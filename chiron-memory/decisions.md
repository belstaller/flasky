# decision

A choice made and the reasoning behind it — the path taken over the alternatives.

## The pre-existing main feed view (`index()`) was moved from URL path `/` to `/feed`, while…

What: The pre-existing main feed view (`index()`) was moved from URL path `/` to `/feed`, while keeping its endpoint name `index`. · Why: The work order required `/` to serve the new anonymous landing page and redirect authenticated users to the main feed, but `/` was already registered as the feed — both could not coexist at the same path, so the feed had to move. · Where: app/main/views.py (index() route decorator changed from `@main.route('/', ...)` to `@main.route('/feed', ...)`). · Learned: The whole codebase references the feed via `url_for('main.index')` / `url_for('.index')` rather than hardcoded paths, so changing only the URL rule (not the endpoint name) meant no other call sites needed updates. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-0 -->
