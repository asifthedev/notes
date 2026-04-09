## Index in Database

Index aik database structure hai jo data ko fastly search mein madad karta hai, jaise kisi kitaab ki index se aap bina saaray pages parhay koi topic dhondh saktay hain.

MongoDB mein index aik special data structure hai jo queries ko fast banata hai by creating a sorted/ordered reference to documents - yeh collection ko scan karnay ki bajaye seedha required data tak pohancha deta hai, jis se search operations bohot tez ho jatay hain.

## Collection Scan

Collection Scan ka matlab hai ke MongoDB query ko match karne ke liye **har document ko check karta hai**, chahe woh relevant ho ya na ho.

## Equality Query

Jab app query mey kisi field ki value as an equality ya exact match k tor per check kartey ho for example:

```mongodb
db.users.find({age: 20})
db.users.find({age: {$eq: 20})
```

Isko equality boltey heyn because app keh rahey ho k ager user ki age exactly 20 k equal ho.

## Range Query

Jab app aik range batatey ho yani app greater, lessor ya phir in dono operator ka use kartey ho to yeah aik range query hoti hey.

```mongodb
db.users.find({age: {$gt: 20}})
```

That is a range query.

## View Indexes

You can view all available indexes on a collection by running:

```mongodb
db.users.getIndexes()
```

**NOTE** By default mongo creates an index on `_id` field of each collection in the database.

## Creating an Index

Let say we want to create an index for `users` collections on it's `age` field here's how we can do that the using this code snippet:

```mongodb
db.users.createIndex({age: 1})
```

## Droping an Index

```mongodb
db.users.dropIndex({age: 1})
```

## Selecting Field

Apko index us field per create karna chaye jo apko lagta hey k app frequently use karney waley ho data query karnay kelye.

## When to use Index?

Jis field per app index create kar rahey heyn, ya ager app ka query pattern 30% results return karta hey to thk hey mager ager app query pattern majority documents ko return karta hey to tabh index optimization k bajye query ko slow kar deyta hey

Woh is liye k phir pehlay mongo har index key ko dehkna parta hey or phir us key k document ko jisko woh point kar rahi hey to kaam double ho jata hey.

## Compount Indexes

Jab ham aik say ziydada fields ko use kar k index create kartey heyn to isay compound index kaha jata hey.

```mongodb
db.users.createIndex({age: 1, gender: 1})
```

Compound index is useful jab apka query pattern ya filter criteria mey aik say ziyda field use ho raha hey hotey heyn.

**NOTE:** MongoDB compound index follows the left-most prefix rule; equality fields should come first, sort field second, range fields last, and once a range is used, fields after it cannot use the index.

### Left-most prefix rule in Compound Index

Now ager mey left say right order mey koee element use karunga to mongodb index use kareyga, but ager right say left mey karunga to yeah index use nahi kareyga

Let say mey ager age use karung to index use hoga,

```mongodb
db.users.find({age: {$gt: 30})
```

 but ager mey `age` chor ka sirf `gender` use karunga to index use nahi hoga

```mongodb
db.users.find({gender: "male"})
```

One other things is k the order of fields doesn't matters in filter object, but which field you are skipping does matter.

```mongodb
db.users.find({gender: "male", age: 32})
```

### Equality, Sort, Range

