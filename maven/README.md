#### Start a Maven build container
**NOTE**: Mount user maven repository into container  
**NOTE**: Mount current directory into container "workspace"  

```bash
docker run -it --rm --name maven \
  --volume ~/.m2/repository:/m2repository \
  --volume ${PWD}:/workspace \
  andahme/build-step:maven
```

