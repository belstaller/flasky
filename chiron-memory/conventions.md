# convention

A rule the codebase follows — naming, patterns, and where things live.

## All internal navigation in this codebase links via `url_for('main.index')` / `url_for('.i…

What: All internal navigation in this codebase links via `url_for('main.index')` / `url_for('.index')`, never a hardcoded `/` path string. · Why: This is what made moving the feed's route from `/` to `/feed` a one-line change with zero broken links. · Where: app/main/views.py, app/templates/*.html. · Learned: verify this convention holds before route-path changes; grep for hardcoded path strings as a safety check rather than assuming. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-1 -->

## Routes that are public but need different behavior for logged-in users (no `@login_requir…

What: Routes that are public but need different behavior for logged-in users (no `@login_required`, but redirect if authenticated) implement the check manually with `if current_user.is_authenticated: return redirect(...)` inside the view body, mirroring the pattern used in `app/auth/views.py`'s `login()` view. · Why: A decorator-based approach (`@login_required`) would block anonymous users entirely, which is wrong for a landing page that must be visible to anonymous visitors and only redirect away authenticated ones. · Where: app/main/views.py (new `landing()` view), app/auth/views.py (source pattern). · Learned: for any future 'public but auth-aware' route, replicate the manual `current_user.is_authenticated` check rather than reaching for a decorator. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-6 -->
