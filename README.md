# FUSE Docker Images [![Docker pulls](https://img.shields.io/docker/pulls/subhrodip/jboss-fuse)](https://hub.docker.com/r/subhrodip/jboss-fuse)

This project builds a Docker image for [JBoss Fuse](https://developers.redhat.com/products/fuse/overview).


### Container Registries for finding this image

- [**DockerHub**](https://hub.docker.com/r/subhrodip/jboss-fuse) 🐬 `docker pull docker.io/subhrodip/jboss-fuse`
- [**GitHub Container Registry**](https://ghcr.io/ohbus/jboss-fuse) :octocat: `docker pull ghcr.io/ohbus/jboss-fuse`

#### Version Specific Dockerfiles can be found at their respective [branches](https://github.com/ohbus/jboss-fuse-docker/branches/all)

## Usage

You can then run a Fuse server with the following command:
```sh
docker run -it subhrodip/jboss-fuse bin/fuse
```
Note that the web console will not be accessible since we have not yet defined users that can log into it
and have not exposed the web console port on the docker host.



## Extending the image



First, create a **`users.properties`** file that contains your users, passwords, and roles.  For example:
```sh
admin=password,Operator, Maintainer, Deployer, Auditor, Administrator, SuperUser
dev=password,Operator, Maintainer, Deployer
```
Then create a Dockerfile with the following content:
```sh
FROM subhrodip/jboss-fuse
COPY users.properties /opt/jboss/jboss-fuse/etc/
```
Then you can build a new Docker image using the following commnad:
```sh
docker build --tag=subhrodip/jboss-fuse-custom .
```
Run your new image:
```sh
docker run -it -p 8181:8181 subhrodip/jboss-fuse-custom
```
The administration console should be available at [http://localhost:8181/hawtio](http://localhost:8181/hawtio)



## Ports Opened by Fuse

You may need to map ports opened by the Fuse container to host ports if you need to access it's services.
Those ports are:

* 8181 - Web access (also hosts the Fuse admin console).
* 8101 - SSH Karaf console access

If you add the `-p 8181:8181` to your `docker run` command, then you should be able to load [http://localhost:8181/hawtio](http://localhost:8181/hawtio) in your web browser to mange the Fuse server.

If you add the `-p 8101:8101` to your `docker run` command, then you should be able to ssh into the Karaf container using a command similar to: `ssh admin@localhost -p 8101`




## Ports used by JBoss AMQ

* 61616 - AMQ Openwire port.
* 1883  - AMQ MQTT port.
* 5672  - AMQ AMQP port.
* 61613 - AMQ STOMP port.
* 61617 - AMQ Openwire over SSL port.
* 8883  - AMQ MQTT over SSL port.
* 5671  - AMQ AMQP over SSL port.
* 61614 - AMQ STOMP over SSL port.

### Respective Enviornemt Variables for changing the port (after configuration change)
- `FUSE_PUBLIC_OPENWIRE_PORT` 61616
- `FUSE_PUBLIC_MQTT_PORT` 1883
- `FUSE_PUBLIC_AMQP_PORT` 5672
- `FUSE_PUBLIC_STOMP_PORT` 61613
- `FUSE_PUBLIC_OPENWIRE_SSL_PORT` 61617
- `FUSE_PUBLIC_MQTT_SSL_PORT` 8883
- `FUSE_PUBLIC_AMQP_SSL_PORT` 5671
- `FUSE_PUBLIC_STOMP_SSL_PORT` 61614



## Image internals

This image extends the [`jboss/base-jdk:8`](https://github.com/JBoss-Dockerfiles/base-jdk/tree/jdk8) image which adds the OpenJDK distribution on top of the [`jboss/base`](https://github.com/JBoss-Dockerfiles/base) image. Please refer to the README.md for selected images for more info.

The server is run as the `jboss` user which has the uid/gid set to `1000`.

Fuse is installed in the `/opt/jboss/jboss-fuse` directory.



## Source

The source is [available on GitHub](https://github.com/ohbus/jboss-fuse-docker).



## Issues

Please report any issues or file RFEs on [GitHub](https://github.com/ohbus/jboss-fuse-docker/issues).
