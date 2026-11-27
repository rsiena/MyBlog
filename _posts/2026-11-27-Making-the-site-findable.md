---
layout: post
title: Making the site findable
date: 2026-11-27
slug: making-the-site-findable
permalink: /2026/11/27/making-the-site-findable/
---

The series so far:

1. [The specification comes first](https://rsiena.github.io/MyBlog/2026/11/08/the-specification-comes-first/). Why I write a specification before any screens, and the tests I hold one to.
2. [The specification had to change](https://rsiena.github.io/MyBlog/2026/11/09/the-specification-had-to-change/). The review of version 3 asked for decisions, not features, and those decisions became version 4.
3. [Build in stages](https://rsiena.github.io/MyBlog/2026/11/10/build-in-stages/). The build order version 4 created, the five stages in the running site, and why payments waited.
4. [What you can do on the site today](https://rsiena.github.io/MyBlog/2026/11/11/what-you-can-do-on-the-site-today/). A tour of Exit 719 as it stood: one account, many groups, what members and owners see, and what was not built yet.
5. [AI is the assistant, not the staff](https://rsiena.github.io/MyBlog/2026/11/15/ai-is-the-assistant-not-the-staff/). Who is in the room while I build: the AI tools I use, the weekly limit on each, and the decisions I keep.
6. [Adding journaling to the site](https://rsiena.github.io/MyBlog/2026/11/20/adding-journaling-to-the-site/). The Journal, from an 18-page specification to the live site, built as seven pull requests and finished by my own Q&A.
7. [Analytics for my sites, and for Grok](https://rsiena.github.io/MyBlog/2026/11/25/analytics-for-my-sites-and-for-grok/). How I get a daily read of my sites and of Grok usage, and keep both as monthly pages on a private site.
8. [Checkout, built last on purpose](https://rsiena.github.io/MyBlog/2026/11/26/checkout-built-last-on-purpose/). In the third post I said payments would wait. Stage 6 was checkout, it needed the classes to exist first, and a priced class told the member that checkout was not in this…
9. This post. Sitemaps, canonical addresses, structured data, and page counts that do not track people.

* * *

A site nobody can find is a private site with a public address. Post 6 mentioned that one stage of the Journal build added search engine pages and first-party view counts. This post is what that means, and what I left out on purpose.

## Search came with the public journal, not after it

I did not treat search engines as a marketing task for later. The stage that made journal posts public was the same stage that decided how a search engine would see them. A public page without those decisions gets indexed under the wrong address, with the wrong description, and sometimes with information that should never have been public.

So the specification answered the questions first. Which pages are public? Which address is the real one? What does a search engine get to read, and what stays behind sign-in?

## One address for every page

Every public page names one canonical address on `https://exit719.com`. A request for the `www` version, or for plain HTTP, redirects there. Search engines see one copy of each page instead of three.

Addresses also change over time. A post gets a better title, an event is renamed, a group changes its web address. When that happens, the old address answers with a permanent redirect to the new one. A link someone shared last week still works, and the search engine moves its record to the new page.

Later, the same build started running a second site. The public address now comes from each site's own settings, so the canonical links, the sitemap, and the feeds on each site point at its own domain and never at the other one.

## A map, and a list of doors to leave closed

The site publishes a sitemap. It lists the home page, the public calendar, each public group's about page and calendar, public events from the last 12 months, and public journal posts. Classes are added only when the class catalog is open to visitors.

The site also publishes a `robots.txt` file. It points at the sitemap and asks search engines to stay out of the account pages, the site administration pages, the member area, search results, the private feeds, and group member lists. Member pages also send a noindex header, so they stay out even if someone links to them.

Public posts are also available as RSS and Atom feeds, with full text, for people who still read that way.

## What a search engine is allowed to read

Each public page sends a short description, Open Graph tags for link previews, and a summary card for X. There is no image pipeline yet, so the preview has no image. I would rather leave the image out than invent one.

Public pages also carry structured data that search engines read directly. A post is marked as a blog post. An event is marked as an event, and a cancelled event says so. The site and each public group are marked as an organization. There is a breadcrumb trail so the page shows where it sits.

The hard part was deciding what to leave out. An event's structured data gives the city, or says Online. It does not give the street address or the meeting link. Members-only events and paid events are not public pages at all. An event older than 12 months can still be opened, and it asks search engines not to index it. A visitor who is not signed in can read a public post and its published comments. They cannot comment, react, or report.

Public is a choice the author makes. Turning on a public journal does not make any existing post public. Turning it off removes the public page, the feed entry, and the sitemap entry, and the post itself is kept.

## Counting without tracking people

I wanted to know whether anyone was reading, and I did not want to build a surveillance system to find out.

The site keeps its own counts. Each row is a day, a kind of page (a public journal post, a public event, or the public calendar), an optional group, and a number. There is no IP address, no account, no path, and no post text in that table. The superuser sees the site's counts. A group owner sees that group's counts.

That answers the question I care about, which is whether people are reading the public pages, without keeping a record of who they are.

## Then the outside tools

Some site operators want Google Analytics or Google Tag Manager as well. So a later change lets the superuser paste a tracking snippet on the site configuration page. It goes into the head or the top of the body on every page that uses the shared layout. It is limited to the superuser, and a blank box removes it.

Exit 719 now has a Google tag installed that way. The first-party counts still run beside it, and they do not depend on it.

## What I left for later

The stage that added all of this also wrote down what it did not do. Verifying the site with Google Search Console and Bing is a DNS step for me as the operator, not a code change. Responsive images, image compression, and page speed tuning are hosting work. Markup for classes waits until classes are published that way.

There is more to do in the page text itself. The home page description is still just the site name. SEO is on my current list of changes, and it will get its own short specification before it gets more code.

## Why this belongs in a build log

SEO is usually the last thing bolted on. Here it was part of the decision about what public means. The sitemap, the canonical addresses, and the structured data follow the same rules that decide who may see a page. Members-only content never reaches the map.

If you have tuned a small site for search, tell me what moved the needle for you. I would rather learn it from you than from six months of guessing.

## Come find it

Check out the site at [exit719.com](https://exit719.com). It is my live test site, up 24/7. Register, read the public journal, and send me your feedback.
