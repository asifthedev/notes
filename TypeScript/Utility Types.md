# Utility Types

TypeScript mein **Utility Types** wo built-in tools hain jo aapko pehle se maujood types ko modify ya transform karne mein madad dete hain. Inka asal maqsad code ki duplication ko kam karna aur types ko flexible banana hai.

## Partial\<Type\>

Ye utility type kisi bhi interface ya type ki saari properties ko **optional** bana deta hai. Ye aksar "Edit Forms" ya "Update API calls" mein kaam aata hai jahan humein saari fields nahi balkay sirf kuch fields bhejne ki zaroorat hoti hai.

```typescript
interface User {
  id: number;
  name: string;
  email: string;
}

// Ab saari properties optional hain
const updateData: Partial<User> = {
  name: "Ali"
};
```

## Required\<T\>

Yeah, partial utility type k opposit hey, yeah sari propertis ko required bana deyta hey, even if they are required in the originally defined type.

```typescript
interface User {
  id?: number;
  username?: string;
  age?: number;
}

let user: Required<User>;
```

## Pick\<Type, Keys\>

Jab aapko kisi bade type mein se sirf **kuch khaas properties** chahiye hon, to aap `Pick` use karte hain.

```typescript
interface User {
    id: number,
    name: string,
    age: number,
    email: string
    address: string
}

type UserContactInfo = Pick<User, "name" | "email">;

const contact: UserContactInfo = {
  name: "Ali",
  email: "ali@example.com",
};
```

### Omit\<Type, Keys\>

Ye `Pick` ka ulta hai. Ye aapko kisi type mein se **kuch properties nikaalne (exclude)** ki ijazat deta hai.

```typescript
// 'id' property ko nikaal kar baaki sab rakho
type UserWithoutId = Omit<User, "id">;
```

## Readonly\<Type\>

Ye kisi bhi object ki properties ko **read-only)** bana deta hai. Aap unhein baad mein change nahi kar sakte.

```typescript
interface User {
  id: number;
  name: string;
}

let admin: Readonly<User> = {id: 1, name: "Asif Shahzad"}

admin.name = "Wasif"
// Cannot assign to 'name' because it is a read-only property.
```

## Record\<Keys, Type\>

Ye tab kaam aata hai jab aapko aik aisa object banana ho jiski **keys** aik khaas union type hon aur **values** ka type fix ho.

```typescript
type Page = "home" | "about" | "contact";

let nave: Record<Page, { title: string }> = {
  home: { title: "Home page" },
  about: { title: "About page" },
  contact: { title: "Contact page" },
};
```

## ReturnType\<Type\>

Ye utility type kisi **function ke return value** ka type extract karne ke liye use hota hai.

```typescript
function getUser() {
  return { id: 1, name: "Ali" };
}

type UserInfo = ReturnType<typeof getUser>; 
// { id: number; name: stri
```

## NonNullable\<T\>

Type mein se `null` aur `undefined` ko nikaal deta hai.

```mongodb
interface UserProfile {
  name: string;
  email: string | null;
}

// Hamein aik aisa type chahiye jahan email pakka ho
type VerifiedUser = {
  name: string;
  email: NonNullable<UserProfile['email']>;
};

const user: VerifiedUser = {
  name: "Zain",
  email: "zain@example.com" // Ab yahan null allow nahi hoga
};
```
