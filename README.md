MongoDB is an open-source document-oriented NoSQL database that is designed to store a large scale of data and also allows you to work with that data very efficiently. It stores data in the form of JSON documents. MongoDB provides a SQL-like query language to query records based on the internal structure of the document itself. Document stores provide high flexibility and are often used for working with occasionally changing data.

In this post, I will mention a few MongoDB commands which are used more frequently by the developers.

## Index

* [Database Operations](#database-operations)
* [Collections](#collections)
* [Create Documents](#create-documents)
* [Read Documents](#read-documents)
* [Update Documents](#update-documents)
* [Delete Documents](#delete-documents)
* [Sorting](#sorting)
* [Limit and Offset](#limit-and-offset)
* [Add and Drop Index](#add-and-drop-index)
* [Range Queries](#range-queries)
* [Text Search](#text-search)

<hr>

### Database Operations
#### 1. Show All Databases
```
show dbs
```

#### 2. Show current Database
```
db
```

#### 3. Create or switch to new Database
```
use hashnode
```

#### 4. Delete Database
```
db.dropDatabase()
```

### Collections

#### 1. Show All Collections of Current Database
```
show collections
```

#### 2. Create new collection
```
db.createCollection('posts')
```

### Create Documents

#### 1. Insert One document
```
db.posts.insertOne(
   {title: "blog post title", body: "blog post content"}
)
```
or 

```
db.posts.insert(
   {title: "blog post title", body: "blog post content"}
)
```

#### 2. Insert Multiple document
```
db.posts.insert( [ 
    {title: "blog post 1 title", body: "blog post 1 content"},
    {title: "blog post 2 title", body: "blog post 2 content"},
])
```


### Read Documents

#### 1. Find One document
```
db.posts.findOne()
```

#### 2. Find Multiple documents
```
db.posts.find()
/* returns a cursor - show 20 results - "it" to display more */
```

#### 3. Find Multiple documents with formatted json
```
db.posts.find().pretty()
/* returns a cursor - show 20 results - "it" to display more */
```

#### 4. Find documents by field value.
```
db.posts.find({'title' : 'blog 1 title'})
```

### Update Documents

#### 1. Update one
```
db.posts.updateOne({"_id": 1}, {$set: {"title": 'updated title'}})
```

#### 2. Update Multiple 
```
/* update only specific fields */ 
db.posts.update({"category": "technology"}, {$set: {"category": 'computer science'}})
```
#### 3. Upsert complete Row
```
db.posts.update({ '_id' : 1 },
{
  title: 'Post one',
  body: 'New body for post 1',
},
{
  upsert: true
})
```

#### 4. Increment Field Value
```
db.posts.update({ "_id": 1 },
{
  $inc: {
    views: 5
  }
})
```

### Delete Documents
#### 1. Delete
```
db.posts.remove({ title: 'Post 1' })
```

### Sorting
#### Fetch results by sorting on field.
```
# ascending order
db.posts.find().sort({ title: 1 }).pretty()

# descending order
db.posts.find().sort({ title: -1 }).pretty()
```

### Limit and Offset
#### Fetch results by pagination.
```
/* Skip 3 results*/
db.posts.find({}).skip(10)

/* Fetch only 3 results*/
db.posts.find({}).limit(3)

/* Sort by title , Skip first 10 results, fetch only next 3 documents*/
db.posts.find({}).sort({"title": 1}).skip(10).limit(3)
```

### Add and Drop Index

#### 1. Add Index
```
/* Create Index on single field */
db.posts.createIndex({"title": 1})  

/* Create compound Index */
db.posts.createIndex({"title": 1, "date": 1})  
```

#### 2. Drop Index
```
db.posts. dropIndex("title_1")  

```

### Range Queries

#### Find documents by range query
```
/* find posts where views are greater than 50 */
db.posts.find({'views' : { '$gt' : 50 }})

/* find posts where views are greater than or equal to 50 */
db.posts.find({'views' : { '$gte' : 50 }})

/* find posts where views are less than 50 */
db.posts.find({'views' : { '$lt' : 50 }})

/* find posts where views are less than or equal to 50 */
db.posts.find({'views' : { '$lte' : 50 }})
```


### Text Search

#### 1. Create Text Index on field
```
db.posts.createIndex({content: "text"})
```
#### 2. Search by Text
```
db.posts.find({
  $content: {
    $search: "post content"
    }
})
```

<hr/>

## Thank you for reading
Hope you find these resources useful. If you like what you read and want to see more about system design, microservices, and other technology-related stuff... You can follow me on 
- [Twitter here](https://twitter.com/vishnuchi).
- Subscribe to my newsletter [here](https://www.getrevue.co/profile/vishnuch).

<a href="https://www.buymeacoffee.com/vishnuchi" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 150px !important;" ></a>


