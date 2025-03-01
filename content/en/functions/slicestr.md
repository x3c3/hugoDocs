---
title: slicestr
description: Creates a slice of a half-open range, including start and end indices.
categories: [functions]
menu:
  docs:
    parent: functions
keywords: []
namespace: strings
relatedFuncs: []
signature:
  - strings.SliceString STRING START [END]
  - slicestr STRING START [END]
---

For example, 1 and 4 creates a slice including elements 1 through 3.
The `end` index can be omitted; it defaults to the string's length.

* `{{ slicestr "BatMan" 3 }}` → "Man"
* `{{ slicestr "BatMan" 0 3 }}` → "Bat"
