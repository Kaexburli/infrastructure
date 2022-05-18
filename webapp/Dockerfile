FROM keymetrics/pm2:15-alpine as base

RUN apk update

#  add libraries needed to build canvas
RUN apk add --no-cache \
build-base \
g++ \
python \
;
RUN pm2 update
RUN apk add git

# Bundle APP files
RUN mkdir -p /home/app

WORKDIR /home/app

RUN git clone --branch main ___GIT_CLONE_REPLACE_URL_TOKEN___ .

WORKDIR /home/app
COPY ./src/.env .env

RUN npm install

WORKDIR /home/app/backend
RUN npm install

WORKDIR /home/app/frontend
RUN npm install
RUN npm run build

WORKDIR /home/app
EXPOSE 5000
EXPOSE 9000

CMD [ "pm2-runtime", "start", "ecosystem.config.js", "--env", "production", "--only", "prod-server, prod-client"]