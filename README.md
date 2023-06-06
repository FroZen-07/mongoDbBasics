# mongoDbBasics
# Basics Queries:

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
> db.books.insertOne({name:'Finny Book', pages:1000, price:900, author:['John', 'Doe']})
{
        "acknowledged" : true,
        "insertedId" : ObjectId("647e7533a3946828b9496353")
}
> db.books.find()
{ "_id" : ObjectId("647e738ea3946828b949634e"), "name" : "The complete Java book", "pages" : 500, "price" : 1000 }
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "name" : "think in python", "pages" : 800, "price" : 4000 }
{ "_id" : ObjectId("647e7404a3946828b9496351"), "name" : "Javascript", "pages" : 300, "price" : 500 }
{ "_id" : ObjectId("647e7477a3946828b9496352"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : "John" }
{ "_id" : ObjectId("647e7533a3946828b9496353"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : [ "John", "Doe" ] }
> db.books.update(
... {_id: ObjectId("647e738ea3946828b949634e")},
... {name:"Complete Reference Java", pages:450, price:700}
... )
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> db.books.find()
{ "_id" : ObjectId("647e738ea3946828b949634e"), "name" : "Complete Reference Java", "pages" : 450, "price" : 700 }
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "name" : "think in python", "pages" : 800, "price" : 4000 }
{ "_id" : ObjectId("647e7404a3946828b9496351"), "name" : "Javascript", "pages" : 300, "price" : 500 }
{ "_id" : ObjectId("647e7477a3946828b9496352"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : "John" }
{ "_id" : ObjectId("647e7533a3946828b9496353"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : [ "John", "Doe" ] }
> db.books.updateOne( {_id: ObjectId("647e7533a3946828b9496353")},{$set:{name:"Complete Reference Java", pages:450, price:700}})
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.books.find()
{ "_id" : ObjectId("647e738ea3946828b949634e"), "name" : "Complete Reference Java", "pages" : 450, "price" : 700 }
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "name" : "think in python", "pages" : 800, "price" : 4000 }
{ "_id" : ObjectId("647e7404a3946828b9496351"), "name" : "Javascript", "pages" : 300, "price" : 500 }
{ "_id" : ObjectId("647e7477a3946828b9496352"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : "John" }
{ "_id" : ObjectId("647e7533a3946828b9496353"), "name" : "Complete Reference Java", "pages" : 450, "price" : 700, "author" : [ "John", "Doe" ] }
> db.books.updateOne( {_id: ObjectId("647e7533a3946828b9496353")},{$rename:{name:"bookName"}})
{ "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 }
> db.books.find()
{ "_id" : ObjectId("647e738ea3946828b949634e"), "name" : "Complete Reference Java", "pages" : 450, "price" : 700 }
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "name" : "think in python", "pages" : 800, "price" : 4000 }
{ "_id" : ObjectId("647e7404a3946828b9496351"), "name" : "Javascript", "pages" : 300, "price" : 500 }
{ "_id" : ObjectId("647e7477a3946828b9496352"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : "John" }
{ "_id" : ObjectId("647e7533a3946828b9496353"), "pages" : 450, "price" : 700, "author" : [ "John", "Doe" ], "bookName" : "Complete Reference Java" }
> db.books.update({pages:800},{$rename:{name:"bookNName"}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> db.books.find()
{ "_id" : ObjectId("647e738ea3946828b949634e"), "name" : "Complete Reference Java", "pages" : 450, "price" : 700 }
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "pages" : 800, "price" : 4000, "bookNName" : "think in python" }
{ "_id" : ObjectId("647e7404a3946828b9496351"), "name" : "Javascript", "pages" : 300, "price" : 500 }
{ "_id" : ObjectId("647e7477a3946828b9496352"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : "John" }
{ "_id" : ObjectId("647e7533a3946828b9496353"), "pages" : 450, "price" : 700, "author" : [ "John", "Doe" ], "bookName" : "Complete Reference Java" }
> db.books.update({pages:800},{$inc:{price:50}})
WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })
> db.books.find()
{ "_id" : ObjectId("647e738ea3946828b949634e"), "name" : "Complete Reference Java", "pages" : 450, "price" : 700 }
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "pages" : 800, "price" : 4050, "bookNName" : "think in python" }
{ "_id" : ObjectId("647e7404a3946828b9496351"), "name" : "Javascript", "pages" : 300, "price" : 500 }
{ "_id" : ObjectId("647e7477a3946828b9496352"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : "John" }
{ "_id" : ObjectId("647e7533a3946828b9496353"), "pages" : 450, "price" : 700, "author" : [ "John", "Doe" ], "bookName" : "Complete Reference Java" }
> db.books.remove({_id: ObjectId("647e738ea3946828b949634e")})
WriteResult({ "nRemoved" : 1 })
> db.books.find()
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "pages" : 800, "price" : 4050, "bookNName" : "think in python" }
{ "_id" : ObjectId("647e7404a3946828b9496351"), "name" : "Javascript", "pages" : 300, "price" : 500 }
{ "_id" : ObjectId("647e7477a3946828b9496352"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : "John" }
{ "_id" : ObjectId("647e7533a3946828b9496353"), "pages" : 450, "price" : 700, "author" : [ "John", "Doe" ], "bookName" : "Complete Reference Java" }
> db.books.find()
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "pages" : 800, "price" : 4050, "bookNName" : "think in python" }
{ "_id" : ObjectId("647e7404a3946828b9496351"), "name" : "Javascript", "pages" : 300, "price" : 500 }
{ "_id" : ObjectId("647e7477a3946828b9496352"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : "John" }
{ "_id" : ObjectId("647e7533a3946828b9496353"), "pages" : 450, "price" : 700, "author" : [ "John", "Doe" ], "bookName" : "Complete Reference Java" }
> db.books.find().pretty()
{
        "_id" : ObjectId("647e73c6a3946828b949634f"),
        "name" : "think in Java",
        "pages" : 600,
        "price" : 2000
}
{
        "_id" : ObjectId("647e7404a3946828b9496350"),
        "pages" : 800,
        "price" : 4050,
        "bookNName" : "think in python"
}
{
        "_id" : ObjectId("647e7404a3946828b9496351"),
        "name" : "Javascript",
        "pages" : 300,
        "price" : 500
}
{
        "_id" : ObjectId("647e7477a3946828b9496352"),
        "name" : "Finny Book",
        "pages" : 1000,
        "price" : 900,
        "author" : "John"
}
{
        "_id" : ObjectId("647e7533a3946828b9496353"),
        "pages" : 450,
        "price" : 700,
        "author" : [
                "John",
                "Doe"
        ],
        "bookName" : "Complete Reference Java"
}
> db.books.find().limit(2)
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "pages" : 800, "price" : 4050, "bookNName" : "think in python" }
> db.books.find().limit(2).pretty()
{
        "_id" : ObjectId("647e73c6a3946828b949634f"),
        "name" : "think in Java",
        "pages" : 600,
        "price" : 2000
}
{
        "_id" : ObjectId("647e7404a3946828b9496350"),
        "pages" : 800,
        "price" : 4050,
        "bookNName" : "think in python"
}
> db.books.find().limit(2).sort({price:1}).pretty()
{
        "_id" : ObjectId("647e7404a3946828b9496351"),
        "name" : "Javascript",
        "pages" : 300,
        "price" : 500
}
{
        "_id" : ObjectId("647e7533a3946828b9496353"),
        "pages" : 450,
        "price" : 700,
        "author" : [
                "John",
                "Doe"
        ],
        "bookName" : "Complete Reference Java"
}
> db.books.find().limit(2).sort({price:-1}).pretty()
{
        "_id" : ObjectId("647e7404a3946828b9496350"),
        "pages" : 800,
        "price" : 4050,
        "bookNName" : "think in python"
}
{
        "_id" : ObjectId("647e73c6a3946828b949634f"),
        "name" : "think in Java",
        "pages" : 600,
        "price" : 2000
}
> db.books.find().sort({price:-1}).pretty()
{
        "_id" : ObjectId("647e7404a3946828b9496350"),
        "pages" : 800,
        "price" : 4050,
        "bookNName" : "think in python"
}
{
        "_id" : ObjectId("647e73c6a3946828b949634f"),
        "name" : "think in Java",
        "pages" : 600,
        "price" : 2000
}
{
        "_id" : ObjectId("647e7477a3946828b9496352"),
        "name" : "Finny Book",
        "pages" : 1000,
        "price" : 900,
        "author" : "John"
}
{
        "_id" : ObjectId("647e7533a3946828b9496353"),
        "pages" : 450,
        "price" : 700,
        "author" : [
                "John",
                "Doe"
        ],
        "bookName" : "Complete Reference Java"
}
{
        "_id" : ObjectId("647e7404a3946828b9496351"),
        "name" : "Javascript",
        "pages" : 300,
        "price" : 500
}
> db.books.find().sort({price:1}).pretty()
{
        "_id" : ObjectId("647e7404a3946828b9496351"),
        "name" : "Javascript",
        "pages" : 300,
        "price" : 500
}
{
        "_id" : ObjectId("647e7533a3946828b9496353"),
        "pages" : 450,
        "price" : 700,
        "author" : [
                "John",
                "Doe"
        ],
        "bookName" : "Complete Reference Java"
}
{
        "_id" : ObjectId("647e7477a3946828b9496352"),
        "name" : "Finny Book",
        "pages" : 1000,
        "price" : 900,
        "author" : "John"
}
{
        "_id" : ObjectId("647e73c6a3946828b949634f"),
        "name" : "think in Java",
        "pages" : 600,
        "price" : 2000
}
{
        "_id" : ObjectId("647e7404a3946828b9496350"),
        "pages" : 800,
        "price" : 4050,
        "bookNName" : "think in python"
}
> dbb.books.find({price:{$eq:4050}})
uncaught exception: ReferenceError: dbb is not defined :
@(shell):1:1
> db.books.find({price:{$eq:4050}})
{ "_id" : ObjectId("647e7404a3946828b9496350"), "pages" : 800, "price" : 4050, "bookNName" : "think in python" }
> db.books.find({price:{$gt:500}})
{ "_id" : ObjectId("647e73c6a3946828b949634f"), "name" : "think in Java", "pages" : 600, "price" : 2000 }
{ "_id" : ObjectId("647e7404a3946828b9496350"), "pages" : 800, "price" : 4050, "bookNName" : "think in python" }
{ "_id" : ObjectId("647e7477a3946828b9496352"), "name" : "Finny Book", "pages" : 1000, "price" : 900, "author" : "John" }
{ "_id" : ObjectId("647e7533a3946828b9496353"), "pages" : 450, "price" : 700, "author" : [ "John", "Doe" ], "bookName" : "Complete Reference Java" }
>


