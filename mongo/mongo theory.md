# Mongo DB

Yeah aik NoSQL aur non-ralational database hey, jo data ko aik JSON formate mey store karta hey jisko ham BSON (Binary JSON) bulatey heyn.

**Schema Flexibility** mongo db mey SQL database ki tarah schema fixed nahi hota yani ager mey pehlay user ka name or age store karwa raha to abh mey uska gender bhi store karwa skta hun, which good for rapidly changing scenarios.

**No-SQL** yani ismey data tabular form mey store nahi hota or koee fixed schema bhi nahi hota jis traha aik SQL database mey hota hey.

**Non Relational** yani ismey foreign key jesa koee concept nahi, but ham manually linke kar saktey data ko.

## Collections

Jesay SQL database mey table hotey jinmey ham records ko store kartey heyn wesay hi mongo db mey Collections hoti hey jinmey data ko store kia jata hey.

## Documents

Collection k ander har JSON entery ko ham document kehtay heyn.

## BSON

**BSON (Binary JSON)**: Yeh ek binary-encoded data serialization format hay jo JSON ko extend karta hay aur additional data types jaise ObjectId, Date, Timestamp, Binary Data, Regular Expressions, aur Decimal128 ki support provide karta hay. MongoDB internally is format ko use karta hay.

**Working process**: Jab aap MongoDB mein koi document insert karte ho, wo automatically BSON binary format mein serialize hota hay aur disk par efficiently store hota hay. Data retrieve karte waqt, MongoDB us binary BSON data ko wapas JSON format mein deserialize kar deyta hay taakeh aap aasan tarike se access kar sako. Yeh process backend mein happen karta hay, isliye user ko directly BSON ke saath kaam nahi karna padta—sirf JSON format dikhai deta hay.

**Benefit**: BSON binary format hone ki wajah se storage space kam lagti hay, transmission faster hota hay, aur JSON se zyada data types support milte hain, jo MongoDB ko powerful aur efficient banata hay.

## Mongosh

Yeah aik CLI client hey jisay ki madad say ham ham mongo database k sath interact kar saktey using commands.

## Mongo DB Compass

Yeah aik Graphical Client hey jis ki madad say ham graphically hamarey mongo database or uskay data ko manage kar saktey.

## Mongo DB Connection String

A stand alone url used to establish a connection with the database through a client such as mongosh or compass etc.

```url
mongodb://username:password@hostname:27017/
```

You can aslo specify a database name you want to connect with

```url
mongodb://username:password@hostname:port/database
```

**Example:_**

```url
mongodb://asifthedev:Asif@123@localhost:27017/test
```

**Fun Fact:** By default mongo db 27017 port run karta hey or hostname us machine ka network address hota hey jispay mongo db run kar raha hey.

## Connect with database

**Using mongosh**

```bash
mongosh connection_string
```

Example:_

```bash
mongosh mongodb://asifthedev:Asif@123@localhost:27017/
```

**Output:_**

```bash
test>  
```

By default test dabase select hota hey.

# 
