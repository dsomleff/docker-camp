# on top of what technology (based image) we would like to build our image. Without this line you will receive an error.
FROM node

# specify folder inside of the container for running commands.
# you can use . (dot symbol) instead of /app
WORKDIR /app

# helps to rerun npm install every time when we change the code and build the image.
COPY package.json /app

# specify which command should be run inside the container, when image is build.
RUN npm install

# list of files which should go to the image (code base).
# you can use . (dot symbol) instead of /app
COPY . /app

# let docker know what port shout be expose from container to local system.
# only for documentation purposes.
# to expose the port use docker run -p 3000:80 e.g.
EXPOSE 80

# this line will be executed when container is running.
# you can put any command that you will to execute every time when container runs.
CMD ["node", "server.js"]
