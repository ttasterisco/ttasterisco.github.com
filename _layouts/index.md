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
  <div>
      <h2>travel tips</h2>    
      {% for post in site.categories["travel-tips"] %}
      <div class="post">
          <div class="date">{{ post.date }}</div>
          <div class="title">
          <a href="{{ post.url }}">{{ post.title }}</a>
          </div>
      </div>
      {% endfor %}      
  </div>
    
  <div>
      <h2>cities</h2>    
      {% for post in site.categories["cities"] %}
      <div class="post">
          <div class="date">{{ post.date }}</div>
          <div class="title">
          <a href="{{ post.url }}">{{ post.title }}</a>
          </div>
      </div>
      {% endfor %}
  </div>

  <div>
      <h2>living</h2>
      {% for post in site.categories["life"] %}
      <div class="post">
          <div class="date">{{ post.date }}</div>
          <div class="title">
          <a href="{{ post.url }}">{{ post.title }}</a>
          </div>
      </div>
      {% endfor %}
  </div>
</div>
