-- Versión de Node
docker version

--Ver Lista de Imagenes
docker images

-- Instalar Node  Versión Release / Estable
docker pull node 

-- Instalar Node Versión 18
docker pull node:18

-- Instalar Node Versión 16
docker pull node:16 

-- Docker Hub Repository
https://hub.docker.com/

-- Instalar Mysql 
docker pull --platform  linux/x86_64  mysql

-- Eliminar imagenes
docker image rm node:16

-- Crear Contenedor
docker create mongo
docker container create mongo

-- Id del contenedor creado
ec711d8b77f030735d25f166af586e305fa236743d21818894f08cba7c3dc2e6

--Iniciar Contenedor
docker start ec711d8b77f030735d25f166af586e305fa236743d21818894f08cba7c3dc2e6

--  Listar Contenedores  Activos o Ejecutandose
docker ps

-- Listar todos los Contenedores Apagados o Prendidos
docker ps -a

-- Detener Contenedor
docker stop ec711d8b77f0( id de la lista de contenedores creados )

-- Eliminar Contenedor por el nombre por defecto
docker rm ec711d8b77f0

-- Crear contenedor con nombre
docker create --name monguito mongo

-- Iniciar Contenedor con Nombre
docker start monguito

-- Crear Contenedor con Puerto Publico
docker create -p27017:27017 name=monguito mongo

-- Ver logs del contenedor
docker logs monguito
docker logs --follow monguito

-- Crear contenedor  + imagen + start
/*-p 27017:27017: Mapea el puerto 27017 del contenedor al puerto 27017 del host. Este es el puerto predeterminado de MongoDB donde escucha las conexiones de clientes.
-d: Ejecuta el contenedor en segundo plano (modo detached).
*/

docker run --name monguito -p27017:27017 -d  mongo

--Crear un contenedor con variables de entorno
docker  create -p27017:27017 --name=monguito -e MONGO_INITDB_ROOT_USERNAME=nico -e MONGO_INITDB_ROOT_PASSWORD=password mongo

-- Listar Redes Docker
docker network ls

-- Crear Red Docker
docker network create mired

-- Eliminar red docker
docker network rm mired

-- Crear IMagen
// el 1 es un Tag de identificación que puede ser la versión
docker build -t miapp:1  .

-- Crear contenedor dentro de una red 
 -- mongo DB
docker create -p27017:27017 --name monguito --network mired -e MONGO_INITDB_ROOT_USERNAME=nico -e MONGO_INITDB_ROOT_PASSWORD=password mongo

-- app node js
docker create -p3000:3000 --name chanchito --network mired miapp:1

-- Crear contenedor en base a docker-compose
docker compose up

-- Eliminar imagen y contenedores creados en base a docker compose
docker compose down

-- Ejecutar  docker compose personalizado
docker compose -f docker-compose-dev.yml  up / down

-- Eliminar Contenedor en base a docker-compose
docker rm nombre_contenedor

-- Ejecutar Composer
docker-compose exec php composer install

-- Ejecutar Migraciones y Seed 
docker-compose exec php php artisan migrate:refresh --seed
