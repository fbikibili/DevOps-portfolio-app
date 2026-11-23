# DevOps Portfolio App

A small Python Flask app with tests, a Dockerfile, and a Jenkins pipeline.

## Endpoints

- `/` returns a short status message.
- `/health` returns `{"status": "ok"}`. Use it to check the app is running.

## Run locally

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python app.py
```

Open http://localhost:5000 and http://localhost:5000/health.

## Run the tests

```bash
source .venv/bin/activate
pytest
```

## Build and run the Docker image

```bash
docker build -t devops-portfolio-app:1.0 .
docker run -d --name portfolio -p 5000:5000 devops-portfolio-app:1.0
curl http://localhost:5000/health
docker stop portfolio && docker rm portfolio
```

## Jenkins pipeline

The `Jenkinsfile` runs three stages:

1. **Install:** creates a virtual environment and installs the requirements.
2. **Test:** runs pytest.
3. **Build Image:** builds the Docker image, tagged with the Jenkins build number.

Jenkins runs in Docker on port 8081, with the Docker socket mounted so it can build images.
