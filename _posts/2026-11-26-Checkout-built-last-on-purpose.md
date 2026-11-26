---
layout: post
title: Checkout, built last on purpose
date: 2026-11-26
slug: checkout-built-last-on-purpose
permalink: /2026/11/26/checkout-built-last-on-purpose/
---

The series so far:

1. [The specification comes first](https://rsiena.github.io/MyBlog/2026/11/08/the-specification-comes-first/). Why I write a specification before any screens, and the tests I hold one to.
2. [The specification had to change](https://rsiena.github.io/MyBlog/2026/11/09/the-specification-had-to-change/). The review of version 3 asked for decisions, not features, and those decisions became version 4.
3. [Build in stages](https://rsiena.github.io/MyBlog/2026/11/10/build-in-stages/). The build order version 4 created, the five stages in the running site, and why payments waited.
4. [What you can do on the site today](https://rsiena.github.io/MyBlog/2026/11/11/what-you-can-do-on-the-site-today/). A tour of Exit 719 as it stood: one account, many groups, what members and owners see, and what was not built yet.
5. [AI is the assistant, not the staff](https://rsiena.github.io/MyBlog/2026/11/15/ai-is-the-assistant-not-the-staff/). Who is in the room while I build: the AI tools I use, the weekly limit on each, and the decisions I keep.
6. [Adding journaling to the site](https://rsiena.github.io/MyBlog/2026/11/20/adding-journaling-to-the-site/). The Journal, from an 18-page specification to the live site, built as seven pull requests and finished by my own Q&A.
7. [Analytics for my sites, and for Grok](https://rsiena.github.io/MyBlog/2026/11/25/analytics-for-my-sites-and-for-grok/). How I get a daily read of my sites and of Grok usage, and keep both as monthly pages on a private site.
8. This post. Prices, the class catalog, Stripe checkout, refunds, and sales, built in phases and tested against Stripe's test environment.

* * *

In the third post I said payments would wait. Stage 6 was checkout, it needed the classes to exist first, and a priced class told the member that checkout was not in this version. That sentence is gone now. This post is about what replaced it, and how it was built.

## The engine was there, the store was not

Payments were built as the last stage of the Journal work, against a fake Stripe connection, and then deployed switched off. Most of the machinery already existed: a webhook, purchase records, and the rule that access starts only after Stripe confirms the payment.

What was missing was everything a person touches. An owner set a price by typing an amount in cents and pasting in a class id, on a payments page that no menu linked to. The price in the class editor and the price Stripe would charge were two separate fields, and they could disagree. A visitor had no page where they could actually buy anything. There was no list of sales and no receipt.

So I did what I do with every feature. I wrote a checkout and sales specification first. It listed what existed, what would change, and what was new, and ended with open questions for me to answer. Nothing in it was built until I approved it.

## The rules came before the features

The first section of that document is not about screens. It is the standing rules:

- No live charges until I approve live mode in writing.
- Sandbox first. Everything is built and tested with Stripe test keys, or with a stand-in that never calls Stripe.
- The switch that says the sandbox test passed is set by hand, by me. The code never sets it.
- Settings that are already saved are kept. A change adds columns with defaults and never resets a value.
- Tests and deploys send no email, and every deploy takes a fresh database backup first.

Those rules are why I could let a coding agent work on money at all.

## Phase 1: prices in plain sight

The owner now sets a price where they already work: on the group settings page and in the class editor. The choices are Free, One-time, Subscription (monthly or yearly), and Pay over X months. More than one can be on at the same time. Amounts are typed in dollars, not cents, and the currency is US dollars for now.

Pay over X months takes the total and an optional extra amount per installment. The monthly charge is the total divided by the months, rounded up to the cent, plus that extra.

Only the owner and the superuser can change a price. A group admin can still save the other settings, sees the price as text, and cannot wipe out a price by saving an empty form. A Buy button appears only when the group can actually take a payment. Otherwise the page says it is not available to buy yet.

## Phase 2: something to find

Find a group now shows each group's description, its web address, and its price, with a Free, Paid, or All filter. The button is the one that fits you: Member, Request sent, By invitation, Buy, Join, or Request to join.

There is also a site-wide class list at `/classes`. A class page there shows the name, description, lesson titles, schedule, price, and city and state. It does not show the lesson bodies, the files, the meeting link, or a street address. An owner can hide a class from the list with one checkbox. The list is for signed-in members unless the superuser opens it to everyone.

## Phase 3: the checkout itself

I chose direct checkout over a cart. Buy goes to one page for one group or class, which lists every active price for it. The payment page is Stripe's hosted Checkout, so the site never sees a card number.

Access starts only after Stripe's signed webhook confirms the payment and the buyer's email is verified. Opening the return page does not grant anything. If the buyer cancels, they go back to the page they came from and see "Checkout canceled. You were not charged." A checkout session expires after 30 minutes, and the number of new sessions per account and per address each hour is limited.

The buyer gets a confirmation. The owner gets a sale notice, which is on by default and can be turned off. My purchases shows each item, the date, the amount, the plan, and the next payment.

## Phase 4: what happens after the sale

This is the part most first versions skip.

A failed renewal does not cut someone off at once. The purchase is marked Past due, and access continues for a 7-day grace period. A later payment puts it back to Paid. A buyer can manage a subscription through Stripe's customer portal from My purchases. An owner can cancel at the end of the period or right away, and can refund from the site instead of logging in to Stripe. Disputes are recorded, and the owner is told. Owners get a sales page with a CSV download. The superuser gets a site-wide sales page.

There is also a platform fee setting. It defaults to zero, and it stays at zero.

## Who receives the money

Each group can connect its own Stripe account. A superuser can also let chosen groups charge the site's Stripe account instead, from one list on the site payments page. Saving that list cannot overwrite a choice someone else made after the page was opened.

## The fix that came from using it

Sales on the site's own Stripe account stayed Pending. The webhook only knew the signing secret for connected accounts. The fix added a second secret and a check: when the buyer lands on the return page, or when the nightly worker runs, the site asks Stripe whether that checkout was paid.

That created a new risk. The return page, the webhook, and the worker could all see the same pending purchase at once. Now only one of them can record the payment. The test runs that race ten times and checks for exactly one payment, one receipt, and one owner notice.

The test suite went from 227 tests at the start of this work to 266 at the end. Every phase arrived as its own pull request, and none of them made a live Stripe call.

## Where it stands

Checkout runs against Stripe's test environment. Live mode stays off until I approve it in writing. The same code also runs a second site, so the design had to work for more than one owner from the start.

If you have built checkout for a membership or a class business, tell me what I missed. The open questions go into the next version of the specification.

## Come try it

Check out the site at [exit719.com](https://exit719.com). It is my live test site, up 24/7. Register, look around, and send me your feedback.
