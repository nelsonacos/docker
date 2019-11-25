# Docker

Para instalar **docker** en linux:

[get.docker.com](https://get.docker.com)

## Comandos Docker Básicos

```bash
docker --help
```

```bash
docker [COMMAND] --help
```

```bash
docker version
```

```bash
docker info
```

```bash
docker run hello-world
```

**Nota:** este es el comando para arrancar contenedores en docker. Para arrancar un contenedor en **docker** es necesario tener creada una **imagen** como no hemos creado la imagen, el comando intenta descargar la imagen desde el repositorio de imagenes de docker:

 [hub.docker.com](https://hub.docker.com)

como existe una imagen hello-world en el repositorio de docker, la descargara y arrancara el contenedor.

Para buscar imagenes en el repositorio de imagenes de docker:

```bash
docker search [image_name]
```

Para ver las imagenes disponibles en local:

```bash
docker images
```

Para descargar una imagen del repositorio de imagenes de docker:

```bash
docker pull [image_name]
```

Para descargar una version especifica de una imagen:

```bash
docker pull [image_name:tag]
```

Para eliminar una imagen:

```bash
docker rmi [image_name]
```

Para arrancar un contenedor docker de manera interactiva:

```bash
docker run -it [image_name]
```

Para arrancar un contenedor y asignarle un nombre:

```bash
docker run --name [container_name] [image_name]
```

Para listar los contenedores:

```bash
docker ps -a
```

Para listar los contenedores en ejecucion:

```bash
docker ps
```

Para listar contenedores aplicando filtros:

```bash
docker ps -a --filter="exited=0"
```

Para detener un contenedor en ejecucion:

```bash
docker stop [container_id]
```

Para arrancar un contenedor que esta detenido:

```bash
docker start [container_id]
```

Para conectarnos a un contenedor:

```bash
docker attach [container_id]
```

Salir del contenedor sin detenerlo:

```bash
CTRL + P + Q
```

Para vincularnos a un contenedor:

```bash
docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
```

Para ver los logs de un contenedor:

```bash
docker logs -f [container_name]
```

Para detener de manera forzada un contenedor:

```bash
docker kill [container_name]
```

Para pausar un contenedor:

```bash
docker pause [container_name]
```

Para reanudar un contenedor:

```bash
docker unpause [container_name]
```

Para reiniciar un contenedor:

```bash
docker restart [container_name]
```

Para inspeccionar un contenedor:

```bash
docker inspect [container_name]
```

Para eliminar un contenedor:

```bash
docker rm [container_name]
```

## Constuir imagenes docker

Construir a partir de un contenedor:

```bash
docker commit [container_name] [image_name]
```

```bash
docker diff [container_name]
```

Construir a partir de un fichero **Dockerfile:**

``` Dockerfile
FROM node:12
  WORKDIR /usr/src/[app_name]
  COPY package*.json ./
  RUN npm install
  COPY . .
  EXPOSE 3000
  CMD [ "npm", "start" ]
```

fichero **.dockerignore**

```.dockerfile
node_modules
  *.log
  docker-compose.yml
  Dockerfile
  data
```

Para construir la imagen:

```bash
docker build -t [image_name] .
```

Lanzar el contenedor:

```bash
docker run -it -p 3000:3000 [image_name]
```

Lanzar el contenedor como servicio:

```bash
docker run -it -p 3000:3000 -d [image_name]
```

## Gestionar Volumenes

Para crear un volumen:

```bash
docker volume create [volume_name]
```

Para listar los volumenes existentes:

```bash
docker volume ls
```

```bash
docker volume inspect [volume_name]
```

Para eliminar un volumen:

```bash
docker volume rm [volume_name]
```

Para eliminar todos los volumenes no usados:

```bash
docker volume prune
```

Para compartir un volumen con un contenedor:

```bash
docker run -v [volume_name]:[mount_path] [image_name] [COMMAND]
```

Para compartir un volumen anonimo:

```bash
docker run -v [absolut_path]:[mount_path] [image_name] [COMMAND]
```

## Gestionar redes

Para crear una red:

```bash
docker network create [net_name]
```
Para connectarse a una red:

```bash
docker network connect [net_name] [container_name]
```

Para listar las redes:

```bash
docker network ls
```
Para eliminar una red:

```bash
docker network rm [net_name]
```

Para desconectarse de una red:

```bash
docker network disconnect
```

Para inspeccionar una red:

```bash
docker network inspect [net_name]
```

Para vincular dos contenedores por nombre :

```bash
docker run -it --link [container_name] [image_name] [COMMAND]
```

Para  lanzar un contenedor y que el contenedor use una interface de red especifica:

```bash
docker run -it --name [container_name] --net=[net_name] [image_name] [COMMAND]
```
