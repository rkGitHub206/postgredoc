## Context and explanation

- On a windows 7 32bit platform, working with docker in not a possibility.

- So the current solution is an reuse of the following source: https://github.com/stellirin/docker-postgres-windows.

- Windows context (nanoserver) and Postgres.


## How to use this image

```console
$ docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d stellirin/postgres-windows
```

## About this container image

A Windows container to run PostgreSQL based on the [EnterpriseDB](https://www.enterprisedb.com/) distribution [PostgeSQL for Windows](https://www.postgresql.org/download/windows/) download page.

This repository builds a Windows based Docker image that is functionality similar to the official [Linux based Docker image](https://hub.docker.com/_/postgres/).

This image includes `EXPOSE 5432` (the postgres port), so standard container linking will make it automatically available to the linked containers. 

The default `postgres` user and database are created in the entrypoint with `initdb`.

Files *.sql are fired at the end of the process to create a table and to fill a PostgeSQL table.


### Testing

The resulting image has not been tested yet, due do limitation of the win 32bit platform used to implement this solution. 

### Additional explanation

#### Linux image and windows
The solution reused here(https://github.com/stellirin/docker-postgres-windows) has been made with the following observations.
The Linux based Docker image cannot run on Windows as a LCOW container. 
This is due to differences in functionality between the NTFS and EXT4 file systems. 
Specifically, Linux commands such as `chown` do not work but the PostgreSQL images rely on them for security.

#### Entrypoint
The entrypoint is written as a batch script because the database is run on `windows/nanoserver`, which doesn't have PowerShell. 
The entrypoint script is a batch script because of these limitations. 

#### Licence
The files are a reuse here from the following source: https://github.com/stellirin/docker-postgres-windows.