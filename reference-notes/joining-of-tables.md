<!-- Title: Joining of Tables -->
<!-- Subtitle: Sweet SQL Moves -->

# Background
When the item we are trying to store becomes more complex, it is useful to separate all their qualities into different tables.

For example: imagine a database of cars.  Cars could have different models, colors, wheels, accessories, add-on features. ETC. It is common to separate these qualities into different tables, then join the tables based on what someone is viewing.

# Why do we bother?
- It allows you to separate concerns, as more people are accessing the database you can have them only access the table they are concerned about (wanting to update their accessories without buying a whole new car for example).
- Allows for complex combinations that are closer to what we find in real life.

# 'Key' Terms
## Foreign key ID
When you have multiple tables, one needs to be aware of the other.  You can have a single model, that comprises multiple vehicles.  And so the vehicle table would need to be aware of the model table.  You can do this with a foreign key id.

In the vehicles table, youd add a new column called 'model id'.  So you can then give an ID to each  model in your model table, and reference it in a column in the vehicle table.

## Primary Key
Within a table, the unique ID for each row of the table.  Each row needs to be unique, and so you would not repeat the ID's as that would make it so two different unique items are trying to exist in the same row of a table.

# Joining Tables with Knex
So!  We know what diff. tables are and why they important.  how do we join them to bring all that data together?

If we wanted to see all models of cars we can do:
`db('models').select('id','name')`
This would give us the id and name of all rows in our models table.

If we wanted to see all vehicles we could do:
`db('vehicles').select()`
This would give us all rows in the vehicles table.

If I wanted to see all red vehicles, I would do:
`db('vehicles').where('color,'red').select()`
This would select all rows from the vehicles table where the color column has the value red.

Now, what if we want to select vehicles that are corollas?  In other words, the vehicles table has to reference the model table.  To do this, you'd write:
````js
db('vehicles').join('models','model_id','=','models.id')
              .where('models.name','corolla')
	      .select()
```

So the first line is joining the two models together, with the point of commonality is the model_id in the vehicles table and the models id column (represented as `models.id`).  In other words, when we were adding new cars to our vehicles table, we were diligent with what number we put in the models_id.  Now we are saying "this column equals the models.id column and so we can join the information from both and know we are talking about the right things.

The select is going to grab _all_ the column data from both tables (since we joined them at the beginning).  So you may want to limit what data you return by chaning the `.select()` command to:
`.select('vehicles.id','models.name')`  
This would return the vehicle ID and the model name that vehicle is.


# Many to  Many

If you have a situation where a row in one table can have multiple entries in another table, you'll have a many to many relation.

A good example is a student who could be a part of many different groups, and you want to run a query to see what groups they are a part of.  There'd be a student table, and there'd be a groups table.  You couldn't map direct one to one, as you'd end up with impossible double entries.  So, instead, you make a _third_ table: students in groups.  This would reference the group id and the student id, and allow you to have multiple entries then for one student per group they are a part of.
