---
title: cc-pkg: A ComputerCraft Package Manager
date: 2020-01-20 23:45:00 -0800
modified: 
permalink: /cc-pkg-a-computercraft-package-manager/
category: Programming
blags: [ComputerCraft, installer, Lua, Minecraft, package management]
tags: writing/blog/published
---

(The latest information and a quick reference is located [here](https://blog.tangentfox.com/cc-pkg/).)

ComputerCraft is a Minecraft mod that adds Lua-based computers. Over time, many programs have been created, and several package managers have come and gone. As I write this, all that I have seen are gone – their original authors have moved on, and shut down the servers hosting packages.

Now it's my turn to sell you a package manager. Unlike the others, I expect this to remain viable – even if I'm gone from the picture. If you want to skip to trying it, here's how it's installed (and how to ask for help):

```
pastebin get 9Li3u4Rc /bin/pkg
/bin/pkg help
```

(I'd also recommend installing the `unix-like` package, which adds `/bin` to your path, along with a few other small tweaks.)

## Why is cc-pkg different?

1. It is built on ComputerCraft's pastebin integration.
2. It does not require a maintainer.
3. It is extremely simple – and flexible.

cc-pkg has the same three sub-commands of the default `pastebin` program: get, run, and put\*. They each do exactly what you'd expect them to do, except they can use names as well as pastebin IDs. Names consist of alphanumeric characters and dashes, and there are two file types cc-pkg can recognize and utilize:

Both are plaintext lists of the form `key=value`. The first is called a `package` and has file paths (all starting with a forward slash) as keys, with names or pastebin IDs as values. This is how cc-pkg knows which files to download and where to put them. The second type is called a `list`, and contains names as keys, with names or pastebin IDs as values. Lists are saved to a local file cc-pkg uses to resolve package names – overwriting any existing entries with the same package name, which is how updating is done.

With just those core features, I think the system is viable.

\*The put command is not implemented as of version ~~1.4.2~~ 1.5.10, the latest at the time of ~~writing~~ ~~finishing~~ updating this introduction.

## Command Extensions

On top of this, if a file is saved to `/lib/pkg-commands/<name>` and a user runs `pkg <name>`, that file will be run with the other arguments. This allows adding new functions, and overwriting the core functions to add additional features, if desired.

## Under the Hood

cc-pkg keeps metadata through the following files:

- `/etc/pkg/names.list`: The master names list. (How cc-pkg knows what to download.)
- `/etc/pkg/ids.list`: Download history of cc-pkg. (An ordered list of every pastebin ID successfully downloaded.)
- `/etc/pkg/<package-name>`: Each package is saved here by name, in addition to the files it specifies.

## API Loadable

It uses global functions so that it can be loaded as an API to make a more advanced package management system on top of it – or just to make programs automatically download requirements using cc-pkg.

- `get(name_or_id, path)`: The core function that installs anything (package/list/file). (`path` is optional.)
- `down(id)`: Downloads from a pastebin ID, returning its content or throwing an error.
- `save(path, data)`: Write to file. (Note: This is not a binary write.)
- `append(path, data)`: Append to file. (Note: This is not a binary write.)
- `id(name_or_id)`: Recursively checks the master names list until a pastebin ID is returned. (Note: On failure, returns the last name resolved.)
- `type(data)`: Recognizes data as a `package`, `list`, or `unknown` type, and returns that type.
- `src(data)`: Combines this data with existing names (overwriting if duplicates exist). (If `get` is used, `src` will be called when needed automatically.)

An example of this is the `pkg-search` package, which adds a search command to look for specific package names within the master list.

## Example Packages & Lists

- A basic package looks like this:  
  `/startup=XsYUCf5b`  
  This is the `multi-startup` package, which makes the computer run all files in `/.startup` when started. It is required for several of my packages to function.
- A package with a dependency looks like this:  
  `/etc/pkg/multi-startup=multi-startup
  /.startup/unix-like.lua=iG9idFgk`  
  This is the `unix-like` package, which requires `multi-startup` to function, and makes the computer operate more like a UNIX computer. (Due to how cc-pkg works, specifying to download a package anywhere will install that package. By convention and for consistency, I use the location cc-pkg installs packages by default.)
- A “meta package” (a package that only lists dependencies) looks like this:  
  `/etc/pkg/ping=ping
  /etc/pkg/touch=touch
  /etc/pkg/which=which`  
  This is only part of the `unix-meta` package, which lists many packages that make a computer operate more like a UNIX computer. Packages are very flexible! They don't even have to install anything themselves.
- A list looks like this:  
  `pocket-computer-chat=qtnShai4
  pocketgps=8SXT1hDN`  
  This is the current list of pocket packages at the time of writing. (These can be added by running `pkg get pocket-packages`.) Remember, lists can reference other names (e.g. `unix-stuff=unix-meta`), allowing one to create aliases for existing packages & lists.
