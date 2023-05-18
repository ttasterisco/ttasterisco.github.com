---
layout: default
css: ["/assets/css/index.css", "/assets/css/about.css"]  # ARGH, Y U NO OVERRIDE THIS IN CHILD TEMPLATE?
---

<div class="header">
  <img class="logo" src="/assets/images/logo.png" width="50px" />

  <div class="icons">
    <a class="icon feed" href="/atom.xml">
      <img src="/assets/images/feed.png">
    </a>
  </div>

  <a class="title link" href="/">{{site.name}}</a>

  <br />

  <div class="subtitle">
    {{site.description}}
  </div>
</div>

<hr class="divider" />

<div class="content">
  <!-- TODO: use tabs for these 3 sections -->

  {% if site.categories["travel-tips"] %}
  <div>
      <h2>travel tips</h2>

      <!-- TODO: write a small intro -->

      {% assign travel_posts = site.categories["travel-tips"] | sort: "title" %}
      {% for post in travel_posts %}
      <div class="post">
        <div class="title">
          <a href="{{post.url}}">{{post.title}}</a>
        </div>
      </div>
      {% endfor %}
  </div>
  {% endif %}

  {% if site.categories["cities"] %}
  <div>
      <h2>cities</h2>

      <!-- TODO: write a small intro -->

      {% assign cities = site.categories["cities"] | sort: "title" %}
      {% for post in cities %}
      <div class="post">
        <div class="title">
          <a href="{{post.url}}">{{post.title}}</a>
        </div>
      </div>
      {% endfor %}
  </div>
  {% endif %}

  {% if site.categories["life"] %}
  <div>
      <h2>living</h2>

      <!-- TODO: write a small intro -->

      {% for post in site.categories["life"] %}
      <div class="post">
        <div class="title">
          <a href="{{post.url}}">{{post.title}}</a>
        </div>
      </div>
      {% endfor %}
  </div>
  {% endif %}
</div>
