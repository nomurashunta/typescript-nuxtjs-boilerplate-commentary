
# RSCSSとは

> cssの記述ルールとしてはBEM、FLOCSS、SMACSSなど様々ありますが、今回はシンプルでVueとの相性が良いRSCSSを採用しています。

## RSCSSについて

RSCSSとはどのようにCSSを書くかを定めた、CSS設計手法の一つです。ルールがシンプルなので比較的導入しやすい手法です。

## cssの見方

そもそもcss全くわからんという人は以下あたりざっくり読んでおくといいかも

http://www.tohoho-web.com/css/basic.html
https://developer.mozilla.org/ja/docs/Learn/CSS/First_steps/Getting_started
https://saruwakakun.com/html-css/basic/css

別に読まなくても問題ないように説明します

### SASS、SCSSについて

https://ferret-plus.com/12503
SCSSとSASSは、Sass（Syntactically Awesome Style Sheets）というRuby製のCSSメタ言語です。

http://www.tohoho-web.com/ex/sass.html
Sass には二つの形式の構文があります。一つは Sass(Syntactically Awesome Stylesheets)構文で、Python と同様インデント(字下げ)でブロックを、改行で文末を示します。もうひとつは SCSS(Sassy CSS)構文で、CSSと同様 { ... } でブロックを、セミコロン(;)で文末を示します。Sass構文ファイルの拡張子は .sass、SCSS構文ファイルの拡張子は .scss を用います。

css
```
.products .text {
   width: 300px;
}
```

scss
```
.products{
       .text {
         width: 300px;
       }
}
```

sass
```
.products
   .text
      width: 300px
```

scssでできること
- 変数が使える
    ```
    $font-stack: Helvetica, sans-serif;
    $primary-color: #333;

    body {
    font: 100% $font-stack;
    color: $primary-color;
    }
    ```
- ネスト（入れ子構造）が利用できる
- スタイルシートを分割できる(別ファイルをインポートできる)
  ```
  @import "../modules/clearfix"
  ```
- 条件分岐、関数が使える
- 継承ができる
  ```
  .list {
      margin     : 20px 0 0 0;
    
      .item {
          list-style      : none;
          font-size       : 100%;
      }
  }
    
  .floatList {
      @extend .list;
    
      .item {
          width           : 300px;
          float           : left;
          font-size       : 90%;
      }
  }
  ```

本来ならコンパイルが必要だが、Nuxtなら `<style lang="scss" scoped>` と指定するだけで自動でやってくれる(多分)  
pugに関してはそういうわけではないので別途パッケージが必要

https://qiita.com/amishiro/items/38fe1b102d7e91a93ada


## セレクタについて

コード見ていると出てくる`.`や`>`などの記号ですが、これはセレクタといい、特定の要素に対してスタイルを適用することを示します。

MDN Web Docs : CSS セレクター 
https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Selectors

```
h1 { color: red; }			/* h1要素に対して指定 */
h1, h2 { color: red; }			/* h1 と h2要素に対して指定 */
ul li { color: red; }			/* <ul>～</ul> の中にある li要素に対して指定 */
.sample { color: red; }			/* class="sample" を持つ要素に対して指定 */
#sample { color: red; }			/* id="sample" を持つ要素に対して指定 */
h1.sample { color: red; }		/* class="sample" を持つ div要素に対して指定 */
a:link { color: red; }			/* <a href="..."> のリンク(未訪問)に対して指定 */
```

とりあえず以下だけ覚えておけばよいと思います。

### 「.」: クラスセレクタ
指定された class 属性を持つすべての要素を選択します。
```
/* class="spacious" であるすべての要素 */
.spacious {
  margin: 2em;
}

/* class="spacious" であるすべての <li> 要素 */
li.spacious {
  margin: 2em;
}

/* "spacious" および "elegant" の両方をクラスリストに含む <li> 要素すべて */
/* 例えば、 class="elegant retro spacious" */
li.spacious.elegant {
  margin: 2em;
}
```

ドットで繋がれてあると「.以下の.以下の‥‥」みたいな感じに連想しがちだが実際はそうではない

### 「>」: 子結合子
親セレクタ中の特定の要素に対してのみスタイルを適用させるものです。

```
/* "my-things"クラスを持つリストの子要素であるリスト項目 */
ul.my-things > li {
  margin: 2em;
}
```

### 「,」: グループ化セレクタ、セレクターリスト
```
/* すべての一致する要素を選択 */
span, div {
  border: red 2px solid;
}
```

https://uxmilk.jp/8077

### 「&」について

これは元々のCSSではなくSASSの機能で、親セレクタを参照するキーワードです。

```
.foo {
    &:hover  { ... } //-> .foo:hover
    &:after  { ... } //-> .foo:after
    &.bar    { ... } //-> .foo.bar
    & + .bar { ... } //-> .foo + .bar
    & > .bar { ... } //-> .foo > .bar
    .bar & { ... }   //-> .bar .foo
}
```

```
.index-page {
  & > .header {
    margin-bottom: 30px;
  }
```

```
.index-page > .header {
	margin-bottom: 30px;
}
```

index-pageクラス以下のheaderクラス以下に対してスタイルを適用するものになっています。

### 

## pugとは

https://pughtml.com/


```
<template lang="pug">
.index-page
  .header
    h1.title 投稿記事
  .content
    .text 今はまだなにもない
</template>
 
<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
 
@Component
export default class IndexPage extends Vue {}
</script>
 
<style lang="scss" scoped>
.index-page {
  & > .header {
    margin-bottom: 30px;
  }
 
  & > .header > .title {
    font-size: 24px;
    font-weight: bold;
  }
 
  & > .content > .text {
    font-size: 64px;
  }
}
</style>
```

各コンポーネントの対応関係がわかりやすいからではないかと思っている



## リセットCSS
https://web-camp.io/magazine/archives/30817

# vue-property-decorator
要はTypescriptのクラスをVueで利用できる形にするものと認識しています。
`@Component` をつけると、続けて定義したクラスをVueが認識できる形に変換してくれます。

```
<script lang="ts">
import { Component, Vue } from 'nuxt-property-decorator';
 
@Component
export default class IndexPage extends Vue {}
</script>
```

```
<script>
export default {
  name: 'SampleComponent'
};
</script>
```

https://qiita.com/simochee/items/e5b77af4aa36bd0f32e5