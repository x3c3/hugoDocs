---
title: strings.ContainsAny
description: Reports whether a string contains any character from a given string.
categories: [functions]
menu:
  docs:
    parent: functions
keywords: []
namespace: strings
relatedFuncs:
  - strings.Contains
  - strings.ContainsAny
  - strings.ContainsNonSpace
  - strings.HasPrefix
  - strings.HasSuffix
  - collections.In
signature: 
  - strings.ContainsAny STRING CHARACTERS
---

```go-html-template
{{ strings.ContainsAny "Hugo" "gm" }} → true
---

The check is case sensitive: 

```go-html-template
{{ strings.ContainsAny "Hugo" "Gm" }} → false
```
