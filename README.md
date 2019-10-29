<!--{% comment %}-->
# kb

Code snippet library and brief technical documentation.

You can browse repository contents here on GitHub.com, but https://jkmartindale.github.io/kb is a bit nicer.
<!--{% endcomment %}-->
{% comment %}
<!--{% endcomment %}
Code snippet library and brief technical documentation.
<p></p>
<ul>
  {% for page in site.pages %}
    {% if page.title %}
      <li><a href="{{ page.url | split: ".html" | first | relative_url }}">{{ page.title }}</a></li>
    {% endif %}
  {% endfor %}
</ul>

{% comment %}-->
{% endcomment %}
