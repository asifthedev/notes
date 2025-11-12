# Multi Stage Image

Multi-stage build Docker ki aik advanced feature hai jo humein **optimized aur lightweight images** banane mein madad karti hai.

Socho ke aap koi cake bana rahe hain. Cake banane ke liye aapko:

1. Pehle saari ingredients aur bartan chahiye
2. Phir cake ban jata hai
3. Lekin serve karte waqt sirf **tayar cake** chahiye, saare bartan aur extra cheezein nahi

Multi-stage build bhi aisa hi kaam karta hai - pehle stage mein code compile/build kartey wakt kuxh utilities, or packages ki need hoti hey, dusri stage mein sirf **final result** hi zrori hota.

## Definition:

Multi-stage build mein hum aik hi Dockerfile mein **multiple FROM statements** use karte hain. Har FROM statement aik naya stage shuru karta hai, aur hum previous stages se sirf zaroori files copy kar sakte hain.

```bash
FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . .

RUN npm run build

FROM node:20-alpine AS runner

WORKDIR /app

COPY package*.json .

RUN npm install --production

COPY --from=build /app/dist ./dist

CMD ["npm", "start"]
```


