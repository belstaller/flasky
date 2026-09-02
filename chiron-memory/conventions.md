# convention

A rule the codebase follows — naming, patterns, and where things live.

## Simple templates that extend `base.html` (e.g

What: Simple templates that extend `base.html` (e.g. 403.html, 404.html) follow a minimal `{% block title %}` + `{% block page_content %}` structure with a `<h1>` inside a `div.page-header`. · Why: — · Where: app/templates/404.html, app/templates/403.html, app/templates/landing.html. · Learned: New stub/placeholder pages in this project should mirror this exact minimal block structure rather than inventing a new template layout. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-2 -->
