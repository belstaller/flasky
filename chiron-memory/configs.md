# config

Setup and configuration — env vars, flags, how to run the project.

## Running the test suite via `python -m unittest` requires the `SERVER_NAME` environment va…

What: Running the test suite via `python -m unittest` requires the `SERVER_NAME` environment variable to be set (e.g. `SERVER_NAME=localhost`). · Why: Without it, `url_for` calls made outside of an active request context (as used in some view/test flows) fail; the testing config in config.py does not set a default SERVER_NAME. · Where: config.py, tests/ (invoked as `SERVER_NAME=localhost python -m unittest ...`). · Learned: Always export SERVER_NAME before running this project's test suite locally. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-3 -->

## No virtualenv ships with the repo; `venv/` is listed in .gitignore, so creating one local…

What: No virtualenv ships with the repo; `venv/` is listed in .gitignore, so creating one locally with `python3 -m venv venv && venv/bin/pip install -r requirements/dev.txt` is safe and expected for running tests. · Why: — · Where: requirements/dev.txt, .gitignore. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-4 -->

## The project defines a custom `python flasky.py test [--coverage]` click command as its in…

What: The project defines a custom `python flasky.py test [--coverage]` click command as its intended test-runner entrypoint. · Why: seen in flasky.py's click command definitions; `python -m unittest discover -s tests` also works directly and was used as a simpler substitute. · Where: flasky.py. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-5 -->

## Running the app or test suite via a bare `python3 -c ...` script (outside the project's n…

What: Running the app or test suite via a bare `python3 -c ...` script (outside the project's normal test runner) fails at import time unless the SERVER_NAME environment variable is exported first, because config.py's ProductionConfig class (around line 42) depends on it being set. · Why: Hit this while manually smoke-testing the rendered landing page and re-running tests from an ad hoc shell command — import of config.py raised until SERVER_NAME was set. · Where: config.py, ProductionConfig. · Learned: Export SERVER_NAME before any manual python3 invocation that imports the app/config in this repo; it's a pre-existing repo quirk unrelated to whatever feature is being worked on, not something to 'fix'. <!-- id: dd874d2b-9dc3-427c-8427-e8dae9ba2b15-3 -->
