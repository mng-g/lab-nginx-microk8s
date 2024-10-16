FROM node:lts-slim
WORKDIR /app
COPY package*.json /app
RUN npm install
COPY . /app
EXPOSE 7777
CMD ["npm","run", "start"]