---
title: Hosts
description: Hosting providers that support Eaglercraft servers
published: true
date: 2026-03-19T19:55:12.961Z
tags: 
editor: markdown
dateCreated: 2026-01-07T15:44:59.660Z
---

# Hosts
In order to have a eagler server you need a VPS service, Dedicated Server or a Selfhosted Server

> There is no official host that Eaglercraft uses!

A few recommended VPS (and dedicated host) services are listed below (but keep in mind these are not the only options):

> Both a VPS (Virtual Private Host) and a dedicated host (seperste physical machine) allow you to run almost any servers/software within your allocated specs, unlike many common Minecraft server hosts which are usually one-click setup, restricting you to specific software.
{.is-info}


### Dollar Dollar Nodes (https://ddnodes.com)
	- Pros
      - Free
      - Reliable
      - Preconfigured for Eaglercraft
      - Optional upgradability
      - Customizable
      - Good Support
	- Cons
      - Free servers are not as powerful as paid ones
  	  - Limited space availability (beta)
  	  - Only central US servers

### Hetzner (https://www.hetzner.com/cloud/)
	- Pros
		- Cheap
		- Reliable
		- Sells Managed Servers and Co-locations
	- Cons
		- Hosting options might not be as cheap compared to other hosts (compared to other options) with higher specs

### Q-FI (https://qficloud.com)
	- Pros
		- Build a custom VPS
	- Cons
 		- No Dedicated Servers

### FiberState (https://www.fiberstate.com/#deals)
	- Pros
		- Sells Dedicated Servers (Faster than VPS)
		- Good Dedicated Server Deals
	- Cons
		- No VPS

### ABR Hosting (https://abrhosting.com/)
	- Pros
		- Staff team will help you with eagler support
		- Sells VPS, Dedicated Servers, Game servers, and more
	- Cons
		- Hosting not as cheap as some other hosts

---

> You could use [Github Codespaces](https://github.com/features/codespaces) or Repl.it, however, it is **highly discouraged for many reasons** such as having security concerns and that free resources are limited which can limit your ability to list your server on [Eagler Server List](https://servers.eaglercraft.com).
{.is-warning}

:warning: Please note that if you use another host (especially popular Minecraft hosts and VPS providers), **you must make sure it will work with Eaglercraft**. 

For example, some hosts don't allow installing custom plugins such as EaglerXServer. 

Also note that getting SSL to work (for `wss://`, required for any client that is not an offline download) is even harder as most game hosts don't natively support web connections or allow running other software such as [CertBot](https://certbot.eff.org/) (for SSL certificates), [Cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/) (a web tunnel, requires paid Cloudflare domain, also has SSL), or [Ngrok](https://ngrok.com/) (web tunnel with SSL). You may have better luck on dedicated servers or non-gaming hosting providers (oddly enough).