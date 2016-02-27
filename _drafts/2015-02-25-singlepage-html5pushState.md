---
layout: post
title: Single Page and HTML5 pushState
description: "Demo post displaying the various ways of highlighting code in Markdown."
category: CSS/HTML/Javascript
tags: [HTML5, pushState]
comments: true
share: true
---

最近一段时间做单页面程序的时候，页面之间都是通过Ajax请求跳转的，因为浏览器地址栏URL未改变，所以浏览器前进和回退是不可用的。后来查询到可以使用HTML5的新API解决
###主要的两个API
1. **history.replaceState(state, title, url)**
state：表示与该URL对应产生的新的history的状态信息，当用户前进或者后退的时候触发popstate事件的时候，这个state对象会被传递给event对象。在Firefox中，该对象会被序列话到磁盘上，限制大小为640K，超过会报异常。
title：这个参数现在为止浏览器都会忽略，所以不管，设置为空字符串就可以。
url：就是我们想要在地址栏显示的地址，但是浏览器不会立即去加载这个地址，当然不允许跨域。
1. **history.pushState(state, title, url)**
三个参数和replaceState意义一只，不同的是replaceState替换当前url的history信息，而pushState新建当前url的history信息。
注：貌似pushState()和window.location = "#foo"挺类似的都会创建与当前document关联的history信息。

###window.onpopstate
当用户点击前进或者后退时候，将会触发[popstate](https://developer.mozilla.org/en-US/docs/Web/Events/popstate)事件
{% highlight css %}
window.addEventListener('popstate', function(e) {
  // e.state 表示history的状态信息
});
{% endhighlight %}

[^1]: <http://en.wikipedia.org/wiki/Syntax_highlighting>

### Pygments Code Blocks

To modify styling and highlight colors edit `/assets/less/pygments.less` and compile `main.less` with your favorite preprocessor. Or edit `main.css` if that's your thing, the classes you want to modify all begin with `.highlight`.

{% highlight css %}
#container {
    float: left;
    margin: 0 -240px 0 0;
    width: 100%;
}
{% endhighlight %}

{% highlight html %}
{% raw %}
<nav class="pagination" role="navigation">
    {% if page.previous %}
        <a href="{{ site.url }}{{ page.previous.url }}" class="btn" title="{{ page.previous.title }}">Previous article</a>
    {% endif %}
    {% if page.next %}
        <a href="{{ site.url }}{{ page.next.url }}" class="btn" title="{{ page.next.title }}">Next article</a>
    {% endif %}
</nav><!-- /.pagination -->
{% endraw %}
{% endhighlight %}

{% highlight ruby %}
module Jekyll
  class TagIndex < Page
    def initialize(site, base, dir, tag)
      @site = site
      @base = base
      @dir = dir
      @name = 'index.html'
      self.process(@name)
      self.read_yaml(File.join(base, '_layouts'), 'tag_index.html')
      self.data['tag'] = tag
      tag_title_prefix = site.config['tag_title_prefix'] || 'Tagged: '
      tag_title_suffix = site.config['tag_title_suffix'] || '&#8211;'
      self.data['title'] = "#{tag_title_prefix}#{tag}"
      self.data['description'] = "An archive of posts tagged #{tag}."
    end
  end
end
{% endhighlight %}


### Standard Code Block

    {% raw %}
    <nav class="pagination" role="navigation">
        {% if page.previous %}
            <a href="{{ site.url }}{{ page.previous.url }}" class="btn" title="{{ page.previous.title }}">Previous article</a>
        {% endif %}
        {% if page.next %}
            <a href="{{ site.url }}{{ page.next.url }}" class="btn" title="{{ page.next.title }}">Next article</a>
        {% endif %}
    </nav><!-- /.pagination -->
    {% endraw %}


### Fenced Code Blocks

To modify styling and highlight colors edit `/assets/less/coderay.less` and compile `main.less` with your favorite preprocessor. Or edit `main.css` if that's your thing, the classes you want to modify all begin with `.coderay`. Line numbers and a few other things can be modified in `_config.yml` under `coderay`.

~~~ css
#container {
    float: left;
    margin: 0 -240px 0 0;
    width: 100%;
}
~~~

~~~ html
{% raw %}<nav class="pagination" role="navigation">
    {% if page.previous %}
        <a href="{{ site.url }}{{ page.previous.url }}" class="btn" title="{{ page.previous.title }}">Previous article</a>
    {% endif %}
    {% if page.next %}
        <a href="{{ site.url }}{{ page.next.url }}" class="btn" title="{{ page.next.title }}">Next article</a>
    {% endif %}
</nav><!-- /.pagination -->{% endraw %}
~~~

~~~ ruby
module Jekyll
  class TagIndex < Page
    def initialize(site, base, dir, tag)
      @site = site
      @base = base
      @dir = dir
      @name = 'index.html'
      self.process(@name)
      self.read_yaml(File.join(base, '_layouts'), 'tag_index.html')
      self.data['tag'] = tag
      tag_title_prefix = site.config['tag_title_prefix'] || 'Tagged: '
      tag_title_suffix = site.config['tag_title_suffix'] || '&#8211;'
      self.data['title'] = "#{tag_title_prefix}#{tag}"
      self.data['description'] = "An archive of posts tagged #{tag}."
    end
  end
end
~~~