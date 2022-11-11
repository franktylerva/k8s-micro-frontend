FROM node:lts-alpine3.16

WORKDIR /usr/src/app
COPY package.json ./
RUN yarn install
COPY ./src ./src
COPY ./public ./public
ENV PUBLIC_URL=/feature-a
RUN yarn build

FROM alpine

COPY --from=0 /usr/src/app/build /feature-b