---
layout: post
title: "learning riak"
published: true
date: 2013-07-09 10:15
comments: true
categories: 
---

The Flatiron School just started allowing us to order any programming book we want (as long as we explain why it might be useful), so I decided to take full advantage and explore the world of "NoSQL" by reading the Riak handbook over the long weekend.

My general sense of people using "NoSQL" data stores was that in 95% of use cases a RDBMS made more sense. But, as long as Mongo stayed hip, people would blindly use it. I wanted to answer this question for myself: If your data is relational, does it make sense to use Mongo?
<!--more-->
This whole line of inquiry eventually led me to the CAP theorem and Riak.  Around 2000, Eric Brewer came out with his paper/conjecture called the CAP Theorem [Brewer Paper](http://www.cs.berkeley.edu/~brewer/cs262b-2004/PODC-keynote.pdf). The CAP Theorem was eventually proved and started a lot of the discussions around NoSQL. CAP Theroem essentially says that in any distributed system you can't have consistency (c), availability (a), and partition tolerance (p) all at the same time: You can only choose two out of the three.

Consistency means that if you have many nodes with the same data, and you read data from more than one at once, you should get the exact same result. Availability means that I should be able to read from all nodes at all times. Partition tolerance means that if nodes are physically separated from each other, usually by network problems, they should still be able to serve both reads and writes.  

The theorem states that since we assume that all computers will have network problems and be partitioned from the rest of the nodes at SOME point, you HAVE to pick P as one of the two of three in CAP you are allowed.  So then the question really is, do you compromise your availability or consistency?

A simple example:

Suppose you have three nodes, all with the same data. You try to write data to all three, but one node is unreachable. When you go to read data, you might get stale data from the node that missed the write earlier. If the system allows you to read from the stale node before it's been synced up, the system has chosen availability of data as its focus.If it won't give you the data until everything has been synced up, it's chosen consistency and sacrificed availability. 

So, either you can get all data all of the time, and some of it might be wrong, or you get can all of the data most of the time and it's always right.  According to the book, many developers claim that their systems are AC systems. This shows a fundamental misunderstanding of CAP. At some point, all systems will face network partitions, or a node will go down; you can't choose P. The lack of P chooses you. 

So what does Riak choose?  The cool thing about Riak is that it let's you decide. Riak was based on a paper that came out of Amazon in 2007 about Dynamo DB, Amazon's internal "eventually consistent" database. Project Voldemort and CouchDB are also based on this idea of eventual consistency. Riak alows you to tune your needs of consistency and availability. Interally each group within Amazon has different business cases for when they would prefer to have their data be always available and possibly wrong, or always correct and sometimes unavailable. 

Let's say you have a system with five nodes. You can specify that for any write to be successful it has to be written to W node.  The higher W value you pick the higher your consistency but the higher probability that a write might fail due to an unreachable node. As you lower W your data becomes more likely to successfully write but has a higher probability of being inconsistent - you're more likely to read data from a node that hadn't been updated. A higher W will also affect speed: The more nodes that must be written to, the higher the network latency.

For reads, the logic is similar. If you need to read consistent data from R nodes for a read to be successful you increase your consistency but also increase the probability that a node is unreachable or has to wait for an update. As you lower your R, the probability a read is successful increases but the read is more likely to have inconsistent data. As you tune both R and W towards N you are lowering your ability to tolerate P (partitions). If R and W are 100%, you can no longer tolerate any partition.

The most common scenario in real world applications is that a write will reach all the relevant nodes eventually, so that all nodes have the same data. Eventually, the data in the whole cluster will be consistent for this particular piece of data, no matter how long it takes, even after network partitions. This is the origin of the term eventual consistency.

## Does Riak replace traditional RDBMS's?

In a word, no.  Riak is really cool, and I'm excited to play with it, but it solves a very different use case than the traditional SQL databases. 

The Riak data model doesn't really focus on objects that relate to each other. You can use linking to relate object, but there's not really any way to query Riak in the way most web developers are used to. You can use map reduce to replicate that functionality, but you'd have to write ad hoc map reduce statements every time you needed data which is not really what it's for.  Map reduce is really for batch processing of data, not real-time application access to the database. You can also add Lucene to Riak to do full text search of data, but again, this isn't really what we want.

The simplest example of why Riak doesn't cut it is there's really no notion of a collection of Objects. Riak has buckets, but this is really just a string key they add to your actual key. You can't ask Riak for all the things in X bucket. It still has to sort through every key in the db to see if it matches the string "X". For this same reason, you can't count all the objects in a bucket. Riak does have the notion of relationships through "linking" but this really works more like a graph db than traditional relationships as we think of them in the SQL world. 

The best way to think of Riak is a key-value store on steroids. It deals really well with distributed storage and replication, fails gracefully, and allows you to tune the AC part of CAP to your heart's content.