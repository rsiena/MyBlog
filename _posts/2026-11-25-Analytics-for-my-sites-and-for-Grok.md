---
layout: post
title: Analytics for my sites, and for Grok
date: 2026-11-25
slug: analytics-for-my-sites-and-for-grok
permalink: /2026/11/25/analytics-for-my-sites-and-for-grok/
---

I run about ten websites, and I want a daily read of how each one is doing without logging into Google Analytics and starting over. I also want to see what my Grok bots are using, because a weekly limit is easy to hit if you never look. Both of those records should add up over time, not disappear after a month. This is how I read them every day, and how I keep them as monthly pages on a private site.

## It used to run on my computer

For a long time the Google Analytics piece was a Python script on my own machine. It ran at 8 AM, used the Google Analytics Data API with a service account, and wrote the dashboards into a local folder. That was enough, until it was not. Google disabled that route for me, and the morning job stopped.

I still wanted the daily numbers. The answer was not to give up on the record. It was to change how the numbers were collected.

## The morning Google Analytics run

A Grok Bot named Silva Analytics now runs every morning at 7:30 AM Central. It opens Google Analytics 4 in a browser and exports the reports I care about: Pages and screens, plus channels, sources, devices, countries, new users, and the daily figures.

A Python build script turns those exports into HTML dashboards. There is one page per month for each site, and a rolling June-to-date page that covers the current stretch. The main number on each page is month-to-date users. The other reports fill in the rest of the page: where the traffic came from, which devices and countries showed up, and how the month is trending. When a month closes, that page is archived and is never overwritten. Last September stays last September.

I track about ten properties: the Silva Method and Alcyone class sites, Dream Secrets, Exit 719, Silva Graduate, my own site, and the other sites in the same studio.

## Off my computer, onto a private site

The dashboards used to live in a folder on my PC. That works only when I am at that machine, and it is a weak place to keep a history I care about. I moved them to a Linux server I run in AWS: Ubuntu, on a small EC2 instance in us-east-2, with nginx in front and HTTPS from Let's Encrypt.

The site is private. It uses a simple username and password, basic authentication, so the numbers are not on the public internet. After the morning build, the bot publishes the new pages with rsync over SSH. That only worked after I allowlisted the bot computer's IP range in the AWS security group. A locked SSH port is the right default. A scheduled publisher just needs a way in.

I kept the look of the old dashboards: a dark and gold theme, tabs, KPI cards, and Chart.js charts. The new process supplies the data. The pages should feel familiar, and the figures should be the correct ones.

## Grok usage, every evening

Grok Bot is the AI assistant I use in my daily work. Each bot I have set up, including the one that builds these dashboards, draws from a weekly usage limit. I wanted those figures on the same site as the website stats, so I have one place to look.

A scheduled routine runs every evening around 8:45 PM Central, weekends included. It pulls my Grok Bot usage report for the last 30 days, broken out by day and by bot, along with my plan, the percent of the weekly limit I have used, and the credits I have left.

That report alone is not a history. It only looks back 30 days, and it shows each bot's share of usage, not a dollar amount. So the routine saves a snapshot every day. A script rescales and merges those snapshots into a running history, then renders one Grok Usage page per month and publishes it to the same private site. The monthly pages stay. The history I have starts on October 22, 2026, which is as far back as the first report would go.

The November page already told me something useful. So far this month, my Exit 719 Web Site bot is about 75% of my Grok usage, Silva Analytics is about 10%, and Research is about 6%. Those are shares of the total, not dollars, but they are enough to see where the week's limit is going.

## What I took from this

**Have a fallback when an API goes away.** The Data API path worked until Google turned it off for me. The browser export is slower and more brittle, and it still produces the daily pages. The lesson is not that APIs are useless. It is that a number you want next year cannot depend on a single door remaining open.

**Archive closed months, and do not overwrite them.** A dashboard that only shows today is a report. A dashboard that still has September is a record. Once a month is closed, that page stays put.

**Put private numbers behind a login, on a server you control.** Usage for my sites, and usage for my own AI tools, does not belong in an open folder on my desk. Basic authentication on HTTPS is enough for this. The server is small, and it is mine.

**Know what your AI tools actually cost you.** A weekly limit and a credits balance are easy to glance at and forget. A page per month, built from daily snapshots, shows which bot is doing the heavy work. I would rather see that clearly than be surprised when the week runs short.

If you keep a private dashboard for your own sites, or you have found a way to hold on to AI usage after the official report rolls off, I would like to hear how you do it.

Check out my public site at [exit719.com](https://exit719.com). It is one of the sites these dashboards watch, and it is up 24/7. Register, look around, and send me your feedback.
