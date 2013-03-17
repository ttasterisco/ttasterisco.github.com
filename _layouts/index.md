---
layout: default
css: ["/assets/css/index.css", "/assets/css/about.css"]  # ARGH, Y U NO OVERRIDE THIS IN CHILD TEMPLATE?
---

<div class="header">
  <div class="contact">
    <a href="/about.html">
      ?
    </a>
  </div>

  <div class="title">
    <a class="link" href="/">{{site.name}}</a>
  </div>

  <br />

  <div class="subtitle">
    highly opiniated writings.
  </div>
</div>

<hr class="divider" />

<div class="content">
  {{ content }}
</div>
