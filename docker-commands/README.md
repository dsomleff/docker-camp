# Docker Commands Blueprints

```
docker build - t feedback:volumes .
```
- `docker build` - create an image
- `- t feedback: volumes` - with the name "feedback" and tag "volumes"
- `.` - image will be build based on Dockerfile

</br>

```
docker run -d -p 3000:80 --rm --name feedback-app -v feedback:/app/feedback feedback:volumes
```
- `docker run ` - create a container
- `-d` - in detached mode
- `-p 3000:80` - run it on port 80
- `--rm` - remove after container will stop
- `--name feedback-app` - name container like "feedback-app"
- `-v feedback:/app/feedback` - add named volume like "feedback:/app/feedback"
- `feedback:volumes` - specify based on what image container will be build "feedback:volumes"
