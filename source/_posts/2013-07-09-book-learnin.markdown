---
layout: post
title: "book learnin"
date: 2013-07-09 11:25
published: false
comments: true
categories: 
---

## They built it, so go to them
If you can't get a mentor to come to you, you'll have to go where the mentors are. Find the wisdom that those mentors have freely offered to those willing to look.  Books are one of the best and worst ways to learn.  It always amazes me that the smartest people in the world write books for us mere mortals and all we have to do is reach out and grab their wisdom.  Add to that twitter, blogs etc and the sum total of amazing programming knowledge in an easily consumable format is astronomical.

##  Buyer Beware
I generally have a tendency to use reading as a way to hide from programming.  As long as I'm reading I can convince myself I'm getting better.  I often find my subconscious starts skimming as soon as I reach tougher concepts in any book but quieting my conscious mind by saying I get this I don't need to read it carefully.  As I've noticed this habit I've started to institute two rules for myself.  Program before you read, and prove that you know it.<!--more-->

## Get the most out of books
When I first started working at Lifebooker I felt in completely over my head.  After some time I started to feel like I was becoming a productive member of the team, and was hoping to figure out the best way to grow.  I had a nagging sense that my code worked, but wasn't the best it could be.  Books were an amazing place to find inspiration on how to do the same thing better.  I read:

- Refactoring - Improving the Design of Existing Code
- Design Patterns in Ruby
- Metaprogramming Ruby
- Objects on Rails
- Rails Antipatterns

These books gave me a view into how good code is written.

The first one was some of the best advice I ever got from [Nick](http://nick.is/) at Hacker School.  I was trying to learn Javascript.  He suggested that rather than doing what was comfortable, which would have been reading every book known to man on Javascript and THEN starting to code, that I should reverse the process.  He knew I already knew enough JS to get by, so I should pick a simple project and build it only stopping for a few minutes to Stack Overflow or consult a reference if I got stuck on a particular bit of syntax.  I decided to build a simple HTML based tic toe game without doing any reading.  The first time I built it it was terrible but I had a working game in about 4 hours, substantially faster than I thought I would be able to do it.  I did a code review with Nick and he pointed out that I had coupled the game implementation with its view and wasn't using idiomatic javascript.  So I rewrote the game using what he taught me and tried to seperate the game from the view.  This time I had two objects, the game, and the view, and they just passed messages to each other.  This was actually the first time rails MVC pattern actually clicked for me.  Rails enforces good practices on you so I had never really taken time to reflect on what I was doing and why it made.  I did another code review with Nick and he pointed out some more optimizations I could do to my JS code so I made those and reviewed again.  The last iteration I decided to add backbone.js so I could see what backbone gave me as opposed to what I had built from scratch.

However, before I heard this advice