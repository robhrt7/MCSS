---
layout: default-en
title: MCSS
description: Multilayer CSS
---

## 简介

Multilayer CSS organization methodology is a guideline to structure your CSS.
多层 CSS 组织方法论是你构造 CSS 的指导手册.

Core methodology principles are based on [BEM]((http://bem.info/)) and [OOCSS](http://oocss.org/) ideas. MCSS was invented in [Odnoklassniki.ru](http://corp.mail.ru/en/communications/odnoklassniki) (Top 10 world social network) developers team and is recommended for other developers as core for own documentation and team based methodologies.
核心方法论的原则基于[BEM](http://bem.info/)和[OOCSS](http://oocss.org/)的想法.MCSS 是由[Odnoklassniki.ru](http://corp.mail.ru/en/communications/odnoklassniki)(全球十大顶级社交网络)的开发团队发明的,并且推荐其他开发者作为自己和团队的基本方法论.

Despite the fact that this methodology originated in a large project with more than 60 developers and many inner services it can easily be used for small and medium sized projects as well. Its scalability gives developers an opportunity to chose the level of strictness of selected rules.
无论是一个超过60个开发者参与的大型项目和很多内部服务,它也能被用于中小型项目.它的可扩展性给了开发者选择规则的严格程度.

Documentation is still being constantly improved, along with secondary tools, such as front-end documentation engine [Source](http://sourcejs.com). Originally documentation was written in russian and not all information is translated yet, but in upcoming updates all contents will be translated and main project language will be changed to english.
文档还在持续改进,和一些代理工具一起,比如前端文档引擎[Source](http://sourcejs.com). 原始的文档是用俄语写的,不是所有的内容都被翻译了,但是即将来临的更新会翻译所有的内容并且主要项目语言会变成英文.

*Please don't hesitate to leave your questions in [Issues section on Github](http://github.com/operatino/MCSS/issues) or leaving comments below.*
*有问题就在[Github 的 Issues](http://github.com/operatino/MCSS/issues) 或者 下面的评论框留言, 不要犹豫.*

### Fast navigation

* [Main principles](#main)
* [Style storing rules](#style-storing)
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

**MCSS** methodology is very scalable and does not force using specific code style, file system organization or specialized tools to work with it. The main thing is about separating rules for different blocks.
**MCSS** 的方法论是非常灵活的并且不需要强制使用特定的编码风格, 文件系统组织或者特定的工具才能工作.主要的事情就是分割规则到不同的块.

CSS modules (and blocks in them) are separated in to layers, where each layer has its own rules for exploitation and interaction with other layer modules.
CSS 模块(和里面的块) 被分割成层, 每个层都有自己的规则去利用和交互别的层.

![image]({{ site.baseurl }}/images/modules.jpg)

<a id="style-storing"></a>
### 样式存放规则
All styles of specific modules must be placed in separate section or CSS file:
所有的特定模块的样式必须被放在被分离的部分或者 css 文件:

{% highlight css %}
/* Module name
-------------------------------------------------- */
.module { }

.module_list { }
  .module_list.__modifier { }
/* /Module name */
{% endhighlight %}

Modified selector with cascade, also are stored near other parent selectors:
层叠的修饰选择器也要被放在靠近父级选择器的附近:

{% highlight css %}
/* Module name
-------------------------------------------------- */
.module { }

.module_list { }
    .module_list .other-module { }
/* /Module name */
{% endhighlight %}

The only exception is the **context layer:**
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

This part of documentation will be moved to separate document module and will be described more accurate (already available in [russian]({{ site.baseurl }}/modules/css_placement.html)).
这部分文档会被一到单独的文档模块并且被更精确的描述([俄文版]({{ site.baseurl }}/modules/css_placement.html)的已经有了)

## Zero layer or Foundation
## 第0层或者地基
Foundation includes resets and insignificantly changeable styles, which describe main layout base and apply on all pages.
地基包含了重置和无关紧要的可变的样式,描述了主要的基本布局并且应用与所有页面.

Foundation styles like all resets are connected from the very start, either in separate file or in the beginning of common CSS file:
基础样式就像所有的重置一样,都在开头的单独文件或者 common 的 CSS 文件头部:

<a id="interaction"></a>
## Module interaction scheme
## 模块交互方案

![image]({{ site.baseurl }}/images/layers.jpg)

### Style linking order
### 样式链接顺序

Every layer styles must be linked to the page in right order to maintain right relations between selectors of different modules/layers:
每一个层样式必须被页面以正确的顺序被连接来保持正确的关系在不同的模块/层的选择器中:

	0_layer_foundation
		reset.css

	1_layer_base
		base_modules.css

	2_layer_project
		project_modules.css

	cosmetic.css

<a id="1"></a>
## 1 layer — base
## 1 层 - 基础
First layer - is a website framework, the core part of interface. It is based on most reusable and abstract constructions:
第一层 - 是一个网站框架, 界面的核心部分.它是基础的在大多数可重用的和抽象的构造.

* forms 表单
* buttons 按钮
* navigation blocks 导航块
* and etc 其它

Base layer styles must be integrated with designers style guides as close as possible. As modules of first layer are meant to be reused across all website interfaces, they must look appropriate and fit to other interface parts without modification.

基础层样式必须尽量和设计师的样式指导相整合.因为第一层的模块意味着要贯穿整个网站的界面,它们必须在不修改的情况下和其他界面显得和谐.

**Starting to use MCSS in your project, the first thing you should do - is creating a set of reusable standards.**
**开始使用 MCSS 在你的项目中, 第一件事你应该做的 - 是创建一系列可服用的标准.**

You can easily reuse popular frameworks such as [Bootstrap](http://twitter.github.com/bootstrap/), [960gs](http://960.gs/), [inuit.css](https://github.com/csswizardry/inuit.css) and others as part of the first layer.
你可以很容易的使用流行的框架比如[Bootstrap](http://twitter.github.com/bootstrap/), [960gs](http://960.gs/), [inuit.css](https://github.com/csswizardry/inuit.css) 和其他来作为第一层的一部分.

### Rules
### 规则

First layer fundamental rule - all entities should be abstract, both with their names and mark-up.

第一层基础规则 - 所有的存在都应该是抽象的,包括它们的名字和mark-up

* Class names should not look "foreign" in any place on the interface.
* Module blocks should have default style, but also should be easy to modify according to various project modules and tasks.

* 类名不应该看上去"不协调"在界面的任何地方.
* 模块应该有默认的样式,但是也可以被容易的修改根据不通的项目模块和任务.

First layer styles could be cascade-modified from other modules of the same layer and 2nd layer. This is due to the Rule regarding location of related styles in one place.
第一层的样式可以被层叠修改从同一层的其他模块或者第二层.因为一个规则:regarding location of related styles in one place.

**Base styles should be separated from 2nd layer modules and stay independent from project layer styles.**
**基础样式应该从第二层模块中分割出来并且保持项目层样式的独立性**

Forms standard:

{% highlight css %}
.input-field { }
    .input-field_text { }
{% endhighlight %}

Form standard interaction with button standard - cascade modification from 1st layer:

{% highlight css %}
.input-field { }
    .input-field .button { }
{% endhighlight %}

Project module interaction with the standard in the 2nd layer:

{% highlight css %}
.project-module { }
    .project-module .input-field { }
{% endhighlight %}

**2 layer modification from the 1st one is forbidden!** In this case, layers are mixing up, causing chaos:

{% highlight css %}
    .input-field .project-module { }
{% endhighlight %}

Base styles are connected right after the foundation, prior to 2nd layer, to support low level priority in selector weight.

### Advantages
### 优势
Reusable and well thought-of first layer modules allow saving time on support of popular constructions, eliminating the need to maintain several similar modules.
重用和好的思考出的第一层模块允许节省时间在支持流行结构,减少维持多个相似的模块.

Re-usability also as well affects the final size of CSS-files and page rendering time.
重用性也会影响 css 文件的最终尺寸和页面加载时间.

Having well-developed base allows to create new interfaces easily, most of which consist of standard elements.
有了高大上的基础允许容易创建界面,大多数标准元素的组合.

The samples of standard designs can be reused from one project to another, allowing accelerating the development both of the layout and backend functionality connected with it.
标准的设计例子可以在项目之间重用,促进了布局和后端的连接.

<a id="2"></a>
## 2 layer — project
Second layer includes isolated, project modules, which further construct the page:
第二层包含单独的,项目模块,增进页面结构

* Registration form 注册表单
* Login block 登录块
* Shopping cart 购物车
* and etc 其它

### Rules
### 规则

It is recommended to use as many as possible unique CSS classes in second layer layout; even if current design does not need styling, better practice is to assign unique CSS class to it. Such approach provides better availability of each separate layout block, which allows easily correct styles, without affecting HTML structure.
建议使用尽可能多的唯一的 css 类在第二层;即使当前的设计不需要样式,更好的实践是飞陪唯一的 css 类.这样的方法使得每个分开的层块能被更好的访问到,允许更容易的纠正样式,而不影响 html 结构


Each module has to be as isolated as possible - independent interface block, which interacts with the base layer only.
每个模块应该尽量的独立 - 独立于界面块, 只和基础层交互.

To use the first layer construction in project module, we need to assign one more CSS class into HTML:
使用第一层的结构在项目模块里, 我们需要分配另一个 css 类在 html 里.

{% highlight html %}
<header class="toolbar">
    <a href="/" class="toolbar_logo"></a>
    <menu class="toolbar_dropdown_ul umenu">
        <li class="umenu_li"></li>
        <li class="umenu_li"></li>
    </menu>
</header>
{% endhighlight %}

Example displays second layer module **.toolbar**, which uses first layer standard **.umenu**. To modify standard for project needs, CSS cascade is used:

{% highlight css %}
/* Toolbar
-------------------------------------------------- */
.toolbar { }

.toolbar_dropdown_ul { }
    .toolbar_dropdown_ul .umenu_li { }
/* /Toolbar */
{% endhighlight %}

**Project layer styles may be cascade-modified only from other project layer modules!**

**This is right:**

{% highlight css %}
.project-module .other-project-module { }
{% endhighlight %}

This is wrong:

{% highlight css %}
.base-module .project-module { }
{% endhighlight %}

### Advantages
Module isolation provides easy access to their styles, without risk of affecting other interface parts. When working in team, each team member can develop single layer separately, not getting in to conflict with other developers.
模块分离提供了更容易去样式它们,不必冒着影响其他界面部分的风险.当团队合作时,每个小组成员可以开发单独的分隔的层, 不会和其他开发者冲突.

Styles of each module may be applied only to those pages, where they are needed.
每个模块的样式可以只被应用于他们需要的页面.

When functionality is disappearing from the website, it is easy to get rid of unnecessary styles - all that is required is to throw out one module with corresponding styles.
当网站的功能不需要时,很容易放弃不必要的样式 - 所需要做的就是扔掉一个模块和相应的样式.

<a id="3"></a>
## 3 layer — cosmetic

Third layer consists of simple, slightly affecting styles:

* links colors
* low-level OOCSS - two properties for CSS class (.font-size_XL, .margin-t_L)
* global modifiers

Layer can be nonexistent in some cases of methodology usage, but in big projects, this layer allows to solve the duplicate styling issue and to describe rare, non-project conditions, going 'DRY'.

### Rules
Third layer styles should be organized in a way to keep layout safe when styles are being discarded. Losses should be minor e.g. colors, paddings, etc.

It is allowed to use some of simple OOCSS classes, two classes for block maximum, for rare, non-project situations:

{% highlight html %}
<div class="font-size_XL margin-t_L color_red"></div>
{% endhighlight %}

**Cosmetic layer styles cannot be modified with cascade from other layers, except the context selectors.**

Cosmetic styles are applied at the end of CSS. It is not recommended to use **!important**.

### Advantages
Styles doesn't have major effect to website layout, however helps dealing with duplicate code issue and eliminating the need to produce small project and base modules.

Simple selectors allow to quickly deal with rare situations, when we need to apply a couple of properties for non-project module.

<a id="context"></a>
## Context
This layer includes styles of high context and @media-rules that can be used for changing standard styles for features of different context:

* .ie8, .ie9 - browsers
* .touch
* .logged-in
* media-queries

**Context layer is an exception in style location rules.** Styles of this layer are being distributed between all layers, which are being cascade-modified from context:

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

You can check MCSS in action in this [demo]({{ site.baseurl }}/examples/layers/). In the following example, all layers are stored in one [CSS file]({{ site.baseurl }}/examples/layers/css/style.css), but they could be also separated to individual files (blocks):

![image]({{ site.baseurl }}/images/file-system.png)

In second [demo]({{ site.baseurl }}/examples/mcss_with_bootstrap/), you can see how MCSS works with Bootstrap, as first (base) layer.

Site of the project is also designed by MCSS methodology; do not hesitate to look at the [source]({{ site.baseurl }}/theme/stylesheets/stylesheet.css).

<a id="dictionary"></a>
### Abbreviation dictionary
To escape large CSS selector names, we suggest using abbreviation dictionary:

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

<a id="recommendations"></a>
## Recommendations

### Code style
Along with methodology, we advise to use following useful practices to improve quality of your code:

* [Principles of writing consistent, idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [Google HTML/CSS style guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml) - style guide for HTML and CSS code configuration
* [CSScomb](http://csscomb.ru/) - tool for CSS-property sorting

### Best practices
* Do comment CSS as much as you can, all non-standard constructions, magical numbers — this will be useful not only to the members of your team, but for you as we'll, when you will be back to reviewing the code after couple of months.
