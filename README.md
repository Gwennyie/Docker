# PSUSphere Docker

A containerized version of the PSUSphere Django project. Anyone with Docker installed can run it with a single command.

## Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop) (on Windows, use the WSL 2 engine)
- Check that Docker works:

```
docker --version
```

## Option 1: Run from Docker Hub (for clients)

You don't need the source code for this. Only the `for_client/docker-compose.yml` file is required.

1. Download or clone this repository and open the `for_client` folder:

```
git clone https://github.com/Gwennyie/Docker.git
cd Docker/for_client
```

2. Start the app with a single command:

```
docker compose up -d
```

3. Open http://localhost:8000 in your browser.

4. (First time only) Create an admin account:

```
docker compose exec web python manage.py createsuperuser
```

### Useful commands

| Command | What it does |
|---|---|
| `docker compose ps` | Shows running containers |
| `docker compose logs -f web` | Follows the app logs |
| `docker compose down` | Stops and removes the containers |
| `docker compose pull` | Downloads the latest image |

## Option 2: Build the image yourself (for developers)

From the root of this repository:

```
docker compose up --build
```

Then open http://localhost:8000.

To build the image without starting it:

```
docker build -t psusphere-docker:latest .
```

## Publishing a new version to Docker Hub

```
docker login
docker tag psusphere-docker:latest gwennyie/psusphere-docker:latest
docker push gwennyie/psusphere-docker:latest
```

Docker Hub page: https://hub.docker.com/r/gwennyie/psusphere-docker

To update a client machine afterwards:

```
docker compose pull
docker compose down
docker compose up -d
docker compose exec web python manage.py migrate
```

## Project structure

```
Docker/
├── Dockerfile                  # Instructions for building the image
├── docker-compose.yml          # Builds the image locally
├── requirements.txt            # Python dependencies
├── .dockerignore               # Files excluded from the image
├── for_client/
│   └── docker-compose.yml      # Pulls the image from Docker Hub
├── manage.py
├── projectsite/
├── studentorg/
├── static/
└── templates/
```

## Environment variables

| Variable | Purpose |
|---|---|
| `DEBUG` | Enables Django debug mode |
| `DJANGO_SECRET_KEY` | Django secret key (development value only) |
| `DJANGO_ALLOWED_HOSTS` | Comma-separated list of allowed hosts |
| `SITE_ID` | Django sites framework ID |

## Stopping the app

```
docker compose down
```