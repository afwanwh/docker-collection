Wordpress Docker Development Setup
==================================

This docker-compose file contains 3 images:
* Wordpress
* phpmyadmin
* MySQL

## How to run docker-compose file for the first time
Inside folder wordpress run below commands

```
mkdir working-dir
docker-compose up -d
```

## How to tear down
```
docker-compose down --volumes
```
