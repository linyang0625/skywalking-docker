# Apache SkyWalking OAP Server Docker Files

<img src="http://skywalking.apache.org/assets/logo.svg" alt="Sky Walking logo" height="90px" align="right" />

**SkyWalking**: an APM(application performance monitor) system, especially designed for 
microservices, cloud native and container-based (Docker, Kubernetes, Mesos) architectures.

# Notice

This image can only connect to Elasticsearch **7** when setting `SW_STORAGE`=`elasticsearch`.

# How to use this image

## Start a `standlone` container with `H2` storage

```
$ docker run --name oap --restart always -d apache/skywalking-oap-server:7.0.0-es7
```

## Start a `standlone` container with `elasticsearch` storage whose address is `elasticsearch:9200`

```
$ docker run --name oap --restart always -d -e SW_STORAGE=elasticsearch -e SW_STORAGE_ES_CLUSTER_NODES=elasticsearch:9200 apache/skywalking-oap-server:7.0.0-es7
```

# Configuration

We could set up environment variables to configure this image. They are defined in [backend-setup](https://github.com/apache/skywalking/blob/v7.0.0/docs/en/setup/backend/backend-setup.md). The whole default value of those configruation items is stored in dist [application.yml](https://github.com/apache/skywalking/blob/v7.0.0/dist-material/application.yml) 

# Extend image

If you intend to override or add config files in `/skywalking/config`, `/skywalking/ext-config` is the location for you to put extra files.
The files with the same name will be overridden, otherwise, they will be added in `/skywalking/config`.

If you want to add more libs/jars into the classpath of OAP, for example, new metrics for OAL. These jars can be mounted into `/skywalking/ext-libs`, then
`entrypoint` bash will append them into the classpath. Notice, you can't override an existing jar in classpath.

# License
[Apache 2.0 License.](/LICENSE)
