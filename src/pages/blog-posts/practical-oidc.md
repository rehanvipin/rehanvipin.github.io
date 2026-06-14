---
title: 'Curl & OIDC'
pubDate: 2026-06-13
description: 'How to make curl work with oidc'
tags: ["blogging", "security"]
layout: ../../layout/BlogPost.astro
---
# Using curl to access OIDC endpoints
I came across an interesting setup for OIDC. Pretty much every industry has been using it at this point.
However, the way it was used was for inter-application communications. IMO, that's not the best use case for it. Especially considering that there are no separate resource servers and application servers.

In any case, that setup is not the usual way most people interact with OIDC, and there's not a lot of non-AI non-ADs explanation of how this setup works and how you'd use your normal dev tools to interact with it. I thought a small post should help.

I don't actively work on my blog's SEO, so not a lot of people might actually read this :P

<br/>

**Article under progress**