# CloudRouter (w/ Quagga) Docker Container

CloudRouter container with [Quagga](http://www.nongnu.org/quagga/).

### Pull pre-built image
```
docker pull cloudrouter/quagga-fedora
```

## Building
```sh
docker build --tag=cloudrouter/quagga-fedora .
```

### Run

#### Create configuration directory on host
```
export QUAGGA_CONFIG=$(pwd)/quagga-config
mkdir -p ${QUAGGA_CONFIG}
```

#### Run `bgpd` and `zebra`
```
docker run \
  --detach \
  --volume ${QUAGGA_CONFIG}:/etc/quagga \
  --publish 179:179 \
  --publish 2605:2605 \
  cloudrouter/quagga-fedora
```

#### Connect to the container
```
telnet localhost 2605
```

#### Stopping the container
To stop, identify the container id, then stop it.

```
$ docker ps
CONTAINER ID        IMAGE                COMMAND                CREATED             STATUS              PORTS                                          NAMES
a0c599f711e0        cloudrouter/quagga-fedora:latest   "/usr/bin/supervisor   8 seconds ago       Up 7 seconds        0.0.0.0:179->179/tcp, 0.0.0.0:2605->2605/tcp   backstabbing_tesla
$ docker stop a0c599f711e0
```

## Volumes
The following volumes can be mounted from the host.

| Volume  | Description |
| :------------ | :------------ |
| /etc/quagga | Quagga configuration files. |

## Ports
| Port  | Description |
| :------------ | :------------ |
| **179** | BGP/tcp port |
| **2605** | Telnet port |
