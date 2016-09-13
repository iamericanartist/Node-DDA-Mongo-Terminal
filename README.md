# MongoDB in the terminal

## Introduction

[MongoDB](https://www.mongodb.com/) is a free and open-source document-oriented databse. Data in MongoDB is stored in JSON-like documents with dynamic schemas.

### Installation

##### On a Mac
`brew update` and `brew install mongodb` should pretty much do it. Then `sudo mkdir -p /data/db` and `sudo chown -R $(whoami) /data`. `npm install mongo-hacker` can also be useful.

##### On other operating systems
https://docs.mongodb.com/manual/administration/install-community/

### Documents and Collections

In mongo, each database can be broken into multiple collections. For example, a database containing information about an NSS class could have a collection for students and a collection for teachers. Each collection will contain individual documents. A student document might contain information such as name, favorite color, birthday, and a list of likes. The data in each document is stored in JSON-like format. The values in each key : value pair can be almost any type (string, number, object, array, etc). In addition to the key : value pairs that you add, mongo will automatically add a key of "_id" with a unique  identifier. Since Mongo has a dynamic schema, documents within the same collection are NOT required to have the exact same sets of keys.

### Inserting Data

In order to [insert](https://docs.mongodb.com/manual/reference/method/db.collection.insert/) data, make sure you `use [name of database]`, then `db.[name of collection].insesrt()` and pass it the information you wish to insert in a json format. For example:
`
use nssClass
db.teachers.insert({
  name: "Scott",
  likes: ["Moe's", "koala bears", "javaScript"]
})
`

### Finding (Querying) data

The [.find()](https://docs.mongodb.com/manual/reference/method/db.collection.find/) method takes two arguments, the query, which specifies which fields of the document to search, and the projection, which specifies which fields to display. For Example:
`
db.teachers.find({name: "Scott"}, {name: true})
`
The query above returns the _id field and name. The _id is always returned unless specifically set to false.

[Query operators](https://docs.mongodb.com/manual/reference/operator/query/) can be used to create more specific searches. For example:
`
db.teachers.find({$or:[{name: "Caitlin"}, {name: "Callan"}]}, {favoriteColor: true})
`

You can also use good old regex:
`
db.teachers.find({name: /^C/ }, {favoriteColor: true})
`
### Updating Data

The [.update()](https://docs.mongodb.com/manual/reference/method/db.collection.insert/) method accepts a query and a json object of information. Beware, if you do not use a query operator, like `$set`  the entire document will be replaced by the json you pass to the update(). For example:
`
db.teachers.update({name: "Scott"}, 
                    {$set:{favoriteColor: "Green-ish"}})
`

The update method also includes an optional argument for options. "Upsert" will insert adocument if one does not already exist that matches the query parameters.

`
db.students.update( { name: "Jack"},
                    { $set:{favoriteColor: "Gray"}}, 
                    { upsert : true})
`

###Deleting data

The [.remove()](https://docs.mongodb.com/manual/reference/method/db.collection.remove/) method removes a documentfrom the collection. By default, .remove() will delete all documents that match the query parameter, unless you set the justOne option to true. For example:
`
db.students.remove( {name: "Dan"}, {justOne: true})
`

The [.drop()](https://docs.mongodb.com/manual/reference/method/db.collection.drop/) method takes no arguments and will drop the entire collection.

### More Mongo

Here's a neat [question](http://stackoverflow.com/questions/2298870/mongodb-get-names-of-all-keys-in-collection) on stackoverflow about how to get the names of all keys present in a collection.


## Topics Covered

-   Installation
-   Documents and Collections
-   .insert()
-   .find()
-   .update()
-   .remove()
-   .drop()

## Requirements

- instructions for how to install shared db

Import the sample dataset from mongoDB's [website](https://docs.mongodb.com/getting-started/shell/import-data/). This will import a database named "test" with a collection of "restaurants."

- instructions for how to record queries 

Create a markdown (.md) file where you can record the queries that return the requested information. You can then push the markdown file to github.

Provide the following:

1. Provide a query showing just the names (and nothing else) of the Italian restaurants.
2. Provide a query showing how many Bakeries have a name that start with M.
3. Provide a query showing the zip codes (and _id's) of all restaurants with the word "Ice" in their cuisine.
4. Provide a query showing the street and street number of Chinese restaurants in ascending order by zip code.
5. Show only the American restaurants in Manhattan.
6. Provide a query showing the restaurants that have been graded exactly 4 times.
7. Provide a query showing only _id, name and 2 grades from each restaurant on Broadway.
8. Provide a query showing the 5 pizza restaurants in the Bronx with the highest score on an evaluation.
9. Provide a query to find all of the restaurants in Brooklynn and list only the 51st-60th results when ordered alphabetically by name.
10. Provide a query that returns all pizza and Italian restaurants in reverse alphabetic order.


## Additional Reading

-   [MongoDB](https://www.mongodb.com/)
-   [.insert()](https://docs.mongodb.com/manual/reference/method/db.collection.insert/)
-   [.find()](https://docs.mongodb.com/manual/reference/method/db.collection.find/)
-   [.update()](https://docs.mongodb.com/manual/reference/method/db.collection.insert/)
-   [Query operators](https://docs.mongodb.com/manual/reference/operator/query/)
-   [.remove()](https://docs.mongodb.com/manual/reference/method/db.collection.remove/)
-   [.drop()](https://docs.mongodb.com/manual/reference/method/db.collection.drop/)


***  
[Original Link](https://github.com/nashville-software-school/node-milestones/blob/mongo-cs/03-database-driven-application/exercises/02-mongo-terminal.md)
