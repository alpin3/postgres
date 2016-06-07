# alpin3/postgres

Multiple purpose PostgreSQL database based on Alpine

Image is based on the [gliderlabs/alpine](https://registry.hub.docker.com/u/gliderlabs/alpine/) base image

## Docker image size

[![Latest](https://badge.imagelayers.io/alpin3/postgres.svg)](https://imagelayers.io/?images=alpin3/postgres:latest 'latest')

## Docker image usage

```
docker run [docker-options] alpin3/postgres


```

## Variables

Following environment variables will be used when running:

### Standard

`PGDATA` - location of PostgreSQL database files (default: /var/lib/postgresql/data)
`POSTGRES_USER` - PostgreSQL username (if not specified: postgres)
`POSTGRES_PASSWORD` - PostgreSQL password (if not specified: empty)

### Specific to this image

`POSTGRES_DB` - PostgreSQL database name (if not specified: same as `POSTGRES_USER`)
`POSTGRES_FIX_OWNERSHIP` - PostgreSQL fix ownership of PGDATA


## Remarks

Note that if you don't specify any POSTGRES environment parameters, 
postgres will listen on all interfaces with ALL privileges as postgres
user. 

You just need to minimaly specify `POSTGRES_USER` as env variable in 
order to create PostgreSQL database with same name. Password will be 
empty. 

By default, only permissions to access `POSTGRES_DB` is given to 
`POSTGRES_USER`. No SUPERUSER permissions will be given.

But you don't need SUPERUSER permissions really. If you connect locally, 
it should not ask you for password, so you can use following procedure:

```
docker exec -it postgres_containerid /bin/sh
# gosu postgres psql
```

Only if nothing is specified, user postgres will 
have SUPERUSER privileges with access allowed from all hosts.

## Examples

Quick testing (you can connect to this host from any hosts with username postgres):

```
docker run -it --rm alpin3/postgres
```

Typical usage, create user test and database test:

```
docker run -it -v /host/dir/for/db:/var/lib/postgresql/data -e POSTGRES_USER=test alpin3/postgres
```

Typical usage, create user test with password Passw0rd and database testdb
```
docker run -it -v /host/dir/for/db:/var/lib/postgresql/data -e POSTGRES_USER=test -e POSTGRES_PASSWORD=Passw0rd -e POSTGRES_DB=testdb alpin3/postgres
```

### Todo
- [ ] Provide more examples

