**Tags:** [[Cloud]] [[Sysadmin]]
Images
------------
Images are instructions for what containers should do. `docker pull IMAGE` downloads the docker image `IMAGE`. When specifying a tag (a variation, or different version of an image), you must include a colon `:` between the image name and tag, for example, `ubuntu:22.04` (image:tag). To delete an image, `docker image rm IMAGE_ID`. 

Commands
------------------
When using the `run` command, specifying the `-it` options allow us to interact with the container directly, and then `/usr/bin/bash` in the `[COMMAND]` area to run a shell inside of the container. `-d` option will run the container in the background (detached mode). `-v` mounts a file or directory from the host OS to the container at the specified location (when mounting a file, the location can't end with a directory name but end with the name of the file that will be mounted). `docker run -p 80:80 webserver` binds a port from the host OS to an exposed port in the container, generally used if you are running an application like a web server for example. The `--rm` argument tells docker to delete the container once it has finished executing what it has been instructed to do. `--name` argument is used to give a name to the container, usually the same as the application running on it. `docker build -t NAME .` builds the image and gives it the `NAME` you provided, and the `.` tells docker to look into the working directory for the dockerfile to build from. `docker network create NET_NAME` creates a 'network' that allows the containers who are members of it to interact with each other. `--net` argument for the `run` command specifies which network we want to run the container as a member of. Howver, this can be automated easier using compose (see the docker compose section below).

Dockerfiles
------------------
Dockerfiles are text files that serve as a set of instructions that determine what the container should do and how the docker image should be assembled.
The syntax is `INSTRUCTION argument`.

| Command   | Description                                                                           |
| --------- | ------------------------------------------------------------------------------------- |
| `COPY`    | copies files from the host system to the working directory of the container           |
| `FROM`    | sets the base image and build stage, all dockerfiles start with this                  |
| `RUN`     | executes commands within the container                                                |
| `WORKDIR` | sets the working directory of the container                                           |
| `CMD`     | determines what command runs when the container is started                            |
| `EXPOSE`  | tells the person running the container what port they should publish on (`-p` option) |

`RUN` can take chained commands separated by `&&`. This is done to optimise and reduce the build time, since each `RUN` instruction is its own layer which takes a lot more time.

Docker compose
---------------------------
In summary, docker compose allows multiple containers to interact with each while running separately in isolation (eg. a server container interacting with a database container).
The syntax is `docker-compose COMMAND`.

| Command | Description                                                                     |
| ------- | ------------------------------------------------------------------------------- |
| `up`    | (re)creates and builds then starts the containers specified in the compose file |
| `start` | starts already built containers specified in the compose file                   |
| `down`  | stops and **deletes** the containers specified in the compose file              |
| `stop`  | stops **without deleting** the containers specified in the compose file         |
| `build` | builds without starting the containers specified in the compose file            |

##### docker-compose.yml

This type of file (*.yml*) needs to be formatted with indentation, best-practice is consistent double spaces. `name` contains `build`, `ports`, `volumes`, `networks`, `image`, and `environment`, all on the same level. `services` contains one or multiple `name` on the same level. `version` and `services` are on the same level.

| Instruction   | Description                                                                           |
| ------------- | ------------------------------------------------------------------------------------- |
| `version`     | written at the top of a file and specifies which version of compose the file is using |
| `services`    | marks the beginning of the containers to be managed                                   |
| `name`        | the name of the container for which we will define a configuration                    |
| `build`       | defines the directory containing the dockerfile we will use to build this container   |
| `ports`       | publishes ports to the exposed ports                                                  |
| `volumes`     | specifies the directories that should be mounted into the container from the host     |
| `environment` | passes environment variables                                                          |
| `image`       | defines the image the container should be built with                                  |
| `networks`    | defines what networks the containers will be a part of                                |

