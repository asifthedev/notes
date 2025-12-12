# Aggregation Pipeline

Ismay aik document multiple stages say pipe/guzarta hey or har stage per data k uper kuxh specific operations perform kiye jatey jo data ko mazeed refine kartey jatey heyn.

Aggregation has multiple aggregation operators that we use within the `aggregate()` method.

```mongodb
db.students.aggregate([])
```

## $match

The `$match`works like `find()` operator in `aggregate()`.

```mongodb
db.students.aggregate([{$match: {name: "Ahmad"}}])
```

Ham `$match` aggregation operator mey comparison operator ko bhi use kar saktey heyn

```mongodb
db.students.aggregate([{$match: {marks: {$gt: 80}}}])
```

Or `$match`aggregation operator mey ham logical operators ko bhi use kar saktey heyn

```mongodb
db.students.aggregate([
{$match: {$and: [{name: "Ahmad"}, {marks: {$gt: 80}}]}}])
```

### $count

This aggregation operator will count the number of documents.

```mongodb
db.students.aggregate(
    [{$match: {name: "Asif"}, {$count: "_id"}]
)
```

Woh student dhikao jaha per name field ki vlaue `Asif` hey or phir un sabko `_id` field k base per count kar do.

### $sort

```mongodb
db.students.aggregate(
    [{$match: {name: "Asif"}}, {$sort: {marks: -1}}])
```

Esay stuents ko dhikao jinkay name field ki value "Asif" hey, or marks k hisab sort karo jis studnet k marsk sab say ziyada heyn woh uper ana chaye (Decending Order -1).

We can sort by multiple fields.

```mongodb
db.students.aggregate(
    [{$match: {department: "CS"}}, {$sort: {gpa: -1, name: 1}}]
)
```

### $project

Use to control k documents k konsay fields dhiknay chayee or kon say nahi it works like projection as in `find()` etc.

```mongodb
db.students.aggregate(
    [{$match: {department: "CS"}}, {$project: {name: 1, gpa: 1, _id: 0}]
)
```

Jis document mey students ka department `CS` hey uskay sirf name or age field hi dhikao.

**Adding Custom Field**

App apni custom field bhi add kar saktey ho $project operator k zariya say

```mongodb
db.students.aggregate([
    {$match: {department: "CS"}},
    {$project: {name: 1, gpa: 1, isValid: {$gt: ["$gpa", 3.5]}}}
])
```

### $sortByCount

Yeah operator har field mey har type ki value kitni dafa aa rahi hey usay count karta hey phir sabh values ko unkey coresspondin count k hisaab say display karta hey

```mongodb
db.students.aggregate([{$sortByCount: "$department"}])
```

**Output_**

```mongodb
[
  { _id: 'CS', count: 4 },
  { _id: 'Mathematics', count: 2 },
  { _id: 'Physics', count: 2 }
]
```

### $skip

Skip mey ham batatey hey k **x** number of documents ko skip kar k usay next walay jitnay bhi hey dhikao, let say hamaray pass yeah products collection hey:

```mongodb
[
  { _id: 1, name: 'iPhone', price: '$400' },
  { _id: 2, name: 'Apple Watch', price: '$100' },
  { _id: 3, name: 'Mouse', price: '$50' },
  { _id: 4, name: 'Keyborad', price: '$120' },
  { _id: 5, name: 'CPU', price: '$1120' }
]
```

Abh app yeah chahtey ho k pehlay do record ko skip kar diya jaye or aglay sarey najar ayen

```mongodb
db.products.aggregate([
    {$match: {}} // display everthing inside products collection
    {$skip: 2} // skip first two documents & display rest
])
```

**Output**

```mongodb
[
  { _id: 3, name: 'Mouse', price: '$50' },
  { _id: 4, name: 'Keyborad', price: '$120' },
  { _id: 5, name: 'CPU', price: '$1120' }
]
```

Now let say k pehlay skip karney k baad bhi apkey pass hazaro records heyn and app aik certain amount of document ko hi at a time dehkna chatey ho for that we can use `$limt` usko ham aglay section mey pareh gey.

### $ limit

Limit is used to limit the number of record you want to see, ho skta apki koee query 1000 records ouput kar rahi ho per app sirf kuxh records hi dehkna chahatey hun us case mey ap kitnay number of document show hongay isko limit kar saktey ho.

Let say hamaray pass aik **products** name ki collection hey jis k ander yeah record majood hey, for sake of demonstration:

```mongodb
[
  { _id: 1, name: 'iPhone', price: '$400' },
  { _id: 2, name: 'Apple Watch', price: '$100' },
  { _id: 3, name: 'Mouse', price: '$50' },
  { _id: 4, name: 'Keyborad', price: '$120' },
  { _id: 5, name: 'CPU', price: '$1120' }
]
```

If you run the code snippet give below it will output every document inside products collection.

```mongodb
db.products.aggregate([{$match: {}}])
```

But let say you only want to see the first 2 documents:_

```mongodb
db.products.aggregate([{$match: {}}, {$limit: 2}])
```

**Output:**

```mongodb
[
  { _id: 1, name: 'iPhone', price: '$400' },
  { _id: 2, name: 'Apple Watch', price: '$100' }
]
```

### $sample

Yeah apko given size count mey random documents ko dhikata hey let say meyray pass whai purani products ki collection hey or mey us mey say 2 random records ko dehkna chahta hun

Yani jab bhi mey yeah qurey run karun mujeh 2 randome documents najar aney chayee

```mongodb
db.products.aggregate([
    {$sample: {size: 2}}
])
```

**Output:**

```mongodb
[
  { _id: 3, name: 'Mouse', price: '$50' },
  { _id: 1, name: 'iPhone', price: '$400' }
]
```

