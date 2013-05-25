---
layout: default
title: Словарь сокращений - MCSS
description: Словарь сокращений. Многослойная система организации CSS
project-name: MCSS
project-url: https://github.com/operatino/MCSS
pages-url: /MCSS
author: <a href="https://github.com/operatino">operatino</a>

res-watch-on-github: Посмотреть на Github
res-download-archive: Скачать в архиве
---

# Словарь сокращений

Что бы не раздувать названия классов, советуется использовать сокращения для самых популярных слов. Если вся команда придерживается одного словаря сокращений, название классов и других элементов остаются читабельными и легко воспринимаемыми.

## Сокращения

    a - link (<a> tag)
    ac - action
    add - additional
    aft - after
    aux - auxillary

    b - body | bottom

    cat - catalog | category
    cl - clear
    cnt - content | counter
    cnts - contents
    col - column

    dec - decorate
    def - default
    del - delete
    descr - description
    dm - delim
    dyn - dynamic

    e - error

    f - footer
    fr- friend
    ft- font

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

    n - name
    ntf - notification
    num - number

    opt - options
    ovr - overlay

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

*Словарь открыт для [обсуждения](http://github.com/operatino/MCSS/issues) и пулл-реквестов.*

Имея предопределенный словарь сокращений можно свободно автоматизировать как зашифровку, так и расшифровку с помощью препроцессоров, или реализовать функционал подсказок.

## Применение сокращений

Сокращения можно применять везде, до тех пор, пока название остается понятным для стороннего человека.

### Аббревиатуры

Не рекомендуется использовать аббревиатуры для специфичных названий и сокращения сложных слов. Если нужно сократить длинное название, лучше упростить само название до одного слова, нежели использовать аббревиатуру, например:

	Left Column User Avatar -> user-avatar -> u-avatar -> uavatar

Приведенная запись будет намного понятней чем:

	Left Column User Avatar -> lcua

### Расшифровка

Каким бы простым сокращение не было, очень хорошей практикой считается оставлять рядом расшифровывающий комментарий, как минимум в первых вхождениях:

{% highlight css %}
.uavatar_ic { } /* User avatar icons */
{% endhighlight %}

### В MCSS

В MCSS, основное правило именования классов заключаются только в необходимости использовать название модуля в начале каждого класса этого модуля. Сокращения по словарю тоже можно использовать в названии модуля, если оно состоит не из одного слова.

{% highlight css %}
.user-avatar -> .u-avatar /* User avatar */

.u-avatar_header -> .u-avatar_h /* User avatar header */
{% endhighlight %}

Ради экономии символов, можно опускать разделитель слов в названии модуля, и добавлять специфические сокращения не по словарю, до тех пор, пока названия остается легко воспринимаемым.

{% highlight css %}
.user-avatar -> .u-avatar -> .uavatar -> .u-ava /* User avatar */
{% endhighlight %}
