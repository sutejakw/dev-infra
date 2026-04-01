# dev-env

Docker-based local development environment providing databases, caching, and container management.

## Services

### Infrastructure (`infra/`)

| Service    | Image           | Container        | Port  |
| ---------- | --------------- | ---------------- | ----- |
| MySQL      | mysql:8.0       | infra_mysql      | 3306  |
| PostgreSQL | postgres:16     | infra_postgres   | 5432  |
| Redis      | redis:7-alpine  | infra_redis      | 6379  |

All services are connected via a `devnet` bridge network and persist data under `infra/db_data/`.

**Default credentials:**

| Service    | User       | Password   | Database     |
| ---------- | ---------- | ---------- | ------------ |
| MySQL      | dev_user   | dev_pass   | default_db   |
| MySQL      | root       | root       | -            |
| PostgreSQL | dev_user   | dev_pass   | default_db   |

### Portainer (`portainer/`)

Web-based Docker management UI.

| Port | Protocol |
| ---- | -------- |
| 8000 | HTTP     |
| 9443 | HTTPS    |

Access at `https://localhost:9443`.

## Usage

Start infrastructure services:

```sh
cd infra
docker compose up -d
```

Start Portainer:

```sh
cd portainer
docker compose up -d
```

Stop services:

```sh
docker compose down
```

## Connecting to Services

MySQL:

```sh
docker exec -it infra_mysql mysql -u dev_user -pdev_pass default_db
```

PostgreSQL:

```sh
docker exec -it infra_postgres psql -U dev_user -d default_db
```

Redis:

```sh
docker exec -it infra_redis redis-cli
```

## Project Structure

```
dev-env/
├── infra/
│   ├── docker-compose.yml    # MySQL, PostgreSQL, Redis
│   └── db_data/              # Persistent volumes
│       ├── mysql/
│       ├── postgre/
│       └── redis/
└── portainer/
    └── docker-compose.yml    # Portainer CE
```
