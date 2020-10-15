FROM node:12.19.0-alpine3.10

WORKDIR /usr/src/app

COPY ./express/package*.json /usr/src/app/

RUN npm install

COPY ./express /usr/src/app/

USER node

EXPOSE 3000
CMD [ "npm", "start" ]