# This is a container for the frontend

# This is the image that we are going to use to create our image
FROM node:latest

# make the 'app' folder the current working directory
WORKDIR /usr/src/app

# copy both 'package.json' and 'package-lock.json' (if available)
COPY package*.json ./

# copy project files and folders to the current working directory (i.e. 'app' folder)
COPY . .

# Establishing the endpoint of the frontend
RUN echo "VUE_APP_API_ENDPOINT=\"http://127.0.0.1:4001/api\"" > .env.production

# install project dependencies
RUN npm install
RUN npm install -g @vue/cli

# build app for production with minification
RUN npm run build

# To install NGINX and execute the website on it
FROM nginx:latest
COPY --from=0 usr/src/app/dist /usr/share/nginx/html

# Exposing 80 port for incoming requests
EXPOSE 80
