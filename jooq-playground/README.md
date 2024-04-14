# JOOQ vs Hibernate

This project captures my understanding of Jooq vs Hibernate ORM framework in Java.

Personal experience of Hibernate/JPA in my projects

## Where Hibernate Outshines

* Hibernate/JPA takes an java object first approach where java objects are modelled.
* Hibernate makes it a breeze when directly working with the object model for simple CRUD ops.
* If writing becomes complex where we have to load 20 objects in memory and then do some operation,
  Hibernate is the best choice and was designed for this.
* Hibernate has a lot of features like lazy loading, caching, etc.
    * Hibernate has first level and second level caches which can result in optimised querying of
      data (https://vladmihalcea.com/jpa-hibernate-first-level-cache/)

## Where JOOQ Outshines

* JOOQ puts the database first approach. Databases can outlast application layer.
* JOOQ provides type safe way to write SQL queries and they are checked at compile time itself.
* JOOQ can be easy to use for developers who are comfortable with SQL.
* JOOQ code generation capabilities auto generates models basis the database and they are kept in
  sync by database management tools like liquibase/flyway.

## Hibernate Problems I faced

* Managing composite keys and when the relationships started getting deeper, it was difficult to
  perform object relational mapping.
* 1-1 relationships gets loaded eagerly because of JPA proxying. Resulting in additional queries,
  performance hibernate byte code enhancement didn't help either.
* N + 1 query issues are more probable when using hibernate with in-experienced developers, the N+1
  query issues can be caught in integrations tests buts it a tedious process for the reviewing
  developer.

## JOOQ Advantages I see

* Use JOOQ for OLAP for reporting/batch-processing.
* Write Queries are going to complex with JOOQ or plain SQL. (Hibernate should help here)
* Simple select queries and slightly complex read queries are going to result in optimised
  performance as we are leaving out the ORM's leaky abstraction.
* Type safety in writing SQL queries, unlike JPA where only at runtime we get to know whether the
  SQL is right.
* Simple DSL, code generation capabilities, type safety and performance are the key advantages of
  JOOQ.
* With that JOOQ was is not a replacement for Hibernate, it is a complement to Hibernate.

## Object Relational Mapping: The Vietnam of Computer Science (Ted Neward)

* Ted Neward draws a parallelization between the Vietnam war and the object relational mapping.

### Object Relational Impedance Mismatch

* Objects and relational databases are constructed differently.
* Objects are typically characterised by the following:
    * State - state is akin to data
    * Identity - unique identity of object distinct from the state.
    * Behaviour - The methods/functions for clients to interact with object
    * Encapsulation - hiding internal details, and provide evolutionary capability to objects
    * Types/Abstraction/Polymorphism.
* Relational Systems - Describe a form of knowledge storage and retrival based on predicates and
  truth statements.
    * Relational systema are characterized by the following:
        * Relation - A truth predicate about the world, a statement of facts that provides meaning
          to a predicate.
        * Attribute - An attribute describes a predicate
        * Tuple - It is the context to a relation.
        * Relation Value - A relation value is a combination of relations along with tuples
        * Relation Variable - Stores a set of relation values

* Trying to slave objects to fit the relational system is the impedance mismatch, where we ignore
  one half of the equation. This is synonmous with Kennedy's administration during the Vietnam war
  where he was not commited to an approach.
* As Westermoreland the war head of the American side during the war quoted (unleashing the full
  troops to Vietnam). Unleashing the objects fullest capabilities, left with some kind of hybrid
  object-relational mapping, preferable with some automations of the object-table mappn so that
  dev's can concentrate on the Domain Model. This is where the potential quagmire starts.

  
## References

* Hibernate First Level Cache: https://vladmihalcea.com/jpa-hibernate-first-level-cache/
* Martin Fowler's ORM Hate: https://martinfowler.com/bliki/OrmHate.html
* Reddit Post on Hibernate vs JOOQ https://www.reddit.com/r/java/comments/4mermo/what_are_your_thoughts_on_hibernate_vs_jooq/
* Google Groups Discussion by JOOQ Developer: https://groups.google.com/g/jooq-user/c/gmBf6g6sdQA
* https://web.archive.org/web/20220823105749/http://blogs.tedneward.com/post/the-vietnam-of-computer-science/
