+++
title = "Why Microservices?"
date = "2023-01-22T21:17:36-06:00"
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["microservices", "architecture"]
keywords = ["", ""]
description = "Making the case for microservices architecture."
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
ToC = true
+++

## What are microservices?

**Microservices** are small, independently-managed units of software corresponding to fine-grained business domains.

**Synchronous microservices** collaborate directly with one another in order to accomplish business tasks.

**Event-driven microservices** only collaborate directly with an event queue, publishing events for other services to process and processing events produced by other services.

In contrast, a **monolith** is a single, large piece of software whose functionality covers multiple business domains.

While monolithic architectures are suitable for smaller organizations, microservices make sense for larger enterprises and those experiencing rapid growth.

In particular, Software as a Service (SaaS) applications are well-suited to a microservices approach, due to their requirement to operate without maintenance downtime.

## How can microservices help?

### Enable massive scalability

A monolithic codebase must be scaled as a single, unwieldy mass.

With microservices, each narrowly-focused software component can be scaled as much as needed to support demand.

Event-driven microservices maximixe this flexibility by skirting the need to scale interdependent services as a group.

Additionally, lesser-used components can run on lower-powered hardware to reduce costs.

### Improve robustness

If one part of a monolith fails, the whole system is likely to fail.

The clear boundaries between components in a microservices architecture allow the system to continue functioning even while certain areas of service are degraded.

### Harness innovation and best-in-class tools

Because teams construct microservices independently, they can choose the best-in-class language or tool for any given software component.

In this way, teams avoid the technical limitations imposed by a monolith built with a single language or paradigm.

Teams can quickly incorporate cutting-edge technologies as pilot projects to uncover novel ways of benefitting stakeholders.

### Speed up software releases

Since teams can release each microservice independently of other services, new features reach customers faster.

Releasing software in small pieces makes it easier to isolate the source of any errors and perform quick rollbacks of problematic code.

Contrast this with the often cumbersome and risky releases of monolithic software, even for small changes.

### Better align technology with the organization

Since the requirements of separate business domains are encapsulated in separate microservices, developers are empowered to make changes quickly and independently from other teams, minimizing coordination costs.

Smaller units of software enable smaller teams, whose lower communication overhead yields increased productivity.

### Aid comprehensibility

Limiting the scope of microservices makes them easier for developers to understand and manage.

Improved comprehension means fewer bugs and faster development.

### Allow rapid composition of new product offerings

Working with smaller building blocks makes composing new products easier.

Extracting a subset of functionality from a monolith is often prohibitively difficult, but microservices are optimized for this type of mix-and-match development.

## Sources

- Bellemare, Adam. Building Event-Driven Microservices: Leveraging Organizational Data at Scale. O'Reilly Media, 2020.

- Mitra, Ronnie, and Irakli Nadareishvili. Microservices: Up and Running: A Step-by-Step Guide to Building a Microservices Architecture. O'Reilly Media, 2021.

- Newman, Sam. Building Microservices. O'Reilly Media, 2021.
