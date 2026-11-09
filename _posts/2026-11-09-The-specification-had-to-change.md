---
layout: post
title: The specification had to change
date: 2026-11-09
slug: the-specification-had-to-change
permalink: /2026/11/09/the-specification-had-to-change/
---
# The specification had to change

Version 3 of the Exit 719 specification was complete enough to review and incomplete enough to break a build. I had it reviewed on purpose. A specification that has never been attacked is a story I am telling myself.

The review did not ask for more features. It asked for decisions. That is the useful kind of review.

## The error system could not report its own failure

The first draft of the error section assumed the database and the mail system were up at the moment something failed. If the failure is the database, or the mail server, both of those paths are dead. The fix was a local log file that does not need PostgreSQL and does not need mail. If that write also fails, the visitor still gets a plain error page. The system does not throw a second error at them.

The same section had no limit on alert mail. One bad loop can send thousands of messages and hide the real alert. Rate limiting went into the specification before any of that code was written.

## Security items that were "standard" and still missing

A superuser can set a new password when a member is locked out. Version 3 did not say to email the member, and it did not say to write an audit row. Without both, a password change can happen in silence. Version 4 says the mail goes out, the new password is not in the mail, and the audit row stores ids, not the password and not the email address.

Custom CSS was allowed for a group, which is what an owner wants, and CSS can still pull data out through `url()` or restyle the rest of the site. The review said the sanitizer belongs in the stage that ships custom CSS, not in a later "we should get to this" list. Stage 3 does not ship without it.

File uploads said "up to the PostgreSQL limit." That limit is about a gigabyte. Any member could fill the disk. The specification now has a per-file cap and a per-owner cap. Virus scanning was called out as out of scope, on purpose, so nobody would assume it was there.

## The learning center was described and not pinned down

A class was implied to belong to a group. The foreign key was never stated. I decided one class belongs to one group. It is not shared. If the group is archived, the class leaves the catalog and the member's home, and the enrollment rows stay.

"Self-paced," "in person," and "live online" were a kind column with no rule about who may invent a fourth kind. They became a lookup table with three seeded rows. An owner picks one of those three.

A lesson can point at a hosted video. The specification says the video bytes are not stored in the database. The columns are a provider name and a provider id. Until a host is chosen, the player does not show a video block at all. Storing a field is not the same as shipping a player.

Tests had no maximum attempts. A member could retry a gated lesson forever. Version 4 adds a maximum, a wait after a failed attempt, an optional time limit, and a survey that is not scored and does not unlock the next lesson.

## Search, privacy, and pages that had no columns

Search said it would find groups, members, and classes, and did not say which fields. Two people would have built two indexes. The specification now names them: member name and email, group name and description, class name and description, using PostgreSQL full-text columns.

Billing history is never deleted. Version 3 did not say why. A deletion request and a financial record were on a collision course. The specification now states the reason those rows stay.

`M_ContentPage` was listed with no columns. That is not a table. It is a name. Version 4 lists the columns a content page needs before anyone is asked to build the editor.

## What I did with the review

I did not paste the review under version 3 and call it done. I wrote version 4. Where version 4 and version 3 disagree, version 4 wins. Version 3 stays in the folder as history. Each open question was attached to the stage that cannot start without it. The Stripe question blocks payments. The CSS question blocked the presentation stage. The Poe table question blocked the first stage.

That is the evolution I care about. The document got shorter in the places that were vague, and stricter in the places that would have produced two different systems.

The next post is the build order those decisions created, and why I did not start with the screen people ask to see first.
