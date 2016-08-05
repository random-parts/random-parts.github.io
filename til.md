---
layout: default
title: Today I Learned
permalink: til/
---
<div class="post-content">
{% assign collection = site.til | group_by: "category" | sort: "name", "first" %}
{% assign counter=0 %}

<div class="tree">
  <ul>
    {% for group in collection %}
    <li><input type="checkbox" id="{{group.name}}" checked><label for="{{group.name}}" id="{{group.name}}"><a href="{{site.baseurl}}{{group.name}}/">{{group.name}}</a></label>
    <ul>
      {% for item in group.items %}
        {% assign counter=counter | plus:1 %}
       <!-- <div class="tabordion"> -->
          <section id="section-{{item.slug}}-{{forloop.index}}">
            <li><a href="{{item.url | prepend: site.baseurl}}">{{item.headline}}</a></li>
          </section>
       <!-- </div> -->
      {% endfor %}
    </ul>
    </li>
    {% endfor %}
  </ul>
</div>