# FROM node:alpine means take the base image from alpine(small linux distro) with node
FROM node:alpine

# start from the app dir
WORKDIR /app

# Copy all the files in my current folder on my drive into the /app directory in the image
COPY . /app

# port 3000 to be accessible for inbound traffic from outside the container
EXPOSE 3000

# The command line to run when starting the container is node server. In other words, Start Node with the server.js file."
CMD ["node", "server"]
