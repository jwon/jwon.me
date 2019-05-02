---
title: "Diagrams With Mermaid"
date: 2019-05-01T15:06:03-07:00
toc: false
images:
tags: 
  - Technology
---

I recently discovered [Mermaid](https://mermaidjs.github.io/), which is a Javascript library for turn markup into pretty diagrams. Here is a basic example copied straight from their homepage:

{{<mermaid align="left">}}
graph LR;
    A[Hard edge] -->|Link text| B(Round edge)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
{{< /mermaid >}}

To show that, all I needed to do was:

```
{{</*mermaid align="left"*/>}}
graph LR;
    A[Hard edge] -->|Link text| B(Round edge)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
{{</* /mermaid */>}}
```

This uses a custom shortcode that looks like:

```
<div class="mermaid" align="{{ if .Get "align" }}{{ .Get "align" }}{{ else }}center{{ end }}">{{ safeHTML .Inner }}</div>
```

I copy-pasted this Hugo custom shortcode from [hugo-theme-learn](https://github.com/matcornic/hugo-theme-learn/blob/master/layouts/shortcodes/mermaid.html), a Hugo theme that provides this shortcode as part of the theme. 

I plan on using creating diagrams to better aid my posts in the future, so stay tuned!