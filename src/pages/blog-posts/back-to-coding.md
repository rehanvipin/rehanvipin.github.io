---
title: 'Back To Coding'
pubDate: 2026-04-19
description: 'Noting down my thoughts when setting up my Dev Environment'
tags: ["blogging", "learning in public"]
layout: ../../layout/BlogPost.astro
---
# Setting Up My Dev Workspace
I wanted to get back to writing code as a hobby and building projects. It's been 4 years or so since I last did that.
Coincidentally, that's about the same time frame when I started working professionally as a software engineer.
So today being a Sunday, I thought it would be a good time to pick up a new course and try to code something.
The journey, has been interesting to say the least.

<br/>

## What do I do?
Firstly, figuring out what I want to work on. Yes, I could have picked up a project and worked on it, but I wanted to build a specific skill. So, I picked AI. Because it's interesting and employable (at least that's what the public says).

I'll document the steps I took to get there.

<br/>

## Linux Desktop Setup
I've moved to a Linux desktop setup long ago. However, it was after I was actively coding on my personal computer. Hence, I didn't really have a great dev setup. I didn't even have enough space on my filesystem.

It used to be easy to find a tree view of files on Windows, with some third party software.
I didn't want to install something new, but make use of the CLI, so I used du and cleared up some space. Interesting to learn how to list the space of hidden files `* ./*`.

I already have VS Code for a code editor, and now I need an AI agent on my desktop. It's not a very powerfull system, so I can't run large models. Given that, I would prefer to try out the cloud models first and then the local ones. Did a bit of research, and looks like OpenCode is a good one. I'm not sure how safe any of these things are, but looks like OpenCode is a bit of a popular one.

I would have used Claude Desktop, but that's not there on Linux for some reason.

### Side Rant Pt. 1
I tried to find out some good models to use for AI enabled development, and stumbled across [models.dev](https://models.dev), but ... why is it so slow ? 
Okay, taking a look, it seems like the performance is really bad. Lighthouse scores it at 38 , and doesn't even score the accessability. It just shows a big red warning mark. That doesn't sound good, does it?

<br/>

## OpenCode
There were three ways to use this thing apparently. Through the terminal, desktop application, and through an IDE.
The IDE part is just like another terminal though, so not too much difference.

Not too hard to set it up, it uses a free model by default. I hope it doesn't mess up my system.