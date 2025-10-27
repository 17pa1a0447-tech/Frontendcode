# Stage 1 - build
FROM node:18 AS build
WORKDIR /app

# copy package files and install
COPY package*.json ./
RUN npm ci

# copy rest of the source and build
COPY . .
# build for production (output to dist/angular-mean-crud-tutorial)
RUN npm run build -- --configuration=production

# Stage 2 - nginx runtime
FROM nginx:stable

# remove default html
RUN rm -rf /usr/share/nginx/html/*

# copy built app
COPY --from=build /app/dist/angular-mean-crud-tutorial /usr/share/nginx/html

# copy custom nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
