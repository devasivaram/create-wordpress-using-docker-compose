# create-wordpress-using-docker-compose

## Description

Let's create another wordpress using docker compose tool, here we use docker volume, Mysql and WordPress image and docker compose tool. Let's move on to the process.

![image](https://user-images.githubusercontent.com/100773863/162557648-0aa8095f-9002-4cdd-a865-5ce6dad00ec8.png)


## Installation

If you need to download docker to the EC2 instance and to add docker-compose tool, then follow this:

~~~sh
sudo yum install docker -y
sudo systemctl restart docker.service
sudo systemctl enable docker.service
sudo systemctl status docker.service
sudo usermod -a -G docker ec2-user
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
~~~

Please exit from the instance and login back to reflect the above changes

## Procedure

> Create one directory

~~~sh
mkdir compose_test
cd compose_test
~~~

## Create yml file for compose

~~~sh
vim docker-compose.yml
~~~
> Add this to yml file

~~~
version: "3"
    
services:

  database:
    image: mysql:5.6
    container_name: databasecompose
    networks:
      - wpnet
    volumes:
      - mysql-data:/var/lib/mysql/
    environment:
      - MYSQL_ROOT_PASSWORD=mysqlroot@123
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wpuser
      - MYSQL_PASSWORD=wpuser@123
    
  wordpress:
    image: wordpress:latest
    container_name: wordpresscompose
    networks:
      - wpnet
    volumes:
      - wp-data:/var/www/html/
    environment:
      - WORDPRESS_DB_HOST=database
      - WORDPRESS_DB_USER=wpuser
      - WORDPRESS_DB_PASSWORD=wpuser@123
      - WORDPRESS_DB_NAME=wordpress
    ports:
      - "80:80"

networks:
  wpnet:

volumes:
  mysql-data:
  wp-data: 
~~~

## Check the syntax

~~~sh
docker-compose config
~~~

>It should exactly result the code added in yml file

> ![image](https://user-images.githubusercontent.com/100773863/162557844-34ee9a65-9622-4bc0-a009-41f817fb1f64.png)

## Now start the docker-compose

~~~sh
docker-compose up -d
dokcer-compose ps
~~~

**Result:**
> ![image](https://user-images.githubusercontent.com/100773863/162558072-e2a1e102-d5bc-48d4-88e4-6426476b0451.png)



**Now, access the domain using the EC2 IP or EC2 hostname and set up the site:**
> ![image](https://user-images.githubusercontent.com/100773863/162557184-82a618d3-422b-4122-9eff-3a60327da29b.png)




## Conclusion
This is how we create wordpress site using docker-compose tool. Please contact me when you encounter any difficulty error while using this terrform code. Thank you and have a great day!


### ⚙️ Connect with Me
<p align="center">
<a href="https://www.instagram.com/dev_anand__/"><img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white"/></a>
<a href="https://www.linkedin.com/in/dev-anand-477898201/"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/></a>










