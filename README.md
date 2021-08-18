# Hazelcast and Fuse on Docker

Test repo for 2 node hazelcast cluser and standalone Red Hat Fuse 7

## Usage

After clone, start with:

```
docker-compose up
```

Default login for Fuse:

* Host: http://localhost:8181
* User: `admin1`
* Pass: `admin12`

Hazelcast Prometheus metrics accessible at 

* Node 1: http://localhost:8080/metrics
* Node 2: http://localhost:8081/metrics

## Credits

Original fuse solution forked from https://github.com/ohbus/jboss-fuse-docker