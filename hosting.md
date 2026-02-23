---
title: How to Host a Server
description: Step-by-step
published: true
date: 2026-02-23T11:35:22.578Z
tags: 
editor: markdown
dateCreated: 2026-01-07T15:46:34.050Z
---

# How to make a server
This guide will show you how to make your own EaglercraftX server. These steps may only apply to 1.8 EaglercraftX and not legacy 1.5 Eaglercraft.

Eaglercraft 1.12 may be able to join, however, this documentation is not catered specifically to 1.12.

## Prerequisites
To properly host your own server you will need:

### A VPS (Virtual Private Server) or Dedicated Server
You must have access to a VPS or a dedicated server that is accessible from the Internet with port forwarding.
A few compatible VPS and dedicated server services are listed on **the [Hosts](/hosting/hosts) page**, but it is advised that you do your own research to find what works for you.

> You could use [Github Codespaces](https://github.com/features/codespaces) or Repl.it, however, it is **highly discouraged for many reasons** such as having security concerns and that free resources are limited which can limit your ability to list your server on [Eagler Server List](https://servers.eaglercraft.com).
{.is-warning}
### Knowledge with Linux and the Linux Terminal
You will need to have some basic knowledge of how to interact with the Linux operating system, and in turn the Linux terminal. Click [here](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview) for a Linux basics guide that should help you with all the knowledge you will need for this tutorial.
### Basic understanding of setting up a working BungeeCord network
EaglercraftX relies on [BungeeCord](https://www.spigotmc.org/wiki/bungeecord/) or [Velocity](https://papermc.io/software/velocity) in order to operate the WebSocket connection that enables Eaglercraft users to connect to your server. If you are unsure of how to setup a basic BungeeCord or Velocity network, the tutorial will be able to provide some insight, but it is recommended that you do your own research to understand how it works. One guide can be found [here](https://shockbyte.com/en-gb/help/knowledgebase/articles/introduction-to-bungeecord-networks), which talks about the basics of how BungeeCord works.

> The latest EaglerXServer plugin allows for connections directly to backend, removing the need for a proxy such as Bungeecord or Velocity. We still recommend utilizing a proxy software and adding the plugin there, as it does not work properly with many server versions.
{.is-info}

## Step 1: Setting up
This step will show you how to install Java 17 on your VPS server.
To keep things simple examples will only be provided for Debian/Ubuntu or distributions based around the APT package manager.

### Installing Java
Installing Java is fairly easy. In this guide, [Eclipse Temurin](https://adoptium.net) will be our JVM of choice, though you could use others.

The commands for installing Eclipse Temurin Java 17 are as follows:
```
apt install -y wget apt-transport-https gpg
wget -qO - https://packages.adoptium.net/artifactory/api/gpg/key/public | gpg --dearmor | tee /etc/apt/trusted.gpg.d/adoptium.gpg > /dev/null
echo "deb https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | tee /etc/apt/sources.list.d/adoptium.list
apt update # update if you haven't already
apt install temurin-17-jdk
```
These commands have been directly taken from [Linux (RPM/DEB/APK) installer packages](https://adoptium.net/installation/linux/) and are only provided here for ease of use. It is encouraged to review the page for changes in case this wiki is outdated.

## Step 2: Downloading the Proxy Software
After installing Java we can get started with downloading the proxy software of our choice. EaglercraftXServer currently supports the two most popular softwares, that being BungeeCord and Velocity.
For simplicity this guide will assume you are using BungeeCord but steps for Velocity are almost the same.

### Installing and preparing the proxy
1. Download the latest [BungeeCord jar file](https://ci.md-5.net/job/BungeeCord/) or [Velocity jar file](https://papermc.io/downloads/velocity) and upload it to a directory on your server.
2. Visit the [EaglercraftXServer releases page](https://github.com/lax1dude/eaglerxserver/releases) and download the EaglerXServer file.
3. Start your BungeeCord server to generate the needed files and directories. This can be done by running `java -jar BungeeCord.jar` inside of the directory where you placed the file.
4. Shutdown your BungeeCord server by typing `end` into the server's console.
5. Inside of your BungeeCord installation's directory there should now be a folder called `plugins`.
6. Drop the downloaded `EaglerXServer.jar` file into this directory and start up your BungeeCord instance again. We don't need it to stay online so just turn it off by typing `end` in the console once again.
7. This should now have generated a new `EaglerXServer` folder in your plugins directory. Inside you will find all files for configuring EaglerXServer.
> Installing EaglercraftXServer on Velocity will generate an `eaglerxserver` folder and all `.yml` files will be `.toml` instead with slightly different formatting (the options are almost all exactly the same).
{.is-info}

This is the expected folder structure after following these steps:
```
📂 Proxy
├── 📁 modules
├── 📂 plugins
│   ├── 📂 EaglerXServer
│   │   ├── 📁 drivers
│   │   ├── 📁 eagcert
│   │   ├── 📄 ice_servers.yml
│   │   ├── 📄 listeners.yml
│   │   ├── 📄 pause_menu.yml
│   │   ├── 📄 server_info.yml
│   │   ├── 📄 server_info_message_api_example.html
│   │   ├── 📄 server_info_message_api_v1.js
│   │   ├── 📄 settings.yml
│   │   ├── 📄 supervisor.yml
│   │   └── 📄 test_image.png
│   └── 📄 EaglerXServer.jar
├── 📄 BungeeCord.jar
├── 📄 config.yml
└── ❓ Other BungeeCord related files.
```

### Configuring BungeeCord and EaglerXServer

After successfully installing BungeeCord and EaglerXServer you will need to configure it properly.

#### Setting the proxy to offline mode

This step is required to allow normal EaglercraftX players to join without the need for a Minecraft: Java Edition account.
> This will allow ___***anyone***___ to join your server with any name ___including yours___ which could lead to some catastrophic events, so make sure to set up an authentication plugin. This is not featured in this guide but updated and popular choices are [AuthMeReloaded](https://github.com/AuthMe/AuthMeReloaded/) and [nLogin](https://docs.nickuc.com/).
{.is-warning}

To switch your proxy into offline mode, you will need to edit the `config.yml` file located in the root of your proxy installation.
In the file look for a line that says:
```yaml
online_mode: true
```
This is where you can control if your proxy will be set to online-mode or offline-mode. We will need this to be set to false like this:
```yaml
online_mode: false
```
With that, your proxy is in offline-mode.

#### Configuring EaglerXServer

**Navigate to `plugins/EaglerXServer` inside of your proxy installation folder.**

First, we will change the server's name to show up properly when you are using services like EaglerServerList.
Open `settings.yml` and set the property `server_name` to a name of your liking.

To finish the setup we will customize your server's motd[^1]:
Open `listeners.yml` and under `listener_01.server_motd` specify your own motd. This field supports [legacy format codes](https://minecraft.wiki/w/Formatting_codes)

> **Be sure the bind address has the ___same port as the proxy server___. Unlike the old plugins, EaglerXServer does not like mismatched ports.**
{.is-warning}


---

## Step 3: Testing the installation
To see if the previous steps worked, start your BungeeCord installation and add the server's IP along with the port specified in `listeners.yml` (usually 25577) to your EaglercraftX multiplayer server list (`ws://ipaddress:port`). Please note this will only work on non-SSL encrypted sites because we have not set up any SSL encryption so you will have to use a offline downloaded HTML file for EaglercraftX.

> Joining the server at this point will kick you back out immediately, this is normal and expected because you have not yet set up a server. You will set one up in the next steps.
{.is-info}

## Step 4: Creating a simple backend server
After confirming that the previously created BungeeCord instance works as expected, it's now finally time to create yourself a backend server so you can actually start playing.

The server software of choice is [PandaSpigot](https://github.com/hpfxd/PandaSpigot). It is an updated 1.8.8 server software that has a lot of performance and bug fixes.

> You may choose to install other server software instead, such as [Paper](https://papermc.io). You can even use newer versions with the [Via*](https://viaversion.com/) suite of plugins. (___**Check out the guide for this on the [Advanced Server Configuration](hosting/advanced) page)**___ This does have drawbacks, however, because Via* does not actually port features from newer versions it works by finding workarounds (blocks released after 1.8 will be shown as placeholders from 1.8 for example).
>
> Some clients are designed to work with newer servers such as TuffClient, but ___if you choose this route, you should understand the shortcomings.___
{.is-info}


### Installing
Create a new empty folder for your backend server. In that folder, place the latest jar file of the server you chose, renamed to `server.jar` (for compatibility and consistancy).
You need to agree to the Minecraft EULA. To do so type `echo eula=true > eula.txt` into your Terminal.

Your server is now ready to start. The start command is `java -jar server.jar` (assuming `server.jar` is the actual name of the jar file).

The server should now be starting. Once it starts, what we need will now be generated, so stop it again using `stop` so we can configure it.

### Configuring the Server
In the same folder that your server jar file is, there should now be a bunch of new files. In order to make your server work, you will need to change some values in `server.properties` to make your server work with the proxy and EaglerCraft. Find the line that says `online-mode=true` and change it to this:

```properties
online-mode=false
```

You will need to change this regardless of if your proxy config is set to `true` or `false` due to the way user authentication works.

Feel free to also change values such as `view-distance` or `simulation-distance` here.

> It is important to close the port that your backend server is running on (default: 25565) on your firewall and/or router because having it open can lead to a backdoor, bypassing the proxy.
> 
> *To secure it farther, [BungeeGuard](https://bungeeguard.com/) can be installed to ensure the backend server only excepts connections from the proxy.*
{.is-warning}

## Step 5: Joining the server (finally!)
### Port Forwarding
Before you join the server there is one last thing you need to do if your server is on a different local network than your client. Unfortunately this differs between VPS hosts and routers.

If you are using a VPS simply Google:
`how to port forward with X VPS`

If you are self hosting and want to make your server public, first make sure you aren't behind CG-NAT, then Google:
`how to port forward with X ISP`

You will want to open the following port (only TCP is necessary):
`25577` if you want Minecraft Java Edition players to be able to join your server.
> If your port in the proxy config file is different, be sure to use that one.
{.is-info}

### Joining the server
At this point you should be able to join your server from multiple platforms:

Minecraft Java Edition @ `127.0.0.1:25577`
EaglercraftX @ `ws://127.0.0.1:25577` (**NEEDS TO BE FROM A non-SSL source like an offline download**)
(replace 127.0.0.1 with the IP to your server and 8081/25577 with the corresponding ports if you changed them)

> A guide for setting up a domain for your server, as well as wss, will eventually be written at some stage.
{.is-warning}

---

[^1]: MOTD: short for 'message of the day', shown on the multiplayer servers screen