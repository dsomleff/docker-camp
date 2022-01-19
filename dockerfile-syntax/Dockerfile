# on top of what technology (based image) we would like to build our image. Without this line you will receive an error.
FROM node

# specify folder inside of the container for running commands.
WORKDIR /app

# list of files which should go to the image (code base).
COPY . /app

# specify which command should be run inside the container, when image is build.
RUN npm install

# let docker know what port shout be expose from container to local system.
# only for documentation purposes.
# to expose the port use docker run -p 3000:80 e.g.
EXPOSE 80

# this line will be executed when container is running.
CMD ["node", "server.js"]
