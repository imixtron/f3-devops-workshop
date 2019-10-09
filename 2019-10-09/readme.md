# Docker commands
Create Docker Image 
```
$ docker create --name <name> -it <image>:<tag> <command>
$ docker create --name ubuntu -it ubuntu:16.04 bash
```

List all processes
```
$ docker ps -a
```

Start Docker container that was created "fc4290c9ace2" is the,tag from the ps command
```
$ docker start <container_id>
$ docker start fc4290c9ace2
```

Attach to the running process of the container can be executed if the container is running
```
$ docker attach <container_id>
$ docker attach fc4290c9ace2
```

Executes Create and Start together, runs the command if -it is provided
```
$ docker run --name ubnutu1 -d ubuntu:16.04 bash
```

## Port
Lets use nginx image `nginx:alpine` that exposes port `80`. Lets say we need to map that port with `6080` 
```
$ docker run -d -p <host_port>:<container_port> nginx:alpine
$ docker run -d -p 6080:80 nginx:alpine
```

let give it a try by running `http://localhost:6080`

## Volumes
Volumes are used to persist data to a storage, volume could be a local directory in your pc or from a hosted service such as aws ebs/DO block storage. To mount a volume we will need to add `-v` flag

> `pwd` command prints working directory, hence `$(pwd)` is replaced with the current directory

```
$ docker run -d -p 6080:80 -v <host_directory>:<container_directory> nginx:alpine
$ docker run -d -p 6080:80 -v $(pwd):/usr/share/nginx/html/ nginx:alpine
```
> If the directory does not exists on container, it is created

Navigate to `http://localhost:6080/html/` to view the contents of `.\html\`

# Executing Dockerfile
We can add all these parameters in a Dockerfile so the effort is reduced while running the command. And it can be used to create our custom repositories, explore Dockerfile for further details

```
$ docker build -t <image>:<tag> .
$ docker build -t ssi-pg:alpha-1 .
```

Run the created image
```
docker run -it -d -p 6080:80 -v $(pwd):/usr/share/nginx/html/ ssi-pg:alpha-1 
```

# Refrences
https://blog.sourcerer.io/a-crash-course-on-docker-learn-to-swim-with-the-big-fish-6ff25e8958b0