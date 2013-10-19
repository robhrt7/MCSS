---
layout: default-en
title: CSS-o-Gram
description: neat, intuitive, fast - like [SSG](http://en.wikipedia.org/wiki/Steyr_SSG_69), but peaceful

context: inner-page cssg
---

## First things first

Any questions - feel free to ask project author via [email](mailto:wdybih@gmail.com).  
All content is available for free distribution.  
[Link to source](https://github.com/XOP/css-o-gram) is mandatory when copying materials. 

**CSSG Generator tool** is on the way. Stay tuned!

### Quick nav

* [Overview](#intro)
* [Let's begin](#basics)
* [Let's dig in](#advanced)
* [Syntax reference](#legend)

<a id="intro"></a>
## Overview

CSSG stands for "CSS Diagram", in fact - a comment block in CSS file, which describes substance structure with CSS classes. Substance can be element, block or project.

This is your trusted companion in large project and assistant for your colleages, if you work in team. Low entry barriers - regular syntax and some logical rules are used.  

### For whom and for what

* Better code structure and getting into new code
* Conversation tool for colleages and developers, distant from front-end
* Detecting potential "bottlenecks" in layout (excessive DOM nesting, classes amount etc.)
* Easier debugging and refactoring
* It's just pretty!

-----
<a id="basics"></a>
## Let's begin

CSSG describes substance structure with familiar cascade of CSS classes.  
Classes naming happens according to accepted rules that you or your company follow.  
Classes standing apart of substance classes are added near main class.  
As a rule, auxillary (cosmetic) classes are not added, except for special cases (described in [Advanced section](#advanced)) 

Along this documentation fictional substance "post" is used as an example.  
Let's assume it's the post in blog or any other block that has head, body, footer and secondary elements.

### Your first CSSG

Let's say your HTML looks something like this:

        <div class="post">
            <div class="post_h">
                <div class="post_h_name">Header</div>
            </div>
            <div class="post_b">
                Content
            </div>
            <div class="post_f">
                Additional information
            </div>
        </div>

CSS looks like that:

    .post {
        font-size: 14px;
    }
    
    .post_h {
        font-weight: bold;
    }
    
    etc.

CSSG illustrates HTML structure with CSS terminology and is placed in document _before_ all other rules:

    /*
        
        post
            post_h
                post_h_name
                post_h_date
        
            post_b
                ...
    
            post_f
        
    */
    
    .post {
        font-size: 14px;
    }

If you've worked with HAML or have idea about it's syntax, this structure will be familiar to you.  
By default all structure elements don't have specific DOM-presentantion, so _class_ is prior to _tag_.  
If it's necessary to exaggerate tag-class connection, habitual zen-coding notation is used:

    /*
        
        post
            post_h
                post_h_name
                i.post_h_date
        
    */

Few notes on syntax:

> descendants illustrated by tab  
> siblings separated by extra line in case of having child elements  
> CSSG structure should fit screen height due to viewing comfort

### Key content

Key content is denoted with ellipsis (...), other content is ignored.  
Ellipsis means that there is no nesting or it is not related to described structure.  
Example of incorrect CSSG:

    /*
        
        post
            post_h
                post_h_name
                    ...
                post_h_date
                    ...
        
            post_b
                ...
    
            post_f
                ...
        
    */

Key content can be located near other important substance part:

    /*
        
        post
            post_h
                post_h_name
                post_h_date
        
            post_b
                ...
                post_b_author
    
            post_f
        
    */

Apart substance, but still related to project, is denoted with figure brackets.  
Key content, complemented with apart substance, is denoted with ellipsis placed nearby.

    /*
    
        post
            post_h
                {date}
            post_b
                post_cnt
                    {... article}
    
    */

### Links

In case of complicated structure, it is more convenient to describe structure skeleton with links to compound sections in the beginning of CSS document.

    >> CSS start
    
    /*
    
        post
            #header
            #body
            #aux
    
    */
    
    >> CSS continues
    
    /* #header
    
        post_h
            post_h_name
        
    */

> link to compound section is denoted by native symbol - #

### Modificators and project classes (mix-ins)

HTML layout changes - due to context or by itself. CSS modificators allow to change substance presentation.  
Modificator in fact is CSS class like **.post\_\_new** or **.\_\_compact**, which is placed near main class.  
Project class (mix-in) allows to re-use substance and is placed separately from main class, e.g. **.post-featured**.

In CSSG all possible modificators placed on the right (aligned independently from nesting level) of target class.  
You choose distance manually, regarding diagram size and reading comfort.  
If project (mix-in) is implied, it is placed _before_ modificators list.

    /*
    
        post                        -project __new __featured
            post_h
            post_b
                post_b              __compact
    
    */

> modificators list in such way points to _availability_ of their simultaneous presence, without extra logic  
> more detailed information about modificators in [Advanced section](#advanced)

### Optional parts

Parts of substance, that may absent (or not compulsory for current substance) are enclosed in square brackets.  
If it's single class, brackets placed on the same line, on the contrary they are placed on separate lines for more convenient reading.

    /*
    
        post
            [post_teaser]
            post_h
            post_b
                [
                post_b_top
                    post_b_top_tx
                ]
    
    */

If optional part is a wrapper, following syntax is used:

    /*
    
        [post_w]
            post
                post_h
                post_b
                    [post_b_cnt]
                        [post_b_tx]
                            ...
                        [/post_b_tx]
                    [/post_b_cnt]
        [/post_w]
    
    */

> hyphens and spaces are not dogmatic in this case. Mind code purity and reading comfort in the first place.  
> furthermore, team might want to choose single syntax, equal for every member.

### Persistent blocks

Practically, large project or framework implies structures, that remain contant in spite of context. 
Examples of such structures - button, form element, social widget etc.

When they can't be ignored or on the contrary - it's _necessary_ to illustrate their presence - following syntax is used:

    /*
    
        post
            post_h
            post_b
            post_f
                post_f_ac
                    <social>
    
    */

> it is important to make up list of persistent, re-usable blocks  
> developers team should obtain single list of blocks

-----
<a id="advanced"></a>
## Let's dig in

### Multiplicity

Multiplicity happens to be typical for some substances, e.g. list elements or some blocks sequence.

In CSSG it will look like this:

    /*
    
        post_cnt
            post_cnt_ul
                post_cnt_li +
    
    */

or like that:

    /*
    
        post_cnt
            post_cnt_i *
    
    */

The main difference between '+' and '\*' is in multiplicity specifics.  
'+' says that element will appear at least 1 time (which is typical for list items - \<li\>)  
'\*' however says that element may appear more than 0 times (any other elements - you name it)

> it's important to feel the distinction between optional elements ([element]) and appearing 0 and more times (element *)  
> insignificant on the first sight, it appears to have contextual meaning

### Modificators - more and meaningful

As it was mentioned in [Basics](#basics), modificators complement substance and theoretically their simultaneous presence is possible.  
Crucial logic described with the help of special syntax.

For example, alternative is illustrated this way:

    /*
        
        post                            ( __current | __regular ) __deleted
    
    */

and even like this:

    /*
    
        post                            ( ( __current | __regular ) | __compact ) __deleted
    
    */

Dot (.) illustrates robust connection between class and another class or modificator

    /*
    
        post                            __compact __featured
            post_h
                post_h_tx . __bold
            post_b
                post_b_cnt
                    ...
    
    */

> alignment on the right for connected class is not necessary

### Inheritance

Substance can be direct descendant of other substance.  
To point this out, define ancestor via "@" symbol.

    /*
    
        post-advanced @ post
            post-advanced_h
            post-advanced_b
    
    */

> it's not necessary to list all modificators, because they inherited by default  
> however, if there is any difference, we must list all possible classes  
> it's accepted that these defined modificators will only be possible

For instance, it is illustrated in the following code, that **post-advanced** will have one possible modificator **__new**, regardless the fact, that **post** has some modificators as well

    /*
    
        post-advanced @ post                __new
            post-advanced_h
            post-advanced_b
    
    */

### Nominal templates

Inheritance is directly connected with nominal templates.  
We simplify illustration of descendant substance and avoid code duplication by setting changeable parts in ancestor substance.  
This is not mandatory, but turns out to be helpful if you have at least two such substances.

As an example, let's say ancestor substance looks like this:

    /*
    
        post
            post_cnt
                % content %
    
    */

or like this, if there is any default content 

    /*
    
        post
            post_cnt
                % content %
                    post_cnt_i
    
    */
 
descendant substance

    /*
    
        post-advanced @ post
    
        % content
            post-advanced_cnt
                post-advanced_cnt_i
    
    */

> when "filling" the template second % symbol is unnecessary

In this case **post-advanced\_cnt** will be inside **post\_cnt** and will override default content from second code piece.  
Without nominal templates, CSSG may look like this:

    /*
    
        post-advanced @ post
    
            post_cnt
                post-advanced_cnt
                    post-advanced_cnt_i
    
    */

There's almost no difference in this case.  
However all notation potential can be seen in context of describing more complex structure

> the **% content %** element has no DOM implementation, it is just a template name

### Dynamics

By dynamics it's meant that some class or element may appear in layout due to scripts and user activity.

    /*
     
        post                    $__disabled | $__active
            post_h
            post_b
                post_cnt
    
    */  

To define dynamic blocks complemented syntax for optional parts is used:

    /*
     
        post
            $[post_msg]                     
            post_h
            post_b
                post_cnt
                    $[post_cnt_msg]
                        post_cnt_tx
                    $[/post_cnt_msg]
    
    */  

### It's <<omplicated

Complex CSS approach can be described with CSSG.

Alternative (mutual exclusive) blocks example:

    /*
    
        post
            post_b
                
                [1]
                post_cnt
                    post_cnt_lst
                
                [2]
                post_cnt2
                    ...
     
    */

When it's necessary to illustrate some valueable class somewhere high in DOM tree:

    /*
        
        blog . __complex    
        
        ///
        
        post
            post_b
                post_cnt
     
    */

CSSG is self-explanatory _as a rule_, but some tough situations may require comments:

    /*
    
        post
            post_h (1)
            post_b
                post_cnt (2)
        _______________________________________________
     
        (1) comment on post_h
        (2) another comment
    
    */


-----
<a id="legend"></a>
## Syntax reference

    element                                             element classname
    ...                                                 key content
    #name                                               link to compound section
    span.element                                        tag detalization
    element . __fixed                                   not applicable without this class
    element                 __modificator               modificators list
    element                 ( __yes | __no ) __maybe    modificators logic
    element                 $__dynamic                  dynamic modificator
    [element]                                           optional element
    $[dynamic]                                          dynamically optional element
    list-item +                                         appears at least 1 time
    common-item *                                       appears at least 0 times
    ///                                                 code break
    [1]                                                 variative block marker                          
    descendant @ ancestor                               inheritance
    % template %                                        template
    (1)                                                 comment link
    -------------------                                 comments break line 
    (1) comment on code                                 comment
