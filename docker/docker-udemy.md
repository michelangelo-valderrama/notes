# Aprende Docker, Compose y Swarm

## Comandos

### `docker container`
Maneja los contenedores.
```sh
$ docker container COMMAND
```
| command | description                      |
| ------- | -------------------------------- |
| `prune` | Elimina los contenedores parados |

### `docker exec`
Ejecuta un comando en un contenedor.
```sh
$ docker exec [OPTIONS] CONTAINER COMMAND
```
| option                | description                               |
| --------------------- | ----------------------------------------- |
| `--interactive`, `-i` | Mantiene el STDIN (standar input) abierto |
| `--tty`, `-t`         | Asigna una pseudo-TTY (pseudo terminal)   |

### `docker inspect`
Imprime información sobre un contendor
```sh
$ docker inspect [OPTIONS] NAME/ID
```
| options          | description                |
| ---------------- | -------------------------- |
| `--format`, `-f` | Imprime usando un template |

```sh
# Ejemplo --format
$ docker pull mariadb
$ docker inspect mariadb > info.json
$ cat info.json
[
  {
    "Id": ...,
    ...,
    "Config": {
      ...,
      "ExposedPorts": {
        "3306/tcp": {}
      }
    },
    ...
  }
]
$ docker inspect -f=='{{.Config.ExposedPorts}}' mariadb
map[3306/tcp:{}]
```

### `docker logs`
Imprime los registros de un contenedor.
```sh
$ docker logs [OPTIONS] CONTAINER
```

### `docker network`
Administra las redes
```sh
$ docker network COMMAND
```
| command      | description                            |
| ------------ | -------------------------------------- |
| `disconnect` | Desconecta un contenedor de una red    |
| `connect`    | Conecta un contenedor a una red        |
| `create`     | Crea una red                           |
| `inspect`    | Imprime información sobre de las redes |
| `ls`         | Lista las redes                        |

> Los contenedores de una red una misma red pueden conectarse entre sí, es decir, desde un contenedor se puede hacer un `ping` a otro, e.g. `ping 172.17.0.2`.

> Docker genera su propio DNS interno, es decir, desde un contenedor se puede hacer un `ping` a otro contenedor con solo poner su nombre, e.g. `ping mysql-container` en vez de `ping 172.17.0.2`.

### `docker port`
Imprime los mapeos de puertos de un contenedor
```sh
$ docker port CONTAINER
```

### `docker run`
Crea e inicializa un nuevo contenedor de una imagen.
```sh
$ docker run [OPTIONS] IMAGE
```
| option                | description                                       |
| --------------------- | ------------------------------------------------- |
| `--env`, `-e`         | Establece variables de entorno                    |
| `--env-file`          | Lee las variables de entorno desde un archivo     |
| `--detach`, `-d`      | Ejecuta en segundo plano e imprime ID             |
| `--interactive`, `-i` | Mantiene el STDIN (standar input) abierto         |
| `--name`              | Nombre de contenedor                              |
| `--network`           | Conecta un contenedor a una red                   |
| `--publish`, `-p`     | Conecta los puertos de un contenedor al anfitrión |
| `--publish-all`, `-P` | Conecta todos los puertos a uno aleatorio         |
| `--tty`, `-t`         | Asigna una pseudo-TTY (pseudo terminal)           |

