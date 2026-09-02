# config

Setup and configuration — env vars, flags, how to run the project.

## Running the test suite via `python -m unittest` requires the `SERVER_NAME` environment va…

What: Running the test suite via `python -m unittest` requires the `SERVER_NAME` environment variable to be set (e.g. `SERVER_NAME=localhost`). · Why: Without it, `url_for` calls made outside of an active request context (as used in some view/test flows) fail; the testing config in config.py does not set a default SERVER_NAME. · Where: config.py, tests/ (invoked as `SERVER_NAME=localhost python -m unittest ...`). · Learned: Always export SERVER_NAME before running this project's test suite locally. <!-- id: 97631443-f707-499e-901c-566cfb28f43c-3 -->
