# Docker Camp

## Containers vs Virtual Machines
>**Containers:**
- Low impact on OS, vary fast, minimal disk usage.
- Sharing, re-building and distribution is easy.
- Encapsulate apps/environment instead of "whole machine". Only necessary things included.

>**VM:**
- Impact on OS, slower, higher disk space usage.
- Sharing, re-building and distribution can be challenging.
- Encapsulate "whole machine" instead of just apps/environment. Included additional extra things.

## Dockerfile
`Dockerfile` is a list of instruction for building image, which describe how container should be setup.
- Every instruction in Dockerfile represent layer. Layer based architecture. More on that in Image section.

>**Syntax:**
- `FROM` - on top of what technology (based image) we would like to build our image. Without this line you will receive an error.

- `COPY` - list of files which should go to the image (code base).
  - `COPY . .` - first dot is all files around Dockerfile. Second dot - where this files should be stored.

  - `COPY . /app` - put all code from the root on local machine into container folder named __app__.
- `RUN` - specify which command should be run inside the container, when image is build. `RUN npm install` e.g..
- `CMD` - this line will be executed when container is running. `CMD ["node", "server.js"]` e.g.. Without this line CMD of based image will be executed. This line should be ALWAYS the last line in the dockerfile.
- `EXPOSE` - let docker know what port shout be expose from container to local system. Doesn't do anything. Only for documentation purposes.
- `WORKDIR` - by default all commands run in the container's root folder. WORKDIR allows to specify folder for running commands.

## Images & Containers
>**Containers:**
- Running "unit of software".
- Run and execute the code.
- Basically the final layer of the Image, that runs code.
- Every new container build from the same Image do not copy the code, environment, etc. from that Image. Docker just add another layer above.

>**Images:**
- Blueprint for container.
- Contains the code + requirements tools (environment) to run that code.
- Based on one image, we can create multiple containers.
- Images locked when you build them. App code it's a snapshot which copied into. So Images are Read-Only!
- Every command in Image represent layers and this layers are cached.
- When Image rebuilds, Docker re-run only the parts that were changed. Non-changeable things are pulling from cache.

## Commands
- `--help` - add this to any command to figure out available options.
- `docker build .` - create an image based on Dockerfile. dot is using for path, where is the dockerfile lives.
- `docker run image_id` - create a NEW container based on image.
  - `-it` - gives ability to interact with soft inside container (node shell e.g.).
  - `-p local_port_number:container_port_number` - flag that publish to local port number from a container port number.
- `docker ps` - list of all running containers
- `docker ps -a` :
  - `ps` stands for processes.
  - `-a` mean show all.
  - `docker start container_name` - restart the existed container.
- `docker stop container_name` - to stop the container run.
