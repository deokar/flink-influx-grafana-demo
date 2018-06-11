# flink-influx-grafana-demo

# Deploy Influx DB
https://hub.docker.com/_/influxdb/

Using this Image

Running the container

The InfluxDB image exposes a shared volume under /var/lib/influxdb, so you can mount a host directory to that point to access persisted container data. A typical invocation of the container might be:

$ docker run -p 8086:8086 \
      -v $PWD:/var/lib/influxdb \
      influxdb
Modify $PWD to the directory where you want to store data associated with the InfluxDB container.

You can also have Docker control the volume mountpoint by using a named volume.

$ docker run -p 8086:8086 \
      -v influxdb:/var/lib/influxdb \
      influxdb
Exposed Ports
The following ports are important and are used by InfluxDB.

8086 HTTP API port
8083 Administrator interface port, if it is enabled
2003 Graphite support, if it is enabled
The HTTP API port will be automatically exposed when using docker run -P.

The administrator interface is not automatically exposed when using docker run -P and is disabled by default. The adminstrator interface requires that the web browser have access to InfluxDB on the same port in the container as from the web browser. Since -P exposes the HTTP port to the host on a random port, the administrator interface is not compatible with this setting.

The administrator interface is deprecated as of 1.1.0 and will be removed in 1.3.0.


# Grafana Docker

http://docs.grafana.org/installation/docker/#grafana-container-with-persistent-storage-recommended


create a persistent volume for your data in /var/lib/grafana (database and plugins)
docker volume create grafana-storage

start grafana

docker run \
  -d \
  -p 3000:3000 \
  --name=grafana \
  -v grafana-storage:/var/lib/grafana \
  grafana/grafana
