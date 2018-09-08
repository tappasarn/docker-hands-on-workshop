FROM node:alpine

WORKDIR /app

COPY package.json /app
RUN npm install

COPY . /app

EXPOSE 3000

# create volume location inside the container
VOLUME ["/app/public"]

CMD ["node", "server"]
