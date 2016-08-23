# Readmes
# Redis week

Split up into groups of four (one person from each team). Each team should tackle one of the following topics:

## Redis data structures & folder structure

#### Redis data structures
There are a lot of data structures contained in Redis but you haven't had the chance to use many, so we want you to do a bit more research into them and recommend the most useful ones. We particularly want you to look into:

* [ ] Lists
* [ ] Sets
* [ ] Sorted sets
* [ ] Hashes

#### Folder structure
There has been a bit of confusion about how teams should organise their code so please do some research and recommend a solid folder structure. A good way would be to look at existing projects on GitHub and analyse their folder structure.

* [ ] What are some common ways of organising your files?
* [ ] Give some examples of repos with different folder structures. Do you understand why they have been organised like that?
* [ ] How many files should be in your root folder?
* [ ] Can you recommend some best practices for how your folder's tree structure should look?
* [ ] What are the best practices for the naming of files?

## Redis connections and best practice

#### Connections

* [ ] How can Redis be deployed to Heroku? Recommend a method.
* [ ] What is Redis Pub/Sub and when is it useful? How can it help to scale applications?
* [ ] What are Redis connections and why can they be troublesome?
* [ ] Why is dwyl's redis-connection the best thing since sliced bread?

#### Redis Best Practice

* [ ] What is persistence and why is this important for databases?
* [ ] What are the different ways of achieving persistence with Redis? Which should you use?
* [ ] Why might you need to optimize Redis?
* [ ] Provide some examples of Redis optimization?


## Websockets & script injections

#### Websockets

We want our web apps to have real-time functionality (because who doesn't these days?) so you'll need to research a bit about websockets:

* [ ] What are websockets?
* [ ] Why are they used?
* [ ] How are they different from HTTP request/response patterns you've seen before?

#### Script Injections
Now that you're using databases, you're opening your web apps up to some serious security vulnerabilities, one of which is script injections.

* [ ] What are HTML script injections?
* [ ] What are some examples?
* [ ] How can you protect against them in your apps?


## Mocking & testing
#### Mocking
Some people like to mock databases for the purposes of testing; we suggest having a debate on the pros and cons of mocking.

* [ ] What does mocking mean in relation to testing?
* [ ] What are some advantages and disadvantages of mocking?
* [ ] Why might it be unreliable?
* [ ] How might you mock a redis database?

#### Testing
* [ ] How can you test your Redis database fully without mocking?
* [ ] How do you ensure you don't fill your database with test insertions?
* [ ] How do you test for error cases?
* [ ] Why do Redis Connections affect tests?(See Dwyl Redis-connection)


## Task for all: write a README summarising your research on these topics.

# Postgres week

Get into 4 jigsaw groups and research the following main topics. Each team will produce a short readme, as well as a brief presentation and/or a tutorial.
### Why Postgres / SQL databases (or not)?
A **presentation** on the following:
* SQL vs NoSQL databases:
  * differences
  * pros and cons
* When to use which and why? Give example use cases.
* Why do some projects use both?

### Choosing tables structure and joining
* Best practices in table structures (e.g. normalization)
* What is a primary key and why is it useful?
* How do you join separate tables?
* Differences between inner / outer joins
* Give a practical example of a database with at least 2 tables.
Follow some of the best practices you found out (e.g. for people records). The example can even be "on paper".

### PG with Node and Heroku
Give a practical tutorial (for your peers to complete) on the following:
* connect to a local pg database from your node server;
* apply some SQL commands of your choice to retrieve and modify a database;
* create a heroku test app with postgres and access the database with SQL commands:
  * from node;
  * from the command line.

### Importing, exporting and migrating databases
Write a readme including:
* A practical walk-through on how-to:
  * import databases from an existing project
  * export databases
* Migrations in Postgres