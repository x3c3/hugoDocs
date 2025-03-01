---
title: partialCached
description: Allows for caching of partials that do not need to be re-rendered on every invocation.
categories: [functions]
menu:
  docs:
    parent: functions
keywords: []
namespace: partials
relatedFuncs:
  - partials.Include
  - partials.IncludeCached
signature: 
  - partials.IncludeCached LAYOUT CONTEXT [VARIANT...]
  - partialCached LAYOUT CONTEXT [VARIANT...]
---

The `partialCached` template function can offer significant performance gains for complex templates that don't need to be re-rendered on every invocation.

**Note:** Each Site (or language) has its own `partialCached` cache, so each site will execute a partial once.

**Note**: Hugo renders pages in parallel, and will render the partial more than once with concurrent calls to the `partialCached` function. After Hugo caches the rendered partial, new pages entering the build pipeline will use the cached result.

Here is the simplest usage:

```go-html-template
{{ partialCached "footer.html" . }}
```

You can also pass additional arguments to `partialCached` to create *variants* of the cached partial. For example, if you have a complex partial that should be identical when rendered for pages within the same section, you could use a variant based upon section so that the partial is only rendered once per section:

{{< code file="partial-cached-example.html" >}}
{{ partialCached "footer.html" . .Section }}
{{< /code >}}

If you need to pass additional arguments to create unique variants, you can pass as many variant arguments as you need:

```go-html-template
{{ partialCached "footer.html" . .Params.country .Params.province }}
```

Note that the variant arguments are not made available to the underlying partial template. They are only use to create a unique cache key. Since Hugo `0.61.0` you can use any object as cache key(s), not just strings.

See also [The Full Partial Series Part 1: Caching!](https://regisphilibert.com/blog/2019/12/hugo-partial-series-part-1-caching-with-partialcached/).
