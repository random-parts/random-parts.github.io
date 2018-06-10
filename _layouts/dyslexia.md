---
layout: default
---

<span class="adhd adhd-intro">
  <h3>An {{page.headline}}</h3>
  {{content}}
</span>

<div class="half">
  <div class="tab">
    <input id="tab-one" type="checkbox" name="tabs">
    <label for="tab-one">Interesting & Helpful Links</label>
    <div class="link-panel">
      {% include data-links.html file='adhd-dyslexia-links' %}
    </div>
  </div>

  <hr>

  <div class="adhd-tabordion">
    {% assign collection = site.versioned_files %}
    {% assign diffs  = site.array %}
    {% assign ver  = site.array %}

    {% for doc in collection %}
      {% if doc.id contains 'diffs' %}
        {% assign diffs = diffs | push: doc %}
      {% else %}
        {% assign ver = ver | push: doc %}
      {% endif %}
    {% endfor %}

    {% for article in ver %}
      <input name="tabs" type="radio" id="{{article.slug}}-{{forloop.index}}" class="input"/>
      {% if article.ver != "1" %}
        <label for="{{article.slug}}-{{forloop.index}}" class="label">Revision {{article.ver}}</label>
      {% else %}
        <label for="{{article.slug}}-{{forloop.index}}" class="label">Version {{article.ver}}</label>
      {% endif %}
      <div class="panel">
        <article>
        <span class="adhd">
          <h4>
            version: {{article.ver}}
            <br>
            commit: <a href='https://github.com/random-parts/random-parts.github.io/commit/{{article.commit}}'>{{article.commit}}</a>
            <br>
            word-count:{{article.content | number_of_words}}
          </h4>
          <p>{{article.content}}</p>
        </span>
        </article>
      </div>
    {% endfor %}
    {% for article in diffs %}
      <input name="tabs" type="radio" id="{{article.slug}}-{{forloop.index}}" class="input"/>
      <label for="{{article.slug}}-{{forloop.index}}" class="label">Compare {{article.ver[0]}}v{{article.ver[1]}}</label>
      <div class="panel">
        <article>
        <span class="adhd">
          <h4>
            compare: <a href='https://github.com/random-parts/random-parts.github.io/commit/{{article.commit[0]}}?short_path={{article.commit[1] | slice: 0, 7}}#diff-{{article.commit[1]}}'>{{article.ver[0]}} vs {{article.ver[1]}}</a>
          <br>
            commit: [<a href="https://github.com/random-parts/random-parts.github.io/commit/{{article.commit[0]}}">{{article.commit[0]}}</a>, <a href="https://github.com/random-parts/random-parts.github.io/commit/{{article.commit[1]}}">{{article.commit[1]}}</a>]
          <br>
            changes: <del>deleted:</del> {{article.diff_del}}, <ins>inserted:</ins> {{article.diff_ins}}
          </h4>
          <p>{{article.content}}</p>
        </span>
        </article>
      </div>
    {% endfor %}
  </div>
</div>
