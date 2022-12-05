---
title: "How I've Setup my Blog"
date: 2022-11-27T00:12:00+01:00
draft: false
toc: false
images:
categories: [blog]
tags: [blog]
---

# Introduction
This blog uses GitHub Pages for the space and publishing, and I use ~~Obsidian~~ VSCode with GitHub CLI & Git + Hugo to generate everything.
In this post, I've decided to put down steps that were done and how to achieve this result.

# Steps towards Environment Setup

## Data Location

Created a folder inside my OneDrive so it would be available in all machines I work from / with, I might move this folder later on to my NextCloud as I have that also available on my Linux laptops with which I work a lot, but as Windows is still my "main OS" I'll go with OneDrive at the moment.
This all to say that doesn't matter where's the data, if you want to edit it from multiple machines you may want to consider a replication / cloud storage service.

## Software setup

I use chocolatey to expedite my software setup... I can't be bothered looking for packages, downloading and installing them and since Chocolatey exists and it's free, I use it, so with the help of the ChocolateyGUI I've created a config with all the necessary packages, however here's a list of the main ones:
- ~~Obsidian~~ Visual Studio Code
- GitHub CLI
- Git

Git was not really necessary since we have the GitHub CLI, but I've installed it anyway as I'm more familiarized with it and might be of use if I feel a bit lost with the CLI.

## Blog GitHub Prep

As I already had the GitHub Page in place from a previous experiment... I decided to simply clone it back to the Data Folder I've created with the command `gh clone repo myusername\blog-source -- --recurse-submodules` and moved on from there.

### Creating a new Pull Request

Need to create a pull request in order to start getting things done. So I've did some tests with it and did first a `gh pr status` to check how it was and got back the current situation of the repository as it follows:
![Pull Req Screenshot](/Pasted%20image%2020221125001001.png)


This made the repository ready for changes and work on. Now, on to the ~~Obsidian~~ part, as we need a vault to work with.

**NOTE:** *Actually, I've decided to take a step back and get away from the Obsidian as an editor as it wasn't able to process images in posts properly and was adding unecessary risks and complications.*

### Working with the repository
So essentially at this point I'm doing the whole site generation, preparation and upload *manually*, which I hope to make completely automatic, leaving me just the work of writting the articles and the rest gets processed on GitHub and published automatically.

But like I said, for now... it's all manual.
Every post I create, I run the following commands in order:
```bash
cd public
git add .
git commit -m "New post - POST NAME HERE"
git push -u origin master
cd ..
git add .
git commit -m "New blog version pushed - POST NAME HERE"
git push -u origin master
```

