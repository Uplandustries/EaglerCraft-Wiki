---
title: Advanced Server Configuration
description: 
published: true
date: 2026-01-09T01:24:11.521Z
tags: 
editor: markdown
dateCreated: 2026-01-07T15:47:16.027Z
---

# Advanced Server Configuration

> If you have come here without first setting up a server, you are in the wrong place.
{.is-warning}

> We plan to eventually add an SSL guide here. Please be patient.
{.is-info}



## How to use a MySQL (or similar) skins database
Normally, EaglerXServer uses a SQLite database for caching skins. If you want to have a cache in a centralized database for access from other proxies, for example, you may want to set this up.

> This guide will not show how to set up a MySQL server, though there are many guides out there.
>
> MariaDB is a popular MySQL choice and [this getting started guide](https://www.mariadbtutorial.com/getting-started/connect-to-mariadb/) has useful information on setting up a MariaDB server, logging in, and creating a database.
{.is-info}

1. Download the JDBC driver from [Oracle](https://dev.mysql.com/downloads/connector/j/) selecting the “Platform Independent” option from the dropdown and selecting 'Download' on the .zip option.
2. Extract the .zip file and put the .jar file in your server folder (the same folder with your server jar and start script). Name it something that you can reference later such as `mysql-connector-j.jar`.
3. Open up your EaglerXServer `settings.yaml` (or `.toml` for Velocity) and scroll down to the ‘skin_service’ section.
4. Set `skin_cache_db_driver_path` to `“mysql-connector-j.jar”` (or whatever you named it)
5. Set `skin_cache_db_driver_class` to `“com.mysql.cj.jdbc.Driver”`
6. Set `skin_cache_db_sqlite_compatible` to `false`
7. Set `skin_cache_db_uri` to `“jdbc:mysql://HOST:PORT/DB?user=USER&password=PASS&sslMode=DISABLED&autoReconnect=true”`, replacing “HOST”, “PORT”, “DB”, “USER”, and “PASS” with the respective info for the database.
> You may also use the format `“jdbc:mysql://USER:PASS@HOST:PORT/DB?sslMode=DISABLED&autoReconnect=true”` for the URI if you wish.
{.is-info}
  - `HOST` could be a host name, IP address, or “localhost” to your MySQL server depending on your network.
  - `PORT` for MySQL defaults to 3306, but may be different depending on what you set it to.
  - `DB` is the database name you set up in your MySQL server.
  - `USER` is a username that has permissions to read and write to the database. 
  - `PASS` is the password for that user. If the password contains any of the following characters, they must be converted with percent encoding: 
        - `:`->`%3A`
        - `/`->`%2F`
        - `?`->`%3F`
        - `#`->`%23`
        - `[`->`%5B`
        - `]`->`%5D`
        - `@`->`%40`