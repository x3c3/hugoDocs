---
title: ge
description: Returns the boolean truth of arg1 >= arg2 && arg1 >= arg3.
categories: [functions]
menu:
  docs:
    parent: functions
keywords: []
namespace: compare
relatedFuncs:
  - compare.Eq
  - compare.Ge
  - compare.Gt
  - compare.Le
  - compare.Lt
  - compare.Ne
signature:
  - compare.Ge ARG1 ARG2 [ARG...]
  - ge ARG1 ARG2 [ARG...]
---

```go-html-template
{{ ge 1 1 }} → true
{{ ge 1 2 }} → false
{{ ge 2 1 }} → true

{{ ge 1 1 1 }} → true
{{ ge 1 1 2 }} → false
{{ ge 1 2 1 }} → false
{{ ge 1 2 2 }} → false

{{ ge 2 1 1 }} → true
{{ ge 2 1 2 }} → true
{{ ge 2 2 1 }} → true
```
