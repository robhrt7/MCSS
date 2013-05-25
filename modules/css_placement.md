---
layout: default
title: Расположение стилей
description: Модуль MCSS
project-name: MCSS
project-url: https://github.com/operatino/MCSS
pages-url: /MCSS
author: <a href="https://github.com/operatino">operatino</a>

res-watch-on-github: Посмотреть на Github
res-download-archive: Скачать в архиве
---

[На главную]({{ page.pages-url }})

# Расположение стилей
Стили каждого модуля должны храниться рядом друг с другом, можно их выделять как в закомментированные секции, так и в отдельные файлы:

{% highlight css %}
/* Module name
-------------------------------------------------- */
.module { }

.module_list { }
    .module_list__modificator { }
/* /Module name */
{% endhighlight %}

Селекторы, модифицируемые каскадом, должны так же храниться рядом с родительским классом:

{% highlight css %}
/* Module name
-------------------------------------------------- */
.module { }

.module_list { }
    .module_list .other-module { }
/* /Module name */
{% endhighlight %}

Исключением могут быть только классы из слоя контекста:

{% highlight css %}
/* Module name
-------------------------------------------------- */
.module { }

.module_list { }
    .touch .module_list { }
    .ie9 .module_list { }
/* /Module name */
{% endhighlight %}

Такая организация стилей упрощает дальнейший рефакторинг кода и позволяет непосвященному разработчику быстро разобраться во всех стилях модуля и быстро приступить к работе с ним.

При чистке кода просто избавляться от старых модулей и от всех его зависимостей.

Про расположение стилей внутри секций можно почитать в модуле про [модификаторы]({{ page.pages-url }}/modules/modifiers.html).
