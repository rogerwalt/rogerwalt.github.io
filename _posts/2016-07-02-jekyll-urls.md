---
layout: post
title:  "How to get correct Jekyll URLs on Github Pages"
date:   2016-07-02 18:30:00 +0200
categories: php
---
You know how it is, lazyness is king.
The full story is of course available in the [Jekyll Documentation](https://jekyllrb.com/docs/github-pages/).
Long story short: Replace your `{{ site.url }}` tags by `{{ site.github.url }}`.

The URL to `main.css` was generated the wrong way, the solution was to edit `head.html` and put this in:

{% highlight html  %}
<link rel="stylesheet" href="{{ site.github.url }}/css/main.css">
{% endhighlight %}

Now I'm still figuring out where the Feed and About page links are generated...
