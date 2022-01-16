FROM node:16.13.2-alpine as build
ARG SERVER_IP
RUN if [[ -z "$SERVER_IP" ]] ; then echo Argument not provided ; else echo Argument is $SERVER_IP ; fi

WORKDIR /app

COPY package*.json ./
RUN npm install --only=prod
COPY . .

RUN sed -i "s/localhost/$SERVER_IP/g" $(find src/ -iname '*api.js')
RUN npm run build

FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html
COPY nginx-default.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
