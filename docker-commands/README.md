# Docker Commands Blueprints

```
docker build - t image-name:image-tag .
```
- `docker build` - create an image
- `- t image-name:image-tag` - like "feedback:volumes" e.g.
- `.` - image will be build based on Dockerfile

</br>

```
docker run -d -p 3000:80 --rm --name container-name -v volume_name:/workdir/shared_folder -v "/path/to/your/project/folder:/workdir" image-name:image-tag
```
- `docker run ` - create a container
- `-d` - in detached mode
- `-p 3000:80` - run it on port 80
- `--rm` - remove after container will stop
- `--name container-name` - name container like "feedback-app" e.g.
- `-v volume_name:/workdir/shared_folder` - add named volume like "feedback:/app/feedback" e.g.
- `-v "/path/to/your/project/folder:/workdir"` - build mounts to allow Docker watch the code changes. If path contains special characters or whitespace use quotes ("").
- `image-name:image-tag` - specify based on what image container will be build, like "feedback:volumes" e.g.
