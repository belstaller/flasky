# convention

A rule the codebase follows — naming, patterns, and where things live.

## Simple templates that extend `base.html` (e.g

What: Simple templates that extend `base.html` (e.g. 403.html, 404.html) follow a minimal `{% block title %}` + `{% block page_content %}` structure with a `<h1>` inside a `div.page-header`. · Why: — · Where: app/templates/404.html, app/templates/403.html, app/templates/landing.html. · Learned: New stub/placeholder pages in this project should mirror this exact minimal block structure rather than inventing a new template layout. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-2 -->

## Routes that are public but need different behavior for logged-in users (no `@login_requir…

What: Routes that are public but need different behavior for logged-in users (no `@login_required`, but redirect if authenticated) implement the check manually with `if current_user.is_authenticated: return redirect(...)` inside the view body, mirroring the pattern used in `app/auth/views.py`'s `login()` view. · Why: A decorator-based approach (`@login_required`) would block anonymous users entirely, which is wrong for a landing page that must be visible to anonymous visitors and only redirect away authenticated ones. · Where: app/main/views.py (new `landing()` view), app/auth/views.py (source pattern). · Learned: for any future 'public but auth-aware' route, replicate the manual `current_user.is_authenticated` check rather than reaching for a decorator. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-6 -->
