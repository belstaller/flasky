# config

Setup and configuration — env vars, flags, how to run the project.

## Running the test suite requires the `SERVER_NAME=localhost` environment variable set, e.g

What: Running the test suite requires the `SERVER_NAME=localhost` environment variable set, e.g. `SERVER_NAME=localhost venv/bin/python -m unittest discover -s tests`. · Why: Tests failed with a traceback when run without it. · Where: tests/, config.py. · Learned: always export SERVER_NAME=localhost before invoking unittest in this project. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-3 -->

## No virtualenv ships with the repo; `venv/` is listed in .gitignore, so creating one local…

What: No virtualenv ships with the repo; `venv/` is listed in .gitignore, so creating one locally with `python3 -m venv venv && venv/bin/pip install -r requirements/dev.txt` is safe and expected for running tests. · Why: — · Where: requirements/dev.txt, .gitignore. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-4 -->

## The project defines a custom `python flasky.py test [--coverage]` click command as its in…

What: The project defines a custom `python flasky.py test [--coverage]` click command as its intended test-runner entrypoint. · Why: seen in flasky.py's click command definitions; `python -m unittest discover -s tests` also works directly and was used as a simpler substitute. · Where: flasky.py. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-5 -->
