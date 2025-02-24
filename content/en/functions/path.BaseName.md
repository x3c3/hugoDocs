---
title: path.BaseName
description: BaseName returns the last element of a path, removing the extension if present.
categories: [functions]
menu:
  docs:
    parent: functions
keywords: []
namespace: path
relatedFuncs:
  - path.Base
  - path.BaseName
  - path.Clean
  - path.Dir
  - path.Ext
  - path.Join
  - path.Split
signature:
  - path.BaseName PATH
---

If `PATH` is empty, `.` is returned.

**Note:** On Windows, `PATH` is converted to slash (`/`) separators.

```go-html-template
{{ path.BaseName "a/news.html" }} → "news"
{{ path.BaseName "news.html" }} → "news"
{{ path.BaseName "a/b/c" }} → "c"
{{ path.BaseName "/x/y/z/" }} → "z"
```
