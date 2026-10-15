from pathlib import Path

readme = r"""# Node.js Web App Integration with MongoDB and Mongo Express using Docker

This project demonstrates how to run a Node.js web application with MongoDB and manage the database through Mongo Express. Docker Compose is used to start and manage the MongoDB services.

## Tech Stack

- **Node.js & Express.js** — web server and application routes
- **MongoDB** — stores application data
- **Mongo Express** — browser-based MongoDB administration interface
- **Docker** — runs MongoDB and Mongo Express in containers
- **Docker Compose** — defines and starts the database services together

## Architecture

- The Node.js application serves the static website from the `public/` directory on port **5050**.
- The application provides `/getUsers` and `/addUser` routes for reading and adding user records.
- MongoDB runs in a Docker container on port **27017**.
- Mongo Express runs in a separate container and is available on port **8081**.
- Mongo Express connects to MongoDB using the Compose service name `mongo`.

## Prerequisites

Install the following tools:

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (or Docker Engine with the Compose plugin)
- [Node.js and npm](https://nodejs.org/)

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/kunals-repo/node-webapp-integration-with-mongo-mongoexpress-dockercontainers.git
cd node-webapp-integration-with-mongo-mongoexpress-dockercontainers
```

### 2. Start MongoDB and Mongo Express

The Compose file in this repository is named `mongocompose.yml`.

```bash
docker compose -f mongocompose.yml up -d
```

Check the running containers:

```bash
docker compose -f mongocompose.yml ps
```

View service logs if needed:

```bash
docker compose -f mongocompose.yml logs -f
```

### 3. Start the Node.js application

Open a terminal in the project directory and run:

```bash
npm install
node server.js
```

The application listens on port **5050**.

> **Connection note:** The current `server.js` connection string uses `localhost:27017`, so this setup expects the Node.js application to run on your host machine while MongoDB runs in Docker. If you later containerize the Node.js application too, update its MongoDB connection hostname to `mongo` and put the app service in the same Compose file/network.

## Access the Services

| Service | URL |
|---|---|
| Node.js web application | http://localhost:5050 |
| Mongo Express | http://localhost:8081 |
| MongoDB | `localhost:27017` |

Mongo Express credentials configured in the sample Compose file are `admin` / `qwerty`.

## Application Routes

| Method | Endpoint | Purpose |
|---|---|---|
| `GET` | `/getUsers` | Retrieves user records from the `apnacollege-db` database's `users` collection |
| `POST` | `/addUser` | Inserts a user record into the `users` collection |

## Useful Docker Compose Commands

Stop and remove the containers:

```bash
docker compose -f mongocompose.yml down
```

Restart the services:

```bash
docker compose -f mongocompose.yml restart
```

## Key Learnings

- Running database services in Docker containers
- Using Docker Compose to manage multiple services
- Connecting Mongo Express to MongoDB through a Compose network
- Integrating a Node.js/Express application with MongoDB
- Exposing container services through port mappings

## Security Note

The repository's Compose file uses sample credentials for learning purposes. Do not use these credentials in production. Replace them with strong credentials, keep secrets out of source control, and use environment variables or a secrets manager.
"""

path = Path("/mnt/data/README.md")
path.write_text(readme, encoding="utf-8")
print(f"Created: {path}")

