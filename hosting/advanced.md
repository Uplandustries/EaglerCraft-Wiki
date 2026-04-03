---
title: Advanced Server Configuration
description: 
published: true
date: 2026-04-03T14:19:57.058Z
tags: 
editor: markdown
dateCreated: 2026-01-07T15:47:16.027Z
---

# Advanced Server Configuration

> If you have come here without first setting up a server, you are in the wrong place.
{.is-warning}

## How to support SSL (WSS)

To get wss:// to work (required for online clients), you need to set up SSL. There are different methods depending whether you are hosting on a VPS, server host, or localhosting. 


### With CertBot (free - VPS or local)

1. You need to be able to port forward freely; not just your main server. If you are hosting with a game host, you may not be able to. Otherwise, check the [Port Forwarding section on the main Hosting page](hosting#port-forwarding).
2. SSL must have a domain/subdomain to name associate the certificates with. You can get free subdomains at:
- [DuckDNS](https://duckdns.org)
- [FreeDNS](https://freedns.afraid.org) (FreeDNS tends to be faster and has more options)
Point it to your server's IP address. Either get it of your VPS provider's page, or go to [your IP](https://www.whatismyip.com) if you're at home, to get your IP.
3. Then you need to set up [CertBot](https://certbot.eff.org/) to generate the certificate for the subdomain. This will allow you to connect with `wss://your-new-subdomain.whatever.com:25565` (Of course with a different subdomain/domain and possible port)

> If you don't want to put in `:25565` for the port, you can set up an [NGINX reverse proxy](https://nginx.org)
> 
{.is-info}

### Using NGrok (free)

1. [Sign up on NGrok](https://dashboard.ngrok.com/signup)
2. [Set up an endpoint](https://dashboard.ngrok.com/get-started/setup/linux). Only do the Installation section, because we need to change some things in the Deploy command.
3. Go to [Domains](https://dashboard.ngrok.com/domains), click on the only entry (Dev Domain), and copy the domain (click the icon)
3. Run `ngrok http --url=the-stupidly-long-dev-domain-you-copied.ngrok-free.dev 25565` (replacing the domain of course)
4. Put `wss://the-stupidly-long-dev-domain-you-copied.ngrok-free.dev` into Eaglercraft (yes wss; no 25565)

> We plan to eventually add other methods for SSL here.
{.is-info}

## How to setup a newer server version (using ViaVersion)

Normally, the Minecraft servers must be the same version as the clients you plan on connecting, but this guide will show how to set up a newer server (even the very latest) to be compatible with almost any Java client version, including Eaglercraft 1.12.2, 1.8.8, and even 1.5.2 (with an additional plugin). This does have drawbacks, however, because Via* **does not actually port features** from newer versions; it works by **finding workarounds** (blocks released after 1.8 will be shown as placeholders from 1.8 for example). ___**If you choose this route, you should understand the shortcomings.**___

1. If you havn't already, follow the main [How to Host a Server](/hosting) guide up until setting up a backend server.

2. Download your prefered version
 - [Paper](https://papermc.io) is a highly recommended choice for almost any server, but there are other options.
 - Follow the 'Installing' and 'Configuring' parts of the [basic setup guide](/hosting#installing-the-server). (EULA and offline mode configs are the same)

3. Download ViaVersion, ViaBackwards, and ViaRewind from the [ViaVersion website](https://viaversion.com) (plus ViaRewindLegacySupport if you wish to have *even* better compatability with 1.8). Put these in the `plugins` folder.

> The latest version of ViaVersion is not directly compatible with  the current version of EaglerXServer (due to removal of reflection). As long as you don't put Via* plugins directly on the same server, you will be fine. **Via plugins go on the backend, while EaglerXServer is on the proxy.** This is another reason to setup EaglerXServer on a proxy instead of the backend server, even though it *may* work on just backend with some adjustments.
{.is-warning}

4. You may also install other plugins, such as AxSmithing (smithing table compatibility), or TuffX (for TuffClient), to the backend server for better compatibility.

5. If you wish to support Eaglercraft 1.5.2, install EaglerXRewind from the [EaglerXServer releases page](https://github.com/lax1dude/EaglerXServer/releases) to the **proxy**.

6. Start up both the client and proxy. You should be ready to join!

## How to use a MySQL (or similar) skins database
Normally, EaglerXServer uses a SQLite database for caching skins. If you want to have a cache in a centralized database for access from other proxies, for example, you may want to set this up.

> This guide will not show how to set up a MySQL server, though there are many guides out there.
>
> MariaDB is a popular MySQL choice and [this getting started guide](https://www.mariadbtutorial.com/getting-started/connect-to-mariadb/) has useful information on setting up a MariaDB server, logging in, and creating a database.
{.is-info}

1. Download the JDBC driver from [Oracle](https://dev.mysql.com/downloads/connector/j/) selecting the "Platform Independent" option from the dropdown and selecting 'Download' on the .zip option.
2. Extract the .zip file and put the .jar file in your server folder (the same folder with your server jar and start script). Name it something that you can reference later such as `mysql-connector-j.jar`.
3. Open up your EaglerXServer `settings.yaml` (or `.toml` for Velocity) and scroll down to the ‘skin_service’ section.
4. Set `skin_cache_db_driver_path` to `"mysql-connector-j.jar"` (or whatever you named it)
5. Set `skin_cache_db_driver_class` to `"com.mysql.cj.jdbc.Driver"`
6. Set `skin_cache_db_sqlite_compatible` to `false`
7. Set `skin_cache_db_uri` to `"jdbc:mysql://HOST:PORT/DB?user=USER&password=PASS&sslMode=DISABLED&autoReconnect=true"`, replacing "HOST", "PORT", "DB", "USER", and "PASS" with the respective info for the database.
> You may also use the format `"jdbc:mysql://USER:PASS@HOST:PORT/DB?sslMode=DISABLED&autoReconnect=true"` for the URI if you wish.
{.is-info}
  - `HOST` could be a host name, IP address, or "localhost" to your MySQL server depending on your network.
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