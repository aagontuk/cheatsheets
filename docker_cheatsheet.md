* See available images

```
docker images
```

* Running a continer

```
docker run IMAGE_NAME
```

* Running a container with tty

```
docker run -it IMAGE_NAME
```

* See all the containers and their status.
Without `-a` only shows the running container. 

```
docker ps -a
```

* Stoping a container

```
docker stop CONTAINER_ID
```

* Restarting a container

```
docker restart CONTAINER_ID
```

* Attaching a tty with stopped container

```
docker restart CONTAINER_ID
docker attach CONTAINER_ID
```

* Removing a container instance

```
docker rm CONTAINER_ID
```

* Create a new image from a container change

```
docker commit CONTAINER_ID IMAGE_NAME
```
