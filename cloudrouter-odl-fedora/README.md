# CloudRouter (w/ OpenDaylight) Docker Container
CloudRouter container with [OpenDaylight](http://www.opendaylight.org/).

## Building
```
docker build --tag=cloudrouter/odl-fedora .
```
## Running
Note that the following assumes that you to already have `cloudrouter/base-fedora` built or available.

To run in interactive mode (default):
```
./cr-odl-run.sh
```
To run in detached mode:
```
./cr-odl-run.sh -d
```
Note that these scripts map the ports used by OpenDaylight 1:1. For more advanced use cases, including specifying your own port mapping, use commands such as:
```
docker run -i cloudrouter/odl-fedora
docker run -d cloudrouter/odl-fedora
```
## Stopping
```
# Stop container
docker stop ${CONTAINER_ID}
```
