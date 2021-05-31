FROM node:latest

WORKDIR /app

COPY ./src ./
COPY package*.json ./
RUN npm install
EXPOSE 80

CMD [ "npm", "start"]

# Some other commands
#COPY package*.json ./
#RUN npm install