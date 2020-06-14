Odoo Core Docker
================

These dockerfiles are for running its core only. You need to setup another
dependencies outside docker container:
* PostgreSQL
* Folder that will be mounted as filestore
* External repo that will be mounted as additional addons.

## How to run docker file for the first time
Below is some sample. In development, make sure PostgreSQL is running first.
```
# Run PostgreSQL docker, I use PostgreSQL using docker.
# Only for dev, not recommended in production.
# Expose port 5432 via 6553 in order to be accessible via pgadmin or any other
# PostgreSQL clients.
docker run --name postgres-container-tag \
    -p 6553:5432 -e POSTGRES_PASSWORD=123456 -d postgres:10

# Run Odoo Enterprise 13
docker run -d -v /absolute/path/to/enterprise:/mnt/enterprise \
    -v /absolute/path/to/odoo-filestore:/var/lib/odoo \
    -v /absolute/path/to/mnt/extra-addons:/mnt/extra-addons \
    -p 8069:8069 --name odoo-enterprise-13 --link postgres10:db -t odoo-enterprise-13

# Open your browser then access localhost:8069. Have fun!
```
