---
layout: post
title: Lessons from Code4rena
subtitle: Useful nuggets of knowledge after 6 months of competing
tags: tech, audit, code4rena
---

# Intro
I stumbled across [code4rena](https://code4rena.com/) around mid-April 2022 after reading [this amazing blog](https://cmichel.io/how-to-become-a-smart-contract-auditor/). For those readers who have not heard of code4rena, it is a decentralised, permissionless (fancy words!) platform for allowing cryptocurrency-based projects to have their code audited by experienced auditors and newbies alike with potentially large sums of money as a reward.

[![Code4rena video](https://code4rena.com/images/C4-banner.png)](https://www.youtube.com/watch?v=5xYMiFv_ds0)

After ~6 months of grinding and learning on code4rena, I still consider myself far away from an experienced auditor, but I have compiled a list of small nuggets of knowledge that may be useful to new auditors. Readers should be aware that this information is personal to me and may not (and will not) apply to all auditors.

## 1. Understand What You Are Reading

When auditing and submitting an issue, context matters. This is advice that I have already seen being repeated by other wardens, but it is always worth to read the full project documentation. Not only does it allow you to better understand how the code works, but when you come across an issue, the severity of that issue can wildly vary based on the specific project and context.

I have noticed that the issues which pay **really** well are issues which take context into account, like [this issue by WatchPug](https://code4rena.com/reports/2022-04-jpegd#h-09-bad-debts-should-not-continue-to-accrue-interest). Issues such as using `transferFrom` instead of `safeTransferFrom` are almost always valid irrespective of context but are therefore much easier to spot, thereby paying less.

Admittedly, I have had this issue in the past with the ENS contest, where I did not understand the full architecture of the program. Therefore, a large portion of my issues were invalidated due to incorrectly assessed impact.
## 2. Dream Big Or Go Home

![Inspirational Quote](https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/8763480f-1d06-4aac-a3db-11da2cd888e1/d9fu9p6-792a92bd-6603-45b9-b931-4f8427ab9edf.png?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcLzg3NjM0ODBmLTFkMDYtNGFhYy1hM2RiLTExZGEyY2Q4ODhlMVwvZDlmdTlwNi03OTJhOTJiZC02NjAzLTQ1YjktYjkzMS00Zjg0MjdhYjllZGYucG5nIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.cSxG360UpF_Srf9EnXpjoaJP28ekoO9IdwwP3JO_Wlw)

In the Code4rena discord, I notice that a lot of new wardens often focus on trying to find low-severity issues/low-hanging fruit before they even start searching for medium and high severity issues.

With the recent boom of wardens, low-hanging fruit are not paying anywhere as much as they used to (the $1.00 high severity issues are proof of that). Additionally, if you don't even try then not only do you miss out on good opportunities but when the report for a contest comes out, you will benefit less as you will not know what you missed out on.

Also, when you are starting off, getting a high severity issue can be a major confidence boost and really help motivate you to carry on.

## 3. Patterns Are Everywhere

![Everywhere meme](https://i.imgflip.com/6umgoo.jpg)

Hopefully, this advice applies to most readers, but I will stress this in case you are not aware. **Read through the [reports](https://code4rena.com/reports)!**. In fact, do not only read them but study them. The human brain remembers surprisingly little by just reading, it may be worth your while to make notes on reports. As questions such as: have I seen a similar issue? Can I categorise this issue? How can I spot this issue again in the future?

By studying past reports and issue patterns, you start developing that "wait a minute, I've seen this" instinct which is really helpful for the auditing process.

Some really cool work has been done in this area by categorising issue types [here](https://github.com/Tomosuke0930/C4-report-categolized) and a [neat YouTube video](https://www.youtube.com/watch?v=95Jj3yxVxNI).

## 4. Be Concise and Clear
Nothing beats that satisfying feeling of finding a high severity issue. But finding the issue is only 50% of the work, you need to make sure that you write a report which the sponsors and judges can understand. I have seen quite a few issues which have correctly found a vulnerability/bug yet were reduced to low/invalid due to poor reports. C4Arena have a good guideline on their website but the main points to include are:
* What is the issue?
* Where is the issue? It is usually sufficient to simply add code line numbers however sometimes more detail is required
* The impact of the issue (this really helps justify whether you have a medium/high issue)
* How can the issue be exploited?
* How can the issue be fixed? (If there is no solution, submitting the issue has no benefit to the sponsor)

## 5. Get That ~~Certified+~~ Backstage Role
As of time of writing, the backstage role is a role on the c4rena discord which allows auditors to look at submitted issues straight after a contest finishes. This is really helpful as it can take months from when a contest ends to when the report is released (it took the OpenSea contest about 4 months from contest end to report release). Getting feedback on a contest you have competed in (and can still remember what the contest was about!) is really helpful and you can learn a lot. Currently, to get the backstage role, wardens must meet certain criteria however with enough sunk time, it should not be too difficult to achieve.

## 6. `Out of scope != Do not read`
Many contests either a. define out of scope contracts or b. make external calls to other protocols. It can be a huge mistake to ignore any external contracts not included in the competition scope. This is because it is common in integrations for two separate contracts to have no vulnerabilities but when they interact together, an issue arises due to the caller and callee having different expectations of how actions should be processed.

A nice example is [this report from the mimo competition](https://github.com/code-423n4/2022-04-mimo-findings/issues/123). A contract in the mimo protocol would take flash loans and always assume that all flash loans it receives were initiated by itself. However, Aave allowed an arbitrary user to call a flash loan and send it to a `receiver`. This means that the mimo contract's assumptions were subverted (as it received a flash loan from Aave which was not initiated by itself) and an attacker could wreak a lot of havoc.
# Outro
Hopefully this post has taught new auditors some nice tricks to help their journey. All in all, as long as you enjoy the process and the satisfaction of finding an issue outweighs the monotony of reading large (often repetitive) programs, you should be well on your way to becoming an experienced auditor.

As University starts, my free time dedicated to auditing will drop sharply but I will still be lurking on the code4rena server and on discord so see you around!

