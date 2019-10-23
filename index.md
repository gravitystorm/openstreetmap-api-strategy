---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

Since a 50+ comment thread on a PR implementing a tiny part of the API upgrade isn't very user-friendly, I thought I'd make a better site to describe the situation.

# The strategy

## Implement incrementally

I think it's important that we can implement changes one at a time against the master branch of the repository. Since we're a small team of volunteers, it might take us a year or more to implement the changes that we want to make. If this all lived on a branch, it would be a burden to maintain. So therefore I'm proposing the concept of "deployed_api_versions" in the codebase. This allows the codebase to contain code that implements 0.7, but stops it from being available on osm.org until we're ready.

## Stick with decimal version numbers for now

We only increment the version number when we're making backwards-incompatible changes. So if you look at SemVer, these should really be major versions.

If I was given free reign, I would call the next version of the API version 7 instead of 0.7, and the one after that can be v8, and so on. But perhaps this is one change too far for now, and we can debate this again at version (0.)8.

## Deploy 0.7 in parallel to 0.6

All previous upgrades have been "big bang" upgrades, where we turned off the API (sometimes for days) during the upgrade, and only one version of the API was ever available at the same time. Given the size of OSM, and the amount of software that uses the API, I don't think this is feasible today. So my strategy is to ensure that 0.7 will be deployed in parallel to 0.6, to give plenty of time for everyone to upgrade.

## No set list of changes

I believe it's a bad approach to make a set list of changes before trying to implement them. So I first want to build a framework that allows us implement changes to the API, then work through each idea and consider them in turn, and then release 0.7 when we agree that there's enough changes to be worth it. Further changes can be made in 0.8.

# Q&A

## Do we even need a new API version?

Well, yes, I think we do. The counter argument would be that we've used 0.6 for over 10 years, and it works fine, and if it was really needing an upgrade it would have been done already. But my belief is that, despite a number of people wanting to upgrade the API in the past, the major stumbling block has actually been coding the changes, not coming up with them. So my strategy is to make the coding feasible.

## What about areas?

It's the most commonly suggested change for 0.7, but I think it's better to leave it for now. Areas act as a kind of bear-trap for making progress on other parts of the API

## What about the version numbers inside the XML responses?

[There's a whole page about version numbers here]({{ '/versions/' | relative_url}})

## Doesn't this break tons of API consumers?

No, that's why we have version numbers. API consumers can keep using 0.6 both the day before and the day after 0.7 is released.

## What about other software that expects data that matches the 0.6 response format?

It's a fact of life that (thankfully) most OSM data is processed without making calls to the API, so people end up with OSM xml files on disk somewhere and use software to process them.

Depending on what elements the software processes (e.g. nodes, or traces, or users, or changesets, or notes) it may or may not need to be updated to process data from 0.7. Given that we don't know what changes are going to be made yet, it's impossible to say.
