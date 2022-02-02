FROM node

WORKDIR /app

COPY package.json /app

RUN npm install

COPY . /app

EXPOSE 80

# specify path to folders (inside container) that should be mapped to some folder outside of container.
# you can add multiple paths.
# that syntax is for Anonymous Volumes.
VOLUME [ "/app/folder-name" ]

CMD ["node", "server.js"]
