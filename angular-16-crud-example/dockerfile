# phase 1: Build Angular app
FROM node:16-alpine as build
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build --prod


# phase 2: Use Nginx to serve the build
FROM nginx:1-alpine-slim

# Update Vulnerable Packages
RUN apk add --no-cache -l openssl 

COPY --from=build /app/dist/angular-16-crud /usr/share/nginx/html
EXPOSE 80