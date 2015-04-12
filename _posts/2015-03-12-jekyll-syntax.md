---
published: ture
title: Jekyll 语法小节
layout: post
author: Yu 
category: 软件世界
tags:
- Jekyll
- 静态博客
- YAML
- Liquid 
---

* Table of contents
{:toc}

最近尝试用Jekyll写个小展示网站，发现Jekyll的功能还是很强大的。之前很多不熟悉的语法，现在也都能摸索着用在模版里。本篇总结记录一下我常用的Jekyll基本语法。

### YAML Front Matter

每写一篇markdown格式的文章，需要在文章的最开始写入一些常规信息变量的取值，具体有:指定模板(layout)， 标题(title)， 描述(description)， 分类(category/categories)， tags， 是否发布(published)， 以及自定义变量(超级好用)。


~~~
---
layout: post
title: title
category: blog
published: true # default true (可以不写这一行)
---
~~~

例如，我想在文章里加入天气情况:

~~~
---
layout: post
title: title
category: blog
published: true # default true (可以不写这一行)
weather: sunny # 天气
---
~~~

然后调用时用`{ {post.weather} }`即可。



### site全局根结点

在全局根结点site中有 site.tags.TAG 和 site.categories.category.CATEGORY 变量，可以列出所有拥有TAG标签或者CATEGORY的文章的列表(这里的变量只能写英文)。
另外<q>site.[CONFIGURATION_DATA]</q>**使得所有在_config.yml中的数据都能够通过site变量调用。**



### Data Files


Jekyll 支持 从 _data 目录中加载 YAML， JSON， 和 CSV 格式的文件数据。

例如创建 _data/user.yml 文件。


~~~
- name: Yu Lijia  
  github: yulijia
  nick: Yu
~~~

在html里这样写：

{% raw %} 
    <ul>
    {% for member in site.data.members %}
      <li>
        <a href="https://github.com/{ { member.github } }">  <!--https://github.com/yulijia-->
        {% assign nick = member.nick %}
        {% assign name = member.name %}
          { { nick} } ( { {name} } )         <!--Yu(Yu Lijia)-->
        </a>
      </li>
    {% endfor %}
    </ul>
{% endraw %}


### 常用语法

#### 字符转义

有时候想输出大括号了，使用 \ 转义即可。

`\{ => {`


#### 输出变量直接使用两个大括号括起来即可。

**注意，本文中所有双大括号之前都加上的了空格，这是为了避免在code中被识别为程序，在正确语法中<q>{ {</q>，<q>} }</q>，<q>{ ％</q> 以及 <q>％ }</q>之间没有空格。**

`{ { page.title } }`

#### 循环

和平常的解释性语言很像

~~~
{ % for post in site.posts % }
    <a href="{ { post.url } }">{ { post.title } }</a>
  { % endfor % }
~~~

#### if判断

注意逻辑“与或”分别是`and`,`or`

~~~
{ % if user % }
  Hello {{ user.name }}
{ % endif % }

# Same as above
{ % if user != null % }
  Hello {{ user.name }}
{ % endif % }

{ % if user.name == 'tobi' % }
  Hello tobi
{ % elsif user.name == 'bob' % }
  Hello bob
{ % endif % }

{ % if user.name == 'tobi' or user.name == 'bob' % }
  Hello tobi or bob
{ % endif % }

{ % if user.name == 'bob' and user.age > 45 % }
  Hello old bob
{ % endif % }

{ % if user.name != 'tobi' % }
  Hello non-tobi
{ % endif % }

# Same as above
{ % unless user.name == 'tobi' % }
  Hello non-tobi
{ % endunless % }
# Check for the size of an array
{ % if user.payments == empty % }
   you never paid !
{ % endif % }

{ % if user.payments.size > 0  % }
   you paid !
{ % endif % }

{ % if user.age > 18 % }
   Login here
{ % else % }
   Sorry, you are too young
{ % endif % }

# array = 1,2,3
{ % if array contains 2 % }
   array includes 2
{ % endif % }

# string = 'hello world'
{ % if string contains 'hello' % }
   string includes 'hello'
{ % endif % }
~~~

#### 自动生成摘要

~~~
  { % for post in site.posts % }
     { { post.url } } { { post.title } }
      { { post.excerpt | remove: 'test' } }
  { % endfor % }
~~~

#### 删除指定文本

remove 可以删除变量中的指定内容


`{ { post.url | remove: 'http' } }`

#### 删除 html 标签
 
`{ { post.excerpt | strip_html } }`


#### 代码高亮并且显示行数

~~~
{ % highlight ruby linenos % }
\# some ruby code
{ % endhighlight % }
~~~

#### 获得数组的大小

`{ { array | size } }`

#### 赋值

`{ % assign index = 1 % }`


#### 搜索指定key

~~~
# Select all the objects in an array where the key has the given value.
{ { site.members | where:"graduation_year"，"2014" } } 
~~~

#### 排序

`{ { site.pages | sort: 'title'， 'last' } }`

#### 转换成JSON

`{ { site.data.projects | jsonify } }`

#### 把一个对象变成一个字符串

`{ { page.tags | array_to_sentence_string } }`


#### 单词的个数

`{ { page.content | number_of_words } }`


#### 得到数组指定范围的结果集

`{ % for post in site.posts limit:20 % }`


-----------------

### 参考文章

- [Jekyll 语法简单笔记](http://github.tiankonguse.com/blog/2014/11/10/jekyll-study/)
- [Jekyll DOCUMENTATION](http://jekyllrb.com/docs/home/)
- [Liquid for Designers](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers)
