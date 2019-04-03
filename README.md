Database Jones
==============

Introduction
------------
See our latest presentation [on slideshare]
(http://www.slideshare.net/jdduncan/building-nodejs-applications-with-database-jones).

This package provides a fast, easy, and safe framework for building 
database applications in Node.js. 

Here is an example using Database Jones to store a single object (a JSON literal)
into an existing MySQL table:
```
var jones = require("database-jones");

var connectionProperties = new jones.ConnectionProperties("mysql");

jones.openSession(connectionProperties).then(
  function(session) {
    var user = { id: 1, name: "Database Jones"};
    return session.persist("user", user);
  }).
  then(function() { console.log("Complete"); }, console.trace).
  then(jones.closeAllOpenSessionFactories);
```

Key features include:

+ Simple API for create, read, update, delete
+ Bulk operations for high performance
+ Support for ACID transactions, both explicit and implicit
+ Flexible mapping from JavaScript objects to relational tables
+ A fluent Query language using domain model tokens
+ Default mapping of a relational table to a simple object 
+ Projection of several related tables to a complex object structure
+ Asynchronous API using well-known node.js callback patterns
+ Promises/A+, allowing easier management of callbacks
+ Connection pooling, allowing in-process scale up

Quick Install
-------------
The whole project can be used directly from a github clone if *core.symlinks* 
is set to true.
```
git config --global --add core.symlinks true
git clone http://github.com/mysql/mysql-js
```
To use the mysql adapter, you will also need node-mysql.

To use the ndb adapter, you need MySQL Cluster, and you must use node-gyp to build
the C++ source code under jones-ndb.  

Sample applications 

More information
----------------
See the complete README.md file under [database-jones](database-jones/README.md)


Directory Structure
-------------------


* database-jones

  Lightweight object mapping layer for SQL and NoSQL databases.  
  
* jones-mysql

  Jones adapter for MySQL.  Licensed GPL v2.  Requires node-mysql.
  
* jones-ndb

  Native Jones adapter for MySQL Cluster.  Licensed GPL v2. 
  Uses the low-level NDBAPI for data operations, but requires jones-mysql
  for certain metadata operations such as creating tables.

* jones-test

  A high-performance stand-alone test harness.  Jones-test is able to manage
  concurrent and serial tests, run hundreds of tests per second, and run 
  combined test suites from several projects (for instance, running both 
  the common database-jones tests and the jones-mysql specific tests all
  from a single test driver).   
  
* jones-promises

  An implementation of Promises/A+ used by database-jones. 
  
* unified\_debug 

  A printf-style debug library providing a single diagnostic 
  environment for both C and JavaScript. 

* perftest

  Contains jscrund, a simple benchmarking tool for Jones.
  
* loader

  A data loader implemented as a Jones application

* samples 

  Sample code using Jones

* shell

  A database command shell based on Jones


