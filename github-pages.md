## github-pages

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
{% raw %}
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
{% endraw %}
So this method isn't perfect, but it's much less distracting than before.
