# docker-tp


# MariaDB
docker run --name mariadb-container -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=mydatabase -e MYSQL_USER=user -e MYSQL_PASSWORD=password -v /path/to/your/init_db.sql:/docker-entrypoint-initdb.d/init_db.sql -v mariadb-data:/var/lib/mysql -d mariadb:11

# Flask
FROM python:3.8
WORKDIR /app
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]


# Lancer le conteneur
docker build -t flask-app "chemin"

docker run --name flask-container --link mariadb-container:mariadb -e DATABASE_URL=mysql://user:password@mariadb:3306/mydatabase -p 5000:5000 -d flask-app



# image
FROM node:16 as build-stage
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install
COPY . .
RUN yarn build
FROM nginx:alpine as production-stage
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build-stage /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]




# conteneur Vue.js
docker build -t vue-app /path/to/your/frontend
docker run --name vue-container -p 80:80 -d vue-app


# Pousse les images pour docker Hub
docker tag flask-app <dockerhub-username>/flask-app:latest
docker tag vue-app <dockerhub-username>/vue-app:latest
docker tag mariadb:11 <dockerhub-username>/mariadb:latest

## connection docker hub
docker login
