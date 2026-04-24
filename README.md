# cicd-buzz

A simple Flask web application that generates random CI/CD and DevOps buzzword phrases. Built as a demonstration project for CI/CD pipelines using Travis CI and Docker.

## Overview

cicd-buzz serves a single-page web app that randomly combines adjectives, adverbs, verbs, and buzzword terms (e.g., *continuous integration*, *devops*) into motivational-sounding tech phrases like:

> "Modern Continuous Integration Substantially Accelerates Devops"

## Project Structure

```
cicd-buzz/
├── app.py                  # Flask application entry point
├── buzz/
│   └── generator.py        # Buzz phrase generation logic
├── tests/
│   └── test_generator.py   # Unit tests (pytest)
├── Dockerfile              # Docker image definition
├── requirements.txt        # Python dependencies
└── .travis.yml             # CI/CD pipeline configuration
```

## Requirements

- Python 3.x (or Python 2.7)
- [Flask](https://flask.palletsprojects.com/) >= 1.0.0
- [pytest](https://pytest.org/) >= 3.0.6

## Local Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/joonasanttonen/cicd-buzz.git
   cd cicd-buzz
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the application:**
   ```bash
   python app.py
   ```
   The app will be available at [http://localhost:5000](http://localhost:5000).

   To use a custom port, set the `PORT` environment variable:
   ```bash
   PORT=8080 python app.py
   ```

## Running Tests

```bash
python -m pytest -v
```

## Docker

**Build the image:**
```bash
docker build -t cicd-buzz .
```

**Run the container:**
```bash
docker run -p 5000:5000 cicd-buzz
```

The app will be available at [http://localhost:5000](http://localhost:5000).

## CI/CD Pipeline

This project uses **Travis CI** for continuous integration and deployment:

- On every push, Travis runs the test suite (`python -m pytest -v`).
- On a successful build, the Docker image is built and pushed to Docker Hub:
  - Pushes to `master` are tagged as `latest`.
  - Pushes to other branches are tagged with the branch name.

The deployment script is located at [`.travis/deploy_dockerhub.sh`](.travis/deploy_dockerhub.sh) and requires the following Travis CI environment variables to be set:

| Variable         | Description                  |
|------------------|------------------------------|
| `DOCKER_USER`    | Docker Hub username          |
| `DOCKER_PASS`    | Docker Hub password          |
| `TRAVIS_REPO_SLUG` | Set automatically by Travis (`username/repo`) |

## License

This project is provided as-is for learning and demonstration purposes.
