## Show Database

```mongodb
show dbs
```

It will list down all of your databases

```bash
> admin      100.00 KiB
> config      72.00 KiB
> local       80.00 KiB
```

## Create Database

```mongodb
use database_name
```

`use` command is use to create a new database or to select an existing database.

```mongodb
use book_store # {ok: 1}
```

The code snippet given above will output `{ok: 1}` that mean database has been created successfully.

**Catch:** new database bananey k baad ager app `show dbs` kartey ho to niya database najar nahi ayega per ban jaye ga, show karwaney kelye database k ander aik new collection banai parey gi.

## Creating a Collection

```mongodb
db.createCollection("books")
```

## Show Collections

```mongodb
show collections
```

## Renaming a Collection

```mongodb
db.collection_name.renameCollection("new_name")
```

**Example:_**

```mongodb
db.book.renameCollection("books")
```

## Getting Help

If you are not sure about option available with a command you can run `.help()` function with any command and it will output all available operation for a command

```mongodb
db.help()
```

## Droping a Collection

```mongodb
db.collectionName.drop();
```

**Example_**

```mongodb
db.books.drop()
```

## Droping a Database

Go into the database you want to drop using `use` command and then run:-

```bash
db.dropDatabase()
```

## Inserting One Document

```mongodb
db.collection_name.insertOne({name: "Asif", age: 23})
```

## Insert Many Documents

```mongodb
db.collection_name.insertMany([
    {name: "Wasif", age: 15},
    {name: "Asim", age: 25}
])
```

## JSON Schema Validation

Schema validation do tarah say hoti hey aik existing collection kelye or aik new collection ko create kartey wakt ki jati hey.

### Schema Validation for New Collection

This is how we perform schema validation while creating a new collection.

```mongodb
db.createCollection("students", {
    validator: {
        $jsonSchema: {
            title: "Student object validation",
            bsonType: "object",
            required: ["name", "age", "course"],
            additionalProperties: false,
            properties: {
                _id: {
                    bsonType: "objectId",
                    description: "Unique identifier for the student"
                }
                name: {
                    bsonType: "string",
                    description: "The name must be of string type"
                },
                age: {
                    bsonType: "int",
                    minimum: 5,
                    maximum: 20,
                    description: "The age must be of string type and between 5 and 20"
                },
                course: {
                    bsonType: "string",
                    enum: ["IT", "CS", "DS"],
                    description: "course must be of type string and have the one of the following value: IT, CS, DS"
                }
            }
        }
    }
})
```

**title**

Yeah jab bhi koee schema validation fail hogi to yeah title bhi sath show hoga.

**required**

Yeah waley fields required heyn.

**additionalProperties**

Yeah is cheez ko validate karta hey k kia jo properties app ney `properties` object mey di hey unke illawa bhi kia user nayi property ko add kar sakta hey ya nahi.

The value `false` batati hey k user sirf wahi properties ko pass kar sakta hey jo schema mey majhood properties object mey di hoee heyn.

## Properties

`properties` object k ander ham apni woh sari properties define kartey heyn jo hamarey har document k ander majood hongi.

Har property name as key use hota hey jiskay against aik object hota hey jismey us property kelye validation hoti hey jesay k `bsonType`

```mongodb
age: {
    bsonType: "int",
    minimum: 5,
    maximum: 20
    description: "The message"
}
```

**bsonType**

The type of data that user is allowd to pass as value such as string, int etc.

**description**

Yeah woh messag hota jo display hota hey jab bhi validation break hoti hey.

**minimum**

The minimum value of age the user is allowd to pass

**maximum**

The maximum value a user is allowd to pass

### enum

Ager app chahtey k user sirf kuxh specific vlaues k ander say hi aik value enter karey to app is cheez ko enum k zariye say ensure kar saktey heyn

```bash
course: {
    bsonType: "string",
    enum: ["IT", "CS"]
}
```

The user can only be allowd to pass one of the value from `enum` array.

## Schema Validation for Existing Collection

```bash
db.runCommand({
    collMod: name_of_existing_collection,
    validator: {
        $jsonSchema: {}
    }
})
```

Yaha `collMod` stand for Collection Modify bs yahi aik niya filed hey baki validator k ander sabh kuxh wesa hi rahey ga jesa aik new collection kelye thaa.

