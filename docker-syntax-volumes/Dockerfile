FROM node

WORKDIR /app

COPY package.json /app

RUN npm install

COPY . /app

# example of using ARG
ARG DEFAULT_PORT = 80

# example of using ENV
ENV PORT $DEFAULT_PORT

EXPOSE $PORT

# specify path to folders (inside container) that should be mapped to some folder outside of container.
# you can add multiple paths.
# that syntax is for Anonymous Volumes.
# we can use this type of volumes to complement Bind Mounts technique and store some folders,
# like node_modules e.g. to have it inside container but not in our local machine.
VOLUME [ "/app/folder-name" ]

CMD ["node", "server.js"]
