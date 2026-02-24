---
title: Entity-Relationship
draft: false
tags:
  - computer-science
  - database
aliases:
  - ER
---
### Data Modelling

[[Data Modelling]] is a design process, that maps requirements to a data model. It is typically used for planning a database structure, as well as to present such structure to non-technical people.

__Main steps__:
- Describe information in database.
- Describe relationship between data items.
- Describe constraints on data

A model usually consists of inter-related entities.

An [[ER Diagram]] is a self-contained description of the database schema.

[[Attribute]] - a data item, and is described as a circle.
[[Entity]] - a collection of data items, described as a rectangle.
[[Relationship]] - Associations between entities, describes as a rhombus.

When linking [[relationships]], a thick line represents [[total participation]], which means an entity __must__ participate in the relationship, whereas a thin line represents [[partial participation]], which means an entity __can__ but isn't required to participate in the relationship.

![[entity-relationship diagram.jpg]]

Arrows represent cardinality: when there's no arrow, that means many instances of that entity can have a relationship with the other entity, when there is an arrow pointing towards an entity, this means that only __one__ instance of that entity can have a relationship with the other entity.

### Inheritance

An entity can be a superclass or a subclass of another entity, and it is represented by an "isa" triangle pointing towards the subclass.![["isa" inheritance diagram.jpg]]

When a superclass has more than one subclass, to specify that one subclass overlaps with another, or it explicitly doesn't. We use an "o" for overlaps, and "d" for disjoint.![[overlapping disjoint diagram.jpg]]

### Weak Entities

A [[weak entity]] is an [[entity]] whose existence depends on another entity. For example, an emergency contact.

It has no key of its own, it instead has a discriminator.![[weak-entity diagram.jpg]]

### Types of Data Models

- [[ER Model]] - World is modelled via entities, relationships, attributes.
- [[Relational Model]] - World is modelled via tuples, relations, and constants.
- [[SQL schemas]] - Good approximation of [[Relational Model]].

### [[Relational Model]]

Mapping an [[ER Model]] to a relational schema.

Attributes --> attributes + domains + constraints.
Entities --> tuples, entity sets --> relations.
Relationships --> relations + constraints.

##### Mapping Rules:
- Each entity becomes a table.
- Each attribute becomes a column with a type.
- The key attribute becomes the primary key.
- A 1:N relationship becomes a foreign key in "many" table.
- An N:M relationship becomes its own table with 2 foreign keys.
- Attributes on a relationship become columns in that table.