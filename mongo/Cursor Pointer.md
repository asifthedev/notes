# MongoDB Cursor / Pointer

### Cursor kya hota hai?

Cursor ek **pointer** hota hai jo MongoDB query ka result **step-by-step** return karta hai.

### 2. Cursor kyun use hota hai?

Agar data bohat zyada ho, MongoDB saara data aik sath nahi bhejta.  
Cursor se data **thoda-thoda** karke milta hai, jis se memory overload nahi hoti.

### 3. Cursor kab milta hai?

Jab bhi aap `find()` query chalate ho — MongoDB **cursor** return karta hai, not data directly.

Example:

```js
db.users.find()
```

Yeh ek cursor deta hai.

### 4. Cursor ko use kaise karte hain?

Aap cursor ko **iterate** karke data dekhte ho.

Example: yeah code pehlay batch mey majood har document ko iterate karey ga phir aglay batch ya cursor ko load karey ga or usay iterate karey ga.

```js
db.users.find().forEach(doc => print(doc))
```

We can also use, `toArray()` it will automatically iterate over all the cursors and return an array of all documents.

```mongodb
db.users.find().toArray()
```

### 5. Cursor ka simple meaning:

- Cursor = **Query result ka pointer**

- Data = **line-by-line** milta hai

- Large data = **smooth** milta hai

- Memory = **save** hoti hai

Agar chaho to origin se end tak *1-page cursor notes* bhi bana doon.


