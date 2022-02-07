# Docker Camp

## Table of Contents
1. [Containers vs Virtual Machines](#cvsvm)
2. [Dockerfile](#dockerfile)
3. [Images & Containers](#iac)
4. [Volumes](#volumes)
5. [Bind Mounts](#bind)
6. [ARGuments and ENVironment Variables](#arg-env)
7. [Cross Container Communication](#ccc)
8. [Commands](#commands)
   - [Images](#comim)
   - [Containers](#comcon)
   - [Volumes](#comvol)

## <a name="cvsvm"></a>Containers vs Virtual Machines
>**Containers:**
- Low impact on OS, vary fast, minimal disk usage.
- Sharing, re-building and distribution is easy.
- Encapsulate apps/environment instead of "whole machine". Only necessary things included.

>**VM:**
- Impact on OS, slower, higher disk space usage.
- Sharing, re-building and distribution can be challenging.
- Encapsulate "whole machine" instead of just apps/environment. Included additional extra things.

## <a name="dockerfile"></a> Dockerfile
`Dockerfile` is a list of instruction for building image, which describe how container should be setup.
- Every instruction in Dockerfile represent layer. Layer based architecture. More on that in [Images & Containers](#iac) section.

>**Syntax:**
- `FROM` - on top of what technology (based image) we would like to build our image. Without this line you will receive an error.

- `COPY` - list of files which should go to the image (code base).
  - `COPY . .` - first dot is all files around Dockerfile. Second dot - where this files should be stored.

  - `COPY . /app` - put all code from the root on local machine into container folder named __app__.
- `RUN` - specify which command should be run inside the container, when image is build. `RUN npm install` e.g..
- `CMD` - this line will be executed when container is running. `CMD ["node", "server.js"]` e.g.. Without this line CMD of based image will be executed. This line should be ALWAYS the last line in the dockerfile.
- `EXPOSE` - let docker know what port shout be expose from container to local system. Doesn't do anything. Only for documentation purposes.
- `WORKDIR` - by default all commands run in the container's root folder. WORKDIR allows to specify folder for running commands.

## <a name="iac"></a>Images & Containers
>**Containers:**
- Running "unit of software".
- Run and execute the code.
- Basically the final layer of the Image, that runs code.
- Every new container build from the same Image do not copy the code, environment, etc. from that Image. Docker just add another layer above.
- Docker allow us to copy files in/out Container.
- Containers have a Read-write mode.

><a name="images"></a>**Images:**
- Blueprint for container.
- Contains the code + requirements tools (environment) to run that code.
- Based on one image, we can create multiple containers.
- Images locked when you build them. App code it's a snapshot which copied into. So Images are Read-Only!
- Every command in Image represent layers and this layers are cached.
- When Image rebuilds, Docker re-run only the parts that were changed. Non-changeable things are pulling from cache.

## <a name="volumes"></a>Volumes
*Allow to store data in containers WITHOUT knowing where data stores.*
- Volumes are folders on your local machine, which are made available into containers. It works in both direction: local -> container and container -> local. If container will be removed, volume (data inside volume) survives.
- Volume could be anonymous or named. In both cases Docker set up a folder on your local/host machine; exact location is unknown. The only way to find this - use `docker volume` commands.
- Anonymous volume (including your local folder) will be always deleted after container was removed.
- Named volume (including your local folder) will be survive after container was removed.
- Named volume is great for data which should be persistent and don't need to edit or view directly, because we don't have access to it.
- Anonymous Volume removed only when you start / run a container with the `--rm` option. If you start a container without that option, the anonymous volume would NOT be removed, even if you remove the container.
- Volumes works in read/write mode, but by using specific syntax, we can make them read only.

## <a name="bind"></a>Bind Mounts
*Allow to store data in containers WITH knowing where data stores*.
- Developer by himself setup the path/folder for storing data on local/host machine.
- Bind Mounts great for editable (by you) data (source code).
- Bind Mount set up not inside Dockerfile, but in the container run command body.
- Docker should have access to folder on your machine, which you like to share. In Docker app -> Preference -> Recourses -> File Sharing.
- We can tell Docker to set up some folders inside the container (node_modules e.g.) and use this folder with code on local machine. It can be achieved with Anonymous Volumes + Bind Mounts combination. We can specify required folder in Dockerfile with VOLUME directive or do it manually when we run the container.

## <a name="arg-env"></a>ARGuments and ENVironment Variables
Docker support build-time Arguments and runtime Environments variables.
>ARGS
- Available ONLY inside Docker
- Set on `docker build` via `--build-arg`

>ENV
- Available inside Docker AND application code
- Set via Dockerfile or `--env` on `docker run` or `.env` file
- Inside Dockerfile we use `ENV` directive

## <a name="ccc"></a>Cross Container Communication
- We can use CCC to sent requests to 3rd party API, which is not the par of our Container
- We can communicate with another Container
- It's a good practice to have multiple Containers for scenario when yoy got app code (1t Container) and DB (2d Container).

## <a name="commands"></a>Commands
>### <a name="comim"></a>Images
- `--help` - add this to any command to figure out available options.
- `docker build .` - create an image based on Dockerfile. dot is using for path, where is the dockerfile lives.
  - `-t` - name and tag your image in a name:tag format.

- `docker images` - list of all images.
- `docker rmi image_id` - delete image and all layers inside it. You can't remove image that using by container. So you need remove container first.
  - `docker image prune` - remove all images with default tag.
  - `docker image prune -a` - remove ALL images.


- `docker tag old_image_name:old_tag(optional) new_image_name:new_tag(optional)` - rename Image.

>### <a name="comcon"></a>Containers
- `docker run image_id` - create a NEW container based on image. Container running in a foreground (Attached mode). No exit after command execution. Instead of image_id we can specify image_name:tag.
  - `-d` - flag to run container in a Detached mode.
  - `-it` - gives ability to interact with soft inside container (node shell e.g.). `i` means interactive mode and `t` means terminal related.
  - `-p local_port_number:container_port_number` - flag that publish to local port number from a container port number.
  - `--rm` - will delete running container when it stops.
  - `--name your_container_name` - give a running container a name.


- `docker ps` - list of all running containers
- `docker ps -a` :
  - `ps` stands for processes.
  - `-a` mean show all.


- `docker start container_name` - restart the existed container. Container running in a background (Detached mode). Exit after command execution.
  - `-a` -  flag to run container in a Attached mode.
- `docker stop container_name` - to stop the container run.
- `docker attach container_name||container_id` - Makes Attached mode on for a container that was started in a Detached mode.
- `docker logs container-name` - fetches the logs that were printed by container.
- `docker rm container_name` - remove container. Works only for stopped containers. You can remove a couple containers at once.
  - `docker container prune` - remove all stopped containers at once.

>### <a name="comvol"></a>Volumes
- `-v your_volume_name:/folder_name_inside_container/folder_path` - specified a named volume
- `docker volume rm VOL_NAME` - remove specific volume
- `docker volume prune` - remove all volumes


- `--env-file ./.env` - to run environment variables from .env file.
