# The Rust Programming Language

## 0. Commands
### `cargo`
```zsh
$ cargo COMMAND
```
| command  | description                       |
| -------- | --------------------------------- |
| `new`    | Crea un nuevo proyecto            |
| `build`  | Compila el proyecto               |
| `run`    | Compila y ejecuta el proyecto     |
| `check`  | Compila pero sin crear el binario |
| `update` | Actualiza los crates del proyecto |

### `cargo new`
Crea un proyecto de Cargo
```zsh
$ cargo new [OPTIONS] <path>
```
| option  | description                               |
| ------- | ----------------------------------------- |
| `--vsc` | Seleccina el Version System Control (VSC) |

### `cargo build`
Compila el proyecto en `target/debug`
```zsh
$ cargo build [OPTIONS]
```
| option            | description                            |
| ----------------- | -------------------------------------- |
| `-r`, `--release` | Compila y optimiza en `target/release` |

## 1. Getting Started

### 1.2. Hello, World!

```rs
// hello-world.rs
fn main() {
  println!("Hello, world!");
}
```

```zsh
$ rustc hello-world.rs 
Hello, world!
```

### 1.3. Hello, Cargo!
**Cargo** es el **build system** de rust y su **package manager**
> A las dependencias de Rust se les llaman `crates`

```sh
$ cargo new hello-cargo
$ cd hello-cargo
$ cargo run
Hello, world!
```

Estructura de trabajo de Cargo:
```zsh
- Cargo.lock
- Cargo.toml
o src/
  - main.rs
o target/
  o debug/
    - binary
```

**Cargo.toml** es el archivo de configuración de Cargo, que usa el formato *TOML* (Tom's Obvious, Minimal Language)

## 2. Programming a Guessing Game

```rs
// guessing_game.rs
use std::io; // (1)

fn main() {
    println!("Guess the number!"); // (2)

    println!("Please input your guess.");

    let mut guess = String::new(); // (3)

    io::stdin() // (4)
        .read_line(&mut guess) // (5)
        .expect("Failed to read line"); // (6)

    println!("You guessed: {guess}"); // (7)
}
```

1. `use std::io` importa el módulo `io` de la librería estandar (**standard library**). Por defecto, Rust importa una lista de funcionalidades básicas en todos los programas de Rust (como el `println` o el `use`), a este conjunto se les llama preludio (**prelude**).
2. `println!` es un **macro** que imprime textos en pantalla.
3. `let` declara un variable y `mut` indica que esta es **mutable**. `String` es un tipo de Rust. La sintaxis `::` indica que los próximo será una función asociada al tipo `String`. `new` es una función asociada que retorna una nueva instancia del tipo `String`.
4. `io::stdin` es una función del módulo `io` que manega los inputs. Además, retorna una instancia del tipo `std::io::Stdin`.
5. `read_line` es un método de `Stdin` que almecena en la variable pasada como argumento el input y retorna una instancia del tipo `Result`. Un `Result` es una enumeración, o **enum**, un tipo que puede tener múltiples estados posibles, o **variantes**. `&` indica que el argumento es una **referencia**. `mut` indica que puede sobreescribir el argumento.
6. `expect` es un método de `Result` (todos los tipos tienen métodos definidos). `Result` tiene dos variantes: `Ok`, que indica que la operación fue exitosa y almacena el valor generado, y `Err`, que indica que la operación falló y contiene información sobre cómo o por qué falló. Si la instancia de `Result` es un valor `Ok`, entonces `expect` retorna el valor que almacena; pero si en un valor `Err`, entonces muestra un mensaje de error.
7. `{}` es un marcador de posición (**placeholder**) que imprime el nombre de una variable. Si se quiere imprimir el valor resultante de una expresión, se usaría:
    ```rs
    let x = 5;
    let y = 10;
    println!("x = {x} and y + 2 = {}", y + 2); // x = 5 and y + 2 = 12
    ```


```rs
// guessing_game.rs
use rand::Rng;
use std::cmp::Ordering; // (1)
use std::io;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..=100); // (2)

    loop {
        println!("Please input your guess.");

        let mut guess = String::new();

        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        }; // (4)

        println!("You guessed: {guess}");

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        } // (3)
    }
}
```

1. `rand::Rng` es un rasgo (**trait**) que define los métodos que `rand` implementa.