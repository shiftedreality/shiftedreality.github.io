---
layout: post
title: "Boosting Extensibility of Adobe Commerce with App Builder"
date: 2026-07-05 09:30:00 -0500
categories: it-ai
tags:
- adobe
- adobe-commerce
- app-builder
- extensibility
- cloud
---

Adobe Commerce's App Builder unlocks a cleaner way to extend the platform without touching the core codebase — and it's the subject of a piece I wrote for the Adobe Tech blog back in 2023 that's still relevant today.

<!-- more -->

A few years ago I published [Boosting Extensibility of Adobe Commerce with App Builder: Developer Best Practices](https://medium.com/adobetech/boosting-extensibility-of-adobe-commerce-with-app-builder-developer-best-practices-f3c391ac135c) on the Adobe Tech blog. It walks through how to use Adobe Developer App Builder to extend Commerce functionality with minimal changes to the core codebase, and it's held up well as App Builder adoption has grown.

The article covers a few key decisions developers face when building on App Builder:

- **Architecture selection** — choosing between a headless app with its own standalone UI versus a headful app that extends the Commerce admin UI directly, and starting with an API-first approach before building out a full application.
- **API Mesh** — using it as a decoupled layer to combine multiple data sources behind a single GraphQL query, instead of wiring up point-to-point integrations.
- **Headful admin apps** — injecting App Builder applications straight into the Commerce back office, including how to authenticate and map Commerce admin users to Adobe organization users, which is especially useful for SaaS-style extensions with their own business logic.
- **Data integration patterns** — when to reach for GraphQL versus REST, how Adobe I/O Events enables event-driven, push-based integrations, and using Lib/State and Lib/Files for caching and longer-term storage with TTL support.
- **Authentication** — the token exchange flow for Commerce admin integrations, including token rotation and access token provisioning for REST requests.

The throughline across all of it is three benefits that make App Builder worth the investment: **composability** (orchestrating APIs from multiple services into one coherent experience), **maintainability** (independent deployment cycles instead of coupling everything to a Commerce release), and **upgradability** (swapping out components without touching Commerce core).

If you're building extensions for Adobe Commerce and haven't looked at App Builder yet, it's worth the read.
