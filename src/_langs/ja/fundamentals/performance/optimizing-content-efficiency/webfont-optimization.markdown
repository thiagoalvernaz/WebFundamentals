---
layout: article
title: "ウェブフォントの最適化"
description: "タイポグラフィは、優れたデザイン、ブランディング、読みやすさ、ユーザー補助にとって重要です。ウェブフォントを使うとこれらすべての品質をさらに高めることができます。テキストの選択、検索、拡大が可能になるほか、高精度の DPI に対応できるようになり、画面のサイズや解像度にかかわらず一貫性のある見栄えの良いテキスト表示になります。優れたデザイン、ユーザー エクスペリエンス、そしてパフォーマンスを実現するうえで、ウェブフォントはとても重要です。"
introduction: "タイポグラフィは、優れたデザイン、ブランディング、読みやすさ、ユーザー補助にとって重要です。ウェブフォントを使うとこれらすべての品質をさらに高めることができます。テキストの選択、検索、拡大が可能になるほか、高精度の DPI に対応できるようになり、画面のサイズや解像度にかかわらず一貫性のある見栄えの良いテキスト表示になります。優れたデザイン、ユーザー エクスペリエンス、そしてパフォーマンスを実現するうえで、ウェブフォントはとても重要です。"
article:
  written_on: 2014-09-20
  updated_on: 2014-09-30
  order: 4
collection: optimizing-content-efficiency
authors:
  - ilyagrigorik
key-takeaways:
  anatomy:
    - "Unicode フォントには数千ものグリフを含めることができる"
    - "フォントには WOFF2、WOFF、EOT、TTF の 4 つの形式がある"
    - "一部のフォント形式では GZIP 圧縮を使う必要がある"
  font-family:
    - "複数のフォント形式を指定するには format() ヒントを使う"
    - "多数の Unicode フォントをサブセットにまとめることでパフォーマンスが向上: unicode-range によるサブセット化を使い、旧式のブラウザの場合は代わりに手動サブセット化を提供する"
    - "スタイル別の派生フォントの数が減り、ページやテキスト表示のパフォーマンスが向上する"
  font-crp:
    - "表示ツリーが形成されるまでフォントのリクエストが後回しにされるため、テキストの表示が遅れることがある"
    - "Font Loading API を使うと、フォントの読み込みと表示に独自の方式を実装して、読み込みの遅いデフォルトのフォントを無効化できる"
    - "フォントのインライン化を使うと、旧式のブラウザで読み込みの遅いデフォルトのフォントを無効化できる"
notes:
  svg:
    - "技術的には <a href='http://caniuse.com/svg-fonts'>SVG フォント コンテナ</a>（リンク先は英語）もありますが、IE や Firefox では一切サポートされておらず、Chrome では現在は廃止されています。使用が限られるため、このガイドでは説明しません。"
  zopfli:
    - "EOT、TTF、WOFF の形式では <a href='http://en.wikipedia.org/wiki/Zopfli'>Zopfli 圧縮</a>（リンク先は英語）の使用をおすすめします。Zopfli は zlib と互換性のある圧縮アルゴリズムで、gzip と比べてファイルサイズの圧縮がおよそ 5% 向上します。"
  local-fonts: 
    - "デフォルトのシステム フォントについては、そのいずれかを参照することがない限り、ユーザーがローカルにインストールすることは実用上はまれです。特に携帯端末では、追加のフォントを「インストール」することは実質的に不可能です。そのため、常に外部フォントの場所のリストを提供するようにしてください。"
  font-order:
    - "派生フォントの指定順序は重要です。ブラウザは、自身がサポートしている最初の形式を選択します。たとえば、新しいブラウザで WOFF2 を使いたい場合は、WOFF の前に WOFF2 宣言を記述します。"
  unicode-subsetting:
    - "unicode-range によるサブセット化は特にアジア系の言語で重要です。これらの言語では、グリフの数が西洋言語よりもずっと多く、通常の「フル装備の」フォントではそのサイズが数十キロバイト単位ではなく数メガバイト単位に及ぶことが多くあります。"
  synthesis:
    - "最適な一貫性と見栄えを保つため、フォントの合成は利用しないようにしてください。代わりに、使用する派生フォントの数を最小限に抑えてそれらの場所を指定してください。そうすることで、ページ上で使用されるときにブラウザがフォントをダウンロードできるようになります。ただし、場合によっては合成の派生フォントが<a href='https://www.igvita.com/2014/09/16/optimizing-webfont-selection-and-synthesis/'>使用可能な選択肢となることがあります</a>（リンク先は英語）。使用の際は注意してください。"
  webfontloader:
    - "Font Loading API は<a href='http://caniuse.com/#feat=font-loading'>一部のブラウザではまだ開発段階です</a>（リンク先は英語）。同様の機能を実現するには <a href='https://github.com/bramstein/fontloader'>FontLoader polyfill</a> または <a href='https://github.com/typekit/webfontloader'>webfontloader ライブラリ</a>（いずれもリンク先は英語）の使用をおすすめします。ただし、JavaScript への依存性がさらに高まります。"
  font-inlining: 
    - "インライン化は状況に応じて使い分ける@font-face では遅延読み込みの動作を使用しますが、これは不要な派生フォントやサブセット フォントのダウンロードを避けるためです。また、インライン化を過度に使用して CSS のサイズを増やすと<a href='/web/fundamentals/performance/critical-rendering-path/'>クリティカル レンダリング パス</a>に悪い影響を与えます。ブラウザはすべての CSS をダウンロードした後でないと、CSSOM を生成して表示ツリーを構築し、ページ コンテンツを画面に表示することができません。"
