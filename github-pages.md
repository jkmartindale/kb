# github-pages

### Resources
- [Liquid template tags and filters](https://shopify.github.io/liquid/)
- [Jekyll-provided filters](https://jekyllrb.com/docs/liquid/filters/)
- [Jekyll-provided tags](https://jekyllrb.com/docs/liquid/tags/)
- [Jekyll variables](https://jekyllrb.com/docs/variables/)
- [Plugins available](https://pages.github.com/versions/)
- [Syntax highlighter language names](https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers)

### Hide content from GitHub.com or GitHub Pages
There's lots of cases where content (such as scripts) won't be rendered properly on GitHub.com but will be rendered on GitHub Pages. Maybe you want to direct people from GitHub.com to GitHub pages, but don't want that text to display on the GitHub Pages version.

Instead of having to maintain two different branches of content or just being content with ugly unrendered content on GitHub.com, do this:
<!-- {% raw %} -->
```md
<!--{% comment %}-->
# GitHub.com

This content will only be visible on GitHub.com.

<!--{% endcomment %}-->
{% comment %}
<!--{% endcomment %}
# GitHub Pages

This content will only be visible on rendered GitHub Pages.

{% comment %}-->
{% endcomment %}
```
Visitors to the markdown file on GitHub.com will see the following at the bottom of the document:
```
{% comment %}

{% endcomment %}
```
<!-- {% endraw %} -->
So this method isn't perfect, but it's much less distracting than before.

### Hide the first heading
Sometimes you want page titles to be programmically generated because you're a lazy typer and setting front matter makes your document look ugly on GitHub.com. You can edit a theme to display the right title but then plugins like [jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag) will use `page.title` for other things you can't control, and that sucks.

GitHub Pages has the plugin [jekyll-titles-from-headings](https://github.com/benbalter/jekyll-titles-from-headings), which sets the title based on the first Markdown heading it sees. That's great except for when the theme already displays the page title so having a heading in addition to that is redundant and dumb.

Good thing the plugin has an option to strip out the heading it used as a title. Just add this to your `_config.yml`:
```yaml
titles_from_headings:
  strip_title: true
```

This option is how this repository can display in-markdown page titles on GitHub.com but only show them in the page header on GitHub Pages.

### List of pages
<!-- {% raw %} -->
```liquid
<ul>
  {% for page in site.pages %}
    {% if page.title %}
      <li><a href="{{ page.url | split: ".html" | first | relative_url }}">{{ page.title }}</a></li>
    {% endif %}
  {% endfor %}
</ul>
```
<!-- {% endraw %} -->
