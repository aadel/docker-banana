# docker-banana

This is a Docker image for Banana.

## What is Banana?

The [Banana](https://github.com/lucidworks/banana) project was forked from Kibana, and works with all kinds of time series (and non-time series) data stored in Apache Solr. It uses Kibana's powerful dashboard configuration capabilities, ports key panels to work with Solr, and provides significant additional capabilities, including new panels that leverage D3.js.

Learn more about Banana on the [Banana project](https://github.com/lucidworks/banana).

## How to use this Docker image

### Banana example

#### 1. Start Solr

Run Solr Container.

See [https://hub.docker.com/_/solr](https://hub.docker.com/_/solr).

Note: add `--network="host"` to the `run` command in order to get Solr and Banana containers communication to work if they run on the same Docker host.

#### 2. Start Banana

```sh
$ docker run -d --name banana -p 9901:9901 aaadel/banana:1.6.26
```

#### 3. Check running containers ID

```sh
$ docker ps
CONTAINER ID        IMAGE                  COMMAND                  CREATED              STATUS              PORTS                    NAMES
6a9d64418686        aaadel/banana:1.6.26   "docker-entrypoint.s…"   About a minute ago   Up About a minute   0.0.0.0:9901->9901/tcp   banana
7c2542dc21b3        solr                   "docker-entrypoint.s…"   7 minutes ago        Up 7 minutes                                 solr

```

#### 4. Open Banana Dashboard in a Browser

```
http://localhost:9901/#/dashboard
```

The default dashboard should be rendered inside the browser window