### Catch

Jab app `additionalProperties` ko `false` set kar detay ho us case mey apko `properties` object k ander `_id` filed zroro define karna parhta hey.

Qn ager yeah nahi hoga to MongoDB khud say insert karney ka try karta hey but as we now `additionalProperties: false` mean k jo properties, `properties` object k ander define wahi add ho sakti heyn to isay error aye ga new document insert kartey wakt

```mongodb
db.runCommand(
    collMod: name_of_existing_collection,
    validator: {
        $jsonSchema: {
            additionalProperties: flase
            properties: {
                _id: {
                    bsonType: "objectId",
                    description: "Uniqure identifier for object"
                }
            }
        }
    }
)
```

### Schema validation for Array?

```mongodb
hobbies: {
    bsonType: "array",
    items: {
        bsonType: "string",
        description: "Item in hobbies array are must be string"
    },
   description: "hobbies must be of type arrray!"
}
```

## Schema validation for Object

```mongodb
address: {
    bsonType: "object",
    required: ["street", "city", "zipCode"]
    properties: {
        street: {
            bsonType: "string",
            description: "The value of street must be of string type"
        },
       city: {...},
       zipCode: {...}
    }
}
```

## General Syntax for Updation

Jab bhi update karna hota hey to sab say pehlay filter object pass kiya jata hey jismay ham yeah kehtay k ager aik document mey aik specific field x ki value ager y ho to us document k jin fileds ko upadte karna hota hey unko ham dosray object `$set` operator k sath pass kartey heyn.

```mongodb
db.collection_name.updationMethodName(
    {field: "value"}, // filter
    {$operator: {field: "value"}} // fields to update
)
```

## Update One

It updates first matching document with the given value against `$set` operator.

```mongodb
db.students.updateOne(
  { rollNumber: "bsf2105505" },
  { $set: { gpa: 3.8 } }
);
```

Jis student ka bhi roll number `bsf2105505` ho uski gpa `3.8` set kardo.

## Update Many

It updates all matching documents with the value given against `$set` operator

```mongodb
db.students.updateMany(
  { class: "IT" },
  { $set: { active: true } }
)
```

Jitnay bhi students ki class IT hey unka activation status `true` kardo.

## $set

The `$set` aik to kisi existing field ki value ko update karney kelye use kia jata hey ya phir kis existing document mey aik new field add karney kelye use hota hey.

```mongodb
db.students.updateOne(
    {rollNumber: "bsf2105505"},
    {$set: {customField: "x"}} // adding a new custom field
)
```

## $unset

The `$unset` is used to remove an existing field from a document.

```mongodb
db.students.updateOne(
    {rollNumber: "bsf2105505"},
    {$unset: {custome: ''}}
)
```

Jis student k rollNumber `bsf2105505` usmey `custome` name ka field remove ho jaye ga. Jis field ko remove karna hey uski value app ney empty string k tor per deyni hey, chahey pehlay uski value kuxh or hi qn na ho

## $inc

The `$inc` is short of increment, yeah kisi bhi numeric field ki value mey provided integer ko add kar deyta hey

```mongodb
db.students.updateOne(
    {rollNumber: "bsf2105505"},
    {$inc: {age: 2}}
)
```

Jis bhi student ka `rollNumber` equal hey `bsf2105505` uskay age field k ander 2 ka increment kar do.

## $mul

It multiplies the value of a numeric field with the provide numeric value.

```mongodb
db.students.updateOne(
    {rollNumber: "bsf2105505"},
    {$mul: {gpa: 100}}
)
```

Jis student ka rolllNumber bsf2105505 hey uskay gpa field ki value ko 100 say multiply kar do

## $rename

It is used to rename the field itself of a document or multiple doucments. Let say I want to change the `gpa` field to `cgpa` in all document in my student collection

```mongodb
db.students.updateMany({}, {$rename: {gpa:"cgpa"}})
```

**Note:** jab bhi hamey sarey document k uper kuxh apply karna hota bina kisi filter k to ham filter ko as an empty object pass kartey hey, or `updateMany()` method ko use kartey heyn.

## $currentDate

It sets the current date as a value of an existing field or creates the field with the given name if it isn't already exist in a document and set the current date as it's value.

```mongodb
db.students.updateMany(
    {},
    {$currentDate: {"createdAt":true}})
```

