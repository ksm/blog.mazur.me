---
layout: post
title:  "Tracking dependencies with DEPENDENCIES.md"
---

A growing list of third-party libraries is something most development projects have to deal with it. On many projects it can be hard to figure out why a certain dependency was added, or whether it still makes sense to keep it. We can track dependencies through a `DEPENDENCIES.md` document just like we track changes via a `CHANGELOG.md`.

## Writing a dependencies document

There needs to be a good reason for why a dependency gets added to a project. That reason is what we need to write down.

Here's an example:

<script src="https://gist.github.com/ksm/9b717002c16156b06a695f4d67ed2d7a.js"></script>

The above example shows how we can differentiate between different types of dependencies. As an added benefit we can have a a nice overview of what licenses our dependencies use.

This is a technique I've used for a few years on a past project, and it saved a lot of my time when re-evaluating whether some dependencies should be removed. 

## Further reading

The above pattern is a distant relative of Lightweight Architectural Decisions. What this boils down to is we want to track the reasoning behind our decisions, regardless of whether they affect the architecture or a dependency. This reasoning is also best kept by committing it to the project repository such that it sits right next to our code.

- [Lightweight Architecture Decision Records](https://www.thoughtworks.com/radar/techniques/lightweight-architecture-decision-records)
- [Documenting Architecture Decisions](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions)

**Feb 7, 2019 update**: Artsy has their dependency process documented and out in the open. It's a great read. Of note is how the team at Artsy decides whether a dependency should go through the Artsy RFC process. Thank you to [Orta Therox](https://twitter.com/orta) for bringing this to my attention.

- [Adding a Dependency Playbook](https://github.com/artsy/README/blob/master/playbooks/dependencies.md)
