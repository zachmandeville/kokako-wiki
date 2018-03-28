<!-- Title: CRUD and REST -->

# C.R.U.D
CRUD refers to the four things you do with data:

CREATE
READ
UPDATE 
DELETE

Not only do you have CRUD on objects, but also on the routes you are using.  You can think about CRUD around HTTP verbs, then:

CREATE // POST
READ // GET
UPDATE // PUT/PATCH
DELETE // DELETE

# RESTful

RESTful is a convention for how to set up your routes on a server.  As long as everyone follows these conventions, then working with how to CRUD them routes will be easier. 

# CRUD with MEOWTOWN

CREATE // POST // /cats  (I would like to create a new thing to be stored amongs the /cats)
READ // GET / /cats  /cats/1 (I would like to read a cat that exists among the /cats)
_or_
/cats/new (may I please have the paperwork to create a new cat.)
_or_
/cats/1/edit (May I  please edit the specific cat from among the /cats)
UPDATE // PUT/PATCH // /cats/1 (I would like to edit the details of this cat within /cats/)
DELETE // DELETE // /cats/1 (I would like to delete the 1 cat from among the /cats)

# To See More
[guides rubyonrails routing html](http://guides.rubyonrails.org/routing.html)
