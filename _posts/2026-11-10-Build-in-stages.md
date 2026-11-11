---
layout: post
title: Build in stages
date: 2026-11-10
slug: build-in-stages
---

After version 4 of the specification was approved, I did not open a editor and start on the home page. I built in the order the specification named. Five stages are in the running site. Payments are not. That is a choice, not a delay I forgot about.

## Why the order is the product

A profile photo needs a file store. A group home page needs a page editor, and the page editor needs a sanitizer. A class you can sell needs the class to exist. If I build checkout first, I am designing a cash register for a store with no shelves.

Each stage has a gate. The code for a later stage does not start because I am excited about it. The specification says which stage a feature waits on. I followed that.

## The five stages

**Stage 1. Poe, per group.** A member's bot key is not one key for the whole site. It belongs to a group. The owner can require a member's own key, set a monthly cap, and limit which bots that member may use. The public Poe catalog does not list private prompt bots. I wrote that limit into the screen instead of pretending the API returns them.

**Stage 2. Documents.** Logos, profile photos, and member files are rows, not paths pasted into a form. Images are resized. A thumbnail is generated. A missing file and a forbidden file return the same message, so a guessed id does not tell you the file exists.

**Stage 3. Pages, menus, and the look of a group.** An owner can write a page. The HTML is cleaned. The CSS is cleaned and scoped to that group so it cannot restyle the rest of the site. The menu can sit on top or on the side, and it collapses on a phone. A superuser can set another member's password. The member is emailed. The new password is not in the email. An audit row is written.

**Stage 4. Labels and search.** Flags, tags, and a welcome sequence. Search covers members and groups, then classes once the learning center exists. A peer sees a name. Email is not handed out just because two people share a search box.

**Stage 5. Campus.** One class belongs to one group. The kind is self-paced, in person, or live online. A self-paced class has lessons in order. The next lesson stays locked until the earlier lesson is finished, or until a real test is passed. A survey does not unlock anything. In-person and live classes show a schedule, a place, and a meeting link. The link is a link. It is not a Zoom integration. A price above zero does not let the member enroll themselves, because checkout is the next stage and it is not built. The owner can still place a member in the class.

## What I refused to start

Stage 6 is payments. It needs the class, and it needs a decision about who receives the money. I did not stub a fake checkout and leave it in the product. A priced class tells the member that checkout is not in this version. That sentence is more honest than a button that cannot charge a card.

I also did not build video hosting. The lesson can store a provider name and an id. The player does not show a player. When a host is chosen, the column is already there.

## How I know a stage is done

A stage is done when the behavior in the specification is in the site and a test fails if it disappears. The suite is the regression net for the earlier stages. A new table is wiped and reseeded with the rest of the test database, or the next test run lies.

I work on a Linux machine, against PostgreSQL, in .NET 10. The same specification is what got deployed. Localhost is where I break it. The public site is where the last green build goes, and only when I decide to ship it.

The last post in this series is what you can actually do on the site today, and what I am still changing in front of you.
