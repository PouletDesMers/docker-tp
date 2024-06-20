# docker-tp



docker run --name mariadb-container -e MYSQL_ROOT_PASSWORD=rootpassword -e MYSQL_DATABASE=mydatabase -e MYSQL_USER=user -e MYSQL_PASSWORD=password -v /path/to/your/init_db.sql:/docker-entrypoint-initdb.d/init_db.sql -v mariadb-data:/var/lib/mysql -d mariadb:11

FROM python:3.9

WORKDIR /app

COPY requirements.txt ./

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]

