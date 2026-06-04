---
title: Database Fundamentals
draft: false
tags:
  - computer-science
  - database
---
 
In this lecture we spoke about why databases matter, fundamental problems, and database types.

A [[database]] is a collection of related data, that typically represents some aspect of the real world.

A [[DMBS]] (Database Management System) is a software that manages a database, allowing apps to store & retrieve data. [[DBMS]] hides complexity from the developer.

[[Data Independence]] - Apps are insulated from storage details. This is the reason why even if hardware on your phone changes, Instagram is still the same.

---
## Fundamental problems

[[Data Redundancy]] - this happens when the same information is stored in different places, such that when the information is updated in one place, it is not propagated to other places. However, this has some benefits, such that it is easier to recover data when it is lost in one place.

[[Lost Updates]] - If an update to data fails, for example a bank transfer, data, in this case your money, could be lost. The solution to this problem was through the [[DBMS]], that allows for the reversal of a process when it fails, so the money would be restored back into its original account.

---
## Relational Databases ([[RDBMS]])

An [[RBDMS]] is a [[database]] that is organised in tables with strict relationships. It uses [[SQL]], and is [[ACID]] compliant. It's best for data where __accuracy__ is crucial.

__Popular Examples__: [[PostgreSQL]]

[[ACID]] - [[Atomicity]], [[Consistency]], [[Isolation]], [[Durability]].


## Not only SQL Databases ([[NoSQL]])
+ See [COMP9313](https://www.handbook.unsw.edu.au/undergraduate/courses/2026/COMP9313?year=2026)

## Retrieval-Augmented Generation [[RAG]]

__Problem__: LLMs hallucinate or forget information.
__Solution__: Store facts in a [[Vector Database]] --> Feed to LLM --> Accurate answers.
__Result__: AI is only as smart as its database.

[Experiment with RAG](https://ragplay.vercel.app/experiment)



---
For a more in depth study of how databases work, see [COMP9315](https://www.handbook.unsw.edu.au/undergraduate/courses/2026/COMP9315?year=2026)
