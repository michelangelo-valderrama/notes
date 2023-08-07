# Aprendiendo Git

working directory -[`$ git add`]-> staging area -[`$ git commit`]-> repository

## Trabajando con Git de forma local

```sh
# Muestra o establece las opciones globales o de repositorio
$ git config NAME
# init.defaultBranch
```

```sh
# Crea un REPOSITORIO o reinicia uno
$ git init [DIRECTORY] [OPTIONS]
# --initial-branch=BRANCH_NAME
```

```sh
# Muestra el estado del ÁRBOL DE TRABAJO
$ git status [OPTIONS]
# -s --short
```

```sh
$ git add [OPTIONS] [NAME]
# -A --all
```

```sh
# Crea un nuevo COMMIT
$ git commit [OPTIONS]
# -m --message MESSAGE
# -a --all -> Prepara 
```

```sh
# Restaura los archivos del ÁRBOL DE TRABAJO
$ git restore NAME
```

```sh
# Restaurar del staging area
$ git reset NAME
```

```sh
# Limpia los archivos no rastreados
$ git clean OPTIONS
# -n --dry-run -> Muestra el resultado sin aplicarlo
# -f --force
# -d -> Borrar directorios
# -i --interactive -> Pregunta antes de borrar cualquier archivo
```