<!--Title: Databases Overview -->
<!--Subtitle: What they are, why they are, when they are, and where -->

# What they are

Big file systems!  The biggest metaphor for a database is a giant spreadsheet.  The columns of the sheet would be the _structure_ of the databse.  The rows would be the actual data.  And so, with DB's there are two worlds: The Structure and the Content.

## The Content
This is the world of CRUD.  

## The Structure
This is database management: how do you add a column, how do you remove a column?  

The worlds are different enough that you'll use different methods to interact and maintain them and it is useful to be able to distinguish and handle both.

# Knex
A library for connecting and communicating with sql.  Like yarn, Knex requires a file to know what it's running and how (similar to the package.json for yarn).  You can create this with.
`yarn knex init`

For our purposes, we can really use the default settings of that knex file.  It tell us "we are going to be using sqlite and storing our data in a data folder with the extension .sqlite3"

## Migration
One of the first things we'll do.  It manages how we migrate data between different database structures.  (for example, having a 'todo-list" table that takes information from your 'people' database.  The file would help how we migrate data between these two tables.

You make a migration file with `yarn knex migrate:make`

The file will have two parts: `exports.up` and `exports.down`  The code we are moving up to our table will be handled with exports.up.

## createTable
In our migrations file we'll want to add a createTable funtion with the details of the structure and shape of our data.  For example:

```js
exports.up = function(knex, Promise) {
//We need to create a table if it doesn't exist yet, and so we'll return the values of the below function.
  Return  knex.schema.createTable('todos', function (table) {
      table.increments(); //When we save data to this table, it'll have an id that increments automatically.
      table.string('name'); //Tell the database it's handling 'string' data with the name 'name'.
      table.timestamps(); //Automatically creates a timestamp for when the data was added.
      })
  };
```

## Rolling Back

If you change your database after you've already migrated it, you can get a disconnect from what you _think_ it should be and how it looks to sql.  When this happens you can rollback yr migration to make your new change and migrate it back up.  You can do this with `yarn knex migrate:rollback`

## Important

If you've already deployed **do not edit your migration**.  Instead, make a new migration for these edits.

# Seed
This seeds your table with some test data 

You can make it with `yarn knex seed:make test-tasks`.  This will make a new seed in yr seed directory called test-tasks

**Migration works with Structure. Seed works with the data.**

# Running a file, like our todo
To run a command line file you want to make sure you say at the top of the file _how_ to execute a file.
`!/usr/bin/env node`

This tells the command line to use node, located at that path set, to execute the file.

Additionally, you need to have executable permissions on the file, you can do that with
`chmod a+x todo`  which says "change the modification rights so all can execute(a+x) the todo file.

## Process.argv

This is a command line argument.  essentially, the commands you pass are given to an array when you can see through process.argv. This is the context for where we defined our command and note variables at the top of our todo file.  

# Sqlite
A type of database that is "light".  It's a full-spec database, but doesn't require a separate server to be running like your big boy SQL.  So we can do stuff with it, but it may not be as resilient high-performance for bigger work.  

We'll be saving our data in a sqlite3 file that is readable by sql but not by us.   To have a more visual access to our database, we can use DB Browser for SQLite.


## Joining Data - Two tables

Vehicles
id:unique indentifier
* wheel - count
* engine-number
* speed-identifier
* colour
* accessories
* door-count
* model-**id**

vehicle table links to models table through the ** unique model id** aka **unique identifier** aka **prime key**

Models 
id: **unique identifier**
corolla - year


Database relationships
one to many
many to manay 
one to one

