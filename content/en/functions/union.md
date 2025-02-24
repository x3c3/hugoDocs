---
title: union
description: Given two arrays or slices, returns a new array that contains the elements or objects that belong to either or both arrays/slices.
categories: [functions]
menu:
  docs:
    parent: functions
namespace: collections
relatedFuncs:
  - collections.Complement
  - collections.Intersect
  - collections.SymDiff
  - collections.Union
signature:
  - collections.Union SET1 SET2
  - union SET1 SET2
---

Given two arrays (or slices) A and B, this function will return a new array that contains the elements or objects that belong to either A or to B or to both. The elements supported are strings, integers, and floats (only float64).

```go-html-template
{{ union (slice 1 2 3) (slice 3 4 5) }}
<!-- returns [1 2 3 4 5] -->

{{ union (slice 1 2 3) nil }}
<!-- returns [1 2 3] -->

{{ union nil (slice 1 2 3) }}
<!-- returns [1 2 3] -->

{{ union nil nil }}
<!-- returns an error because both arrays/slices have to be of the same type -->
```

## OR filter in where query

This is also very useful to use as `OR` filters when combined with where:

```go-html-template
{{ $pages := where .Site.RegularPages "Type" "not in" (slice "page" "about") }}
{{ $pages = $pages | union (where .Site.RegularPages "Params.pinned" true) }}
{{ $pages = $pages | intersect (where .Site.RegularPages "Params.images" "!=" nil) }}
```

The above fetches regular pages not of `page` or `about` type unless they are pinned. And finally, we exclude all pages with no `images` set in Page parameters.

See [intersect](/functions/intersect) for `AND`.
