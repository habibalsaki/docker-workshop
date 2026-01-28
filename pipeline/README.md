### Running PostgreSQL in a Container
Create a folder anywhere you'd like for Postgres to store data in. We will use the example folder ny_taxi_postgres_data. Here's how to run the container:

```docker
docker run -it --rm \
  -e POSTGRES_USER="root" \
  -e POSTGRES_PASSWORD="root" \
  -e POSTGRES_DB="ny_taxi" \
  -v ny_taxi_postgres_data:/var/lib/postgresql \
  -p 5432:5432 \
  postgres:18
```

### Explanation of Parameters
-e sets environment variables (user, password, database name)
-v ny_taxi_postgres_data:/var/lib/postgresql creates a named volume
Docker manages this volume automatically
Data persists even after container is removed
Volume is stored in Docker's internal storage
-p 5432:5432 maps port 5432 from container to host
postgres:18 uses PostgreSQL version 18 (latest as of Dec 2025)

### Alternative Approach - Bind Mount

First create the directory, then map it:

```docker
mkdir ny_taxi_postgres_data

docker run -it \
  -e POSTGRES_USER="root" \
  -e POSTGRES_PASSWORD="root" \
  -e POSTGRES_DB="ny_taxi" \
  -v $(pwd)/ny_taxi_postgres_data:/var/lib/postgresql \
  -p 5432:5432 \
  postgres:18
```

Named Volume vs Bind Mount
Named volume (name:/path): Managed by Docker, easier
Bind mount (/host/path:/container/path): Direct mapping to host filesystem, more control