The value true is telling MongoDB to use current date as field's value.

## $min

Ager provided value jo ham dey gay woh field ki existing value say choti hey to provide value ko field ki existing value say replace kardo.

```mongodb
db.students.updateOne(
    {rollNumber: "bsf2105505"},
    {$min, {age: 20}}
)
```

Ager `age` ki existing value hamari di hoee value $20$ say choti hey to existing value ko replace kardo 20 k sath, yani hamari value k sath.

## $max

Ager hamari di hoee value field ki exsisting value say bari hey to usay replace kar do us value jo ham ney di hey.

```mongodb
db.students.updateOne(
    {rollNubmer: "bsf2105505"},
    {$max: {age: 22}}
)
```

Ager hamari di hoee age 22 bari hey student ki existing age say to hamri di hoee value 22 ko new age ki value k tor per set kardo.

## $push

Push is used to add a new value in an array, yani jis field ki type array hogi to us array k ander age mujeh koee new value add karni hey to mey `$push` ka use karunga.

```mongodb
db.students.updateOne(
    {rollNumber: "bsf2105505"},
    {$push: {courses: "Human Resources"}}
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

Ager ham aik field jis ki type array hey us k agery $1$ pass karey gey with `$pop` operator to yeah us array k end say aik value remove kar deyga

But ager ham $-1$ pass karey gey to yeah start say remove karey ga.

## $pull

`$pull`removes all instances of a specified value from an array field. `$pull` targets elements by their actual value, removing every occurrence that matches.

```mongodb
db.students.updateOne(
    {rollNumber: "bsf2205509"},
    {$pull: {courses: "Linear Algebra"}}
)
```

Jis student ka roll number `bsf2205509` hey uskay courses waley array field me say `Linear Algebra` wali value ko remove kardo.

Ager yeah value muliple time bhi hey to sari occurrences ko remove kardo.

## $pullAll

With `$pullAll` you can specify multiple values as an input and it will remove all those specified values from the array field.

```mongodb
db.students.updateOne(
    {name: "Asif"},
    {$pullAll: {courses: ["JavaScript", "NodeJS"]}}
)
```

## replaceOne()

It's is used to replace the whole record with a new one.

**Syntax**

```mongodb
db.students.replaceOne(
    {name: "Asif"} //filter
    {name: "Asim", age: 25, gender: "male"} // new document
)
```

Jis bhi student ka name `Asif` woh poray document ko is new document say replace kar do.

## deleteOne()

Use to delete one record at a time.

**Syntax**

```mongodb
db.students.deleteOne(
    {name: "Asif"} // filter
)
```

Jis bhi student ka name `Asif` hey usay delete kar do.

## deleteMany()

```mongodb
db.students.deleteMany(
    {class: "CS"}
)
```

Woh sarey students ko delete kardo ji ki class `CS` hey

**Delete All**

If you want to delete everthing from a collection

```mongodb
db.students.deleteMany(
    {} // filter
)
```

It will delete everthing from a collection.

## find()

It will return all matching documents.

```mongodb
db.students.find(
    {grade: "A"})
```

Woh sarey students ko show karo jinka grade A hey.

**Projection Object**

You can also pass a projection object as a second argument jo is baat ko specify karney kelye use hota hey kon say fields documetns k show hun kon say nahi

```mongodb
db.students.find(
    studentId: "S003",
    {name: 1, age: 1})
```

Yani sirf name of age hi show karo us student ki jis ki id `S003` hey

## projection()

Ager app har document mey jo match kar raha hey note `find()` k case mey uskay kuxh specific fields ko dehkna chahatey hey sarey fields ko dehknay k bajaye to app `projection()` method ka find k baad use kar saktey heyn

```mongodb
db.students.find({class: "CS"}).projection(name: 1, grade: 1)
```

Yani jin students ki class CS hey unka sirf name or grade hi dhikao, ager app chahtey heyn koee field na aye to app `0` use kar saktey heyn lakin by default jo field nahi diye jatey as 1 woh khud hi nahi aatey.

# findOne()

It will only return one matching document, even if multiple records jo match kar rahey hey per yeah sirf pehla record hi return karey ga.

```mongodb
db.students.findOne(
    studentId: "S002")
