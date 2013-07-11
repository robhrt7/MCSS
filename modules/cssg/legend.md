---
layout: default
title: CSS-o-Gram
description: Справка по синтаксису

context: cssg
styles: |
    .content code {line-height: 1.8;}
---

    element 											класс элемента
    ... 												ключевой контент
    #name 												ссылка на часть структуры
    span.element 										конкретизация тэга
    element . __fixed 									без данного класса не используется
    element 				__modificator 				перечисление возможных модификаторов
    element 				( __yes | __no ) __maybe 	комплексная логика модификаторов
    element 				$__dynamic 					динамический модификатор
    [element] 											опциональный элемент
    $[dynamic] 											динамически опциональный элемент
    list-item + 										появление 1 и более раз
    common-item * 										появление 0 и более раз
    /// 												разрыв кода
    [1] 												маркер вариантного блока
    descendant @ ancestor 								наследование
    % template % 										шаблонизация
    (1) 												ссылка на комментарий
    ------------------- 								отбивка комментариев
    (1) comment on code 								комментарий