# Typescript

## Type Assertions
```ts
const myCanvas = 
  <HTMLCanvasElement>document.getElementById("main_canvas");

const myDiv = 
  document.getElementById("main_div") as HTMLDivElement;
```

## Rest Parameters
```ts
function suma(...numbers: number[]): number {
  return numbers.reduce((prev, curr) => prev + curr, 0);
}
```

## Spread Operator
```ts
const numbers = [1, 2, 3]

console.log(...numbers); // 1, 2, 3
```

## Callbacks
```ts
function operar(
  num1: number,
  num2: number,
  func: (x: number, y:number) => number
) : number {
  return func(num1, num2);
}

console.log(
  operar(2, 3, (a, b) => a + b)
); // 5
```

## Union Types
```ts
let numberOrString: number | string = 0;

numberOrString = 'string';
```

## Intersection Types

```ts
type Human = {
  name: string,
  age: number,
}

type HeroProperties = {
  id: number,
  isActive: boolean,
}

type Hero = Human & HeroProperties;
/*
type Hero = {
  name: string
  age: number
  id: number
  isActive: boolean
}
*/
```

## Indexed Access Types
```ts
type Person = { 
  age: number,
  name: string,
  alive: boolean,
}

type Age = Person["age"]; // type Age = number; 
```

## Typeof Type Operator
```ts
let text = "hello";

let newText: typeof text; // let newText: string;
```

## Type From Function Return
```ts
function createAddress() {
  return {
    planet: "Earth",
    city: "Barcelona",
  };
}

type Address01 = ReturnType<typeof createAddress>; // <--
type Address02 = typeof createAddress; // <-x-

/* 
const myAddress01: Address01 = {
  planet: "planet",
  city: "city",
};
*/

/* 
const myAddress02: Address02 = () => {
  return {
    planet: "planet",
    city: "city",
  };
};
 */
```

## Data Modifiers

| Data      | Class | Childs | Externs |
| --------- | ----- | ------ | ------- |
| public    | rx    | rx     | rx      |
| private   | rx    | --     | --      |
| readonly  | rx    | rx     | r-      |
| protected | rx    | rx     | --      |

## Abstract Classes and Methods
```ts
abstract class Person {
  constructor(protected name: string) { }

  abstract print(): void;
} 

class Employer extends Person {
  constructor(name: string, protected salary: number) {
    super(name);
  }

  print() {
    console.log(`Name: ${this.name}\nSalary: ${this.salary}`);
  }
} 

let person = new Person('person'); // ERROR: Cannot create an instance of an abstract class.
let albert = new Employer('Albert', 1600);
albert.print()
```

## Generic Classes
```ts
class Pila<T> {
  private vec: T[] = [];
  
  insertar(x: T) { this.vec.push(x) }
  
  extraer() {
    if (this.vec.length > 0) return this.vec.pop();
    else return null;
  }

const pila01 = new Pila<Number>();
pila01.insertar(1);
pila01.insertar('2'); // ERROR: Argument of type 'string' is not assignable to parameter of type 'Number'.
}
```

## Non-null Assertion Operator
```ts
function printString(str: string | null) {
  // return str.toLowerCase(); ==> ERROR: 'str' is possibly 'null'
  return str!.toLowerCase();
}
```

## Types
```ts
type Cell = "[X]" | "[O]" | "[ ]";
type Board = [
  [Cell, Cell, Cell],
  [Cell, Cell, Cell],
  [Cell, Cell, Cell]
]

const myBoard: Board = [
  ["[ ]", "[ ]", "[ ]"],
  ["[X]", "[ ]", "[O]"],
  ["[X]", "[ ]", "[O]"],
  // ["[ ]", "[ ]", "[h]"], ==> [ERROR]
  // ["[ ]", "[ ]", "[ ]"] ==> [ERROR]
]
```

## Destructuring Assignment
```ts
const info = {
  name: "name",
  width: 20,
  height: 40,
  color: "#f0f0f0",
}
const { width, height } = info; // 20, 40
```

## Nullish Coalescing Operator
```ts
console.log(Number.id ?? "no tiene id")
```

## Optional Chaining Operator
```ts
const robert = { 
  fullName: { 
    firstName: "Robert" 
  } 
}
console.log(robert.fullName?.lastName) // undefined
```
