{% assign collection = include.collection %}

{% for item in site[collection] %}
[{{item.slug}}]: {{item.url | prepend: site.baseurl | prepend: site.url}}
{% endfor %}

[TILs]: {{"/til/" | prepend: site.baseurl | prepend: site.url}}