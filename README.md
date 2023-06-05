# mongoDbBasics
#Basics Queries:
C:\Users\bitan>mongo
MongoDB shell version v5.0.18
connecting to: mongodb://127.0.0.1:27017/?compressors=disabled&gssapiServiceName=mongodb
Implicit session: session { "id" : UUID("0bd67d1f-6c37-44a2-b65b-57eb428b2f13") }
MongoDB server version: 5.0.18
================
Warning: the "mongo" shell has been superseded by "mongosh",
which delivers improved usability and compatibility.The "mongo" shell has been deprecated and will be removed in
an upcoming release.
For installation instructions, see
https://docs.mongodb.com/mongodb-shell/install/
================
---
The server generated these startup warnings when booting:
        2023-06-06T04:56:44.602+05:30: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
---
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
> use product
switched to db product
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
> db
product
> db.createCollection('prod')
{ "ok" : 1 }
> show dbs
admin    0.000GB
config   0.000GB
local    0.000GB
product  0.000GB
> db
product
> show collections
prod
> db.users.insert({name:'Bitan', age:'20'})
WriteResult({ "nInserted" : 1 })
> show collections
prod
users
> db
product
> show collections
prod
users
> db.users.drop()
true
> show collections
prod
> db.prod.drop()
true
> show collections
> db.dropDatabase()
{ "ok" : 1 }
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
> use lib
switched to db lib
> db
lib
> db.createCollection('books')
{ "ok" : 1 }
> show collections
books
> db.books.insert(
... name: 'The complete Java book',
... }
uncaught exception: SyntaxError: missing ) after argument list :
@(shell):2:4
> db.books.insert( { name: 'The complete Java book', pages:500, price:1000 })
WriteResult({ "nInserted" : 1 })
> db.books.find()
{ "_id" : ObjectId("647e738ea3946828b949634e"), "name" : "The complete Java book", "pages" : 500, "price" : 1000 }
> db.books.insertOne( { name: 'think in Java', pages:600, price:2000 })
{
        "acknowledged" : true,
        "insertedId" : ObjectId("647e73c6a3946828b949634f")
}
> db.books.insertMany( [{ name: 'think in python', pages:800, price:4000 },{name:"Javascript", pages:300, price:500}])
{
        "acknowledged" : true,
        "insertedIds" : [
                ObjectId("647e7404a3946828b9496350"),
                ObjectId("647e7404a3946828b9496351")
        ]
}
> db.books.find()
{ "_id" : ObjectId("647e738ea3946828b949634e"), "name" : "The complete Java book", "pages" : 500, "price" : 1000 }
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "name" : "think in python", "pages" : 800, "price" : 4000 }
{ "_id" : ObjectId("647e7404a3946828b9496351"), "name" : "Javascript", "pages" : 300, "price" : 500 }
> db.books.insertOne({name:'Finny Book', pages:1000, price:900, author:'John'})
{
        "acknowledged" : true,
        "insertedId" : ObjectId("647e7477a3946828b9496352")
}
> db.books.find()
{ "_id" : ObjectId("647e738ea3946828b949634e"), "name" : "The complete Java book", "pages" : 500, "price" : 1000 }
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "name" : "think in python", "pages" : 800, "price" : 4000 }
{ "_id" : ObjectId("647e7404a3946828b9496351"), "name" : "Javascript", "pages" : 300, "price" : 500 }
{ "_id" : ObjectId("647e7477a3946828b9496352"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : "John" }



