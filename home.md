---
title: Eaglercraft Intro
description: 
published: true
date: 2026-01-09T17:09:06.575Z
tags: 
editor: markdown
dateCreated: 2026-01-07T15:25:45.921Z
---

# Welcome to Eaglercraft Documentation!

This service is operated and maintained by members of the Eaglercraft community and aims to provide a central place for documentation of all sorts, including the process of creating and managing an Eaglercraft server, the history of Eaglercraft amongst other things.

Eaglercraft is an AOT compiled port of Minecraft 1.8.8, designed to run in a browser environment, using [TeaVM](https://github.com/konsoletyper/TeaVM) and [LAX1DUDE](https://github.com/lax1dude)'s OpenGL 1.3 emulator to simulate a Java virtual machine fully compatible with Minecraft Java Edition.

Eaglercraft is primarily Minecraft 1.8.8, however, a 1.12 version endorsed by LAX1DUDE is available by PeytonPlayz. The 1.12 version still lacks certain features, but is being updated.

---

## Need a guide on [getting started with playing Eaglercraft?](/playing)

## Want to find out how to [create your own Eaglercraft server?](/hosting)

---

> A new, re-written plugin for Eaglercraft servers has been recently released. Some parts of this documentation may not be up-to-date with the latest plugin.
{.is-warning}


There is a [YouTube channel](https://youtube.com/@eaglercraft-official) for Eaglercraft. Please note, whilst this channel is approved by ayunami2000, it is not owned by the Eaglercraft developers and rather by members of the community.

Eaglercraft is currently on version ___u53___.

> Eagler Server List has been shut down until farther notice. The Arch MC team has taken over the project, however we have no ETA on when it will be back online.
{.is-warning}


<!--
**Looking for documentation pertaining to Eagler Server List?** [Look no further](/EaglerServerList/Introduction).
{.is-info}
-->

> Due to a limitation with the hosting of this service, client links, client source code, and tutorials on how to develop clients for Eaglercraft are unavailable to mitigate the risk of DMCA.
{.is-info}
## Development
The development of Eaglercraft began in early 2020, porting the 1.5.2 version of Minecraft Java. Minecraft using Java yielded a significant challenge given that web browsers discontinued support for running Java applications in 2016. Instead, LAX1DUDE, the sole developer at the time, opted to use TeaVM, as it provided support for WebAssembly, which is a binary format for developing web applications, as well as JavaScript, the go-to language for providing functionality to a website. Initially, LAX1DUDE opted to use JavaScript, but after seeing some performance issues, he attempted to migrate the ported game to work with WebAssembly, but unfortunately, [some complications](https://github.com/konsoletyper/teavm/issues/521) were encountered with using WebAssembly, and thus LAX1DUDE reverted Eaglercraft back to JavaScript ahead of its release in December 2021. In recent times, the development team of Eaglercraft managed to re-implement WebAssembly support and got it to work properly, and now both versions are available in parallel.