```

## count()

Jab bhi find mey koee filter pass kartey heyn or kehtay heyn k mujeh iskay against record dhikao, to ager app yeah count karna chahtey heyn k kisi bhi find query k against kitnay record millay heyn to `count()` usko hi batata hey.

```mongodb
db.students.find({major: "Computer Science"}).count()
```

Kitnay esay students heyn jinka major `Computer Science` hey batao.

## sort()

Use to show record in ascending and descending order.

```mongodb
db.students.find({major: "Computer Science"}).sort({grade: 1})
```

Yani jin bhi students ka major `Computer Science` unko grade k hisab say sort karo or yaha $1$ ka mtlb hey ascending order mey show karo and $-1$ ka mtlb hey descending order mey.

## skip(count)

```mongodb
db.students.find().skip(2)
```

That mean k pehlay do record $(1, 2)$ skip kar do or aglay saray show karo.

## limit()

```mongodb
db.students.find().skip(10).limit(10)
```

Pehlay 10 to skip kardo per uskay baad ho skta hey 200 records hun to ho sakta hey app sarey na dekhna chahatey ho in that case you can limit records by using `limit()`

Pehlay 10 skip kardo uskay baad jitnay documents bach rahey heyn, unmay say 10 hi dhikaoo.

## Comparison Operators

Chahey `deleteMany()` , `find()` ho ya phir `updateMany()` ho filter to hamey deyna hi parhta hey. Usi filter ko mazeed granular or precise bananey kelye ham comparison operator use kartey hey,

Yeah mostly numeric fileds k uper use hotey heyn and used to compare bara hey chota hey equal hey ya nahi equal hey etc.

### $eq

Stands for equal to.

```bash
db.students.find({rollNumber: {$eq: 2}})
```

Us student ko find karo jiska roll number 2 ho.

### $ne

Stands for not equal to.

```mongodb
db.students.find({rollNumber: {$ne: 2}})
```

Us student ko find karo jiska roll number 2 k equal na ho yani 2 say bara ya chota ho

### $gt

Short of greater than

```mongodb
db.students.find({rollNumber: {$gt: 2}})
```

Un students ko find karo jinka roll number 2 say bara hey.

### $lt

Short of less than.

```mongodb
db.students.find({rollNumber: {$lt: 2}})
```

Un students ko dhikao jinka roll number 2 say kam hey

### $lte

Short of less than or equal to.

```mongodb
db.students.find({rollNumber: {$lte: 2}})
```

Un students ko dhikao jinka roll number 2 say kam ya 2 k brabar ho.

### $gte

Short of greater than or equal to

```mongodb
db.student.find({rollNumber: {$gte: 2}})
```

Un student ko dhikao jinka roll number do say ziyada 2 k equal ho.

### $in

Show me student who's number is `in` [1, 2, 3] to yeah operator sif wahi student dhikaye ga jinka roll number 1, 2, and 3 hey baki nahi dhikay gey

```mongodb
db.students.find({rollNumber: {$in: [1, 2, 3]}})
```

### $nin

Short of not in

```mongodb
db.students.find({rollNumber: {$nin: [1, 2, 3]}})
```

Yani un student ko dhikao jin ka roll number 1, 2,  ya 3 nahi hey, yani not in list of [1, 2, 3]

## Logical Operator

They are use to form a filter by combining mutliple conditions. For example you want the sutdents who have their roll number greater than 2 and less than 4.

**Syntax**:

```mongodb
db.students.find({$logicalOperator: [{condition}, {condition},...]})
```

Yaha dot ka mtlb hey k isi tarah app multiple conditions ko bhi pass kar saktey hey

### $and

A document on which we trying to perfrom an operation will only pass the filter if all of the given conditions are satisfied otherwise not.

For example in example given below, the find() operation will on show a document in which the roll number is 2 and major is CS.

```mongodb
db.students.find( {$and: [{rollNo: {$gt: 2}}, {major: {$eq: "CS"}]} )
```

### $or

A documetn pass the or operator filter if any of the condition among all the given conditions is true, yani ager aik bhi condition match kar gayi tey kam hogiya.

```mongodb
db.students.find($or: [{major: {$eq: "CS"}}, {major: {$eq: "AI"}}])
```

## $regex

It used to search for string pattern using regular expressions in the value of a field.

**Syntax**

```mongodb
db.students.find({field: {$regex: /pattern/flags})
```

**Example:**

```mongodb
db.students.find({name: {$regex: /^As/i}})
```

Un students ko dhikao jinka name `As` start ho raha hey, or `i` flag ka mtlb hey incesntive chahey woh small letter mey hi `as` qn na ho. 

### $expr

Yeah aik hi document k do field ko apas mey compare karney kelye use hota hey.

```mongodb
db.expenditures.find({$expr: {$gt: ["spent", "budget"]}})
```

### $mod

Yeah apke field ki har value ko devide karta hey apki given value say or phir ager remainder woh ata hey jo app ney dey rakha hey to yeah esay record show karta hey

```mongodb
db.expenditures.find({cost: {$mod: [2, 0]}})
```

Ager cost filed ki value ko devide kia jaye 2 say or remainder mey zero a jaye to esay document ko wapi return karo.

### findOneAndUpdate()

Kaam yeah bhi `updateOne()` ki tarah karta hey per ismay or updateOne mey kuxh differences hey first difference is in output.

Jab app `updateOne()` ki help say kuxh update kartey heyn to kuxh esa answer ata hey. 

```bash
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```

But when you update a document using `findAndUpdateOne()` it return the same documetn back on which you are performing the update operation.

```mongodb
db.products.findOneAndUpdate({sku: "HDR-010"}, {$set: {name: "Asif"}})
```

If we run the code snippet given above it return back the object itself before updating the object, you can also view an object after updation py passing the third argument of `findOneAndUpdate()`

```mongodb
{
  _id: ObjectId('6922708d2a07b7ec0963b123'),
  sku: 'HDR-010',
  name: 'Asif Shahzad',
  category: 'Audio',
  price: 349.99,
  description: 'Noise-cancelling wireless headphones',
  tags: [ 'headphones', 'sony', 'audio' ]
}
```

#### **Options**

The third object is option object which let you specify more options about `findOneAndReplace()`.

```mongodb
db.products.findOneAndReplace(<search query>, <dataToUpdate>, <options>)
```

**returnDocument**

Document update k baad (after) ya phir update k pehlay (before) return hona chayee.

```mongodb
db.products.findOneAndReplace(
    {sku: "HDR-010"},
    {$set: {name: "Asif"}},
    {returnDocument: "after"}
)
```

**projection**

It let you specify kon kon say field najar ayen or kon kon say na najar ayen

```mongodb
db.products.findOneAndReplace(
    {sku: "HDR-010"},
    {$set: {name: "Asif"}},
    {
        returnDocument: "after", // show document after updation
        projection: {name: 1, sku: 1} // on display name and sku
    }
)
```

**sort**

Let say k app k pass 2 students hey  dono hi ka name same hey or app us studnet ka grade A set karna chahtey jiskay marks sab say ziyada heyn.

Sort will help you, first sort the documents based on a field value in our case the marks field and then who ever satisfying the filter first usko usko update kar do

```json
{_id: 1, name: "Ahmad", marks: 85}
{_id: 2, name: "Ahmad", marks 90}
```

Now let's write our update query.

```mongodb
db.students.findOneAndUpdate(
    {name: "Ahmad"},
    {$set: {grade: "A"}},
    {
        returnDocument: "after",
        projection: {name: 1, grade: 1, _id: 0},
        sort: {marks: -1} // decending order mey,
    }
)
```

The output of the above code is...

```mongodb
{ _id: 2, name: 'Ahmad', marks: 90, grade: 'A' }
```

**upsert**

upset ka mtlb hey ager record na milay search query jo app ney pass kar rakhi hey to is record ko insert as new record insert kardo

```mongodb
db.students.findOneAndUpdate(
    {name: "Asif"}, 
    {$set: {_id: 3, name: "Asif", marks: 85}},
    {upsert: true, returnDocument: "after"}
)
```

## findOneAndReplace()

Yeah existing doucment ko find karta hey or usay new document k sath replace kardeyga.

```mongodb
db.students.findOneAndReplace(
    {name: "Asif"},
    {_id: 3, name: "John Elia", marks: 67},
    {returnDocument: "after"}
)
```

## findOneAndDelete()

It will find a delete a document and return the deleted document back. It supports two options `{sort: -1/1, projection: {...}`

```mongodb
db.students.
```
