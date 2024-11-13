Development
===========

Best is to use the devcontainer in the parent folder. Then run new docker builds like:

__For inside the dev container__

```shell
docker build --build-arg BUILD_ARCH=amd64 --build-arg BUILD_FROM="homeassistant/amd64-base:latest" -t local/test-addon:011 . 
```

__Limitations__

We need different production settings in plexripper to work properly.

__To Do:__

* optimize container build
* Fix ingress
* extend configs
    * adjust paths
* add security layer if on host network
* fix ingress port/urls in the app is not on network, by ingress
* fix communication with supervisor (for ingress path, port etc.)
* allow to select a version of plexripper


