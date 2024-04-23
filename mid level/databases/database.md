Where you store your data permanently, saving the data permanently on [[Physical memory]]. **MOSTLY** are [[relational database]] or [[non relational database]], the key difference being where you can create [[relational database|foreign keys]], and the way the data is stored on a low level

Databases are far and wide, most of them use a [[database manager]], or you can talk to them directly, most common for smaller databases like sqlite or cloud databases like firestore. Even the definition of database is complicated, something like [[redis]] can be used as a database

> [!info]
> Databases must be running on a [[port]] (postgresql default is 5432) 
> to connect to a cloud database you need the full [[socket]]

# types of databases

as i said, mostly there are two, [[relational database]] and [[non relational database]] (noSql), but here are some other **paradigms** (there are many more), i have included some information on when to use them and some examples, but remember the [[CAP theorem]], each has some great advantages and some great drawbacks

## relational
check the [[relational database]] for an actual in-depth explanation but for comparations. But remember that generally **SQL** databases are **slower** for **writing** than NoSQL databases Meanwhile they are **faster** for **reading**

>[!example]
>- PostgreSQL: the most **reliable** and capable of handling big and complex amounts of data
>- MySQL: a great option as well
>- SQLite: a smaller DB, perfect for **embedding** a db on some other software or for few users
>- cockroachdb: When you want PostgreSQL but scaling horizontaly

### when?
- Lot of **reads** and **writes** and **updates**
- You want **speed** on complex queries, but don't want as much speed (b-trees under the hood)
- You want to perform **complex relations** with your data
- You want to **query** and **join** multiple values
-  You have a **strict** structure you will always follow
- You want to use [[SQL]]
- You need a robust Database ACID compliance
- In reality **most** of the **use cases** can be done with this DBs
- Can be  **primary database**


## key-value
Every key is unique and it points to a value, it normally works with a [[hashmap]] under the hood (some DB use other solutions). There are no queries nor joins or any complex thing. And you can **store anything**, a string, a full json object, whatever. you simply can **set** a new value and **get** and old one. This are the **FASTEST** databases. As so they are mostly used for caching data and a lot of the times live on memory only.

>[!example]
>[[redis]], memcache and aws [[elasticCache]].
It's worth mentioning that aws [[dynamoDB]] and [[S3]] also works like this type of DB.

### when?
- Lot of **reads** and **writes**
- You want **speed**
- You want to cache data
- You always retrieve the **full object**
- You want to query a **single value**
- **don't** want to create relations in between different data
- **don't** want to **process data** before receiving it 
- Most likely **not primary database**

## wide column
Similar to key-value (actually uses a Log-structured merge tree), but now you have multiple value spaces, so you can save the user data un different columns. There is **no** **schema** and therefore **no joins** but you **can query**. It handles unstructured data. It's **easier to scale** and scales horizontally great. It can't use [[SQL]] so each DB uses a different query language (CQL for cassandra and scanning on hbase). These databases have 2 main keys, a **partition** key and a **filtering** key, with these you can divide the data in as many partitions as needed and order them as you **wish**

It's great to store time series data and **historical records** that won't be used in this precise moment, like netflix that uses it to store the users viewing preferences and later analyze them (you can save in one column the time and in the other the actual values, and then query them based on time) an example of this is 
```cql
SELECT * FROM myTable WHERE t = '2017-01-01' - 2d;
```

>[!example]
> **cassandra** and apache **hbase**

### when?
- **Lot** of writes, **low** reads and updates
- You have data that doesn't have a defined structure
- Need to scale horizontally 
- want **minimal** processing of data before receiving it (you can query and use where, but there are no joins)
- You are not going to use [[SQL]]
- You want to query **multiple values**
- You want a good amount of **speed**
- Most likely **not primary database**


## document oriented (NoSQL)

These are most likely the ones you think when you mention [[non relational database]]. You store documents as the values in a key-value paradigm, documents are anything you want, but mostly objects like a JSON or BSON. They **don't** use a **schema**, and are unstructured, on this DB is common practice to **denormalize** your data, this means to repeat as much as possible (because there are no joins (unless there are like on mongo) ). 

The **biggest strength** of this DBs can be it's ability to **scale**, the can be scaled horizontally perfectly via **sharding** (**partitioning**) and are also great for big data storage, you create your partitions based on your primary key hash (the keys lesser than x go to partition A while the keys greater than x go to partition B) 

Most times documents are **grouped** in **collections** that can have subCollections, these collections are somewhat as tables. Fields in a collection can be indexed to be searched, and there can be a hierarchy on the collections. As you can see these DBs try to create some query structure while maintaining non strictly relational, but this **queries** are extremely **slow**, if you find yourself doing a lot of queries on this DBs you should have used a relational. These DBs are fast on reading but slower on writing

>[!example]
> - **mongoDb**
> - **firestore** (from firebase)
> - aws dynamoDB, documentDB and s3 (s3 is a object oriented DB but it's bassicly the same)

### when?******
- **Lot** of writes, **lower** reads, and **NO updates** (singular updates, if you want to change, **change all** the document)
- You get a lot of **unstructured** data
- You want to **scale** 
- You want a **easy** solution
- **Don't** need to **process** the data as much
- The data schema you receive constantly changes
- You want a good amount of **speed**
- can be **primary database**


## search engine

As the name implies, are the best databases for search engines, You enter some text (a title) and they create indexes to categorize the similar characteristics among data. This also works on auto completion of words. Finally the data stored on the db can be enhance with multiple algorithms that can solve typos an other errors 

>[!example]
> - aws **OpenSearch** and **orama** 
### when?******
- You have a **search engine** and want to improve it
-  **never a primary database**

## Graph
Databases that structure their data as nodes, and it's relations as the edges of the graphs, This are mostly used for specific applications as recommendation engines, And are the best databases to store relations

> [!example]
> **Neo4j** and aws **neptune**

### when?
- If you really need to store relations between a great amount of users 
- If you need something like this you will know it, they are very niche
- **never a primary database**

## vector
For storing previous machine learning inputs and their embeddings, These are very niche for **[[AI]]** cases where you need to store the state of any deep learning or LLM program. You can save this on normal DBs and there are some implementations like pgvector for postgresql

> [!example]
> There are multiple contenders but currently no one has been decided as the best

### when?
- When creating a Very big **AI** project where saving the state is necessary
- **never a primary database**