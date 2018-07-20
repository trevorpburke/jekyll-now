---
title: PostgreSQL Efficiency Tips - pgpass
tags: postgresql postgres psql Efficiency
---

Quick post today about one of my favorite and simplest tips to increase efficiency working with Postgres databases.

### <a name="pgpass"></a> pgpass

Testing environments exist to prevent failures and issues occuring in production application servers. Same exists for database servers. Often, I'll need to work with various testing environments depending on the request, client, or coworker.

To prevent having to input my database password everytime I access these environments via `psql` I have a `pgpass` file I keep within my home directory (`~/.pgpass` the '.' prefix obscures it from general file system viewing)

Here's what my `~/.pgpass` looks like (fictionalized here):

    testing_env_1:5432:client_123:trevorburke:pAsSwOrD1234  

The syntax here is:

    hostname:port:database:username:password

Because I'm often access databases with the same username, password, and port number my `~/.pgpass` looks more like this:

    *:5432:*:trevorburke:pAsSwOrD1234

The '*' character is a wildcard character that will apply my username and password to any hostname and database. Because my username and password is consistent across environments I don't need to list out each specific environment, but if my password is different i can simply add another line with the accompanying information.

