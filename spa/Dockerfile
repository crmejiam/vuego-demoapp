# This is a container for the frontend

# This is the image that we are going to use to create our image
FROM node:latest

# make the 'app' folder the current working directory
WORKDIR /app

# Establishing the endpoint of the frontend 
EXPOSE 80
RUN echo "VUE_APP_API_ENDPOINT=\"http://127.0.0.1:4001/api\"" > .env.production

# copy both 'package.json' and 'package-lock.json' (if available)
COPY package*.json ./

# install project dependencies
RUN npm install

# copy project files and folders to the current working directory (i.e. 'app' folder)
COPY . .

# build app for production with minification
RUN npm run build

# To install NGINX and execute the website on it
FROM nginx:latest
COPY --from=0 /app/dist .
COPY nginx.conf /etc/nginx/nginx.conf

