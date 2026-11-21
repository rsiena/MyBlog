---
layout: post
title: Adding journaling to the site
date: 2026-11-20
slug: adding-journaling-to-the-site
permalink: /2026/11/20/adding-journaling-to-the-site/
---

The series so far:

1. [The specification comes first](https://rsiena.github.io/MyBlog/2026/11/08/the-specification-comes-first/). Why I write a specification before any screens, and the tests I hold one to.
2. [The specification had to change](https://rsiena.github.io/MyBlog/2026/11/09/the-specification-had-to-change/). The review of version 3 asked for decisions, not features, and those decisions became version 4.
3. [Build in stages](https://rsiena.github.io/MyBlog/2026/11/10/build-in-stages/). The build order version 4 created, the five stages in the running site, and why payments waited.
4. [What you can do on the site today](https://rsiena.github.io/MyBlog/2026/11/11/what-you-can-do-on-the-site-today/). A tour of Exit 719 as it stood: one account, many groups, what members and owners see, and what was not built yet.
5. [AI is the assistant, not the staff](https://rsiena.github.io/MyBlog/2026/11/15/ai-is-the-assistant-not-the-staff/). Who is in the room while I build: the AI tools I use, the weekly limit on each, and the decisions I keep.
6. This post. The Journal, from an 18-page specification to the live site, built as seven pull requests and finished by my own Q&A.

* * *

The first five posts covered the specification, the review that changed it, the stage order, what the site does today, and how I use AI. This one follows a single feature, the Journal, from the first document to the live site.

## It started as a document

I did not start with a screen. I started by writing a detailed document that said what the new features would be: who can post, who can read, what a group journal holds, and what a visitor who is not signed in may see.

Then I worked that document over with AI. We went through a few drafts before I approved the final one. The drafts were where the questions came out. Does a group journal show only that group's posts? (Yes.) Can a visitor comment? (No.) What order is the feed in when you first open it?

When the specification was finished, it was over 18 pages.

## The first wall

When I asked the assistant to implement it, the answer was, more or less, "that is beyond my scope." Eighteen pages is not a prompt. It is a project.

So I set up Cursor and handed the work to its coding agent, which reads the existing code, changes it, and opens a pull request for me to review. The fix for the wall was not a bigger request. It was a smaller one, repeated. The specification was split into seven stages, and each stage became its own pull request:

1. The groups foundation: families of groups, enrollment, and who can see what.
2. Member handles and the Journal core.
3. The member feed, follows, reactions, and comments.
4. Notices, email digests, and moderation.
5. The public calendar and event requests.
6. The public journal, search engine pages, and first-party view counts.
7. Payments, built against a fake Stripe connection so nothing could charge a real card.

Each stage had to build and pass its tests before it was merged. Then my PC pulled the change, and only then did the next stage start. Nothing went to the live site until all seven were done.

## The overnight run

I started the bot at around 9 PM, and it worked until about 6 AM the next day. That run used about 50% of my weekly allotment. By the time I finished the fixes and changes, I had used about 80%. In the end it was well worth it.

## Testing found the real changes

After the build, I did my own Q&A, the way a member would use it, and came up with a list of changes. Then they were implemented and tested again. A few of them:

- The feed opens newest first, and you can switch it to other orders, including most popular.
- Reactions (Like, Love, Insightful, Celebrate, Support) show as emojis, with the name when you hover.
- You can edit your own posts.
- The Journal menu goes straight to the journal, with Your drafts, New post, and a Show choice of All, Following, Discover, or Mine.
- A visitor who is not signed in sees only public journal entries on the home page and cannot comment. A signed-in member sees their own posts, their groups' posts, and the members they follow.

None of those were wrong in the specification. They were things I could only feel by using it. I spent another 30% or so of the weekly allotment over the next couple of days on that round of Q&A.

## Ideas I took from the process

**Split the specification before you hand it over.** A document that is too big to build in one pass is a document that has not been broken into stages yet. The seven stages made each run small enough to review.

**One pull request per stage.** Every change arrived as something I could read, test, and either merge or send back. If a stage was wrong, only that stage had to be redone.

**Let the tests grow with the site.** The test count went from 122 after the first stage to more than 150 by the time the Journal shipped, and it keeps climbing. Each fix adds a test so the same bug cannot quietly come back.

**Build the risky part against a fake.** Payments were built and tested against a fake Stripe connection. The checkout pages exist, but payments stay switched off on the live site until I have tested them with Stripe and approved it.

**Write down what bit you.** After launch, one class page failed because a new database table had been created without giving the site's own database account access to it. The fix took a minute. The lesson went into the project notes, so every new table now gets that access when it is created.

**Batch your Q&A.** A weekly limit rewards one good list of changes over twenty small requests. I test, collect everything I find, and hand it over as one document.

## Come try it

Check out the site at [exit719.com](https://exit719.com). This is my live test site, up 24/7. You are welcome to register, explore the Journal, and send me your feedback.
