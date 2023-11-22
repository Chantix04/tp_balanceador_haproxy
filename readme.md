## Tp2 -- Balanceador de Carga con HAPROXY

1)- Creamos una segunda carpeta para mi segunda web, esta contrenda index.php
1.5)- Creamos la red con este comando docker network create mynetwork
2)- Creamos dos contenedores php con este comando:
	docker run -d --name web1 --network mynetwork -p 8081:80 -v C:\Users\gstnr\Desktop\php\aplicacion-php:/var/www/html php:apache-bullseye ---> posicionarse en la carpeta aplicacion-php
	docker run -d --name web2 --network mynetwork -p 8082:80 -v C:\Users\gstnr\Desktop\php\aplicacion-php2:/var/www/html php:apache-bullseye ---> posicionarse en la carpeta aplicacion-php2
3)-Ahora creamos un contenedor mysql con este comando:
	docker run -d --name mysql --network mynetwork -e MYSQL_ROOT_PASSWORD=root1 -v C:\Users\gstnr\Desktop\php\aplicacion-php:/docker-entrypoint-initdb.d -v C:\Users\gstnr\Desktop\php\base_de_datos:/var/lib/mysql mysql:debian --> posicionarse en carpeta global
4)- Creamos el contenedor de mi haproxy con este comando: 
	docker run -d --name haproxy-container --network mynetwork -p 8085:80 -v C:\Users\gstnr\Desktop\php/balanceador/haproxy.cfg:/usr/local/etc/haproxy/haproxy.cfg haproxy:latest  ----> posicionarse en carpeta goblal
5)- Instalo las dependencias en los contenedores web1 y web2:
    docker exec -it web1 bash
    docker exec -it web2 bash
    apt-get update
    docker-php-ext-install mysqli
    docker-php-ext-enable mysqli


Verificar IP de mysql para cambiar en los archivos.php asi poder tener la conexion completa