Alwasy follow this pattern on fields when creating a compound index. for more information read this [article](https://www.mongodb.com/docs/manual/core/indexes/index-types/index-compound/#std-label-index-type-compound) by mongodb

## Partial Index

An index on a subset of documents in a collection. Sometime we only want index on specific type of documents but not on all, in that case we can use partial index.

Partial indexes only index documents that meet a specified filter condition. They're smaller, more efficient, and perfect for scenarios where you only need to index a subset of documents.

### Common Use Case: Optional Unique Fields

**Problem**

You want email addresses to be unique when provided, but the field is optional (not all documents have it).

**Solution**

Use a partial index with `partialFilterExpression`:

```javascript
db.users.createIndex(
  { email: 1 },
  { 
    unique: true,
    partialFilterExpression: { 
      email: { $exists: true, $type: "string" } 
    }
  }
)
```

- **Only indexes documents** where `email` exists and is a string
- **Enforces uniqueness** only on indexed documents
- **Allows multiple documents** with missing/null email fields
- **Prevents duplicate emails** among documents that have the field

```javascript
// ✅ Valid - all have unique emails or no email
{ name: "Alice", email: "alice@example.com" }
{ name: "Bob", email: "bob@example.com" }
{ name: "Charlie" }  // no email field
{ name: "David", email: null }  // null email (not indexed)

// ❌ Invalid - duplicate email
{ name: "Eve", email: "alice@example.com" }  // Error: duplicate key
```

- Documents without the indexed field won't use the partial index for queries
- The filter expression must match your query conditions to use the index
- Null values aren't indexed unless explicitly included in the filter

## Time to Live Index (TTL)

Yeah index date type k field k uper create hota hey or after givne interval yeah documents ko remove kar deyta hey.

For example you want to delete a log after month it has created, in that case you can use TTL index to perfrom this automatic deletion.

MongoDB will apply the TTL expiration rules to **all documents** in the collection, both old and new.

**Note:**

**Single field only** - Can only be created on one field

You can only create a TTL index on field who's type is date.

The document after creating TTL index will be deleted automatically.

**Example**

```mongodb
// Step 1: Insert documents BEFORE creating TTL index
db.sessions.insertMany([
  {
    userId: "user1",
    createdAt: ISODate("2025-12-20T10:00:00Z")  // 1 day old
  },
  {
    userId: "user2",
    createdAt: ISODate("2025-12-21T09:00:00Z")  // 1 hour old
  },
  {
    userId: "user3",
    createdAt: ISODate("2025-12-21T10:00:00Z")  // Just now
  }
])

// Step 2: Create TTL index (expires after 30 minutes)
db.sessions.createIndex(
  { createdAt: 1 },
  { expireAfterSeconds: 1800 }  // 30 minutes
)
```

In the example above:

- ✅ `user1` (1 day old) → **Deleted within ~60 seconds** (already expired)
- ✅ `user2` (1 hour old) → **Deleted within ~60 seconds** (already expired)
- ⏰ `user3` (just created) → **Will be deleted after 30 minutes**

## Coverd Query

A query that is coverd by the value of the index without going through any doucment in the collection, for example:

```mongodb
> db.countries.createIndex({name: 1})
> db.countries.find({name: "UK"}, {_id: 0, name: 1})
```

Abh yeah query mey projection object k zariya say ham yeah keh diya k hamey sirf name of the country hi chaye to woh to pehlay index value k tor par index mey hey.

To iskalya hamey bilkul bhi kisi document ko check karnay ki zrorat nahi hey index k ander, isay kehtay hey coverd query.

A query that is coverd by the value of the index.

## Query Plan

Jab bhi ap koee query run kartey ho to mongo db k ander majood query optimizer different type ko approaches ya plan ki apas mey race karwata jisko ham plane trial bhi bol saktey heyn.

Har approace ka trial kar check kia jata k konsa query plan 100 documents sab say pehlay return karta hey jo bhi query plan yeah race win karta hey usay winning plane kehtay hey or usay cache kar liya jata for future use.

Or baki planes ko reject kar diya jata hey.

**When the cached plan gets deleted?**

The cache plane deleted under these four scenarios if:

1. 1000 documents have inserted after the plan was cache (As collection is changed a lot)

2. Index rebuild 

3. More indexes are added (Maybe new indexes perform better)

4. Mongodb server started.

**How to view your query plan?**

```mongodb
// Execution stats - shows what actually happened
db.users.find({ age: { $gt: 25 } }).explain("executionStats")

// Query planner - shows the plan MongoDB chose
db.users.find({ age: { $gt: 25 } }).explain("queryPlanner")

// All plans - shows all considered plans (verbose)
db.users.find({ age: { $gt: 25 } }).explain("allPlansExecution")
```

## Multi Key Index

A **multikey index** is automatically created when you index a field that contains an **array**. MongoDB creates separate index entries for each element in the array.

```javascript
// Documents with array field
[{
  _id: 1,
  name: "Alice",
  tags: ["mongodb", "databases", "nosql"]  // Array field
},
{
  _id: 2,
  name: "Asif",
  tags: ["node", "mongodb"]
}]
// Create index on array field
db.articles.createIndex({ tags: 1 })
// MongoDB automatically makes this a multikey index
```

Behind the scenes, MongoDB creates index entries like: 

```javascript
┌─────────────┬──────────────┐
│ Index Key   │ Document ID  │
├─────────────┼──────────────┤
│ "databases" │ 1            │  ← From Alice's tags
│ "mongodb"   │ 1            │  ← From Alice's tags
│ "mongodb"   │ 2            │  ← From Asif's tags  
│ "node"      │ 2            │  ← From Asif's tags
│ "nosql"     │ 1            │  ← From Alice's tags
└─────────────┴──────────────┘
```

**Note** you cannot create compound index on two fields of array type because size of index or both hi bara ho jata hey (Cartesian Product Explosion), that's why mongodb allow only one array field in compound index. 

Example:

```mongodb
{
  _id: 1,
  tags: [/* 10 elements */],
  categories: [/* 20 elements */],
  keywords: [/* 15 elements */]    
}
// This is NOT allowed:
db.collection.createIndex({ tags: 1, categories: 1, keywords: 1 })
// Error: cannot index parallel arrays
```

### Why Not Allowed?

Agar MongoDB dono arrays ko index kare, to **Cartesian product** banta hai and the size of the Index keys would be:

```javascript
// Would create:
10 × 20 × 15 = 3,000 index entries for ONE document!
```

### Multi Key Indexes on Embedded Documents

Ham multi key index embedded documetn poray pay bhi create kar saktey heyn (No Recommended) or iski kisi specific key per bhi.

First let see creating index on the specific key of the embedded document.

```mongodb
{
  _id: 1,
  title: "Product A",
  reviews: [
    { user: "Alice", rating: 5, comment: "Excellent!" },
    { user: "Bob", rating: 4, comment: "Good product" },
    { user: "Charlie", rating: 3, comment: "Average" }
  ]
}
```

## Creating Index on rating Key

```javascript
db.products.createIndex({ "reviews.rating": 1 })
```

Behind the scene, Index entries:

```mongodb
3 → document 1  (Charlie's rating)
4 → document 1  (Bob's rating)
5 → document 1  (Alice's rating)
```

#### Characteristics

- **Index Key**: Scalar (single) value (number/string)
- **Size**: Small (only the specific field value)
- **Entries**: Har embedded document kelye aik hi key baney gi
- **Sorting**: By the indexed field value
- **Most common scenario** (99% of cases)

### Index on Full Array (Embedded Documents)

```mongodb
db.products.createIndex({ reviews: 1 })
```

Abh ham index bana diya reviews yani poray array per or har index key aik pora ka pora document hoga

Index entries (sorted by entire object):

```java
{user:"Alice", rating:5, comment:"Excellent!"} → document 1
{user:"Bob", rating:4, comment:"Good product"} → document 1
{user:"Charlie", rating:3, comment:"Average"} → document 1
```

- Exact document matching (rare)
- Looking up complete embedded documents
- **Rarely used** in practice

## Text Index

It's a type of multi key index, jo ham string type k text field jin k uper aksar hamey search implement karni hoti hey banatey heyn

Yeah string ander say important words ka array banata hey or phir un per index keys bana kar index banata hey, yeah stop words ko ignore kar deyta hey.

Let say hamray pass yeah documents hey or ham `desc` field per text index create karna chatay heyn.

```mongodb
[
  {
    name: 'Apple smart watch',
    desc: 'An beautiful smart watch with blu',
    price: 1299
  },
  {
    name: 'Sony smart TV',
    desc: 'A mindblowing smart LED TV',
    price: 1299
  }
]
```

Creating Text index:

```mongodb
db.products.createIndex({desc: "text"})
```

**Droping Text Index**

You can drop a text index as you have made like that

```mongodb
db.products.dropIndex({desc: "text"}) // WRONG
```

You have to mention the name of the text index, given by mongodb

```mongodb
db.products.dropIndex({desc: "text"})
```

**Warning!!**

```mongodb
db.products.createIndex({desc: 1})
```

Yeha exact match karey ga pora ka pora description mathc hona chaye, it's not text index.

**NOTE**

You can only have one text index per collection. You can not create multiple text indexes on the same collection.

### Searching Text Index

You can search text index by using `$text` and `$search` operator.

```mongodb
db.products.find({$text: {$search: "smart watch"}})
```

Now esa nahi hey `smart watch` keyle exact match dehka jaye ga balkey ager koee document in `smart` or `watch` mey say koee bhi word contain karta hey to woh show ho jaye ga.

**Output**

```mongodb
[
  {
    name: 'Apple smart watch',
    desc: 'An beautiful smart watch with blu',
    price: 1299
  },
  {
    name: 'Sony smart TV',
    desc: 'A mindblowing smart LED TV',
    price: 1299
  }
]
```

**Exact Match**

```mongodb
db.products.find({$text: {$search: "\"smart watch\""}})
```

Exact match kelye quote mey close kardo value to abh wahi document aye ga jiskay description mey pora smart watch string hogi.

**Exempting Terms**

```mongodb
db.products.find({$text: {$search: "smart -watch"}})
```

Abh woh document ayega jismay smart to hoga per -watch nahi.

### Best Match in Text Search

Mongodb aik score calculate karta hey jis document mey ziyada term match hoti heyn ya jo orignal search query k pass hota hey text search k scenario mey woh sabh say top per and in that way decending order mey record ko score k base per display kia jata hey.

Let say ager mujeh is query ka score dehkna hey

```mongodb
db.products.find(
 {$text: {$search: "smart watch"}},
 {score: {$meta: "textScore"}})
```

## Compound Text Index

Lastly we've seen we cannot only create a singe index per collection but what if we have to create multiple text index or text indexes on multiple fields of documents in single collection.

We can use compound index:

```mongodb
db.products.createIndex({name: "text", desc: "text"})
```

Now if I search any product mongodb will search through both, the name and text, and if any of them include the given terms it will return that document

For example:

```mongodb
db.products.find({$text: {$search: "black"}})
```

**Output**

```mongodb
[
  {
    _id: ObjectId('6949f88032ac9d14b863b112'),
    name: 'Black Dress',
    desc: 'Black Cotton Dress',
    price: 2400
  },
  {
    _id: ObjectId('6948c31cb037112d9763b114'),
    name: 'HP Laptop',
    desc: 'A beautiful black HP Laptop',
    price: 1299
  }
]
```

Pehlay mey title or description dono mey hi word black per dosray mey sirf description mey.

### Configuring Multi Key Text Index on Creation

While creating and performing text search on multikey text index, you can pass a secondary object to configure the behavior of text index.

```mongodb
db.products.createIndex(
 {name: "text", desc: "text"},
 {default_language: "german", weights: {name: 10}})
```

 **default_language**

When creating a text index it let you specify the language in which you are going to perform text search on documents in your collection, ya phir jis language mey apka data hey.

**weights**

Yeah bata hey k compound text index mey kis field score ko kitni importance deyni hey in the above example `name` field has 10X more importance then description.

**NOTE** it is the recommended practice.

### Configurating Text Index in Find

```mongodb
db.products.find(
 {$text: {$search: "Black"}},
 {
    $caseSenstive: true,
    language: 'german', 
    weights: {}})
}
```

Below are **hands-on practice setups** for **both scenarios**, written the way you’d actually use them in a real project. You can copy-paste and run them in MongoDB shell or Node.js.

---

# Scenario 1: Single-Language App (Index-time configuration)

### Use case

- Blog, ecommerce, docs site

- All content in English

- Title should matter more than body

---

## Step 1: Sample data

```js
db.articles.insertMany([
  {
    title: "Learn MongoDB Text Search",
    body: "MongoDB provides powerful text indexing features"
  },
  {
    title: "Text Indexing in Databases",
    body: "Text search is essential for modern applications"
  },
  {
    title: "MongoDB Aggregation",
    body: "Aggregation pipelines are different from text search"
  }
])
```

---

## Step 2: Create text index (IMPORTANT PART)

```js
db.articles.createIndex(
  { title: "text", body: "text" },
  {
    weights: {
      title: 5,
      body: 1
    },
    default_language: "english"
  }
)
```

Why this matters:

- Matches in `title` score **5x higher**

- English stemming & stop words are baked into the index

---

## Step 3: Query (no language needed)

```js
db.articles.find(
  { $text: { $search: "MongoDB text" } },
  { score: { $meta: "textScore" } }
).sort({ score: { $meta: "textScore" } })
```

### What to observe

- Documents with **MongoDB in the title** appear first

- Score is consistent and predictable

- Fast queries

---

## When to practice this scenario

- Default choice for 80–90% of apps

- SEO-like relevance needed

- Performance matters

---

# Scenario 2: Multilingual App (Query-time language)

### Use case

- Blog or forum with mixed languages

- Same fields, different languages per document

---

## Step 1: Insert multilingual data

```js
db.posts.insertMany([
  {
    title: "Hello World",
    body: "Learning JavaScript programming",
    language: "english"
  },
  {
    title: "Hola Mundo",
    body: "Aprendiendo programación en JavaScript",
    language: "spanish"
  },
  {
    title: "Bonjour le monde",
    body: "Programmation JavaScript pour débutants",
    language: "french"
  }
])
```

---

## Step 2: Create index (language neutral)

```js
db.posts.createIndex(
  { title: "text", body: "text" },
  {
    default_language: "none",
    weights: {
      title: 4,
      body: 1
    }
  }
)
```

Why `default_language: "none"`:

- Prevents MongoDB from assuming English

- Allows query-time language control

---

## Step 3: Search in Spanish

```js
db.posts.find(
  {
    $text: {
      $search: "programación",
      $language: "spanish"
    }
  },
  { score: { $meta: "textScore" } }
).sort({ score: { $meta: "textScore" } })
```

---

## Step 4: Search in French

```js
db.posts.find(
  {
    $text: {
      $search: "programmation",
      $language: "french"
    }
  }
)
```

### What to observe

- Correct documents match per language

- Same index, different parsing behavior

- Weights remain fixed (title still more important)

---

# Real-World Practice Exercise

Try this to **see the difference clearly**:

1. Search Spanish text **without** `$language`

2. Search again **with** `$language: "spanish"`

3. Compare results

```js
// Wrong (language ignored)
db.posts.find({ $text: { $search: "programación" } })

// Correct
db.posts.find({
  $text: {
    $search: "programación",
    $language: "spanish"
  }
})
```

You’ll notice fewer or poorer matches without the language override.

---

# Decision Cheat Sheet

Use **index-time language & weights** when:

- Content is mostly one language

- Ranking quality matters

- You want best performance

Use **query-time language** when:

- Documents are multilingual

- Language varies per request

- You can’t predict language at index time
