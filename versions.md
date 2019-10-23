---
layout: page
title: Version Numbers
permalink: /versions/
---

# Version numbers

The version numbers in the API and in the XML attact a lot of heat, so let's discuss them thoroughly.

## SemVer

A popular concept in software is to use SemVer, or Semantic Versioning, where the numbers used imply something about the compatibility. In summary:

Given a version number MAJOR.MINOR.PATCH, increment the:

 * MAJOR version when you make incompatible API changes,
 * MINOR version when you add functionality in a backwards compatible manner, and
 * PATCH version when you make backwards compatible bug fixes.

### Semver applied to Rest APIs

https://stackoverflow.com/questions/27901549/semantic-versioning-of-rest-apis explains things clearly - in semantic versioning, only the major number is of interest to API consumers.

### In OpenStreetMap

To be clear: **We don't use SemVer in the API versions**. We currently use this system:

 * First number has always been zero
 * Second number is changed when we make backwards incompatible changes to the API.

If we want to move to SemVer for our API in future, we could simply convert the second number to be the MAJOR number. So instead of version `0.8`, we can just call it version `8`. I don't think that we should make this change for 0.7 though.

## Version numbers in the OpenStreetMap API

We only change the version number when we have to make a backwards-incompatible change. In the lifetime of 0.6 we've made dozens of backwards-compatible changes to the API - for example adding notes, or adding comments to changesets.

## Version numbers in the XML

These simply reflect the API version used to generate the response. In particular, they don't represent either of the following concepts:

 * an "underlying data model". The abstract data model for OpenStreetMap changes frequently, for example adding comments to changesets, and we don't change the version number. Therefore it doesn't represent an abstract data model version.
 * an "OSM document format". If you consider the API 0.6 changes, only a small number of elements of openstreetmap data were affected by adding changesets. But the version number in all responses changed, even though e.g. traces and user preferences had identical content. So the number changes with the API, not the format of the document.
