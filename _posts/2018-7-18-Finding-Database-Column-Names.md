---
layout: post
title: Navigating an Unfamiliar or Confusing Database
---
## A Tale of `psql` Tricks

Thus far in my career I've worked with varyingly complex databases, from well-documented with foreign keys explicitly defined to absolute mayhem. This range of DDL quality has led me to one of the most useful tools within the PostgreSQL ecosystem: `information_schema`

When I'm searching for a key to join tables or searching through hundreds of tables within a database for a certain value I rely on `information_schema.columns`

Here's a sample of this table:

                         View "information_schema.columns"
          Column          |                Type                | Modifiers 
    --------------------------+------------------------------------+-----------
    table_catalog            | information_schema.sql_identifier  | 
    table_schema             | information_schema.sql_identifier  | 
    table_name               | information_schema.sql_identifier  | 
    column_name              | information_schema.sql_identifier  | 
    ordinal_position         | information_schema.cardinal_number | 
    column_default           | information_schema.character_data  | 
    is_nullable              | information_schema.yes_or_no       | 
    data_type                | information_schema.character_data  | 


So, let's say I need to find tables that contain the value `entered_date` because I need to update some records, but I don't know all the tables that contain this value. Here's how I'd find them:

    SELECT 
      table_name,
      column_name
    FROM information_schema.columns
    WHERE column_name = 'entered_date';

Though this is beyond the scope of this post, I could then use a little Bash to UPDATE the `entered_date` value from those tables.

    #!/usr/bin/bash
    declare -a arr=("table_1"
                    "..."
                    "table_15")
    for i in "${arr[@]}"
    do
        psql -h HOSTNAME -U user database -c "UPDATE $i SET entered_date = '2018-07-18' WHERE id='123456'"
    done 

