# PostgreSQL

## Setup

Pulling the Postgres image from the dockerhub

```bash
docker pull postgres:17.5
```

Create a container and run the image

> [The postgres data location is different.](https://stackoverflow.com/a/76217607/16027098)

```bash
docker run --name postgres-17_5 -h 127.0.0.1 -e POSTGRES_PASSWORD=db_postgres_pwd -d -p 5432:5432 -v postgres-17_5-data:/var/lib/postgresql/data postgres:17.5
```

Breaking down the command

| Flag     | Value                                  | Description                                                                                                                                                   |
| -------- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `--name` | `postgres-17_5`                        | assigns a descriptive name to the container.                                                                                                                  |
| `-h`     | `127.0.0.1`                            | The hostname which required in docker environment. See [here for more details](https://forums.docker.com/t/cant-connect-to-postgres-through-docker/120051/5). |
| `-e`     | `POSTGRES_PASSWORD=db_postgres_pwd`    | sets the `postgres` password for PostgreSQL.                                                                                                                  |
| `-d`     |                                        | runs the container in detached mode.                                                                                                                          |
| `-p`     | `5432:5432`                            | maps port 5432 from the container to port 5432 on the host, enabling external access to PostgreSQL.                                                           |
| `-v`     | `postgres-17_5-data:/var/lib/postgres` | create a volume called `postgres-17_5-data` if not exist and map the volume to the `/var/lib/postgres` of the container.                                      |

> [!NOTE]
> The default username is `postgres` and the database is `postgres`.

## References

* [DockerHub](https://hub.docker.com/_/postgres/)
