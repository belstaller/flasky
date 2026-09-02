# decision

A choice made and the reasoning behind it — the path taken over the alternatives.

## The main feed (`index()` view) was moved from route `/` to `/feed`, while root `/` was as…

What: The main feed (`index()` view) was moved from route `/` to `/feed`, while root `/` was assigned to a new unauthenticated-only landing page. · Why: Flask can't have two views on the same path; the work order required `/` to serve a marketing landing page for anonymous visitors and redirect authenticated users to the feed, so the feed had to move — `/feed` was chosen (alternative considered: `/home`). The `index` endpoint name was kept unchanged so no `url_for('main.index')`/`url_for('.index')` call site needed updating. · Where: app/main/views.py. · Learned: when reassigning a root route, check whether the endpoint name (not just the path) is what call sites depend on — renaming only the path avoids cascading changes. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-0 -->
