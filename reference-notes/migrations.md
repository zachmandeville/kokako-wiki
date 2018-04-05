<!-- Title: Migrations -->
<!-- Subtitle: A detailed study of how they work and when to use them. -->

# Scenario

People table that has an address index.  But the people keep adding new addresses.  So you realize that you need to have a separate 'addresses' table.  We want to migrate all the addresses to this new table.  In this case--we need MIGRATIONS!

# Migrations
Our Scenario for above has 5 migrations:
1. Create people table
2. Add batch address and rename address to home address
3. Add work address
4. Create Address Table
5. Move Adddress Data

The point of migrations is to allow the database structure to change over time.

# Migration structure
up and down:  the up moves forward in time, the down migration moves backwards in time.

## Side note: 
For this bootcamp, we should focus on the up.  the down is hard to comprehend right now, and we can instead--when we face an issue -- just delete the db and migrate up again.


