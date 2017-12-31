# Docker Image with InfluxDB and Grafana

This is a Docker image based on Phil Hawthorne who forked from Samuel Bistoletti.

Change log:
- Update INFLUXDB_VERSION to 1.4.2 (Note that as of version 1.3 there the UI on port 8083 is depreciated) 
- Update GRAFANA_VERSION to 4.6.2
- Update influxdb.conf with "max-row-limit = 0" (This is now the default as of version 1.3)

## Quick Start

To start the container with persistence you can use the following:

```sh
docker run -d \
  --name influxdb-grafana \
  -p 3003:3003 \
  -p 8086:8086 \
  -p 22022:22 \
  -v /path/for/influxdb:/var/lib/influxdb \
  -v /path/for/grafana:/data \
  pahowart/influxdb-grafana:latest
```

To stop the container launch:

```sh
docker stop docker-influxdb-grafana
```

To start the container again launch:

```sh
docker start docker-influxdb-grafana
```

## Mapped Ports

```
Host		Container		Service

3003		3003			grafana
8086		8086			influxdb
22022		22				sshd
```
## SSH

```sh
ssh root@localhost -p 22022
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
4. Choose `direct` as `access`
5. Fill remaining fields as follows and click on `Add` without altering other fields

Basic auth and credentials must be left unflagged. Proxy is not required.

Now you are ready to add your first dashboard and launch some queries on a database.

## InfluxDB

Username: root
Password: root
Port: 8086
```

### InfluxDB Shell (CLI)

1. Establish a ssh connection with the container
2. Launch `influx` to open InfluxDB Shell (CLI)