---

{% wrap content%}

{% include modules/toc.liquid %}

ウェブフォントの最適化は全体的なパフォーマンス対策の重要な要素です。フォントはそれぞれ追加のリソースです。一部のフォントによってテキストの表示が妨げられることがありますが、ページでウェブフォントを使用しているからと言って必ずしも表示が遅れるというわけではありません。むしろ、最適化されたフォントを使用して、それらのフォントをページ上でどのように読み込んで適用するのかを適切に決めれば、全体のページ サイズが減少してページの表示時間が向上します。

## ウェブフォントの詳細

{% include modules/takeaway.liquid list=page.key-takeaways.anatomy %}

ウェブフォントはグリフの集まりであり、それぞれのグリフが文字や記号を記述するベクター形状になっています。そのため、特定のフォント ファイルのサイズは 2 つの単純な変数によって決まります。1 つは各グリフのベクターパスの複雑さで、もう 1 つは特定のフォントにおけるグリフの数です。たとえば、ごく一般的なウェブフォントの 1 つである Open Sans には、ラテン文字、ギリシャ文字、キリル文字などの 897 個のグリフが含まれています。

<img src="images/glyphs.png" class="center" alt="フォントのグリフ テーブル">

フォントを選択する際は、どの文字セットがサポートされているのかを考慮することが重要です。ページ コンテンツを複数の言語にローカライズする必要がある場合は、一貫性のある外観やエクスペリエンスをユーザーに提供できるフォントを使用してください。たとえば、[Google の Noto フォント ファミリ](https://www.google.com/get/noto/)は全世界の言語のサポートを目的としたものです。ただし、Noto の合計サイズは、すべての言語を含めると 130MB を超える ZIP のダウンロードになります。

ウェブでフォントを使用する際は、タイポグラフィがパフォーマンスに悪影響を及ぼさないように十分注意する必要があります。幸い、ウェブ プラットフォームには必要な基本要素がすべて用意されています。以降このガイドでは、実際に両者の長所を生かす方法について説明します。

### ウェブフォントの形式

現在ウェブでは、[EOT](http://en.wikipedia.org/wiki/Embedded_OpenType)、[TTF](http://en.wikipedia.org/wiki/TrueType)、[WOFF](http://en.wikipedia.org/wiki/Web_Open_Font_Format)、[WOFF2](http://www.w3.org/TR/WOFF2/)（いずれもリンク先は英語）の 4 種類のフォント コンテナが利用されています。残念ながら、幅広い選択肢があるにもかかわらず、新旧のすべてのブラウザで動作する単一の普遍的な形式はありません。EOT は [IE のみ](http://caniuse.com/#feat=eot)です。TTF は [IE で一部しかサポートされていません](http://caniuse.com/#search=ttf)。WOFF は最も幅広くサポートされていますが、[一部の旧式のブラウザで利用できません](http://caniuse.com/#feat=woff)。WOFF 2.0 のサポートについては[多数のブラウザで作業が進行中です](http://caniuse.com/#feat=woff2)（いずれもリンク先は英語）。

ではどのようにすればよいでしょうか。すべてのブラウザで動作する単一の形式がないため、一貫性のあるエクスペリエンスを提供するために複数の形式を提供する必要があります:

* WOFF 2.0 派生フォントはサポートしているブラウザで利用できる
* WOFF 派生フォントは大多数のブラウザで利用できる
* TTF 派生フォントは古い Android ブラウザ（4.4 以前）で利用できる
* EOT 派生フォントは古い IE ブラウザ（IE9 以前）で利用できる
^

{% include modules/remember.liquid title="Note" list=page.notes.svg %}

### 圧縮を利用したフォント サイズの縮小

フォントはグリフの集まりであり、それぞれのグリフは文字の形状を記述する 1 組のパスです。個々のグリフはもちろん異なりますが、似通った情報が多数含まれており、GZIP や互換性のある圧縮アルゴリズムを使用して圧縮できます:

* EOT 形式と TTF 形式はデフォルトで圧縮されません。これらの形式を提供する場合は [GZIP 圧縮](/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer#text-compression-with-gzip)を適用するようにサーバーを設定します。
* WOFF には圧縮が組み込まれています。WOFF 圧縮アルゴリズムで最適な圧縮設定を使用します。
* WOFF2 では独自の前処理アルゴリズムと圧縮アルゴリズムが使用されており、他の形式よりも約 30% ファイルサイズが縮小します。詳しくは[レポート](http://www.w3.org/TR/WOFF20ER/)（リンク先は英語）をご覧ください。

なお、一部のフォント形式には[フォント ヒンティング](http://en.wikipedia.org/wiki/Font_hinting)情報や[カーニング](http://en.wikipedia.org/wiki/Kerning)情報などの追加のメタデータが含まれています（いずれもリンク先は英語）。プラットフォームによってはこれらは不要な場合があり、その場合はファイルサイズをさらに最適化できます。使用できる最適化オプションについてはフォント圧縮アルゴリズムのマニュアルをご覧ください。この方法を利用する場合は、対象のインフラストラクチャで最適化されたフォントをテストし、それぞれの特定のブラウザに提供してください。たとえば、Google のフォントにはフォントごとに 30 あまりの最適化された派生フォントが含まれており、プラットフォームやブラウザごとに最適な派生フォントを自動的に検出して提供します。

{% include modules/remember.liquid title="Note" list=page.notes.zopfli %}

## @font-face を利用したフォント ファミリの定義

{% include modules/takeaway.liquid list=page.key-takeaways.font-family %}

CSS アットルールの @font-face を使うと、特定のフォント リソースについて、その場所、スタイル属性、使用すべき Unicode コードポイントを定義できます。こうした @font-face 宣言を組み合わせて使うことで「フォント ファミリ」を構築できます。ブラウザはこの「フォント ファミリ」を使用することで、どのフォント リソースをダウンロードして現在のページに適用する必要があるかを判断します。この仕組みについて詳しく見てみましょう。

### 形式の選択

それぞれの @font-face 宣言によってフォント ファミリの名前が提供されますが、それらは複数の宣言の論理的なグループである[フォント プロパティ](http://www.w3.org/TR/css3-fonts/#font-prop-desc)（リンク先は英語）として機能します。これには、スタイル、ウェイト、ストレッチ、そして、フォント リソースの場所の優先順位付きリストを指定する [src ディスクリプタ](http://www.w3.org/TR/css3-fonts/#src-desc)（リンク先は英語）などがあります。

{% highlight css  %}
@font-face {
  font-family: 'Awesome Font';
  font-style: normal;
  font-weight: 400;
  src: local('Awesome Font'),
       url('/fonts/awesome.woff2') format('woff2'), 
       url('/fonts/awesome.woff') format('woff'),
       url('/fonts/awesome.ttf') format('ttf'),
       url('/fonts/awesome.eot') format('eot');
}

@font-face {
  font-family: 'Awesome Font';
  font-style: italic;
  font-weight: 400;
  src: local('Awesome Font Italic'),
       url('/fonts/awesome-i.woff2') format('woff2'), 
       url('/fonts/awesome-i.woff') format('woff'),
       url('/fonts/awesome-i.ttf') format('ttf'),
       url('/fonts/awesome-i.eot') format('eot');
}
{% endhighlight %}

最初に、前の例では _Awesome Font_ という単一のファミリを定義しています。このファミリには 2 つのスタイル（normal と _italic_）があり、それぞれが異なるフォント リソース セットを指し示しています。さらに、それぞれの「src」ディスクリプタには、カンマで区切られた派生リソースの優先順位付きリストが含まれています:

* 「local()」ディレクティブを使うと、ローカルにインストールされているフォントの参照、読み込み、使用ができます。
* 「url()」ディレクティブを使うと、外部フォントの読み込みができます。また、オプションの「format()」ヒントを含めることで、指定した URL によって参照されるフォントの形式を指定できます。

^
{% include modules/remember.liquid title="Note" list=page.notes.local-fonts %}

ブラウザは、フォントが必要であると判断すると、指定されたリソース リストを指定された順序で調べ、該当するリソースの読み込みを試みます。たとえば前の例では次のようになります:

1. ブラウザは、ページのレイアウトを実行し、指定されたテキストをページに表示するためにどの派生フォントが必要なのかを判断します。
2. それぞれの必要なフォントについて、ブラウザは、ローカルのフォントが使用できるかどうかを調べます。
3. ローカルのフォント ファイルが使用できない場合は、外部定義を順番に調べます:
  * 形式ヒントが存在する場合、ブラウザは自身がサポートしているかどうかを調べ、サポートしている場合はダウンロードを開始します。サポートしていない場合は次の形式ヒントを調べます。
  * 形式ヒントが存在しない場合、ブラウザはリソースをダウンロードします。

ローカル / 外部ディレクティブと適切な形式ヒントを組み合わせて使うことで、使用可能なすべてのフォント形式を指定して、残りの処理をブラウザに任せることができます。ブラウザは、どのリソースが必要なのかを判断して、最適な形式を自動的に選択します。

{% include modules/remember.liquid title="Note" list=page.notes.font-order %}

### unicode-range によるサブセット化

スタイル、ウェイト、ストレッチなどのフォント プロパティに加えて、@font-face ルールではそれぞれのリソースでサポートされる 1 組の Unicode コードポイントを定義することもできます。これを使って、大きい Unicode フォントをより小さいサブセット（ラテン、キリル、ギリシャの各文字のサブセットなど）に分割し、特定のページでテキストの表示に必要なグリフだけをダウンロードできます。

[unicode-range ディスクリプタ](http://www.w3.org/TR/css3-fonts/#descdef-unicode-range)（リンク先は英語）を使うと、カンマで区切られた範囲値のリストを指定できます。範囲値はそれぞれ次の 3 つのうちいずれかの形式で指定できます。

* 1 つのコードポイント（例: U+416）
* 範囲（例: U+400-4ff）: ある範囲のコードポイントの始めと終わりを表す
* ワイルドカード範囲（例: U+4??）: 「?」文字は任意の 16 進数を表す

たとえば、前述の _Awesome Font_ ファミリをラテン語と日本語のサブセットに分割し、ブラウザがそれぞれのサブセットを必要に応じてダウンロードするようにできます:

{% highlight css %}
@font-face {
  font-family: 'Awesome Font';
  font-style: normal;
  font-weight: 400;
  src: local('Awesome Font'),
       url('/fonts/awesome-l.woff2') format('woff2'), 
       url('/fonts/awesome-l.woff') format('woff'),
       url('/fonts/awesome-l.ttf') format('ttf'),
       url('/fonts/awesome-l.eot') format('eot');
  unicode-range: U+000-5FF; /* Latin glyphs */
}

@font-face {
  font-family: 'Awesome Font';
  font-style: normal;
  font-weight: 400;
  src: local('Awesome Font'),
       url('/fonts/awesome-jp.woff2') format('woff2'), 
       url('/fonts/awesome-jp.woff') format('woff'),
       url('/fonts/awesome-jp.ttf') format('ttf'),
       url('/fonts/awesome-jp.eot') format('eot');
  unicode-range: U+3000-9FFF, U+ff??; /* Japanese glyphs */
}
{% endhighlight %}

{% include modules/remember.liquid title="Note" list=page.notes.unicode-subsetting %}

unicode-range によるサブセットを使い、スタイル別の派生フォントにそれぞれ別々のファイルを使うことで、より高速かつ効率よくダウンロードされる複合フォント ファミリを定義できます。ブラウザでは、必要な派生フォントやサブセットをダウンロードするだけで済み、ページ上で表示されたり使用されたりすることが決してないサブセットをダウンロードする必要がなくなります。

ただし、unicode-range には 1 つだけ、[すべてのブラウザがサポートしているわけではない](http://caniuse.com/#feat=font-unicode-range)（リンク先は英語）という小さな欠点があります。unicode-range ヒントを無視してすべての派生フォントをダウンロードするブラウザもあれば、@font-face 宣言をまったく処理できないブラウザもあります。こうした問題に対処するには、旧式のブラウザで代わりに「手動サブセット化」を使う必要があります。

旧式のブラウザは必要なサブセットだけを選択できる機能を備えておらず、複合フォントを構築できないため、代わりに、必要なサブセットをすべて含んだ単一のフォント リソースを提供して、残りをブラウザから隠す必要があります。たとえば、ページでラテン文字しか使われていない場合は、それ以外のグリフを取り除いて、特定のサブセットを単独のリソースとして利用することができます。

1. ** どのサブセットが必要かを判断する方法 ** 
  - unicode-range によるサブセット化がブラウザでサポートされている場合は、自動的に正しいサブセットが選択されます。ページでは、サブセット ファイルを提供し、該当する unicode-range を @font-face ルールで指定するだけで済みます。
  - unicode-range がサポートされていない場合は、ページで不要なサブセットをすべて隠す必要があります。つまり、デベロッパーが必要なサブセットを指定する必要があります。
2. ** フォント サブセットを生成する方法 **
  - オープンソースの [pyftsubset ツール](https://github.com/behdad/fonttools/blob/master/Lib/fontTools/subset.py#L16)（リンク先は英語）を使ってフォントのサブセット化と最適化を行います。
  - フォント サービスによっては独自のクエリ パラメータを通じて手動サブセット化が行えるものがあり、この方法を使ってページに必要なサブセットを手動で指定できます。詳しくはフォント提供者のマニュアルをご覧ください。


### フォントの選択と合成

フォント ファミリはそれぞれ、複数のスタイル別の派生フォント（標準、太字、斜体）と、スタイルごとの複数のウェイトで構成されますが、さらにスタイルに含まれるグリフ形状がスタイルごとに大きく異なる場合があります。たとえば、スペーシングやサイジングが異なる場合や、形状が完全に異なる場合があります。

<img src="images/font-weights.png" class="center" alt="フォント ウェイト">

たとえば上の図は、400（標準）、700（太字）、900（極太）の 3 つの異なる太字ウェイトを提供するフォント ファミリを表しています。それ以外のウェイトの派生フォント（グレーで表示）はすべて、ブラウザによって最も近い派生フォントに自動的にマッピングされます。

<div class="quote">
  <div class="container">
    <blockquote class="quote__content g-wide--push-1 g-wide--pull-1 g-medium--push-1">指定されたウェイトに対応するフェイスが存在しない場合は、それに近いウェイトのフェイスが使用されます。一般に、太字のウェイトは、より重いウェイトのフェイスにマッピングされ、細字のウェイトは、より軽いウェイトのフェイスにマッピングされます。
    <p><a href="http://www.w3.org/TR/css3-fonts/#font-matching-algorithm">CSS3 のフォント マッチング アルゴリズム</a></p>（リンク先は英語）
    </blockquote>
  </div>
</div>

_italic_ の派生フォントにも同様のロジックが適用されます。フォント デザイナーはどの派生フォントを生成するのかをコントロールし、ユーザーはどの派生フォントをページ上で使用するのかをコントロールします。派生フォントはそれぞれ別々のダウンロードになるため、派生フォントの数は少なく保つことをおすすめします。たとえば、_Awesome Font_ ファミリ用に 2 つの太字の派生フォントを定義できます: 

{% highlight css %}
@font-face {
  font-family: 'Awesome Font';
  font-style: normal;
  font-weight: 400;
  src: local('Awesome Font'),
       url('/fonts/awesome-l.woff2') format('woff2'), 
       url('/fonts/awesome-l.woff') format('woff'),
       url('/fonts/awesome-l.ttf') format('ttf'),
       url('/fonts/awesome-l.eot') format('eot');
  unicode-range: U+000-5FF; /* Latin glyphs */
}

@font-face {
  font-family: 'Awesome Font';
  font-style: normal;
  font-weight: 700;
  src: local('Awesome Font'),
       url('/fonts/awesome-l-700.woff2') format('woff2'), 
       url('/fonts/awesome-l-700.woff') format('woff'),
       url('/fonts/awesome-l-700.ttf') format('ttf'),
       url('/fonts/awesome-l-700.eot') format('eot');
  unicode-range: U+000-5FF; /* Latin glyphs */
}
{% endhighlight %}

前の例で宣言した _Awesome Font_ ファミリは 2 つのリソースで構成されています。これらは同じラテン グリフ セットを対象としています（U+000-5FF）が、標準（400）と太字（700）の 2 つの異なる「ウェイト」を提供します。しかし、いずれかの CSS ルールで、異なるフォント ウェイトを指定したり、font-style プロパティを斜体に設定したりした場合はどうなるでしょうか。

* 正確に一致するフォントが見つからない場合、ブラウザは最も近いものを代用します。
* スタイル別に一致するフォントが見つからない場合（前の例で斜体の派生フォントを宣言しなかった場合など）、ブラウザは独自の派生フォントを合成します。

<img src="images/font-synthesis.png" class="center" alt="フォントの合成">

<div class="quote">
  <div class="container">
    <blockquote class="quote__content g-wide--push-1 g-wide--pull-1 g-medium--push-1">斜体の形状が非常に異なるキリルなどの文字では合成による方法が適さない場合があることにも注意する必要があります。合成フォントに頼るよりも実際の斜体フォントを使用する方が常に優れています。
    <p><a href="http://www.w3.org/TR/css3-fonts/#propdef-font-style">CSS3 の font-style</a></p>（リンク先は英語）
    </blockquote>
  </div>
</div>

前の例では、Open-Sans の場合における実際のフォントと合成フォントの違いを示しています。合成の派生フォントはすべて、1 つの 400 ウェイトのフォントから生成されます。ご覧のように、著しい違いが見られます。太字とオブリークの派生フォントについては、生成方法の詳細が指定されていません。したがって、その結果はブラウザごとに異なり、またフォントに大きく依存します。

{% include modules/remember.liquid title="Note" list=page.notes.synthesis %}


## 読み込みと表示の最適化

{% include modules/takeaway.liquid list=page.key-takeaways.font-crp %}

「完全装備の」ウェブフォントにはスタイル別の派生フォントとグリフがすべて含まれていますが、その中には必要のないものも含まれています。そのため、ダウンロードのサイズが数メガバイトに及ぶことがよくあります。この問題に対処するため、@font-face CSS ルールではフォント ファミリをリソースのコレクション（Unicode サブセット、個別の派生スタイルなど）に分割できるようになっています。

これらが宣言されている場合、ブラウザは必要なサブセットや派生フォントを判断して、テキストの表示に必要な最小限のセットをダウンロードします。この動作は大変便利ですが、クリティカル レンダリング パスの中でパフォーマンスのボトルネックが生じたり、テキストの表示が遅れたりするなど、回避すべき副作用が生じる可能性もあるので注意が必要です。

### ウェブフォントとクリティカル レンダリング パス

フォントの遅延読み込みは、目に見えない形で重要な影響をもたらし、テキストの表示を遅らせる場合があります。ブラウザは、どのフォント リソースがテキストの表示に必要なのかを知る前に[表示ツリーを構築する](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction)必要がありますが、表示ツリーは DOM ツリーや CSSOM ツリーに依存しています。その結果、フォントのリクエストが他の重要なリソースよりもずっと遅れることになり、リソースを取得するまでブラウザでのテキストの表示が妨げられる場合があります。

<img src="images/font-crp.png" class="center" alt="フォントのクリティカル レンダリング パス">

1. ブラウザが HTML ドキュメントをリクエストする
2. ブラウザが HTML レスポンスの解析と DOM の構築を始める
3. ブラウザが CSS、JS、その他のリソースを検出し、リクエストを発信する
4. すべての CSS コンテンツを受信した時点で、ブラウザが CSSOM を構築し、DOM ツリーと結合して表示ツリーを構築する
  * ページ上の指定されたテキストの表示に必要な派生フォントがどれかが表示ツリーで示された時点で、フォント リクエストが発信される
5. ブラウザがレイアウトを実行し、コンテンツを画面に描画する
  * フォントがまだ使用できない場合、ブラウザはテキスト ピクセルを表示できない可能性がある
  * フォントが使用できるようになるとブラウザがテキスト ピクセルを描画する

最初のページ コンテンツの描画（表示ツリー構築のすぐ後に実行される可能性があります）と、フォント リソースのリクエストとの間に起こる「競合」によって、「空テキストの問題」が生じます。この場合、ブラウザはページ レイアウトを表示しますがテキストをすべて省略します。各種ブラウザ間での実際の動作の違いは次のようになります:

* Safari では、フォントのダウンロードが完了するまでテキストの表示が保留されます。
* Chrome と Firefox では、フォントの表示が最大 3 秒間保留されます。その後で代替フォントを使用し、フォントのダウンロードが完了すると、ダウンロードされたフォントを使用してもう一度テキストを再表示します。
* IE では、リクエストされたフォントがまだ使用できない場合は代替フォントを使用して即座に表示を行い、フォントのダウンロードが完了した時点で再表示を行います。

こうしたさまざまな表示方法についてはそれぞれに賛否両論があります。再表示は目障りだという人もいれば、すぐに結果が表示される方が良い、フォントのダウンロードが完了すればページの再表示は気にならないという人もいます。ここではどちらが良いかという議論には立ち入りません。重要なのは、遅延読み込みではバイト数が減少するものの、テキストの表示が遅れる可能性もある、ということです。次に、この動作を最適化する方法について見てみましょう。

### Font Loading API を利用したフォントの表示の最適化

[Font Loading API](http://dev.w3.org/csswg/css-font-loading/)（リンク先は英語）はスクリプト記述のインターフェースとなるもので、CSS フォント フェイスの定義や操作、それらのダウンロードの進行情報の追跡、デフォルトの遅延読み込み動作の無効化が行えます。たとえば、特定の派生フォントが必要になることがわかっている場合に、そのフォントを定義し、フォント リソースの取得を直ちに開始するようブラウザに指示することができます:

{% highlight javascript %}
var font = new FontFace("Awesome Font", "url(/fonts/awesome.woff2)", {
  style: 'normal', unicodeRange: 'U+000-5FF', weight: '400'
});

font.load(); // don't wait for render tree, initiate immediate fetch!

font.ready().then(function() {
  // apply the font (which may rerender text and cause a page reflow)
  // once the font has finished downloading
  document.fonts.add(font);
  document.body.style.fontFamily = "Awesome Font, serif";

  // OR... by default content is hidden, and rendered once font is available
  var content = document.getElementById("content");
  content.style.visibility = "visible";

  // OR... apply own render strategy here... 
});
{% endhighlight %}

また、フォントの状態を（[check()](http://dev.w3.org/csswg/css-font-loading/#font-face-set-check)（リンク先は英語）メソッドを通じて）確認し、ダウンロードの進行状況を追跡できるので、ページにテキストを表示するための独自の方法を定義することもできます。

* フォントが使用可能になるまですべてのテキストの表示を保留できます。
* フォントごとに独自のタイムアウトを実装できます。
* 代替フォントを使用して表示の保留を解除し、フォントが使用可能になった時点で、目的のフォントを使用した新しいスタイルを表示できます。

特に、ページ上のさまざまなコンテンツに対して上記の方法を組み合わせることもできます。たとえば、「フォントが使用可能になるまで一部のセクションでテキストの表示を保留する」、「代替フォントを使用し、フォントのダウンロードが完了したら再表示する」、「さまざまなタイムアウトを指定する」などの方法を利用できます。

{% include modules/remember.liquid title="Note" list=page.notes.webfontloader %}

### インライン化を利用したフォントの表示の最適化

Font Loading API を利用する代わりに「空テキストの問題」を解消する単純な対策として、フォント コンテンツを CSS スタイルシートにインライン化する方法があります:

* 一致するメディア クエリを持つ CSS スタイルシートは、ブラウザによって高い優先順位で自動的にダウンロードされます。これは、CSSOM の構築に必要だからです。
* フォント データを CSS スタイルシートにインライン化すると、ブラウザは表示ツリーの構築を待つことなく、そのフォントを強制的に高い優先順位でダウンロードします。これは、デフォルトの遅延読み込み動作に対する手動の無効化として機能します。

インライン化による方法はそれほど柔軟性がなく、さまざまなコンテンツに対して独自のタイムアウトや表示方法を定義することはできませんが、単純で確実な解決策であり、すべてのブラウザで有効です。最適な結果を得るため、インライン化したフォントは単独のスタイルシートに分けておき、最大限の存続期間で利用してください。そうすることで、CSS を更新する際に訪問者にフォントの再ダウンロードを強制せずに済みます。

{% include modules/remember.liquid title="Note" list=page.notes.font-inlining %}

### HTTP キャッシュを利用したフォントの再利用の最適化

フォント リソースは通常は静的なリソースであり、頻繁に更新されることはありません。そのため、最大限の存続期間まで利用するのが理想的です。必ずすべてのフォント リソースに対して[条件付き ETag ヘッダー](/web/fundamentals/performance/optimizing-content-efficiency/http-caching#validating-cached-responses-with-etags)と[最適なキャッシュ管理ポリシー](/web/fundamentals/performance/optimizing-content-efficiency/http-caching#cache-control)の両方を指定してください。
    
フォントをローカル ストレージやその他のメカニズムを利用して保存する必要はありません。こうしたメカニズムにはそれぞれパフォーマンスに関する制限があります。ブラウザの HTTP キャッシュは、Font Loading API や webfontloader ライブラリとともに、ブラウザにフォント リソースを提供するための最も確実で最適なメカニズムとなります。


## 最適化のチェックリスト

一般的な理解とは裏腹に、ウェブフォントを利用した場合、必ずしもページの表示が遅れたり、その他のパフォーマンス指標に悪影響が生じたりするわけではありません。適切に最適化されたフォントを利用した方が、全体的なユーザー エクスペリエンスがはるかに向上します。優れたブランディングを実現できるほか、読みやすさ、使い勝手、検索能力が向上すると同時に、複数の解像度に対応した拡張性のある解決策を実現でき、あらゆる画面形式や解像度に適切に対応できるようになります。ぜひウェブフォントを積極的に活用してみてください。

とは言え、十分な配慮をせずに実装すると、大量のダウンロードや不要な遅延を招く可能性があります。そこで必要になるのが Google の最適化ツールキットです。これを利用して、ブラウザ自身でフォント アセットを最適化し、それらをどのように取得してページ上で利用するのかを最適化できるようにします。

1. ** フォントの利用を調査し監視する: ** ページ上であまり多くのフォントを使用しないようにし、フォントごとに使用する派生フォントの数を最小限に抑えます。こうすることで、ユーザー エクスペリエンスの一貫性が高まり、動作が高速になります。
2. ** フォント リソースをサブセット化する: ** 多数のフォントをサブセット化したり、複数の unicode-range に分割したりすることで、特定のページで必要なグリフだけを提供できます。その結果、ファイルサイズが減少し、リソースのダウンロード速度が速くなります。ただし、サブセットを定義する際はフォントの再利用を考慮して注意深く最適化してください。たとえば、ページごとに異なる文字セットをダウンロードする際、文字セットに重複が生じないようにします。スクリプト（ラテン、キリルなど）に基づいてサブセット化することをおすすめします。
3. ** ブラウザごとに最適化されたフォント形式を提供する: ** それぞれのフォントを WOFF2、WOFF、EOT、TTF の各形式で提供します。EOT 形式と TTF 形式はデフォルトで圧縮されないため、必ず GZIP 圧縮を適用します。
4. ** 再検証と最適なキャッシュ ポリシーを指定する:** フォントは静的なリソースであり、頻繁に更新されることはありません。サーバーで長期間にわたって最大限存続させるようにします。また、再検証トークンを用意して、異なるページどうしの間でフォントが効率よく再利用されるようにします。
5. ** Font Loading API を使用してクリティカル レンダリング パスを最適化する: ** デフォルトの遅延読み込み動作では結果としてテキストの表示が遅れる場合があります。 Font Loading API を使うと特定のフォントに対してこの動作を無効化することができ、ページ上のさまざまなコンテンツに対して独自の表示方法やタイムアウトを指定できます。API をサポートしていない旧式のブラウザの場合は、webfontloader JavaScript ライブラリを利用するか、CSS インライン化による方法を利用できます。

{% endwrap %}

