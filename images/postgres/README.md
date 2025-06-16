# PostgreSQL

## Setup

Pulling the Postgres image from Docker Hub:

```bash
docker pull postgres:17.5
```

Create a container and run the image:

> The postgres data is located at `/var/lib/postgresql/data`.<sup>[[1]](https://stackoverflow.com/a/76217607/16027098)</sup>

```bash
docker run --name postgres-17_5 \
  -h 127.0.0.1 \
  -e POSTGRES_PASSWORD=db_postgres_pwd \
  -d \
  -p 5432:5432 \
  -v postgres-data:/var/lib/postgresql/data \
  postgres:17.5
```

Breaking down the command

| Flag     | Value                                  | Description                                                                                                                                                   |
| -------- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--name` | `postgres-17_5`                        | Assigns a descriptive name to the container.                                                                                                                  |
| `-h`     | `127.0.0.1`                            | The hostname is required in docker environment. See [here for more details](https://forums.docker.com/t/cant-connect-to-postgres-through-docker/120051/5). |
| `-e`     | `POSTGRES_PASSWORD=db_postgres_pwd`    | Sets the `postgres` user's password.                                                                                                                  |
| `-d`     |                                        | Runs the container in detached mode(background).                                                                                                                          |
| `-p`     | `5432:5432`                            | Maps container port 5432 to host port 5432, allowing external connection from host.                                                           |
| `-v`     | `postgres-17_5-data:/var/lib/postgresql/data` | Create a volume called `postgres-17_5-data` if not exist and map the volume to the `/var/lib/postgresql/data` of the container.                                      |

> [!NOTE]
> The default username is `postgres` and the database is `postgres`.

## References

* [DockerHub](https://hub.docker.com/_/postgres/)
