---
layout: default-cn
title: MCSS
description: Multilayer CSS
---

## 简介

多层 CSS 组织方法是你构造 CSS 的指导手册.

核心方法的原则基于[BEM](http://bem.info/)和[OOCSS](http://oocss.org/)的想法.MCSS 是由[Odnoklassniki.ru](http://corp.mail.ru/en/communications/odnoklassniki)(全球十大顶级社交网络)的开发团队发明的,并且推荐其他开发者作为自己和团队的基本方法.

无论是一个超过60个开发者参与的有很多内部服务的大型项目,还是中小型的项目.它都能胜任,它的可扩展性给了开发者选择规则的严格程度.

文档还在持续改进,和一些从属工具一起,比如前端文档引擎[Source](http://sourcejs.com). 原始的文档是用俄语写的,不是所有的内容都被翻译了,但是即将来临的更新会翻译所有的内容并且主要项目语言会变成英文.

*有问题就在[Github 的 Issues](http://github.com/operatino/MCSS/issues) 或者 下面的评论框留言, 不要犹豫.*

### 快速导航

* [主要原则](#main)
* [样式存放规则](#style-storing)
* [Module interaction scheme](#interaction)
* [1 layer — base](#1)
* [2 layer — project](#2)
* [3 layer — cosmetic](#3)
* [Context](#context)
* [Real life examples](#examples)
* [Abbreviation dictionary](#dictionary)
* [Recommendations](#recommendations)

<a id="main"></a>
### 主要原则

**MCSS** 的理论是非常灵活的并且不需要强制使用特定的编码风格, 文件系统组织或者特定的工具才能工作.最主要的就是分割规则到不同的块.
CSS 模块(和其中的组建) 被分割成不同的层, 每个层都有自己的规则去利用和交互别的层.

![image]({{ site.baseurl }}/images/modules.jpg)

<a id="style-storing"></a>
### 样式存放规则
所有的特定模块的样式必须被放在独立的部分或者不同的 css 文件中:

{% highlight css %}
/* Module name
-------------------------------------------------- */
.module { }

.module_list { }
  .module_list.__modifier { }
/* /Module name */
{% endhighlight %}

层叠的修饰选择器也要被放在靠近父级选择器的地方:

{% highlight css %}
/* Module name
-------------------------------------------------- */
.module { }

.module_list { }
    .module_list .other-module { }
/* /Module name */
{% endhighlight %}
    
唯一的例外是 **上下文层**

{% highlight css %}
/* Module name
-------------------------------------------------- */
.module { }

.module_list { }
    .touch .module_list { }
    .ie9 .module_list { }
/* /Module name */
{% endhighlight %}

这部分文档会被一到单独的文档模块并且被更精确的描述([俄文版]({{ site.baseurl }}/modules/css_placement.html)的已经有了)

## 第0层或地基
地基包含了重置和无关紧要的可变的样式,描述了主要的基本布局并且应用与所有页面.

基础样式就像所有的重置一样,都在最顶端的单独文件或者 common CSS 文件头部:

<a id="interaction"></a>
## 模块交互结构

![image]({{ site.baseurl }}/images/layers.jpg)

### 样式链接顺序

每一个层的样式必须被页面以正确的顺序被链接来保持在不同的模块/层的选择器中的正确的关系:

	0_layer_foundation
		reset.css

	1_layer_base
		base_modules.css

	2_layer_project
		project_modules.css

	cosmetic.css

<a id="1"></a>
## 第1层 - 基础
第一层 - 是一个网站框架, 界面的核心部分.它是基于可重用的和抽象的构造之上的.

* 表单
* 按钮
* 导航块
* 其它

基础层样式必须尽量和设计师的样式指导相整合.因为第一层的模块意味着要贯穿整个网站的界面,它们必须在不修改的情况下和其他界面显得和谐.

**开始在你的项目中使用 MCSS, 第一件事你应该做的 - 是创建一系列可复用的标准.**

你可以很容易的使用流行的框架比如[Bootstrap](http://twitter.github.com/bootstrap/), [960gs](http://960.gs/), [inuit.css](https://github.com/csswizardry/inuit.css) 或其它框架来作为第一层的一部分.

### 规则

第一层基础规则 - 所有的存在都应该是抽象的,包括它们的名字和标记容器.

* 类名不应该在界面的任何地方看上去"不协调".
* 模块应该有默认的样式,但是也可以根据不同的项目模块和任务被容易的修改.

第一层的样式可以被同一层的其他模块或者第二层层叠修改.因为一个规则:相关的样式只出现在一个地方.

**基础样式应该从第二层模块中分割出来并且保持项目层样式的独立性**

标准表单:

{% highlight css %}
.input-field { }
    .input-field_text { }
{% endhighlight %}

标准表单和标准按钮交互 - 从第一层层叠样式:

{% highlight css %}
.input-field { }
    .input-field .button { }
{% endhighlight %}

项目模块和和标准交互在第二层:

{% highlight css %}
.project-module { }
    .project-module .input-field { }
{% endhighlight %}

**第二层从第一层修改是被禁止的!** 在这个例子中, 不同的层混合了, 造成了混乱: 

{% highlight css %}
    .input-field .project-module { }
{% endhighlight %}

基础样式是正确的被链接的在地址之后,优先于第二层,来支持底层的选择器权重优先.

### Advantages
### 优势

重用性和受到好评的第一层模块允许节省时间在支持流行结构,减少维护多个相似的模块.

重用性也会影响 css 文件的最终尺寸和页面加载时间.

有了完善的基础允许容易创建界面,大多数标准元素的组合.

标准的设计例子可以在项目之间重用,促进了布局和后端的开发者的沟通.

<a id="2"></a>
## 第2层 - 项目
第二层包含单独的,项目模块,增进页面结构:

* 注册表单
* 登录块
* 购物车
* 其它

### 规则

建议使用尽可能多的唯一的 css 类在第二层;即使当前的设计不需要样式,更好的实践是分配唯一的 css 类.这样的方法使得每个分开的层块能被更好的访问到,允许更容易的纠正样式,而不影响 html 结构

每个模块应该尽量的独立 - 独立于界面组建, 组建只和基础层交互.

使用第一层的结构在项目模块里, 我们需要分配另一个 css 类在 html 里:

{% highlight html %}
<header class="toolbar">
    <a href="/" class="toolbar_logo"></a>
    <menu class="toolbar_dropdown_ul umenu">
        <li class="umenu_li"></li>
        <li class="umenu_li"></li>
    </menu>
</header>
{% endhighlight %}

下面的例子是第二层的模块**.toolbar**,它使用第一层的标准**.umenu**.来修改项目需要的标准, CSS 层叠样式被使用:

{% highlight css %}
/* Toolbar
-------------------------------------------------- */
.toolbar { }

.toolbar_dropdown_ul { }
    .toolbar_dropdown_ul .umenu_li { }
/* /Toolbar */
{% endhighlight %}

**项目层样式只能被其他项目层的模块层叠修改**

**这是对的:**

{% highlight css %}
.project-module .other-project-module { }
{% endhighlight %}

这是错的:

{% highlight css %}
.base-module .project-module { }
{% endhighlight %}

###优势
模块的分离使得修改它们的样式更容易,不必冒着影响其他界面部分的风险.当团队合作时,每个小组成员可以开发单独的分隔的层, 不会和其他开发者冲突.

每个模块的样式可以只被应用于他们需要的页面.

当网站的功能不需要时,很容易放弃不必要的样式 - 所需要做的就是扔掉一个模块和相应的样式.

<a id="3"></a>
## 3 layer — cosmetic

Third layer consists of simple, slightly affecting styles:
第三层由简单的轻微的影响样式组成:

* links colors 超链接颜色
* low-level OOCSS - two properties for CSS class (.font-size_XL, .margin-t_L)
* 低层次的 OOCSS - 二属性
* global modifiers 全局修饰

Layer can be nonexistent in some cases of methodology usage, but in big projects, this layer allows to solve the duplicate styling issue and to describe rare, non-project conditions, going 'DRY'.
这一层可以不存在在一些方法论用例中, 但是在大型项目中, 这一层允许解决重复的样式问题并且描述罕见的没有项目的情况,更加'DRY'

### Rules
Third layer styles should be organized in a way to keep layout safe when styles are being discarded. Losses should be minor e.g. colors, paddings, etc.
第三层样式应该被组织成保持层安全,当被丢弃时.损失应该是最小的,比如 颜色 内边距等等.

It is allowed to use some of simple OOCSS classes, two classes for block maximum, for rare, non-project situations:
允许使用一些简单的OOCSS 类,

{% highlight html %}
<div class="font-size_XL margin-t_L color_red"></div>
{% endhighlight %}

**Cosmetic layer styles cannot be modified with cascade from other layers, except the context selectors.**
**装饰层样式不能被其他层的层叠样式修改,除了上下文选择器**

Cosmetic styles are applied at the end of CSS. It is not recommended to use **!important**.
装饰层样式被放在 CSS 的尾部.不推荐使用 **!important**

### Advantages
Styles doesn't have major effect to website layout, however helps dealing with duplicate code issue and eliminating the need to produce small project and base modules.
样式对网站布局没有大的影响,帮助处理重复代码的问题并且减少生产小项目和基础模块的生产.

Simple selectors allow to quickly deal with rare situations, when we need to apply a couple of properties for non-project module.
简单选择器允许快速处理少数情境, 当我们需要应用一些属性到没有项目模块的情境时.

<a id="context"></a>
## Context
This layer includes styles of high context and @media-rules that can be used for changing standard styles for features of different context:
这层包含了高层的上下文和媒体规则可以改变标准的样式为了未来的不同上下文:

* .ie8, .ie9 - browsers 浏览器
* .touch 触摸
* .logged-in 登录 
* media-queries 媒体查询

**Context layer is an exception in style location rules.** Styles of this layer are being distributed between all layers, which are being cascade-modified from context:
**上下文层在样式位置上是个例外** 这一层的样式分布在所有的层忠,可以根据上下文层叠修饰:

{% highlight css %}
/* Module name
-------------------------------------------------- */
.module { }

.module_list { }
    .touch .module_list { }
    .ie9 .module_list { }

@media screen and (max-width: 1000px) {
    .module { }
    }
/* /Module name */
{% endhighlight %}

<a id="examples"></a>
## Real life examples
## 现实生活中的例子

You can check MCSS in action in this [demo]({{ site.baseurl }}/examples/layers/). In the following example, all layers are stored in one [CSS file]({{ site.baseurl }}/examples/layers/css/style.css), but they could be also separated to individual files (blocks):
你可以检出 MCSS 实战在这里[demo]({{ site.baseurl }}/examples/layers/).在下面的例子中,所有的层都被储存在一个[CSS 文件]({{ site.baseurl }}/examples/layers/css/style.css), 但是它们可以被分割在单独的文件(块)中:

![image]({{ site.baseurl }}/images/file-system.png)

In second [demo]({{ site.baseurl }}/examples/mcss_with_bootstrap/), you can see how MCSS works with Bootstrap, as first (base) layer.
在第二个[demo]({{ site.baseurl }}/examples/mcss_with_bootstrap/), 你会看到 MCSS 如何和 Bootstrap 一起工作, 作为第一层(基础)层.

Site of the project is also designed by MCSS methodology; do not hesitate to look at the [source]({{ site.baseurl }}/theme/stylesheets/stylesheet.css).
本站也是基于 MCSS 理论来设计的, 快看看 [源码]({{ site.baseurl }}/theme/stylesheets/stylesheet.css).

<a id="dictionary"></a>
### Abbreviation dictionary
### 缩写字典
To escape large CSS selector names, we suggest using abbreviation dictionary:
避免大型的 CSS 选择器名字, 我们建议使用缩写字典:

    a - link (<a> tag)
    ac - action
    add - additional
    aft - after
    aux - auxillary

    b - body | bottom
    bg - background
    brd - border
    btn - button

    cat - catalog | category
    cl - clear
    cnt - content | container
    cnts - contents
    col - column

    dec - decorate
    def - default
    del - delete
    descr - description
    dm - delim
    dyn - dynamic

    e - error
    el - element
    ext - external

    f - footer
    fr - friend
    ft - font

    gen - general

    h - header
    hl - highlight
    hv - hover
    hld - holder

    i - item
    ic - icon
    img - image
    ir - input radio
    is - input submit
    it - input text
    itx - textarea


    l - left | label
    lbl - label
    lk - link
    lr - layer
    lst - list

    mod - module | modifier

    n - name
    ntf - notification
    num - number

    opt - options
    ovr - overlay

    ph - placeholder
    pht - photo
    priv - privacy

    r - right
    rfr - refresh

    scr - screen | scroll
    sel - select
    sett - settings
    sm - small
    spr - sprite

    t - title | t
    tx - text

    w - wrapper

In future, dictionary will mo moved to separate documentation module.
在未来, 字典会被移到单独的模块.

<a id="recommendations"></a>
## Recommendations
## 推荐规范

### Code style
### 代码风格
Along with methodology, we advise to use following useful practices to improve quality of your code:
除了方法论, 我们建议使用下面的有用的实践来提升你代码的质量.

* [Principles of writing consistent, idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [Google HTML/CSS style guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml) - style guide for HTML and CSS code configuration
* [CSScomb](http://csscomb.ru/) - tool for CSS-property sorting

### Best practices
### 最佳实践
* Do comment CSS as much as you can, all non-standard constructions, magical numbers — this will be useful not only to the members of your team, but for you as we'll, when you will be back to reviewing the code after couple of months.
* 尽可能多的注解CSS,所有不标准的结构,神奇数字 - 将会很有用不仅对于你团队的成员, 也对你自己, 当你几个月后复查代码时.
