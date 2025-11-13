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
db.runCommand(
    collMod: name_of_existing_collection,
    validator: {
        $jsonSchema: {}
    }
)
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


