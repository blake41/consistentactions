---
layout: post
title: "book learnin"
date: 2013-07-09 11:25
published: false
comments: true
categories: 
---

I generally have a tendency to use reading as a way to hide from programming.  As long as I'm reading I can convince myself I'm getting better.  I often find my subconscious starts skimming as soon as I reach tougher concepts in any book but quieting my conscious mind by saying I get this I don't need to read it carefully.  As I've noticed this habit I've started to institute two rules for myself.  Program before you read, and prove that you know it.  Thi

The first one was some of the best advice I ever got from Nick at Hacker School.  I was trying to learn Javascript.  He suggested that rather than doing what was comfortable, which would have been reading every book known to man on Javascript and THEN starting to code, that I should reverse the process.  He knew I already knew enough JS to get by, so I should pick a simple project and build it only stopping for a few minutes to Stack Overflow or consult a reference if I got stuck on a particular bit of syntax.  I decided to build a simple HTML based tic toe game without doing any reading.  The first time I built it it was terrible but I had a working game in about 4 hours, substantially faster than I thought I would be able to do it.  I did a code review with Nick and he pointed out that I had coupled the game implementation with its view and wasn't using idiomatic javascript.  So I rewrote the game using what he taught me and tried to seperate the game from the view.  This time I had two objects, the game, and the view, and they just passed messages to each other.  This was actually the first time rails MVC pattern actually clicked for me.  Rails enforces good practices on you so I had never really taken time to reflect on what I was doing and why it made.  I did another code review with Nick and he pointed out some more optimizations I could do to my JS code so I made those and reviewed again.  The last iteration I decided to add backbone.js so I could see what backbone gave me as opposed to what I had built from scratch.