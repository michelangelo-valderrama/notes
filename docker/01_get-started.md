# Get Started

## Part 1: Overview

### What is a container?
**Contenedor:** Proceso aislado en una máquina independiente de los demás procesos de la máquina anfitriona. Además, aprovechan los recusos de su máquina anfitriona.

Los contenedores:
- son instancias ejecutables de una **imagen.**
- pueden correr ejecutarse en máquinas locales, virtuales o en la nube.
- son portables (multiplataforma).
- están aislados de otros contenedores y tienen sus propias aplicaciones, configuraciones, etc.

### What is a container image?
**Imagen:** Archivo que provee toda la información necesaria para crear y configurar contenedores. La imagen contiene información de todos los binarios, depencias, varibles de entorno, comandos... para crear contenedores específicos.

## Part 2: Containerize an application

### Build the app's container image
**Dockerfile:** Archivo de texto que contiene un script de instrucciones. Docker usa el `Dockerfile` para construir una imagen.

Ejemplo de `Dockerfile`:
```Dockerfile
# syntax=docker/dockerfile:1

# INSTRUCCIÓN argumentos
FROM node:18-alpine # "Imagen padre"
WORKDIR /app # Directorio de trabajo para las intrucciones del "Dockerfile"
COPY . . # Copia los archivos de la ruta "." y los pega en la ruta "." del contenedor
RUN yarn install --production # Comando a ejecutar después de descargar la "Imagen padre"
CMD ["node", "src/index.js"] # Comando por defecto a ejecutar al iniciar el contenedor
EXPOSE 3000
```

Comando para construir una nueva imagen:
```sh
$ docker build -t getting-started .
# docker build [OPTIONS] PATH
# t- getting-tarted --> --tag STRING
# Nombre por el que referirse a la imagen
```

### Start an app container

Comando para crear e iniciar un nuevo contenedor:
```sh
$ docker run -dp 127.0.0.1:3000:3000 getting-started
# docker run [OPTIONS] IMAGE
# -d --> --detach Inicia el contenedor en segundo plano e imprime su ID
# -p localhost:3000:3000 --> --publish HOST:CONTAINER Crea una asignación de puertos entre el anfitrión y el contenedor
$ echo "http://localhost:3000"
```

Comando para ver los contenedores:
```sh
$ docker ps
```

## Part 3: Update the application

### Update the source code
Para actulizar la aplicación, se hace lo mismo de antes:
```sh
$ docker build -t getting-started .
$ docker run -dp 127.0.0.1:3000:3000 getting-started
# [error]:
docker: Error response from daemon: driver failed programming external connectivity on endpoint great_moore (2dab70db1e6b5a5a32f9a5c3c5722e83071378b1602c03c9588c3bd969300816): Bind for 127.0.0.1:3000 failed: port is already allocated.
# Un puerto solo puede escuchar un proceso, luego hay que eliminar el viejo contenedor
```

### Remove the old container

Primero hay que parar el contenedor:
```sh
$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                      NAMES
d4974bdad1c1   55844aab3598   "docker-entrypoint.s…"   22 minutes ago   Up 22 minutes   127.0.0.1:3000->3000/tcp   happy_blackburn

$ docker stop d4974bdad1c1
# docker stop CONTAINER-ID
```

Después, ya se puede eliminar:
```sh
$ docker rm d4974bdad1c1
# docker rm CONTAINER-ID

$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

```

También se puede eliminar un contenedor sin pararlo primero, para ello hay que *forzarlo*:
```sh
$ docker rm -f d4974bdad1c1
# docker rm -f DOCKER-ID
# -f --> --force
```

## Part 4: Share the application

### Push the image

Comando para logearse a Docker Hub:
```sh
$ docker login -u michelangelovalderrama
# docker login [OPTIONS] [flags]
# -u michelangelovalderrama --> --username STRING
```

Comando para darle un nuevo nombre a una imagen:
```sh
$ docker tag getting-started michelangelovalderrama/getting-started
# docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

Comando para hacer un `push` a Docker Hub:
```sh
$ docker push michelangelovalderrama/getting-started
# docker push NAME:[TAG]
```

## Part 5: Persist the DB

