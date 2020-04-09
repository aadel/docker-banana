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


#### 2. Start Banana

Create config.json that contains Solr connection url and authentication settings:

```
{
    "serverPort": 9901,
    "solrUrl": "http://solr:8983",
    "basicAuth": false,
    "username": "",
    "password": "",
    "couchbaseUrl": "http://couchbase:8092"
}
```

```sh
$ docker run -d --name banana -p 9901:9901 -v /path/to/config.json:/opt/banana/config.json aaadel/banana
```

#### 3. Check running containers ID

```sh
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS               NAMES
7c2542dc21b3        solr                "docker-entrypoint.s…"   4 seconds ago        Up 4 seconds                            solr
d41a73f4325a        aaadel/banana       "docker-entrypoint.s…"   About a minute ago   Up About a minute                       banana

```

#### 4. Open Banana Dashboard in a Browser

```
http://localhost:9901/#/dashboard
```

The default dashboard should be rendered inside the browser window
