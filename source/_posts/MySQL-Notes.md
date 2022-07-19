---
title: MySQL Notes
date: 2022-07-19 09:18:33
tags: MySQL
---

<h1>
    MySQL Notes
</h1>


This is a class note taken by tinf on [Coursera](https://www.coursera.org/learn/intro-sql/)

<!--more-->

<h2>
    Prepare Env (on Ubuntu)
</h2>
<h3>
    Install MySQL
</h3>

```console
sudo apt update && sudo apt install mysql-server
```

<h3>
    Put server on
</h3>

```zsh
sudo service mysql start
```

<h3>
    Log in to the server
</h3>

```zsh
mysql -u root -p
```




<h2>
    Basic operations (On MySQL-cli)
</h2>

<h3>
    Display all databases on server
</h3>

```sql
SHOW DATABASES;
```


<h3>
    Display all databases on server
</h3>

```sql
CREATA DATABASES "Database's name";
```


<h3>
    Choose database
</h3>

```sql
USE "Database's name";
```


<h3>
    Create table
</h3>

```sql
CREATE TABLE "Table's name"(
    "Column's name" "DataType" ("limmit"),
    "Column's name" "DataType" ("limmit"),
    .
    .
    .
);
```


<h3>
    Show details of table
</h3>

```sql
DESCRIBE "Table's name";
```


<h3>
    Insert data into table
</h3>

```sql
INSERT INTO "Table's name" ("column1", "column2", ...) VALUES ("Data1", "Data2", ...);
```


<h3>
    Delete data from table (with condition)
</h3>

```sql
DELETE FROM "Table's name" (WHERE "Condition");
```


<h3>
    Change content from table
</h3>

```sql
UPDATE "Table's name" SET "Target column's name" == "New content" WHERE "Target column's name" = "Target content"
```


<h3>
    Show data in table(with condition)(with fixed)(search keyword)
</h3>

```sql
SELECT * FROM "Table's name" (WHERE "condition") (ORDER BY "Column's name") (WHERE "Column's name" LIKE '%"Keyword"%');
```


<h3>
    Count number of data (with condition)
</h3>

```sql
SELECT COUNT(*) FROM "Table's name" (WHERE "Condition");
```


---


<h2>
    Data Types
</h2>

<h3>
    String
</h3>

<h4>
    Understand character sets and indexable for searching
</h4>

* CHAR : Allocates the entire space (for small strings and unknow length)
* VARCHAR : Depending on the date length (less space)

<h4>
    Usage: normal string data
</h4>


<h3>
    Text
</h3>

<h4>
    Have a character set but not used with index or sorting and can only prefix
</h4>

* TINYTEXT : up to 255 characters
* TEXT : up to 65K
* MEDIUMTEXT : up to 16M
* LONGTEXT : up to 16G

<h4>
    Usage: paragraphs or HTML pages
</h4>


<h3>
    Binary Type 
</h3>

<h4>
    8-32 bits depending on character set and not indexed or sorted
</h4>

* BYTE : up to 255 bytes
* VARBINARY : up to 65K bytes

<h4>
    Usage: small image or sensor signal
</h4>


<h3>
    Binary Large Object(BLOB)
</h3>

<h4>
    No translation, index, or character set
</h4>

* TINYBLOB : up to 255 bytes
* BLOB : up to 65K
* MEDIUMBLOB : up to 16M
* LONGBLOB : up to 4G

<h4>
    Usage: Large raw data, files, images, word doc, PDFs, movies
</h4>


<h3>
    Interger 
</h3>

<h4>
    little storage, easy to compare, sort , indexed
</h4>

* TINYINT : (-128, +128)
* SMALLINT : (-32768, +32768)
* INT : (2 Billion)
* BIGINT : (10**18 ish)

<h4>
    Usage: small image or sensor signal
</h4>


<h3>
    Float
</h3>

<h4>
   Wide range of values but limmilted accuracy
</h4>

* FLOAT(32-bit) : 10**38 with 7 digits accuracy
* DOUBLE(64-bit) : 10**308 with 14 digits accuracy

<h4>
    Usage: Scientific data
</h4>


<h3>
    Dates
</h3>

<h4>
    Represent time with integer
</h4>

* TIMESTAMP : 'YYYY-MM-DD HH:MM:SS'(1970, 2037)
* DATETIME : 'YYYY-MM-DD HH:MM:SS'
* DATE : 'YYYY-MM-DD'
* TIME: 'HH:MM:SS'

<h4>
    Buit-in MySQL function NOW()
</h4>


---


<h2>
    Relation Databases  
</h2>

<h3>
  1. Database design
</h3>

>1. Find the core of the database
>2. Use the core to create the first table
>3. Put non-duplicate columns into the first table
>4. Find relation between other columns and point to  more table
<h3>
    2. Database Normalization
</h3>

>* Do not replicate data, use point
>* Use integers for keys
>* Add special 'key' column to each table, for reference (By AUTO_INCREMENT)


<h3>
    3. Code for build a relation databases
</h3>

```sql=
CREATE DATABASE Music DEFAULT CHARACTER SET utf8;

USE Music;  (Command line only)

CREATE TABLE Artist (
  artist_id INTEGER NOT NULL AUTO_INCREMENT,
  name VARCHAR(255),
  PRIMARY KEY(artist_id)
) ENGINE = InnoDB;

CREATE TABLE Album (
  album_id INTEGER NOT NULL AUTO_INCREMENT,
  title VARCHAR(255),
  artist_id INTEGER,

  PRIMARY KEY(album_id),
  INDEX USING BTREE (title),

  CONSTRAINT FOREIGN KEY (artist_id)
    REFERENCES Artist (artist_id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE = InnoDB;

CREATE TABLE Genre (
  genre_id INTEGER NOT NULL AUTO_INCREMENT,
  name VARCHAR(255),
  PRIMARY KEY(genre_id)
) ENGINE = InnoDB;

CREATE TABLE Track (
  track_id INTEGER NOT NULL AUTO_INCREMENT,
  title VARCHAR(255),
  len INTEGER,
  rating INTEGER,
  count INTEGER,
  album_id INTEGER,
  genre_id INTEGER,

  PRIMARY KEY(track_id),
  INDEX USING BTREE (title),

  CONSTRAINT FOREIGN KEY (album_id) REFERENCES Album (album_id)
    ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT FOREIGN KEY (genre_id) REFERENCES Genre (genre_id)
    ON DELETE CASCADE ON UPDATE CASCADE
) ENGINE = InnoDB;


INSERT INTO Artist (name) VALUES ('Led Zepplin');
INSERT INTO Artist (name) VALUES ('AC/DC');

INSERT INTO Genre (name) VALUES ('Rock');
INSERT INTO Genre (name) VALUES ('Metal');

INSERT INTO Album (title, artist_id) VALUES ('Who Made Who', 2);
INSERT INTO Album (title, artist_id) VALUES ('IV', 1);

INSERT INTO Track (title, rating, len, count, album_id, genre_id)
    VALUES ('Black Dog', 5, 297, 0, 2, 1);
INSERT INTO Track (title, rating, len, count, album_id, genre_id)
    VALUES ('Stairway', 5, 482, 0, 2, 1);
INSERT INTO Track (title, rating, len, count, album_id, genre_id)
    VALUES ('About to Rock', 5, 313, 0, 1, 2);
INSERT INTO Track (title, rating, len, count, album_id, genre_id)
    VALUES ('Who Made Who', 5, 207, 0, 1, 2);
```



<h3>
    4. Put data back (JOIN)
</h3>

* Merge multilple databases and list all combinations

```sql
Database1 JOIN Database2 JOIN ...
```
    
* Filter to prevent JOIN from output all the combinations

```sql
ON "Foreign key of Database1" = "Foreign key of database2"
```
    
    
<h3>
    Types of keys
</h3>

* Primary key : Generally an integer AUTO_INCREMENT field
* Logical key : Generally a string for UI application to search (do not use logical key as primary key!!!)
* Foreign key : Generally an integer pointing to another table 
