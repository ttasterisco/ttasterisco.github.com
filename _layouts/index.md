---
layout: default
css: ["/assets/css/index.css", "/assets/css/about.css"]  # ARGH, Y U NO OVERRIDE THIS IN CHILD TEMPLATE?
---

<div class="header">
  <div class="icons">
    <a class="icon feed" href="/atom.xml">
      <img src="/assets/images/feed.png">
    </a>
  </div>

  <div class="title">
    <a class="link" href="/">{{site.name}}</a>
  </div>

  <br />

  <div class="subtitle">
    {{site.description}}
  </div>
</div>

<hr class="divider" />

<div class="content">
  {{ content }}
</div>
