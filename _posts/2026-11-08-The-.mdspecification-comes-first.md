---
title: The specification comes first
date: 2026-11-08
---
# The specification comes first

I am building a membership site called Exit 719. Before I wrote the screens, I wrote a specification. This post is about that document, and why I will not start a system without one.

A specification is not a wish list. It is the agreement about what the system is. A developer uses it to write the code. A person who joins later uses it to see why a row is kept, who may see a file, and what happens when someone asks to be deleted. If those answers live only in my head, the system is one person wide.

## What I already had

This project did not start on a blank page. The folder already held an earlier set of documents: a system description, a Poe bot specification, and a document-storage specification. Those were version 2. They described pieces. They did not yet describe one product with a build order.

I wrote version 3 as that single description. It covered accounts, groups, files, pages, classes, search, mail, and what to do when something fails. It was long enough to build from, and it was still wrong in places. A long document that has not been reviewed is a draft with good manners.

## What a useful specification contains

I hold a specification to a few tests.

- Every feature says whether it is already built, partly built, or new.
- A new feature names the stage it waits on. A later stage is not a reason to start that feature early.
- Tables are named. If a screen needs a column, the column is in the document.
- Permissions are named. Guessing an id does not grant access.
- Outside services are named, and the document says what happens when they are down.
- Open questions have an owner and a stage. A question with no stage is a question nobody has to answer.

I also draw the tables, the people who use the system, and the build order. A diagram is faster to argue with than forty pages of prose. The prose still has to win when the diagram and the prose disagree.

## Names were part of the specification

I locked the names before I locked the screens.

The code project is still called User Management. That is the folder and the solution. The product names were separate. Alcyone Circle was the site. Alcyone Campus was the learning area. Alcyone Commons was the shared pages, files, and member lists. Alcyone Members was the signed-in person's own area. Alcyone Hall was rejected on purpose so it would not leak onto a menu.

The name in the header can still be changed by the person who operates the site. The name on the running site is now Exit 719. The specification kept the code names so a rename of the product would not force a rename of the projects.

## Why this is the first post

People ask to see the software. The software is the result. The specification is the work that makes the result repeatable. I can hand the document to another developer and they can see which stage they are in, which table they may touch, and which idea they must not start yet.

The next post is about the review of version 3, and the decisions that became version 4. That is where the specification stopped being a description and became a build plan.

If you build systems and you skip this step, I would like to hear what you use instead. If you are following Exit 719, the specification is the map. The site at [exit719.com](https://exit719.com) is how far along that map I am.
