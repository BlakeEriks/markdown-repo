# Typescript

## What is TypeScript

Typescript is a strongly typed language built on top of javascript. It is compiled into javascript and can thus be run anywhere that javascript can be run.

## Type Inference

Types can be either explicitly typed, or the types can be inferred.

```tsx
let greeting = "Hello World!" // Type is inferred as a string

let greeting: string = "Hello World!" // Type explicity set as a string
```

## Interfaces

Interfaces allow us to type the fields in a js object.

```tsx
interface User {
	id: number
	name: string
}

const user: User = {
	id: 1,
	name: "Sam"
}
```

Interfaces can be used to annotate function return types and parameters

```tsx
const getUser = (): User => {}
const setUser = (user: User) => {}
```

## Types

Types already available in javascript

- boolean
- bigint
- null
- number
- string
- symbol
- undefined

Typescript extends this list with the addition of

- unknown
- any
- never
- void

There are two syntaxes for building types → **interfaces** and **types**. Prefer interface if possible, and use type when specific features are required.

## Composing Types

Complex types can be created by composing simple ones. This can be done with primitives or with literals.

```tsx
interface MyInterface {
	bool: boolean
	anotherBool: true | false
	boolOrString: boolean | string
	evenNumbersUnderFive: 2 | 4
}
```

## Generics

Generics pass variables to types. 

```tsx
type StringArray = Array<string>
```

Interfaces can be created that use generics

```tsx
interface Satchel<T> {
	get: () => T
	add: (item: T) => void
}
```