---
layout: default
title: travel
category: travel
permalink: /travel/
---
{% assign collection = site[page.category] | sort: "headline", "first" %}

<h1>{{page.category}}</h1>
<nav>
  <ul>
  {% for article in collection %}
    {% if article.headline %}
    <div class="tabordion">
      <section id="section-{{article.slug}}-{{forloop.index}}">
        <input type="radio" name="sections" id="option-{{article.slug}}-{{forloop.index}}">
        <label for="option-{{article.slug}}-{{forloop.index}}">{{article.headline}}<span><a href="{{page.url | prepend: site.baseurl}}{{article.slug}}">single view</a></span></label>
        <article>
        <div class="wrapper">
          {% if article.strava %}
            {% include strava.html strava_embed=article.strava headline=article.headline %}
          {% endif %}
          {{article.content}}
        </div>
        </article>
      </section>
    </div>
    {% endif %}
  {% endfor %}
  </ul>
</nav>