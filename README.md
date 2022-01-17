# Docker Camp

## Containers vs Virtual Machines
**Containers:**
- Low impact on OS, vary fast, minimal disk usage.
- Sharing, re-building and distribution is easy.
- Encapsulate apps/environment instead of "whole machine". Only necessary things included.

**VM:**
- Impact on OS, slower, higher disk space usage.
- Sharing, re-building and distribution can be challenging.
- Encapsulate "whole machine" instead of just apps/environment. Included additional extra things.

## Dockerfile
- `Dockerfile` is a blueprint for image, which describe how container should be setup.

## Commands
- `docker build .` - create an image based on Dockerfile.
- `docker run image_id` - run container based on image.
- `-p port_number:port_number` - flag that publish port number to a port number.
- `docker ps` - list of all running containers.
- `docker stop container_name` - to stop the container run.
