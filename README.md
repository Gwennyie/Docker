# PSUSphere Docker

Run the PSUSphere Django project with Docker. No Python setup needed.

## Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop), installed and running

## Run it

The image is pulled from Docker Hub (`gwennyie/psusphere-docker`), so you only need the `for_client` folder.

```
git clone https://github.com/Gwennyie/Docker.git
cd Docker/for_client
docker compose up -d
```

Then open **http://localhost:8000** in your browser.

> Use `localhost`, not `0.0.0.0`. Browsers can't open `0.0.0.0`.

## Create an admin account (first time only)

```
docker compose exec web python manage.py createsuperuser
```

## Stop the app

```
docker compose down
```

## For developers: build the image yourself

From the root of this repository:

```
docker compose up --build
```

## Files

| File | Purpose |
|---|---|
| `Dockerfile` | Builds the image |
| `docker-compose.yml` | Builds and runs the image locally |
| `for_client/docker-compose.yml` | Pulls the image from Docker Hub and runs it |
| `requirements.txt` | Python dependencies |
| `.dockerignore` | Files left out of the image |
