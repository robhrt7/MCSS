---
layout: default
title: Словарь сокращений

context: inner-page
---

Чтобы не раздувать названия классов, рекомендуется использовать сокращения для самых популярных слов. Если вся команда придерживается одного словаря сокращений, название классов и других элементов остаются читабельными и легко воспринимаемыми.

## Сокращения

    a - link (<a> tag)
    ac - action
    add - additional
    aft - after
    aux - auxiliary

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

## Модификаторы

Помимо классов, большое значение имеет использование общей конвенции нейминга модификаторов. Речь идет о наиболее часто встречающихся, которые можно отнести к стандартным.
*Примечание: в скобках указан сокращенный вариант модификатора - может использоваться в проектах, где важен каждый символ, например, верстка для мобильных устройств.*

    __active (__ac) - активность в любом качестве
    __disabled (__na) - выключенный элемент

    __visible (__vis) - видимый элемент
    __hidden (__hid) - скрытый элемент

    __anim - анимируемый элемент

    __loading - загрузка
    __process - любой процесс

    __glow - подсветка элемента
    __mod - модификация элемента

    __big, __small (__sm) - большой, малый - простые модификации размеров
    __xs, __s, __m, ... - вариации размеров

    __i-N - порядковый номер элемента
    __q-N - количество элементов в контейнере

    __redesign - редизайн элемента (чаще присваивается врапперу)
    __ver-1, __ver-2 (__v-1, __v-2) - версионность элемента
