### Project of WordPress with MySQL DB
 
### Project structure:
```
.
├── README.md
├── docker-compose.yaml
```

### Create a directory for the project:
```
$ mkdir docker-compose-wordpress-mysql
$ cd docker-compose-wordpress-mysql
```

### Create a docker-compose.yml file in your project directory and paste the following code in:
```
version: '3'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "80:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
       WORDPRESS_DB_NAME: wordpress
volumes:
    db_data: 
```
In this example, WordPress is using the default port 80.

### Build and run your app with Compose

From your project directory, start up your application by running docker compose up
```
$ ubuntu@ip-172-31-21-183:~/docker-compose-wordpress-mysql$ docker-compose up -d
Creating network "docker-compose-wordpress-mysql_default" with the default driver
Creating volume "docker-compose-wordpress-mysql_db_data" with default driver
Pulling db (mysql:5.7)...
5.7: Pulling from library/mysql
e83e8f2e82cc: Pull complete
0f23deb01b84: Pull complete
f5bda3b184ea: Pull complete
ed17edbc6604: Pull complete
33a94a6acfa7: Pull complete
f153bd2953e4: Pull complete
ab532edfb813: Pull complete
c76bdfe4f3d0: Pull complete
8a7ffe2f2551: Pull complete
857ada4fbbcc: Pull complete
b7c508404c3c: Pull complete
Digest: sha256:f57eef421000aaf8332a91ab0b6c96b3c83ed2a981c29e6528b21ce10197cd16
Status: Downloaded newer image for mysql:5.7
Pulling wordpress (wordpress:latest)...
latest: Pulling from library/wordpress
9e3ea8720c6d: Pull complete
07353b772b5e: Pull complete
5908153120ba: Pull complete
8681ad2eeea6: Pull complete
92711ce78973: Pull complete
bf1c5be6427e: Pull complete
1d02a81768ed: Pull complete
d674a0135f85: Pull complete
6d87d0359817: Pull complete
5e8c2df9b69e: Pull complete
aacfb138e3c1: Pull complete
2db2528ade33: Pull complete
beeef66f0c04: Pull complete
f06b38c16403: Pull complete
a2c661d6acd5: Pull complete
e4ac8d746152: Pull complete
f264881ab77b: Pull complete
0436c0c6e94a: Pull complete
328897f635d0: Pull complete
b2ea761ddb4a: Pull complete
3d15d55761e9: Pull complete
Digest: sha256:f3b8d54fe9b80e88255121a46933ca1961fb9f3f39e6981a668cdb7f019a5bbd
Status: Downloaded newer image for wordpress:latest
Creating docker-compose-wordpress-mysql_db_1 ... done
Creating docker-compose-wordpress-mysql_wordpress_1 ... done
ubuntu@ip-172-31-21-183:~/docker-compose-wordpress-mysql$
```
Compose pulls a MySQL image, builds an image for your code, and starts the services you defined.

Enter http://localhost/ in a browser to see the application running.

If this doesn’t resolve, you can also try http://127.0.0.1:8000.

You should see this view in your browser:

+ ![image](https://github.com/fjblsouza/flask-redis/assets/110574485/ae8e08cb-c2e7-42ba-ab3c-72966f1fea76)

Listing images at this point should return wordpress and mysql.
```
ubuntu@ip-172-31-21-183:~/docker-compose-wordpress-mysql$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
wordpress    latest    b8ee07adfa91   5 days ago    616MB
mysql        5.7       dd6675b5cfea   4 weeks ago   569MB
ubuntu@ip-172-31-21-183:~/docker-compose-wordpress-mysql$
```
### Stop and remove the containers
```
$ docker compose down 
```
