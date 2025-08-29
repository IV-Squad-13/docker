FROM node:18 AS build
ARG CLIENT_PATH
WORKDIR /app
COPY ${CLIENT_PATH}/package*.json ./
RUN npm install
COPY ${CLIENT_PATH} ./
RUN npm run build

FROM nginx:stable-alpine
ARG CLIENT_PATH
RUN rm /etc/nginx/conf.d/default.conf
COPY ${CLIENT_PATH}/nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist /usr/share/nginx/html
RUN chmod -R 755 /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]