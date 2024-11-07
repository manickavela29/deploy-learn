
## Template of docker cmd

```bash
# Building the docker image 
docker build -t username/image-name:tag directory

# Building the docker container
docker run username/image-name:tag

# Opening the bash terminal interactively
docker run -it username/image-name:tag bash
```

### CMDs for demo

```bash
docker build -t manix29/hello-world:v1 .
docker run manix29/hello-world
docker run -it manix29/hello-world bash
```

## Pushing to registry
docker push manix29/hello-world