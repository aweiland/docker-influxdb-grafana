# Docker Image with InfluxDB and Grafana

This is a Docker image based on Phil Hawthorne.

Change log:
- Update INFLUXDB_VERSION to 1.6.1 (Note that as of version 1.3 the UI on port 8083 is removed)
- Update influxdb.conf with "max-row-limit = 0" (This is now the default as of version 1.3)
- Update GRAFANA_VERSION to 5.2.2
- Commented out SSH components which should not be used. From host terminal use: docker exec -it "containerID" bash

## Quick Start

To start the container with persistence you can use the following:

```sh
docker run -d \
  --name influxdb-grafana \
  -p 3003:3003 \
  -p 8086:8086 \
  -v /path/for/influxdb:/var/lib/influxdb \
  -v /path/for/grafana:/var/lib/grafana \
  -v /path/for/grafana/plugins:/var/lib/grafana/plugins \
  -v /path/for/grafana/provisioning:/var/lib/grafana/provisioning \
  -v /path/for/grafana/logs:/var/log/grafana \
  pahowart/docker-influxdb-grafana:latest \
```

To stop the container launch:

```sh
docker stop influxdb-grafana
```

To start the container again launch:

```sh
docker start influxdb-grafana
```

## Mapped Ports
. 
```
Host		Container		Service

3003		3003			grafana
8086		8086			influxdb
```
Password: root

## Grafana

Open <http://localhost:3003>

```
Username: root
Password: root
```

### Add data source on Grafana

1. Using the wizard click on `Add data source`
2. Choose a `name` for the source and flag it as `Default`
3. Choose `InfluxDB` as `type`
4. Choose `proxy` as `access` (Note "proxy" means grafana backend will pull data from influx. "direct" means browser will connect directly to influx)
5. Fill remaining fields as follows and click on `Add` without altering other fields

Basic auth and credentials must be left unflagged. Proxy is not required.

Now you are ready to add your first dashboard and launch some queries on a database.

## InfluxDB

Username: root
Password: root
Port: 8086
```

### InfluxDB Shell (CLI)

1. From the docker host open a terminal and enter --> docker exec -it "containerID" bash
2. Launch `influx` to open InfluxDB Shell (CLI)

Sample CLI commands
Create a new database:

CREATE DATABASE <dbname>

Show list of databases:

SHOW DATABASES

Use a database:

USE <dbname>
