Odoo Development Docker
=======================

## Concept
In Odoo development, a developers sometimes needs debugging from source codes.
The only source codes that should care are Odoo core itself, additional addons,
and Enterprise source code if you are working with enterprise environment.

> Driven by purpose above, this dockerfile is created with mounted source codes style
> instead of copying source code to docker image. That's why this docker image is called `dev-mount`.

## What you need to do?
### Prepare your source codes and data_dir
In order to run this docker image in a container, you must prepare following folders
- Odoo source code, let's say the name is `/folder/to/odoo`
- [Optional] Your development folder, let's say the folder name is `/folder/to/extra-addons`
- Config file folder that contains `odoo.conf` file. We could take `/folder/to/config` as a name.
- If you run enterprise, you need to define Odoo Enteprise source code folder. Put `/folder/to/enterprise` as a name
- The last one is data_dir folder where Odoo stores file-based information. Give it name `/folder/to/data_dir`

### Configuration File
As mentioned above, config file `odoo.conf` should contain text below.

- For Community Edition
```
[options]
addons_path = /opt/odoo-dir/odoo/addons,/opt/odoo-dir/extra-addons
data_dir = /opt/odoo-dir/data-dir
db_host = db
db_port = 5432
db_user = odoo
db_password = 123456
```
- For Enterprise Edition
```
[options]
addons_path = /opt/odoo-dir/enterprise,/opt/odoo-dir/odoo/addons,/opt/odoo-dir/extra-addons
data_dir = /opt/odoo-dir/data-dir
db_host = db
db_port = 5432
db_user = odoo
db_password = 123456
```

### PostgreSQL
For development purpose, I choose to run PostgreSQL using docker image. Here what I do.
```
docker run --name postgres-container-tag \
    -p 5432:5432 -e POSTGRES_PASSWORD=123456 -d postgres:12
```
After you run PostgreSQL container, connect to PostgreSQL instance using pgAdmin and create
user `odoo` and give it password `12345`. You can choose another name and password but you
must change the value of parameter `db_user` and `db_password` in `odoo.conf`.

### Run Odoo
- Community Edition
```
docker run -d -v /folder/to/odoo:/opt/odoo-dir/odoo \
    -v /folder/to/data_dir:/opt/odoo-dir/data-dir \
    -v /folder/to/extra-addons:/opt/odoo-dir/extra-addons \
    -v /folder/to/config:/opt/odoo-dir/config \
    -p 8069:8069 --name odoo18-ce-dev --link postgres17:db -t afwanwh/odoo18-dev-community:latest
```
