---
layout: default-ja
title: MCSS
description: Multilayer CSS
---

## はじめに

Multilayer CSS構成システムは[BEM](http://bem.info/)と[OOCSS](http://oocss.org/)の原理を基にしています。この方法は[Odnoklassniki.ru](http://corp.mail.ru/en/communications/odnoklassniki)（世界のソーシャルネットワークのTOP10）開発チームによって作り出され、ドキュメントとチームベースのシステムの中核として開発者にお勧めです。

この方法は60人以上の開発者と多くの内部サービスという巨大なプロジェクトから生まれましたが、中小規模のプロジェクトにも簡単に導入できます。その拡張性により、開発者はルールの厳格さのレベルを選択できます。

このドキュメントはドキュメント作成エンジン[Source](http://sourcejs.com)などの補助ツールを使い、常に改善されています。オリジナルのドキュメントはロシア語で記述されており、全ての情報はまだ翻訳されていませんが、翻訳のプルリクエストはお気軽にどうぞ。

*何か質問があれば[Issues section on Github]({{ site.project-url }}/issues)またはメールアドレス<r@rhr.me>まで。*

### ナビゲーション

* [基本原則](#main)
* [スタイルの格納ルール](#style-storing)
* [モジュールの対応図](#interaction)
* [レイヤー 1 — ベース（ファーストレイヤー）](#1)
* [レイヤー 2 — プロジェクト (セカンドレイヤー)](#2)
* [レイヤー 3 — コスメティック (サードレイヤー)](#3)
* [コンテキスト](#context)
* [実際の例](#examples)
* [略語辞典](#dictionary)
* [推奨事](#recommendations)

<a id="main"></a>
### 基本原則

**MCSS**は非常に拡張性が高く、特定のコードスタイルやファイルシステム構成、または特定のツールなどを強制しません。重要なのはそれぞれのブロックごとにルールを分けるということです。

CSSモジュール（及び、その内部ブロック）はレイヤーごとに分離され、そのそれぞれのレイヤーは他のレイヤーモジュールと連携したり、一方的に利用するような独自のルールを持つことになります。

![image]({{ site.baseurl }}/images/modules.jpg)

<a id="style-storing"></a>
### スタイルの格納ルール

モジュールの全てのスタイルは、分割されたセクションまたはCSSファイルに配置されなければなりません：

{% highlight css %}
/* モジュール名
-------------------------------------------------- */
.module { }

.module_list { }
  .module_list.__modifier { }
/* /モジュール名 */
{% endhighlight %}

同様に、カスケードにより変更されたセレクターも他の親セレクターの近くに格納されます：

{% highlight css %}
/* モジュール名
-------------------------------------------------- */
.module { }

.module_list { }
    .module_list .other-module { }
/* /モジュール名 */
{% endhighlight %}

唯一の例外は**コンテキストレイヤー**です：

{% highlight css %}
/* モジュール名
-------------------------------------------------- */
.module { }

.module_list { }
    .touch .module_list { }
    .ie9 .module_list { }
/* /モジュール名 */
{% endhighlight %}

この章は個別のドキュメントとして、より正確に説明する予定です（[ロシア語版]({{ site.baseurl }}/modules/css_placement.html)では既にそうなっています）。

## ゼロレイヤーすなわちファンデーション（下地）

ファンデーションには、リセットとちょっとした変更を加えるだけのメインレイアウトのベースを記述した、全ページに適用されるスタイルが含まれます。

全てのリセットのようなファンデーションスタイルは、分割ファイルと共通CSSファイルの先頭とのどちらの場合でも、スタート直後に配置されます：

<a id="interaction"></a>
## モジュールの対応図

![image]({{ site.baseurl }}/images/layers.jpg)

### スタイルのリンク順序

全てのレイヤースタイルは、異なるモジュール／レイヤーのセレクター間の正しい関係を維持するために、正しい順序でページにリンクされなければなりません：

	0_layer_foundation
		reset.css

	1_layer_base
		base_modules.css

	2_layer_project
		project_modules.css

	cosmetic.css

<a id="1"></a>
## レイヤー 1 — ベース（ファーストレイヤー）

ファーストレイヤーはウェブサイトの骨子で、インターフェースの中心部分です。最も再利用可能で抽象的な構造に基づいています。

* フォーム
* ボタン
* ナビゲーションブロック
* その他

ベースレイヤースタイルはできるだけデザイナーのスタイルガイドと統合しなければなりません。ファーストレイヤーのモジュールは、全てのウェブサイトインターフェースに再利用されることを意図しているので、変更することなく他のインターフェース部分にフィットし、適切であるように見えなければなりません。

**プロジェクトにMCSSを導入するときに最初にすべきことは、再利用可能な標準スタイルのセットを作成することです。**

[Bootstrap](http://twitter.github.com/bootstrap/)や[960gs](http://960.gs/)、[inuit.css](https://github.com/csswizardry/inuit.css)などのポピュラーなフレームワークはファーストレイヤーの一部分として簡単に再利用できます。

### ルール

ファーストレイヤーの主要ルールは、全ての構成要素は名前とマークアップのどちらも抽象的である必要があるということです。

* クラス名はインターフェースのいかなる場所においても「無関係である」ように見えてはなりません。
* モジュールブロックはデフォルトスタイルを持たなくてはなりませんが、様々なプロジェクトモジュールやタスクに応じて簡単に変更できる必要もあります。

ファーストレイヤースタイルは同じレイヤーやセカンドレイヤーの他のモジュールからカスケードによって変更される可能性があります。これは関連するスタイルの位置は一ヶ所にあると見なすルールによるものです。

**ベーススタイルはセカンドレイヤーモジュールから分離され、プロジェクトレイヤースタイルから独立した状態を保たなければなりません。**

フォームの標準：

{% highlight css %}
.input-field { }
    .input-field_text { }
{% endhighlight %}

フォームの標準とボタンの標準の相互作用 - ファーストレイヤーからのカスケードによる変更：

{% highlight css %}
.input-field { }
    .input-field .button { }
{% endhighlight %}

セカンドレイヤー内におけるプロジェクトモジュールとフォームの標準の相互作用：

{% highlight css %}
.project-module { }
    .project-module .input-field { }
{% endhighlight %}

**ファーストレイヤーからのセカンドレイヤーの変更は禁止です！** この場合、レイヤーは混同され、混乱を引き起こします：

{% highlight css %}
    .input-field .project-module { }
{% endhighlight %}

ベーススタイルはセカンドレイヤーより優先されてファンデーションの直後に配置され、セレクター詳細度における優先度を低い状態で維持します。

### メリット

再利用可能でよく考えられたファーストレイヤーは、よくある構造をサポートする時間を節約し、複数の類似モジュールを維持する必要性を排除します。
また、再利用可能性は最終的なCSSファイルサイズとページのレンダリング時間に良い影響を与えます。

より良く開発されたベースを持つことで、大部分が標準要素で構成された新しいインターフェース作成が簡単になります。

標準デザインサンプルは、あるプロジェクトから別のプロジェクトへ再利用可能で、レイアウトとそれに関連づけられたバックエンド機能の両方の開発を促進できます。

<a id="2"></a>
## レイヤー 2 — プロジェクト（セカンドレイヤー）

セカンドレイヤーは、分離された、ページを構成するプロジェクトモジュールを含みます：

* 登録フォーム
* ログインブロック
* ショッピングカート
* その他

### ルール

セカンドレイヤーレイアウトでは、可能な限りユニークなCSSクラスの使用が推奨されます。現在のデザインがスタイリングを必要としない場合でも、それに対してユニークなCSSクラスを割り当てることはベタープラクティスです。このようなアプローチにより、HTMLの構造に影響を与えることなく正しいスタイルを容易に適用できるようになり、個々のレイアウトブロックごとに有用性を維持できるようになるでしょう。

ベースレイヤーのみと作用する独立したインターフェースブロックの各モジュールはできる限り分離される必要があります。

プロジェクトモジュール内でファーストレイヤー構造を利用するには、HTMLにもう1つCSSクラスを割り当てる必要があります：

{% highlight html %}
<header class="toolbar">
    <a href="/" class="toolbar_logo"></a>
    <menu class="toolbar_dropdown_ul umenu">
        <li class="umenu_li"></li>
        <li class="umenu_li"></li>
    </menu>
</header>
{% endhighlight %}

セカンドレイヤーモジュール**.toolbar**がファーストレイヤー標準の**.umenu**を利用している例です。プロジェクトモジュールの要求のために標準を変更する場合、CSSカスケードが使用されます：

{% highlight css %}
/* Toolbar
-------------------------------------------------- */
.toolbar { }

.toolbar_dropdown_ul { }
    .toolbar_dropdown_ul .umenu_li { }
/* /Toolbar */
{% endhighlight %}

**プロジェクトレイヤースタイルは、他のプロジェクトレイヤーモジュールからのみ、カスケードによる変更が行われる可能性があります！**

**正しい記述：**

{% highlight css %}
.project-module .other-project-module { }
{% endhighlight %}

誤った記述：

{% highlight css %}
.base-module .project-module { }
{% endhighlight %}

### メリット

モジュールを分離することで、他のインターフェース部分へ影響が及ぶ危険性なしに、そのスタイルへ簡単にアクセスできるようになります。チームで作業する場合、各チームメンバーが別々に1つのレイヤーを開発することで、他の開発者とのコンフリクトが発生しなくなります。

各モジュールのスタイルは、ページが必要とする箇所に適用することができます。

ウェブサイトから機能性が失われているとき、不要なスタイルを簡単に取り除くことができます。あるモジュールと対応するスタイルを投げ捨てればよいのです。

<a id="3"></a>
## レイヤー 3 — コスメティック（サードレイヤー）

サードレイヤーはシンプルで、わずかに影響するスタイルから成ります：

* リンクカラー
* シンプルなOOCSS - 少数のプロパティで構成されるCSSクラス（.font-size_XL, .margin-t_L）
* グローバルな修飾子

MCSSを利用するいくつかのケースではこのレイヤーは存在しないかもしれません。しかし大きなプロジェクトにおけるこのレイヤーは、スタイルの重複問題を解決し、稀にある非プロジェクトモジュールの記述を「DRY」なまま可能にします。

### ルール

サードレイヤースタイルはスタイルが破棄されている場合でもレイアウトを安全に保つ方法で構成されなければなりません。色やパディングなどのように、損失は小さくあるべきです。

稀にある非プロジェクトモジュールのために、シンプルなOOCSSクラスをブロックで最大3つまで使用できます：

{% highlight html %}
<div class="font-size_XL margin-t_L color_red"></div>
{% endhighlight %}

**コスメティックレイヤースタイルはコンテキストセレクター以外の他のレイヤーからカスケードによる変更を行ってはいけません。**

コスメティックスタイルはCSSの最後に適用されます。**!important** の使用はお勧めしません。

### メリット

スタイルはウェブサイトのレイアウトに対して大きな影響は持っていませんが、重複コード問題への対処や、小さなプロジェクトモジュール・ベースモジュールを作る必要性の排除といった助けになります。

非プロジェクトモジュールに少々のプロパティを適用する必要が出たとき、シンプルなセレクターはその稀な状況にすぐに対処できます。

<a id="context"></a>
## コンテキスト

このレイヤーは上位コンテキストのスタイルと、様々な状況のために標準スタイルを変更するのに使用される@mediaルールを含みます。

* .ie8, .ie9 - ブラウザー
* .touch
* .logged-in
* メディアクエリー

**コンテキストレイヤーはスタイル配置ルール上の例外です。**このレイヤーのスタイルは、コンテキストからカスケードによる変更が行われている全てのレイヤー間に配置されています：

{% highlight css %}
/* モジュール名
-------------------------------------------------- */
.module { }

.module_list { }
    .touch .module_list { }
    .ie9 .module_list { }

@media screen and (max-width: 1000px) {
    .module { }
    }
/* /モジュール名 */
{% endhighlight %}

<a id="examples"></a>
## 実際の例

こちらの[デモ]({{ site.baseurl }}/examples/layers/)でMCSSの動作を確認できます。この例では、全てのレイヤーは1つの[CSSファイル]({{ site.baseurl }}/examples/layers/css/style.css)に格納されていますが、個別のファイル（ブロック）に分割することもできます：

![image]({{ site.baseurl }}/images/file-system.png)

2つ目の[デモ]({{ site.baseurl }}/examples/mcss_with_bootstrap/)では、ファースト（ベース）レイヤーとしてのBootstrapを持つMCSSがどのように動作するかを確認できます。

プロジェクトのサイトも同様にMCSSでデザインされています。[ソース]({{ site.baseurl }}/theme/stylesheets/stylesheet.css)を見るのをためらったりしないでください。

**[Here](https://github.com/therobhrt/markup-process) you can find more complex example of MCSS methodology usage with video recording of development process.**

<a id="dictionary"></a>
### 略語辞典

長いCSSセレクター名を避けるため、略語辞典の利用をお勧めします：

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

将来的には、辞典は別のドキュメントに移動する予定です。

<a id="recommendations"></a>
## 推奨事

### コードスタイル

MCSSに加えて、コード品質を向上させるために以下に挙げる便利な実例の利用をお勧めします：

* [Principles of writing consistent, idiomatic CSS](https://github.com/necolas/idiomatic-css)
* [Google HTML/CSS style guide](http://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml) - HTMLとCSSのコード設定のためのスタイルガイド
* [CSScomb](http://csscomb.ru/) - CSSプロパティのソートを行うツール

### ベストプラクティス

* CSSにできるだけ多くのコメントを書きましょう。全ての非標準構成に、マジックナンバーに。私たちがそうするように、数ヶ月経ってコードレビューのためにあなたが戻ってきたときには、これはチームメンバーだけでなく、あなたにとっても役立つものとなります。