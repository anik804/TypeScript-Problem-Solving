## 🎯 Interview Questions - Blog Task

### Topic 1: Differences Between Interfaces and Types in TypeScript

TypeScript offers two ways to define custom types: `interface` and `type`. While they can often be used interchangeably, there are key differences that affect how you model your data and extend types.

### ✅ Similarities

Both can describe the shape of an object:

```ts
interface User {
  name: string;
  age: number;
}

type UserType = {
  name: string;
  age: number;
};

interface UserInterface {
  name: string;
  age: number;
}

type UserType = {
  name: string;
  age: number;
};

// Demonstrating Declaration Merging with Interface
interface Car {
  wheels: number;
}

interface Car {
  color: string;
}

const myCar: Car = {
  wheels: 4,
  color: 'red',
};

// Type cannot be merged like this
type Bike = {
  wheels: number;
  color: string;
};

---

### Topic 2: The use of 'keyof' Keyword in TypeScript

#### The `keyof` keyword is a **type operator** that returns a union of the property names of a given type. It is useful when you want to ensure that the keys you use to access an object are valid keys of that object.

```ts
// Defining a sample type
type Person = {
  name: string;
  age: number;
  job?: string; // optional property
};

// keyof creates a union of property names of the type
type PersonKeys = keyof Person;  // "name" | "age" | "job"

// Using keyof in a function to access object properties
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user: Person = { name: 'Alice', age: 30 };

// Valid usage with keyof
const userName = getProperty(user, 'name'); // ✅ Type is string
console.log(userName); // Output: Alice

// Invalid usage with a non-existent key (compile-time error)
// const invalid = getProperty(user, 'salary'); // ❌ Error: "salary" is not a key of Person
