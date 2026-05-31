# Ollama with Docker Compose (Minimal Ubuntu)

This project runs Ollama in a container based on minimal Ubuntu.

## What's Included

- Base image: Ubuntu 24.04
- Ollama installation using:

  ```sh
  curl -fsSL https://ollama.com/install.sh | sh
  ```

- Service exposed on port 11434
- Persistent volume for models at `/root/.ollama`

## Requirements

- Docker
- Docker Compose (the `docker compose` plugin)

## Project Structure

- `Dockerfile`: builds the Ubuntu image and installs Ollama
- `docker-compose.yaml`: defines the service, port, and volume

## Start the Service

```sh
docker compose up -d --build
```

## Verify Ollama Is Running

```sh
docker compose ps
curl http://localhost:11434/api/tags
```

If everything is working, the `api/tags` call will return JSON.

## Download and Run a Model

```sh
docker compose exec ollama ollama pull llama3.2
docker compose exec ollama ollama run llama3.2
```

## Logs and Troubleshooting

```sh
docker compose logs -f ollama
```

## Stop and Clean Up

Stop:

```sh
docker compose down
```

Stop and remove the volume (deletes downloaded models):

```sh
docker compose down -v
```

## GPU Note

This Compose setup runs on CPU by default. If you want to use an NVIDIA GPU, add runtime/device configuration in `docker-compose.yaml`.
