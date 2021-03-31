
<style>
.column-left{
  float: left;
  width: 47.5%;
  text-align: left;
}
.column-right{
  float: right;
  width: 47.5%;
  text-align: left;
}
.column-one{
  float: left;
  width: 100%;
  text-align: left;
}
</style>

## RSCSSとは
 

### SASS、SCSSについて

https://ferret-plus.com/12503
SCSSとSASSは、Sass（Syntactically Awesome Style Sheets）というRuby製のCSSメタ言語です。

http://www.tohoho-web.com/ex/sass.html
Sass には二つの形式の構文があります。一つは Sass(Syntactically Awesome Stylesheets)構文で、Python と同様インデント(字下げ)でブロックを、改行で文末を示します。もうひとつは SCSS(Sassy CSS)構文で、CSSと同様 { ... } でブロックを、セミコロン(;)で文末を示します。Sass構文ファイルの拡張子は .sass、SCSS構文ファイルの拡張子は .scss を用います。

```
.products .text {
   width: 300px;
}
```


```
.products{
       .text {
         width: 300px;
       }
}
```


```
.products
   .text
      width: 300px
```

scssでできること
- 変数が使える
    <div class="column-left">

    ## scss

    ```
    $font-stack: Helvetica, sans-serif;
    $primary-color: #333;

    body {
    font: 100% $font-stack;
    color: $primary-color;
    }
    ```
    </div>
    <div class="column-right">

## css

```
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
```
</div>

<div class="column-one">

- ネスト（入れ子構造）が利用できる
記述がわかりやすくなる


本来ならコンパイルが必要だが、Nuxtなら `<style lang="scss" scoped>` と指定するだけで自動でやってくれる(多分)  
pugに関してはそういうわけではないので別途パッケージが必要

https://qiita.com/amishiro/items/38fe1b102d7e91a93ada

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


</div>