## $group

Yeah documents ko aik specific field ki base per group kar deyta hey for example

```mongodb
db.students.aggregate([
    {$group: {_id: "$department"}}, 
])
```

Uper waley code snippet ki output neachay di gayi hey per yeah sirf unique groups k bata rahi hey k is field mey yeah 3 groups heyn

```mongodb
[ { _id: 'Physics' }, { _id: 'CS' }, { _id: 'Mathematics' } ]
```

Now let say you want to know the number of records fall under a group, k esay kitnay students heyn jo aik specific group say belong kartey heyn

```mongodb
db.students.aggregate([
    {$group: {_id: "$departrment", count: {$sum: 1}}}
])
```

Uper wala code run honey per har type k depart k under kitnay students unka count show karey ga.

```mongodb
[
  { _id: 'Physics', count: 2 },
  { _id: 'CS', count: 4 },
  { _id: 'Mathematics', count: 2 }
]
```

### $push operator in \$group

Let say app ko un students ko dehkna hey jo aik group k ander bajaye iskay k app unka count dehko app pora document hi dehkna chahta ho but aik same type k group mey

For example app un sarey documents ka group dehkna chahtay ho jo `CS` department under atey heyn isi tarah baki groups ka bhi to iskelye ham $push operator ka use kar saktey heyn

Yeah operator jab similar type k documents ka aik array bana deyta hey phir jab us type k documetn ata hey usay is array k ander push kar deyta hey

```mongodb
db.students.aggregate([
    {$group: {_id: "department", students: {$push: "$$ROOT"}}
])
```

It will create an array for every type of departmetn and pushes the whole documents to it's corresponding department type of array.

But let say you only want the **name** of the students to be pushed in array in that case you can only specify the name of the filed instead of **$$ROOT**

```mongodb
db.students.aggregate([
    {$group: {_id: "department", students: {$push: "$name"}}])
```

### $max

It's used to check maximum value of any numeric field in a group. For example mey ney documents ko department k base per group kiya huwa hey and abh mey dehkna chata hun k konsa student sab bara hey har group mey in term of age

```mongodb
db.students.aggregate([
    {$group: {_id: "$department", maximum_age: {$max: "$age"}}}
])
```

### $min

It will show you the minimum value of any numeric field for every group.

```mongodb
db.student.aggregate([{
    $group: {_id: "$department", minimum_age: {$min: "$age"}}
}])
```

### $avg

It will show the average value of any numeric field for ever group. Let say I want to know the average gpa in every department.

```mongodb
db.students.aggregate([{
    $group: {_id: "$department", average_gpa: {$avg: "$gpa"}}
}])
```

### $median

Median is also used to calculate the average value for each group but it is less effected by the outliers as compare to simple `$avg` operator.

Chalo phir average gpa calculate kartey heyn using $median operator.

```mongodb
db.students.aggregate([{
    $group: {_id: "$department", 
             median_gpa: {$median:
                 {input: "$gpa", method: "approximate"}}}
}])
```

method field mey `approximate` ka mtlb hey k data k sample k uper median calculate kia jaye gaye instead of exactly.

**Catch**

Ager app grouping nahi karna chahtey or sarey document kelye GPA ki average value dehkna chahtey instead of groups then you can pass `_id` field as `null`

```mongodb
db.student.aggregate([{
    $group: {_id: null},
    median_gpa: {$median: {input: "$gpa", method: "approximate"}}
}])
```

It will output average age for all of the students in collection.

```mongodb
[ { _id: null, median_age: 3.6 } ]
```

### $first

Har group k pehla document dhikata hey

```mongodb
db.students.aggregate([{
    $group: {_id: "$department", first_student: {$first: "$$ROOT"}}
}])
```

`$$ROOT` ka mtlb hey pora document dhikao ager app pora document k jaga sirf aik field dehkna chahtay heyn to yaha `$fieldname` pass kar saktey heyn.

### $last

Har group ka last document dhikata hey

```mongodb
db.students.aggregate([{
    $group: {_id: "$department", last_student: {$last: "$$ROOT"}},
}])
```

### $top

Ham ney first mey dehka k na to ham usmey yeah bata saktey hey k kon, kon say field show honey chaye or konsay nahi or na hi sort kar saktey but `$top` yeah saray features offer karta hey.

```mongodb
db.students.aggregate([
  {
    $group: {
      _id: "$department",
      top_std: {
        $top: {
          output: ["$name", "$gpa", "$age"],
          sortBy: { gpa: -1 }
        }
      }
    }
  }
]);
```

### $topN

The `$top` function only show the first document but if yo want to specify the number of documents you want from the top you can use `$topN` where n mean the number you want from the top.

```mongodb
db.students.aggregate([
  {
    $group: {
      _id: "$department",
      top_std: {
        $topN: {
          output: { name: "$name", gpa: "$gpa" },
          sortBy: { gpa: -1 },
          n: 2
        }
      }
    }
  }
])
```

### $bottom

Yeah top k opposit kaam karta hey syntax same hey top ki traha per yeah bottom say aik record ko show karta.

```mongodb
db.students.aggregate([
  {
    $group: {
      _id: "$department",
      bottom_std: {
        $bottom: {
          sortBy: { gpa: -1 },
          output: { name: "$name", gpa: "$gpa" }
        }
      }
    }
  }
])
```

**Explanation:**
→ sorts students by GPA descending.
→ picks the last document after sorting (lowest GPA in this case).
→ specifies which fields to return.
This will give you the student with the lowest GPA per department

### $bottomN

The \$bottom will only return back only one document from the bottom for each group but `$bottomN` will give you back N number of documents. For more detail read `$topN`
