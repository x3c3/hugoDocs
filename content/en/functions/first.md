---
title: first
description: Slices an array to the first N elements.
categories: [functions]
menu:
  docs:
    parent: functions
keywords: []
namespace: collections
relatedFuncs:
  - collections.After
  - collections.First
  - collections.Last
signature: [first LIMIT COLLECTION]
---

`first` works in a similar manner to the [`limit` keyword in
SQL][limitkeyword]. It reduces the array to only the `first N`
elements. It takes the array and number of elements as input.

`first` takes two arguments:
1. `number of elements`
2. `array` *or* `slice of maps or structs`

{{< code file="layout/_default/section.html" >}}
{{ range first 10 .Pages }}
    {{ .Render "summary" }}
{{ end }}
{{< /code >}}

*Note: Exclusive to `first`, LIMIT can be '0' to return an empty array.*

## `first` and `where` Together

Using `first` and [`where`][wherefunction] together can be very
powerful. Below snippet gets a list of posts only from [**main
sections**][mainsections], sorts it by the `title` parameter, and then
ranges through only the first 5 posts in that list:

{{< code file="first-and-where-together.html" >}}
{{ range first 5 (where site.RegularPages "Type" "in" site.Params.mainSections).ByTitle }}
   {{ .Content }}
{{ end }}
{{< /code >}}


[limitkeyword]: https://www.techonthenet.com/sql/select_limit.php
[wherefunction]: /functions/where/
[mainsections]: /functions/where/#mainsections
