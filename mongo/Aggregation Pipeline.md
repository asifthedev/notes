# Aggregation Pipeline

MongoDB ka **Aggregation Framework** data ko **transform** aur **analyze** karne ke liye use hota hai. 

Is framework mein hum **multiple operations** ko ek sequence mein perform karte hain, jahan data **step-by-step different stages** se guzarta hai. 

Har stage ek **specific operation** perform karti hai—jaise filtering, grouping, sorting, ya reshaping—aur ye process tab tak chalta hai jab tak humein **desired result** mil nahi jata.

Is process ko **pipeline** is liye kaha jata hai kyun ke data ek stage se nikal kar aglay stage mein **pipe** hota rehta hai, bilkul ek flow ki tarah.

## $match

It used to pass a filter to filter the documents same as find, use in the beginning to utilize indexes on the collection.

```mongodb
db.employees.aggregate({$match: {gender: 'male'}})
```

## $group

It is used to group documents by a key and then we use operators with group to get insights from the data based on those groups.

**Syntax**

```mongodb
{
 $group:
   {
     _id: <expression>, // Group key
     <field1>: { <accumulator1> : <expression1> },
     ...
   }
 }
```

| Field   | Description                                                                                                                                                                                                                                                                                                                                                             |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `_id`   | *Required.* The `_id` expression specifies the group key. If you specify an `_id` value of null, or any other constant value, the `$group` stage returns a single document that aggregates values across all of the input documents. [See the Group by Null example.](https://www.mongodb.com/docs/manual/reference/operator/aggregation/group/#std-label-null-example) |
| `field` | *Optional.* Computed using the [accumulator operators.](https://www.mongodb.com/docs/manual/reference/operator/aggregation/group/#std-label-accumulators-group)                                                                                                                                                                                                         |

For example we want to know how many male employees are in each country:

```mongodb
db.employees.aggregate([
    {$match: {gender: "male"}},
    {$group: {_id: "$address.country", total: {$sum: 1}}}
])
```

Here's how to calculate average order value across all documents:

```mongodb
db.orders.aggregate([
  {
    $group: {
      _id: null,  // null groups ALL documents together
      averageOrderValue: { $avg: "$orderValue" }
    }
  }
])
```

Here's how to calculate total sales.

```mongodb
db.orders.aggregate([
  {
    $group: {
      _id: null,
      totalSales: { $sum: "$orderValue" }
    }
  }
])
```

**$min and \$max** - Find minimum/maximum value

```mongodb
db.orders.aggregate([
  {
    $group: {
      _id: "$category",
      lowestPrice: { $min: "$price" },
      highestPrice: { $max: "$price" }
    }
  }
])
```

**$push** - Create array of all values

```mongodb
db.orders.aggregate([
  {
    $group: {
      _id: "$customerId",
      orderIds: { $push: "$orderId" },    // Array of all order IDs
      products: { $push: "$productName" }   // Array of all products
    }
  }
])
```

**$addToSet** - Create array of unique values

```mongodb
db.orders.aggregate([
  {
    $group: {
      _id: "$customerId",
      uniqueProducts: { $addToSet: "$productName" }  // No duplicates
    }
  }
])
```

**\$first and $last** - Get first/last value

```mongodb
db.orders.aggregate([
  { $sort: { orderDate: 1 } },
  {
    $group: {
      _id: "$customerId",
      firstOrder: { $first: "$orderDate" },
      lastOrder: { $last: "$orderDate" }
    }
  }
])
```

**NOTE**: documetns k current flow k hisab say (assending or dececing) k hisab say pehlay or last documetn ko return karta hey, use it after sort.

## $sort

This stage is used to sort documents.

```mongodb
db.employees.aggregate([
    {$match: {gender: "male"}},
    {$group: {_id: "$address.country", total: {$sum: 1}}},
    {$sort: {total: -1}}
])
```

**Output:**

```mongodb
[
  { _id: 'uk', total: 7 },
  { _id: 'usa', total: 6 },
  { _id: 'india', total: 4 }
]
```

## $project

It allows you to select specific fields, rename fields, create new fields based on existing ones, and even exclude certain fields.

```mongodb
db.employees.aggregate([
  {
    $project: {
      _id: 0,
      firstname: 1,
      lastname: 1
    }
  }
])
```

**Adding Field**

```mongodb
db.employees.aggregate([
  {
    $project: {
      _id: 0,
      name: {
        $concat: ["$firstname", " ", "$lastname"]
      }
    }
  }
])
```

### Operators we can use within $project

Assume a document in `employees` collection:

```js
{
  _id: ObjectId("65a1f9"),
  firstname: "john",
  lastname: "doe"
}
```

## `$concat`

Joins strings.

```js
{
  $concat: ["Hello ", "$firstname"]
}
```

### Output

```js
"Hello john"
```

## `$toUpper`

Uppercases a string.

```js
{
  $toUpper: "$firstname"
}
```

### Output

```js
"JOHN"
```

## `$substrCP`

Extracts substring (Unicode-safe).

```js
{
  $substrCP: ["$firstname", 0, 1]
}
```

### Output

```js
"j"
```

```js
{
  $substrCP: ["$firstname", 1, -1]
}
```

### Output

```js
"ohn"
```

## `$strLenCP`

Returns string length.

```js
{
  $strLenCP: "$firstname"
}
```

### Output

```js
4
```

## `$subtract`

Subtracts numbers.

```js
{
  $subtract: [ { $strLenCP: "$firstname" }, 1 ]
}
```

### Output

```js
3
```

### Transformating Data

Assume this document: 

```mongodb
{
  _id: ObjectId('694b4c771444ee363b021328'),
  firstname: 'olivia',
  lastname: 'chen',
  gender: 'female',
  email: 'oliviachen@example.com',
  dob: '1999-04-11T19:30:00Z',
  address: {
    street: '505 maple street',
    city: 'washington d.c.',
    country: 'usa',
    location: { coordinates: { lat: '38.8951', long: '-77.0364' } }
  },
  hobbies: [ 'reading', 'writing', 'painting' ],
  skills: [ { name: 'designer', level: 8 } ]
}
```

**Query**

```mongodb
db.employees.aggregate([
  {
    $project: {
      _id: 0,
      name: "$firstname",
      localtion: {
        type: "Point",
        coordinates: [
          {
            $convert: {
              input: "$address.location.coordinates.long",
              to: "double",
              onError: 0.0,
              onNull: 0.0,
            },
          },
          {
            $convert: {
              input: "$address.location.coordinates.lat",
              to: "double",
              onError: 0.0,
              onNull: 0.0,
            },
          },
        ],
      },
    },
  },
]);
```

**Output**

```mongodb
  {
    name: 'isabel',
    localtion: { type: 'Point', coordinates: [ -1.8904, 52.4862 ] }
  }
```

### Convert to Date

```mongodb
db.employees.aggregate([
  {
    // First stage: keep only required fields and rename firstname
    $project: {
      _id: 0,
      name: "$firstname", // optional, kept for clarity
      dob: 1              // must be kept for grouping in next stage
    }
  },
  {
    // Second stage: group employees by ISO week-based year of birth
    $group: {
      _id: {
        dobYear: {
          // Convert dob to Date and extract ISO week year
          $isoWeekYear: { $toDate: "$dob" }
        }
      },
      // Count employees per year
      total: { $sum: 1 }
    }
  }
]);
```

## What is $unwind?

`$unwind` is an aggregation pipeline stage in MongoDB that deconstructs an array field from input documents to output a document for each element of the array.

**Simple explanation:** It takes a document with an array and creates separate documents for each item in that array, essentially "flattening" the array structure.

**Before $unwind:**

```javascript
{
  _id: 1,
  name: "John",
  hobbies: ["reading", "gaming", "coding"]
}
```

**After $unwind on hobbies:**

```mongodb
{ $unwind: "$hobbies" }
```

Output

```javascript
{ _id: 1, name: "John", hobbies: "reading" }
{ _id: 1, name: "John", hobbies: "gaming" }
{ _id: 1, name: "John", hobbies: "coding" }
```

### Why Use $unwind?

When you need to perform operations on individual array elements rather than the array as a whole.

```javascript
db.employees.aggregate([
  {
    // Deconstruct the hobbies array so each hobby becomes a document
    $unwind: "$hobbies"
  },
  {
    // Group employees by country
    $group: {
      _id: "$address.country",

      // Collect unique hobbies per country (duplicates removed)
      hobbies: { $addToSet: "$hobbies" }
    }
  }
]);

```

## Project an Array

Let say you want to project specified number of elements from the array.

```mongodb
db.employees.aggregate([
  {
    $project: {
      _id: 0,
      name: "$firstname",
      skill: { $slice: ["$skills", 0, 1] },
    },
  },
]);

```

It will only project the one element starting from zero, for last element use -1.

**Project the $size**

```mongodb
db.employees.aggregate([
  {
    $project: {
      _id: 0,
      name: "$firstname",
      skillsCount: {$size: "$skills"},
    },
  },
]);
```

It will display the size of each array basically the number of elements inside array.

**Display array element based on a filter**

Let say you want to display an array element only if it matches the condition.

```mongodb
db.employees.aggregate([
  {
    $project: {
      _id: 0,
      name: "$firstname",
      skills: {
        $filter: {
          input: "$skills",
          as: "el",
          cond: { $gte: ["$$el.level", 8] },
        },
      },
    },
  },
]);

```

Ager skills array k ander majood embedded documetn jisko ham yaha `el` say refer kar rahey heyn uska `$$el.level` 8 k equal ya isay bara ho woh element display kar waao.

**NOTE** yaha baat array k element display karney ki ho rahi hey na k pora document so document sarey his ayengay but unkey ander skills array k elements sirf wahi ayegay jinka skill level 8 k equal ya bara hoga.

## $bucket

`$bucket` groups documents into **fixed ranges (buckets)** based on a numeric or date expression. Buckets are **manually defined** using boundaries.

Documents outside the boundaries go into a **default bucket** (optional).

### Basic Syntax

```js
{
  $bucket: {
    groupBy: <expression>,      // field or expression to bucket by
    boundaries: [ <lower1>, <lower2>, ... ],
    default: "Other",           // optional
    output: {
      count: { $sum: 1 }        // aggregations per bucket
    }
  }
}
```

### Example

```js
db.employees.aggregate([
  {
    $bucket: {
      groupBy: "$age",
      boundaries: [20, 30, 40, 50],
      default: "50+",
      output: {
        totalEmployees: { $sum: 1 }
      }
    }
  }
]);
```

### Key Points

- Boundaries are **inclusive of lower bound, exclusive of upper**

- Requires **sorted, non-overlapping boundaries** (boundaries jo app dey rahey heyn buckets kelye woh sorted or non overlaping honi chaye)

- Works with **numbers and dates**

- For automatic ranges, use `$bucketAuto` instead

## $skip

Yeah documents ko skip kar deyti hey for example ager meyray pass previous stage say 30 documetn millay per mujeh pehlay 10 skip karney hey or aglay 10 (11 - 30) aagey retrun karney heyn to ham skip ko use akr saktey heyn

```mongodb
db.employees.aggregate([
    {$match: {country: "Pakistan"}},
    {$skip: 10}
])
```

Yani pehlay 10 ko skip kar do baki sarey return kardo.

## $limit

Abh pexay ham ney dehka k $skip say ham docs ko skip to kar pa rahey heyn but let say hamey 30 mey 10 skip karney k baad baki bachney waley 20 docs say sirf pehlay 10 hi return karney heyn at a time to phir hame limit use kar saktey heyn

```mongodb
db.employees.aggregate([
    {$match: {country: "Pakistan"}},
    {$skip: 10},
    {$limit: 10}
])
```

Yani 10 ko skip karo pehaly waley or baki bachney waley docs mey say sirf 10 return karo no matter k baki kitnay bach raye heyn.

**NOTE** use \$skip before $limit in aggregation pipeline, order matters here.

## Write Aggregation Pipeline Output into a Collection

You can use `$out` stage

```mongodb
db.employees.aggregate([
    {$match: {country: "Pakistan"}},
    {$skip: 10},
    {$limit: 10}
    {$out: "mycollection"}
])
```

It will save the ouput into `mycollection` and if it already exists in the database it will overwrite all of the existing document and insert those new one.

## $lookup

Use to query documents from multiple collections. It is used to perfrom left join. Where from one collection its all documents are included and from other collection only those documents are included which are common in both collection.

```mongodb
{
  $lookup: {
    from: "collection",
    localField: "field",
    foreignField: "field",
    as: "result"
  }
}

```

## $count

Yeah documents ko count karnay kelye use hoti hey kisi bhi stage k baad ya pehlay ya phir standalone bhi ham isay use kar saktey heyn.

```mongodb
db.customers.aggregate([
  { $match: { city: "New York" } },
  { $count: "NewYourkens" },
]);
```

## $addFields

It is used to add or modify field of documents in a collection. **Note** the changes are only take effect on results and not on the orignal documents in the collection.

**Adding New Field**

```mongodb
db.customers.aggregate([
    {$addFields: {myField: "anyValue"}}
])
```

It will add a new field.

**Overwriting**

If you try to add a field the already exists in collection's documents it will be overwritten with the new field and it's value.
