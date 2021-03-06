# Prometheus Mysql Exporter

* Installs prometheus [mysql exporter](https://github.com/prometheus/mysqld_exporter)

## TL;DR;

```console
$ helm install stable/prometheus-mysql-exporter
```

## Introduction

This chart bootstraps a prometheus [mysql exporter](http://github.com/prometheus/mysql_exporter) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager. The exporter can connect to mysql directly or using the [Cloud SQL Proxy](https://cloud.google.com/sql/docs/mysql/sql-proxy).

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install --name my-release stable/prometheus-mysql-exporter --set datasource="username:password@(db:3306)/"
```

The command deploys a mysql exporter on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the mysql exporter chart and their default values.

|        Parameter                         |                                                          Description                                                 |                 Default                 |
| ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| `replicaCount`                           | Amount of pods for the deployment                                                                                    | `1`                                     |
| `image.repository`                       | Image repository                                                                                                     | `prom/mysqld-exporter`                  |
| `image.tag`                              | Image tag                                                                                                            | `v0.11.0`                               |
| `image.pullPolicy`                       | Image pull policy                                                                                                    | `IfNotPresent`                          |
| `service.name`                           | Service name                                                                                                         | `mysql-exporter`                        |
| `service.type`                           | Service type                                                                                                         | `ClusterIP`                             |
| `service.externalport`                   | The service port                                                                                                     | `9104`                                  |
| `service.internalPort`                   | The target port of the container                                                                                     | `9104`                                  |
| `resources`                              | CPU/Memory resource requests/limits                                                                                  | `{}`                                    |
| `annotations`                            | pod annotations for easier discovery                                                                                 | `see values.yaml`                       |
| `mysql.db`                               | MySQL connection db (optional)                                                                                       | `""`                                    |
| `mysql.host`                             | MySQL connection host                                                                                                | `localhost`                             |
| `mysql.param`                            | MySQL connection parameters (optional)                                                                               | `"tcp"`                                 |
| `mysql.pass`                             | MySQL connection password                                                                                            | `password`                              |
| `mysql.port`                             | MySQL connection port                                                                                                | `3306`                                  |
| `mysql.protocol`                         | MySQL connection protocol (optional)                                                                                 | `""`                                    |  
| `mysql.user`                             | MySQL connection username                                                                                            | `exporter`                              |
| `cloudsqlproxy.enabled`                  | Flag to enable the connection using Cloud SQL Proxy                                                                  | `false`                                 |
| `cloudsqlproxy.image.repo`               | Cloud SQL Proxy image repository                                                                                     | `gcr.io/cloudsql-docker/gce-proxy`      |
| `cloudsqlproxy.image.tag`                | Cloud SQL Proxy image tag                                                                                            | `1.11`                                  |
| `cloudsqlproxy.image.pullPolicy`         | Cloud SQL Proxy image pull policy                                                                                    | `IfNotPresent`                          |
| `cloudsqlproxy.instanceConnectionName`   | Google Cloud instance connection name                                                                                | `project:us-central1:dbname`            |
| `cloudsqlproxy.port`                     | Cloud SQL Proxy listening port                                                                                       | `3306`                                  |
| `cloudsqlproxy.credentials`              | Cloud SQL Proxy service account credentials                                                                          | `bogus credential file`                 |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install --name my-release \
  --set mysql.user="username",mysql.password="password",mysql.host="localhost",mysql.port="3306"  \
    stable/prometheus-mysql-exporter
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml stable/prometheus-mysql-exporter
```

Documentation for the MySQL Exporter can be found here: (https://github.com/prometheus/mysqld_exporter)
A mysql params overview can be found here: (https://github.com/go-sql-driver/mysql#dsn-data-source-name)
