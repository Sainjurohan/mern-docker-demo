# Use Node.js 18.9.1 as the base image
FROM node:18.9.1

# setting the working directory
WORKDIR /app

#copying thepackage.json file and install dependencies
COPY package.json .

RUN npm install

#copying all the other files
COPY . .

# Exposing the port for the backend

EXPOSE 5050

CMD ["npm", "start"]

