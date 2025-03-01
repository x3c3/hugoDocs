---
title: index
description: Looks up the index(es) or key(s) of the data structure passed into it.
categories: [functions]
menu:
  docs:
    parent: functions
keywords: []
namespace: collections
relatedFuncs:
  - collections.Dictionary
  - collections.EchoParam
  - collections.Group
  - collections.Index
  - collections.IsSet
  - collections.Where
signature:
  - collections.Index COLLECTION INDEXES
  - collections.Index COLLECTION KEYS
  - index COLLECTION INDEXES
  - index COLLECTION KEYS
aliases: [/functions/index/]
---

The `index` functions returns the result of indexing its first argument by the following arguments. Each indexed item must be a map or a slice, e.g.:

```go-text-template
{{ $slice := slice "a" "b" "c" }}
{{ index $slice 1 }} => b
{{ $map := dict "a" 100 "b" 200 }}
{{ index $map "b" }} => 200
```

The function takes multiple indices as arguments, and this can be used to get nested values, e.g.:

```go-text-template
{{ $map := dict "a" 100 "b" 200 "c" (slice 10 20 30) }}
{{ index $map "c" 1 }} => 20
{{ $map := dict "a" 100 "b" 200 "c" (dict "d" 10 "e" 20) }}
{{ index $map "c" "e" }} => 20
```

You may write multiple indices as a slice:

```go-text-template
{{ $map := dict "a" 100 "b" 200 "c" (dict "d" 10 "e" 20) }}
{{ $slice := slice "c" "e" }}
{{ index $map $slice }} => 20
```

## Example: load data from a path based on front matter parameters

Assume you want to add a `location = ""` field to your front matter for every article written in `content/vacations/`. You want to use this field to populate information about the location at the bottom of the article in your `single.html` template. You also have a directory in `data/locations/` that looks like the following:

```
.
└── data
    └── locations
        ├── abilene.toml
        ├── chicago.toml
        ├── oslo.toml
        └── provo.toml
```

Here is an example:

{{< code-toggle file="data/locations/oslo" copy=false >}}
website = "https://www.oslo.kommune.no"
pop_city = 658390
pop_metro = 1717900
{{< /code-toggle >}}

The example we will use will be an article on Oslo, whose front matter should be set to exactly the same name as the corresponding file name in `data/locations/`:

{{< code-toggle file="content/articles/oslo.md" fm=true copy=false >}}
title = "My Norwegian Vacation"
location = "oslo"
{{< /code-toggle >}}

The content of `oslo.toml` can be accessed from your template using the following node path: `.Site.Data.locations.oslo`. However, the specific file you need is going to change according to the front matter.

This is where the `index` function is needed. `index` takes 2 arguments in this use case:

1. The node path
2. A string corresponding to the desired data; e.g.&mdash;

```go-html-template
{{ index .Site.Data.locations "oslo" }}
```

The variable for `.Params.location` is a string and can therefore replace `oslo` in the example above:

```go-html-template
{{ index .Site.Data.locations .Params.location }}
=> map[website:https://www.oslo.kommune.no pop_city:658390 pop_metro:1717900]
```

Now the call will return the specific file according to the location specified in the content's front matter, but you will likely want to write specific properties to the template. You can do this by continuing down the node path via dot notation (`.`):

```go-html-template
{{ (index .Site.Data.locations .Params.location).pop_city }}
=> 658390
```
