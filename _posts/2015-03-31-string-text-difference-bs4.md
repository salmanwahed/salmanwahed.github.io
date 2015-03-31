---
layout: post
title: Difference between .string and .text BeautifulSoup
---


<div class="message">
<a href="http://www.crummy.com/software/BeautifulSoup/bs4/doc/">Beautiful Soup</a> is a Python library for parsing HTML and XML documents. It can be used to parse malformed markup, (i.e. non-closed tags). It creates a parse tree for parsed pages that can be used to extract data from HTML, which is useful for web scraping. It is available for Python 2.6+ and Python 3.
</div>

`.string` on a Tag type object returns a NavigableString type object. On the other hand, `.text` gets all the child strings and return concatenated using the given separator. Return type of `.text` is unicode object.

From the <a href="http://www.crummy.com/software/BeautifulSoup/bs4/doc/#navigablestring">documentation</a>, A NavigableString is just like a Python Unicode string, except that it also supports some of the features described in Navigating the tree and Searching the tree.

From the <a href="http://www.crummy.com/software/BeautifulSoup/bs4/doc/#string">documentation</a> on `.string`, we can see that, If the html is like this,
{% highlight html %}
<td>some text</td>
<td></td>
<td><p>more text</p></td>
<td>even <p>more text</p></td>
{% endhighlight %}

`.string` on the four `td` will return,
{% highlight python %}
some text
None
more text
None
{% endhighlight %}
`.text` will give result like this,
{% highlight python %}
some text

more text
even more text
{% endhighlight %}