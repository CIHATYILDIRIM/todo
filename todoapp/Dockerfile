FROM node:lts-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install -g npm@9.3.1
RUN npm install -g @apidevtools/swagger-cli
COPY . ./
RUN npm install --save nuxt

EXPOSE 8080

CMD [ "npm", "run", "serve" ]