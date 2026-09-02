# architecture

How the system is put together — layers, boundaries, and how data flows.

## The public landing page at `/` is served by a dedicated `main.landing` view rendering `ap…

What: The public landing page at `/` is served by a dedicated `main.landing` view rendering `app/templates/landing.html`, kept separate from the original `main.index` view/`index.html` template. · Why: The landing-page feature was deliberately split across work-order steps (step 1 added the route/template scaffold, step 2 filled in hero/features/how-it-works content) rather than repurposing the existing index page in place. · Where: app/main/views.py, app/templates/landing.html, app/templates/index.html. · Learned: Don't assume `index.html` is the landing page template — check which view/template `main.landing` actually points to before editing. <!-- id: dd874d2b-9dc3-427c-8427-e8dae9ba2b15-0 -->

## Flasky's REST API is implemented as its own blueprint at app/api_1_0/, mounted under the…

What: Flasky's REST API is implemented as its own blueprint at app/api_1_0/, mounted under the URL prefix /api/v1, separate from the main/auth blueprints. · Why: Confirmed by listing app/api_1_0/ before describing the 'REST API' feature on the landing page, since no REST API code exists under app/main or app/auth. · Where: app/api_1_0/. · Learned: Treat app/api_1_0/ as the source of truth for the API surface when linking to or documenting the REST API elsewhere in the app (templates, docs, landing copy). <!-- id: dd874d2b-9dc3-427c-8427-e8dae9ba2b15-2 -->
