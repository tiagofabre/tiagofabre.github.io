---
layout: post
title: "Semantic coupling"
subtitle: "Summary of 'The Perils of Semantic Coupling' by Michael Nygard"
comments: true
categories: "summary semantic coupling complexity"
tags: "english"
---

> This summary blog post series is a mechanism to help me to wrap my head around new concepts. I don't intend to claim the ownership of these ideas and the content inside it.

> Based on Michael Nygard blog post ["The Perils of Semantic Coupling"](https://www.michaelnygard.com/blog/2015/04/the-perils-of-semantic-coupling/)

Many organizations run into trouble when they try to merge companies, create new line of business or create a partnership. Update the codebase to support that is so costly that many times is more expensive than the benefits. This is always a risky and costly process as long as change of cardinality that usually happens in these cases.

An aggravating factor is the amount of shared concepts between the services. Usually it appear as data types or entity names that pop up in many services and it's called `Semantic coupling`.

As an example, let's think about a retailing system with an entity called SKU that represents something that can be sold. Usually it has a large number of attributes that describe how the item is priced, delivered, displayed on the web, upsold/cross-sold, reviewed, categorized and taxed.

<center>
    <img src="/assets/img/mdm-sku.png">
</center>

As shown in the diagram, a lot of contexts require the SKU, now what if a major change is made to it? A change on each context that depends on SKU will needed but the way it's structured this surface is too large and costly.

For example, the pricing service doesn't need to know that it is pricing SKUs. It just needs to price "things that can be priced.". This way we can add an entirely new universe of things to price, without forcing everything on Earth to be a SKU!

During the planning phase we should ask: Does this service really care about about that field? (in this example SKU). Or does it care about something that a SKU happens to possess?

Usually what the service really cares about is Things that can be "Xed" as Priced, taxed, shipped, reviewed, etc. Are SKUs the only things that can be taxed? Are they the only things that can be reviewed? Etc.

Applying these concepts:
- The service will shrink 
- The service will become more general
- Each service will own its own space of identifiers
- The organization will be more maneuverable

> The key point I want to make here is that a concept may appear to be atomic just because we have a single word to cover it. Look hard enough and you will find seams where you can fracture that concept. Don't share the whole thing. Don't couple all your downstream systems to the whole concept, and definitely don't couple your downstream to a complex of related concepts! It's a cardinal sin.
