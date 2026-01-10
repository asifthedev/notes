## Type Interface

The type interface is used to define the structure for an object. They are specially designed for objects and align with the OOP principles, the inheritance.

```typescript
interface User {
    name: string
} 
```

## Nested Objects in Array

Let's say you have been given a task of defining a structure for this menu array, having different types of pizza objects inside.

```typescript
const menu = [
    { name: "Margherita", price: 8 },]
```

Sab say pehlay ham Pizza Item kelye data type banaye gay

```typescript
interface Pizza {
    name: string
    price: number
}
```

Abh ham menu item ka structure define karey gay

```typescript
const menu: Pizza[] = [];

menu.push({name: "Margritta", price: 2})
```

## Nested Objects

Is traha ham nested objects ka structure define kar saktey heyn.

```typescript
interface User {
  name: string;
  age: 22;
  address: {
    country: string;
    city: string;
    street: string;
  };
}
```

Better approach if you have to use a nested object elsewhere in the code.

```mongodb
interface Address: {
    country: string;
    city: string;
    street: string;
};

interface User {
  name: string;
  age: 22;
  address: Address
}
```

## Optional Properties

App object ki kis property ko optional bhi set kar saktey ho using `?` mark signe

```typescript
interface User {
  name: string;
  age: 22;
  address?: Address
}
```

But ager app is proper ko set nahi karey or access karnay ka try karo gey to yeah defined aye ga.

```typescript
interface User {
  name: string;
  age: number;
  address?: {
    country: string;
    city: string;
    street: string;
  };
}

let admin: User = { name: "Asif", age: 22 };

console.log(admin.address);
```
