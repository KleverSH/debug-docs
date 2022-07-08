# Build environment
FROM node:16.13.2-alpine as build

WORKDIR /app

ENV PATH /app/node_modules/.bin:$PATH

COPY package*.json ./

RUN npm ci --silent
RUN npm install react-scripts@3.4.1 -g --silent

COPY . ./

RUN npm run build

COPY build/soar.css src/dist


# Prod environment
FROM nginx:stable-alpine

COPY --from=build /app/src /usr/share/nginx/html


COPY nginx/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
