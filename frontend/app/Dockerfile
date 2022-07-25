FROM node:12.10-slim as builder
RUN apt-get update || : && apt-get install python build-essential -y
WORKDIR '/build'
COPY app ./app
COPY resources ./resources
COPY third_party ./third_party

WORKDIR '/build/app'

RUN npm install
RUN npm rebuild node-sass
RUN npm run build

RUN ls /build/app/dist

FROM nginx
EXPOSE 80
COPY --from=builder /build/app/dist /usr/share/nginx/html


