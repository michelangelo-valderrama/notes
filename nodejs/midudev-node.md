# Midudev Curso NodeJS

## Clase 1

`globalThis` referencia al valor de **objeto global**. En caso de estar en un navegador, este objeto es `window`, pero en **nodejs** es `global`.
```js
console.log(globalThis === global) // true
```

Todos los objetos, variables y funciones globales de javascript son propiedades y métodos de `globalThis`.
```js
globalThis.console.log(globalThis.console)
```

---

