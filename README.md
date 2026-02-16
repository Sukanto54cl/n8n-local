![Docker](https://img.shields.io/badge/docker-ready-blue?logo=docker)
![n8n](https://img.shields.io/badge/n8n-local-orange?logo=n8n)
![License](https://img.shields.io/badge/license-MIT-green)
![Platform](https://img.shields.io/badge/platform-local-lightgrey)

# n8n Local Setup (Docker Compose)

## What is **n8n** ?

[n8n](https://n8n.io/) is an open-source workflow automation platform that lets you connect apps, APIs, and services using visual workflows.  
It allows you to automate tasks by combining triggers, logic, and actions — similar to tools like Zapier or Make  but with more flexibility and the option to self-host locally.  

This repository provides a simple Docker Compose setup to run **n8n** locally for development and experimentation.

---

## Requirements

Make sure you have installed:

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (or Docker Engine)
- Docker Compose (included with Docker Desktop)

Check installation:

```bash
docker --version
docker compose version
```

---

## Project Structure

```text
n8n-local/
├─ docker-compose.yml
├─ .env.example
├─ .gitignore
└─ README.md
```

---

## Environment variables

Copy the example file:

```bash
cp .env.example .env
````

Example .env.example:

```bash
GENERIC_TIMEZONE=Europe/Berlin
TZ=Europe/Berlin
N8N_SECURE_COOKIE=false
````

N8N_SECURE_COOKIE=false is useful for local HTTP usage (especially Safari).
Do not use this setting for production.

---

## Start and Run n8n

### Run:

```bash
docker compose up -d
````

Open in browser:

```bash
http://localhost:5678
````

On first launch, create a local owner account.

### Stop n8n

```bash
docker compose down
````

### Restart

```bash
docker compose up -d
````

### View logs

```bash
docker compose logs -f n8n
````

---

## Data persistence

All workflows and credentials are stored in a Docker volume:

```bash
n8n_data
````

Your data will remain even after restarting containers.

---

## Timezone

Timezone is configured via .env:

```bash
GENERIC_TIMEZONE=Europe/Berlin
TZ=Europe/Berlin
````

Chamge if needed

---

## Update n8n

Pull the latest image and restart:

```bash
docker compose pull
docker compose up -d
````

---

## Remove everything (WARNING)

This removes the container and stored data:

```bash
docker compose down -v
````

---

## Common issues

- **Safari secure cookie warning**

This setup includes:

```bash
N8N_SECURE_COOKIE=false
````

which fixes local Safari cookie restrictions.

- **Port already in use**
  
If port 5678 is busy, stop the conflicting container or change the port:

```bash
ports:
  - "5679:5678"
````

Then open: 

```bash
http://localhost:5679
````

---

## Production note

This setup is intended for local development only.
For production use, you should:
- Enable HTTPS
- Use secure cookies
- Configure authentication properly
- Add reverse proxy (e.g., Nginx or Traefik)