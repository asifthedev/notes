# Array in Monogo

The array is an orderd collection of multiple values.

```mongodb
{
    name: 'John Doe',
    age: 32,
    is_active: true,
    address: ['New York', 'USA'],
    purchases: [
      { product_name: 'iPhone 15', brand: 'Apple'},
      { product_name: 'MacBook Air', brand: 'Apple'}
   ]
}
```

## Filter on string values in an array

Ager app ko array k ander majood kisi string value ko match kar k results nikalney heyn for example woh sarey users jinki `address` array mey `New York` name ki stirng value majood ho woh record dhikao is case mey ham kuxh is traha query likhay gey

```mongodb
db.users.find({address: "New York"})
```

Mongo khud hi samjh jata hey k ham yeah value ko address array k ander search karna cha rahey heyn abh hamey woh sarey record mill jayegay jaha array mey `New York` name ka city hoga

## Filtering on documents as values

Let say k ham purchases name k array jismey multiple products heyn or har product itself aik document hey, document ki kisi key ki value k base pay search karna chatey heyn.

```mongodb
purchases: [
  { product_name: 'MacBook Pro', brand: 'Apple', price: 1999 },
  { product_name: 'iPad Pro', brand: 'Apple', price: 1099 },
  { product_name: 'AirPods Pro', brand: 'Apple', price: 249 }
]
```

For example esay documents dhikao jaha per `purchases` array k ander kisi document ki `brand` key ki value `Apple` ho.

```mongodb
db.users.find("purchases.brand": "Apple")
```

## $in

Now let say you want all of the documetns where the address array contains `Pakistan` OR `UK` , yani koee aik value bhi ho to esay document ko return karo.

```mongodb
db.users.find({address: {$in: ['Pakistan', 'UK']}})
```

## $all

In MongoDB, the **`$all` operator** is used in queries to match array fields that contain **all the specified elements**, *regardless of order* and *regardless of whether the array contains additional elements*.

Suppose we have a document:

```mongodb
{
  "name": "Alice",
  "skills": ["python", "mongodb", "nodejs"]
}
```

If you run:

```mongodb
db.users.find({
  skills: { $all: ["python", "mongodb"] }
});
```

This document **will match**, because the `skills` array contains **both** `"python"` and `"mongodb"`.

Now if you run:

```mongodb
db.users.find({
  skills: { $all: ["python", "react"] }
});
```

This will **not match**, because `"react"` is not in the array.

## $push

Push is used to add a new value in an array, yani jis field ki type array hogi to us array k ander ager mujeh koee new value add karni hey to mey `$push` ka use karunga.

Suppose we have a document:

```mongodb
{
  "name": "Alice",
  "skills": ["python", "mongodb", "nodejs"]
}
```

If you ran the code given below it will ad the value `react` in `skills` array:

```mongodb
db.students.updateOne(
    {name: "Alice"},
    {$push: {skills: "react"}}
)
```

**Note:** ager new value already array mey exist karti bhi hey $push tab bhi add kar deyga
