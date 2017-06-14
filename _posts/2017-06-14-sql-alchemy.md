---
layout: post
title: SQLAlchemy
tags: learning_notes SQLAlchemy
---
## {{page.title}} ##
## What is it?
- a database toolkit and object-relational mapping (ORM) system for the Python programming language
- using the Python Database API (DBAPI) for database interactivity.

### SQLAlchemy's Approach to Database Abstraction
By exposing relational concepts, SQLAlchemy embraces the idea of **"leaky abstraction"**, encouraging the developer to tailor a custom, yet fully automated, interaction layer between the application and the relational database.

dividing the task into two main categories known as **Core** and **ORM**.

SQLAlchemy layer diagram
![SQLAlchemy layer diagram](../images/sqlal-layers.png)

### Compilation
The central class responsible for rendering SQL expression trees into textual SQL is the `Compiled class`.

- SQLCompiler handles data query and manipulation
- DDLCompiler handles CREATE and DROP statements
- TypeComiler focused around string representations of types

*classical mapping*: This form considers the `Table` object and the user-defined class to be two individually defined entities which are joined together via a function called `mapper`.

### `Session` object
loading and persisting data

The job of the **unit of work** is to move all of the pending state present in a particular `Session` out to the database

`Session` provides the entrypoint to acquire a `Query` object, which sends queries to the database using the `Session` object’s current database connection, populating result rows into objects that are then stored in the Session, inside a structure called the `Identity Map`