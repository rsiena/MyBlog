---
layout: post
title: AI is the assistant, not the staff
date: 2026-11-15
slug: ai-is-the-assistant-not-the-staff
permalink: /2026/11/15/ai-is-the-assistant-not-the-staff/
---
# AI is the assistant, not the staff

The series so far:

1. [The specification comes first](https://rsiena.github.io/MyBlog/2026/11/08/the-specification-comes-first/). Why I write a specification before any screens, and the tests I hold one to.
2. [The specification had to change](https://rsiena.github.io/MyBlog/2026/11/09/the-specification-had-to-change/). The review of version 3 asked for decisions, not features, and those decisions became version 4.
3. [Build in stages](https://rsiena.github.io/MyBlog/2026/11/10/build-in-stages/). The build order version 4 created, the five stages in the running site, and why payments waited.
4. [What you can do on the site today](https://rsiena.github.io/MyBlog/2026/11/11/what-you-can-do-on-the-site-today/). A tour of Exit 719 as it stood: one account, many groups, what members and owners see, and what was not built yet.
5. This post. Who is in the room while I build: the AI tools I use, the weekly limit on each, and the decisions I keep.

* * *

The first four posts were about the specification, the review that changed it, the stage order, and what Exit 719 does today. This one is about who is in the room while I build it. Most days that is me, and an AI assistant with a weekly limit.

## What I used to have

At my last company I still did the coding, the AWS work, and the version control. The staff was lean. We had a few coders, a design team, and a CSS team. The coders split their time between SQL Server and C# on .NET 4. The pages were AJAX. We used libraries that already contained the grids, the editors, and the other controls, so a screen started from a part that existed.

That was a small team, and it was still a team. Someone else could look at a page. Someone else owned the stylesheet. Someone else had already built the control I was about to drop on a form.

This time I am solo. Exit 719 is .NET 10, Razor pages, and PostgreSQL, on a Linux machine I set up myself. There is no control library waiting for me, and there is no second developer at the next desk. AI is the assistant I use to review documents and code, and to show me the strong points and the weak ones. It is not a second employee. It does not own the specification, and it does not decide when a stage is done.

## The tools, and the limit on each one

On this computer I use two Grok applications, SuperGrok and Grok Bot. Each one has its own weekly usage limit. When a tool is near the limit, I stop and decide what is worth the rest of the week. That limit is useful. It keeps me from asking for ten half-thought changes at midnight.

I also use Poe when I want another model, or when I want a chunk of code or a document review that should not come from the same model that wrote the draft. Poe can reach the other major models. I send the same review to more than one of them. They do not agree. That is why I do it. A single review agrees with the person who wrote the page. Two reviews argue, and the argument is where the weak spot shows up.

I am also putting Claude Code on this machine, a local application, to help with the code itself. Grok has been the environment and the long specification work. Poe has been the second opinion. Claude Code is the next pair of hands in the editor. None of them replace the decision.

## The prompt is a document, not a sentence

The habit that matters most is the same habit as the specification.

When I want a change, I write a prompt document. I read it more than once. I fix the vague lines before I hand it to the bot. Then the local bot implements that document. The writing is what flushes the idea out. By the time the bot sees it, the feature has a shape: what the screen shows, what it must not do, and what "done" means.

Version 3 of the Exit 719 specification went through that kind of review before it became version 4. A prompt for a smaller change goes through a shorter version of the same pass. If I skip it, I get a confident answer to a question I had not finished asking.

## The machines

I run Zorin Linux. Grok integrated Visual Studio Code on that machine. It could have been another Linux. The point is that the bot sat with me through the setup: the local environment, GitHub, and AWS.

I have built AWS environments myself for years. This time I gave the bot the prompts, it did the setup, and it saved me a few days. It also set up the GitHub repository, prepared the machine, and pushed the builds to the live site when I told it to. I still decide what gets pushed. The bot does not ship on its own.

## The firewall was not a solo job

During this same period I moved the network from Untangle to OPNsense. The bots helped with the OPNsense configuration. Then my wife took that setup and brought it up to her standard.

Ariella is a Cisco expert, with a long list of Cisco certifications. Recruiters notice. The NSA has tried to hire her more than once. She and I have both been in the hacker community for years, and we have been guest speakers at security conferences. After she reworked the firewall, we used the bots for security checks on that install and for some penetration testing of our own network. The bots drafted and compared. She decided whether the result was actually safe.

That is the pattern everywhere else on this project. The assistant finds the weak point. A person who knows the system says whether the fix is real.

## What I want you to take from this

AI has let one person, with a specialist beside him on the network, move at the speed of a small team. It has not let me skip the specification, the review, or the stage order. SuperGrok and Grok Bot are limited each week. Poe is where I go when I want a different model to disagree with the first one. Claude Code is joining the editor. I still read the diff.

If you are building alone and using an assistant, I would like to know which part you refuse to hand over. For me that part is the decision about what the system is, and the decision to put it on the public site.
