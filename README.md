Kalaxia Docker
==============

This repository is meant to run the Kalaxia game API and Front app.

Requirements
------------

* Docker 17.06.0+
* Docker Compose 1.14.0+

Setup
-------

After cloning the project, you have to copy the file containing the environment variables:

```
cp kalaxia.dist.env kalaxia.env
```

You can modify the values if you want, but there is no need to, the default values work perfectly.

Now you can build and run the containers by running the following commands:

```
docker-compose up -d
```

To access the server, update your ``/etc/hosts`` file and set the following line:

```
127.0.0.1 local.kalaxia.com
```

The IP address must be the one of your Docker Machine **if you are using Windows**.

Usage
------

To connect the server to the portal, you must get the ``kalaxia_nginx`` container IP address.

To do so, just type ``docker inspect kalaxia_nginx`` and get the IPV4Address field value.

You also have to get the API public key in order to bind the portal and the server together.

When the API server is started, it creates the keys under ``./volumes/rsa_vault``.

Fetch the content of ``public.pub`` and use it in the portal server configuration.

To get the API logs, you can simply do ``docker logs kalaxia_api``. Use the ``-f`` flag to get logs in real-time when using the API.

PostgreSQL
----------

To connect to the PGSL database, you can go inside the container and then connect to the database:

```
docker exec -it kalaxia_postgresql /bin/bash
psql --username=${POSTGRES_USER} -d ${POSTGRES_DB} -W
```

You will be prompted a password, you can type the one present in ```kalaxia.env``` file or type the environment variable ```${POSTGRES_PASSWORD}```
