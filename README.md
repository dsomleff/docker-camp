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

>**Syntax:**
- `FROM` - on top of what technology (based image) we would like to build our image. Without this line you will receive an error.

- `COPY` - list of files which should go to the image (code base).
  - `COPY . .` - first dot is all files around Dockerfile. Second dot - where this files should be stored.

  - `COPY . /app` - put all code from the root on local machine into container folder named __app__.
- `RUN` - specify which command should be run inside the container, when image is build. fe `RUN npm install`.
- `CMD` - this line will be executed when container is running. fe `CMD ["node", "server.js"]`. Without this line CMD of based image will be executed. This line should be ALWAYS the last line in the dockerfile.
- `EXPOSE` - let docker know what port shout be expose from container to local system.
- `WORKDIR` - by default all commands run in the container's root folder. WORKDIR allows to specify folder for running commands.

## Images & Containers
>**Containers:**
- Running "unit of software".
- Run and execute the code.

>**Images:**
- Blueprint for container.
- Contains the code + requirements tools.
- Based on one image, we can create multiple containers.

## Commands
- `docker build .` - create an image based on Dockerfile.
- `docker run image_id` - run container based on image.
  - `-it` - gives ability to interact with soft inside container (node shell fe).
  - `-p port_number:port_number` - flag that publish port number to a port number.
- `docker ps` or `docker ps -a` - list of all running containers. `ps` stands for processes and `-a` mean show all.
- `docker stop container_name` - to stop the container run.
