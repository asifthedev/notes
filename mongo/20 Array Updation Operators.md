## First Matching Positional Operator `$`

`$` is the **positional operator**.  It updates **only the first array element** that matches the query condition. It works only in update operations.

```mongodb
db.collection.updateOne(
  { skills: { $elemMatch: { name: "developer" } } },
  { $set: { "skills.$.exp": 20 } }
)
```

`"skills.$"` → refers to the **first matched element** inside `skills` array. The `$` updates **only one element**, even if multiple elements match.

## All Positional Operator `$[]`

`$[]` operator array k sarey elements ko update kar deyta hey, ager app filter pass bhi karo gey to yeah usay ignore kar deyga or jitnay bhi elements hey array k ander chahey woh filter pass kartey heyn ya nahi sab ko update kar deyta hey.

**NOTE:** use only when have update all alements of an array, no conditional matching.

Let say hamarey pass aik collection hey jiska name hey `employees` 

```mongodb
{
  _id: ObjectId("673f651771bf64a76286b035"),
  name: "John Smith",
  hobbies: ["reading", "drawing"],
  isDeveloper: true,
  skills: [
    { name: "developer", level: 8, gender: "Male" },
    { name: "tester", level: 10, gender: "Male" }
  ]
}
```

Or ham chatey heyn jaha per `name` field ki value `developer` hey waha per aik new field add kar deyn jiska name hoga `type` to show case either he's a frontend developer or backend.

```mongodb
db.employees.updateMany(
  { "skills.name": "developer" },
  { 
    $set: { 
      "skills.$[].type": "NA" 
    } 
  }
)
```

**Output:** You can see even the second element in skills array hasn't a `developer` but still the `$[]` operator also added the type field in the `tester` 

```mongodb
{
  _id: ObjectId("673f651771bf64a76286b035"),
  name: "John Smith", 
  hobbies: ["reading", "drawing"],
  isDeveloper: true,
  skills: [
    { name: "developer", level: 8, gender: "Male", type: "NA"},
    { name: "tester", level: 10, gender: "Male", type: "NA" }
  ]
}
```

So whenever you want to perform an update operation on all the elements in array use All Positional Operator `$[]`.

## Update All Matching Elemetns in Array

Allows conditional updates on specific elements inside an array. Works with positional identifiers like `$[elem]`.

The normal `$` operator updates only the first match. `arrayFilters` lets you update **all matching elements**, but only those that meet your conditions.

**Example**

```js
db.collection.updateMany(
  {},
  { $set: { "skills.$[elem].exp": 20 } },
  {
    arrayFilters: [
      { "elem.level": { $gt: 7 } }
    ]
  }
)
```

- You define a **placeholder** (e.g., `elem`) inside `$[elem]`.
- You specify conditions for that placeholder inside `arrayFilters`.
- You can use **multiple filters** if needed.

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

## $each

It's has been used with the combination of $push to insert multiple values in an array

```mongodb
db.students.updateOne(
    {name: "Asif"},
    {$push: {courses: {$each: ["A", "B"]}}}
)
```

It will insert both A and B into courses array.

## $addToSet

Only add in new value in an array if it's not already there inside arrray.

```mongodb
db.students.updateOne(
    {rollNumber: "bsf2105505"},
    {$addToSet: {courses: "Cyber Security"}}
)
```

## $pop

It's used to remove an element form the beginning or end of the an array.

```mongodb
db.students.updateOne(
    {rollNumber: "bsf2105505"},
    {$pop: {courses: 1}})
```

Ager ham aik field jis ki type array hey us k agery 1 pass karey gey with `$pop` operator to yeah us array k end say aik value remove kar deyga

But ager ham -1 pass karey gey to yeah start say remove karey ga.

## $pull

`$pull`removes all instances of a specified value from an array field. `$pull` targets elements by their actual value, removing every occurrence that matches.

For example hamray pass yeah aik student hey or ham `react` name ki skill ko remove kar chahatey heyn:

```mongodb
{
  _id: 4,
  name: 'David',
  skills: ['nodejs', 'react', 'react', 'nodejs'],
}
```

To remove all occurences of `react` you can run:

```mongodb
db.students.update({_id: 4}, {$pull: {skills: "react"}})
```

Ager yeah value multiple time bhi hey to sari occurrences ko remove kardo.

**$pull Nested Object**

Let's say we have an employees collection which has skills field

```mongodb
  skills: [
    { name: 'tester', level: 10, expert: true },
    { name: 'designer', level: 12, expert: true },
    { name: 'SQA', level: '5', expert: false },
    { name: 'App Developer', level: '9', expert: true }
  ]
```

And you want to remove a document in skills array where the name of the skill is SQA.

```mongodb
db.employees.updateOne({_id: 1}, {$pull: {skills: {name: "tester"}}})
```

## $pullAll

With `$pullAll` you can specify multiple values as an input and it will remove all those specified values from the array field.

```mongodb
db.students.updateOne(
    {name: "Asif"},
    {$pullAll: {courses: ["JavaScript", "NodeJS"]}}
)
```


