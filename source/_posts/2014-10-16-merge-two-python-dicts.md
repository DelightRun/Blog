---
layout: post
title: 合并两个Python字典 
date: 2014-10-16 19:55:24 +0800
comments: true
categories: [Python]
---

> [原帖在此](http://stackoverflow.com/questions/38987/how-can-i-merge-two-python-dictionaries-in-a-single-expression)

合并两个Python字典，如：

{% codeblock lang:python %}
>>> x = {'a': 1, 'b': 2}
>>> y = {'c': 3, 'd': 4}
{% endcodeblock %}

希望得到：

{% codeblock lang:python %}
>>> z = {'a':1, 'b':2, 'c':3, 'd':4}
>>> z = {'a':1, 'b':2, 'c':3, 'd':4}
{% endcodeblock %}

解决方案有两种

<!-- more -->

方法一
------

本方法速度不如第二种方法快：

{% codeblock lang:python %}
>>> x = {'a': 1, 'b': 2}
>>> y = {'c': 3, 'd': 4}
>>> z = dict(x.items() + y.items())
>>> z
{'a':1, 'b':2, 'c':3, 'd':4}
{% endcodeblock %}
    
在Python3下略有不同：

{% codeblock lang:python %}
>>> x = {'a': 1, 'b': 2}
>>> y = {'c': 3, 'd': 4}
>>> z = dict(list(x.items()) + list(y.items()))
>>> z
{'a':1, 'b':2, 'c':3, 'd':4}
{% endcodeblock %}
    
方法二
------

本方法较方法一速度更快

{% codeblock lang:python %}
>>> x = {'a': 1, 'b': 2}
>>> y = {'c': 3, 'd': 4}
>>> z = dict(x, **y)
>>> z
{'a':1, 'b':2, 'c':3, 'd':4}
{% endcodeblock %}

或者一种等价写法：

{% codeblock lang:python %}
>>> x = {'a': 1, 'b': 2}
>>> y = {'c': 3, 'd': 4}
>>> z = x.copy() # 或z = dict(x)
>>> z.update(y)
>>> z
{'a':1, 'b':2, 'c':3, 'd':4}
{% endcodeblock %}
