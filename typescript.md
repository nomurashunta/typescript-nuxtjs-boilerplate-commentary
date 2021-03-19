# typescriptとは

# tsconfig.jsonについて

`npx tsc --init` を実行すると作成される

重要な点:

tsconfig.jsonが存在するディレクトリは、そのディレクトリがTypeScriptプロジェクトのルート・フォルダであることを示す。

・どのファイルをコンパイルするかを指定する。ファイル名を直接指定するfiles、ファイル名のパターン（グロブ）で指定する includeなど。指定しなかった場合、プロジェクト内の全てのファイルがコンパイルされる。

[tsconfig.json | TypeScript 日本語ハンドブック | js STUDIO](http://js.studio-kingdom.com/typescript/project_configuration/tsconfig_json)

[Documentation - What is a tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)

そもそもtypescriptは言語というよりもnpmのパッケージ

なので yarn add typescriptとかでいれる

`yarn global add typescript`

これでtscとかがglobalに使えるようになる
(実際はグローバルじゃないほうがいいかも)

- npxとは

    [npmとyarnのコマンド早見表 - Qiita](https://qiita.com/rubytomato@github/items/1696530bb9fd59aa28d8)

- tcsとは

[TypeScriptの環境: tsconfig.json の基本](https://maku.blog/p/27m3brm/)

中身の具体的解説

[https://www.typescriptlang.org/docs/handbook/compiler-options.html](https://www.typescriptlang.org/docs/handbook/compiler-options.html)

[https://www.staging-typescript.org/tsconfig](https://www.staging-typescript.org/tsconfig)

[https://qiita.com/ryokkkke/items/390647a7c26933940470](https://qiita.com/ryokkkke/items/390647a7c26933940470)

```json
{
  "compilerOptions": {
    "target": "es2018",
    "module": "esnext",
    "moduleResolution": "node",
    "lib": [
      "esnext",
      "esnext.asynciterable",
      "dom"
    ],
    // <https://maku.blog/p/emdtiio/>
    // <https://omochizo.netlify.app/posts/2020/08/commonjs-esm/>
    // これが一番わかりやすい
    // <https://omochizo.netlify.app/posts/2020/08/commonjs-esm/>
    "esModuleInterop": true,
    // デコレーターを使った時に出るエラーを消すための記述
    // <https://qiita.com/HorikawaTokiya/items/54d90f83df4e72e27631>
    // デコレーターについて→https://www.typescriptlang.org/docs/handbook/decorators.html#decorators
    "experimentalDecorators": true,
    // JSONファイルから型の抽出・生成を行えるようにするための設定
    // <https://kakkoyakakko2.hatenablog.com/entry/2019/12/03/003000>
    // <https://qiita.com/MasanobuAkiba/items/98a678430fa192c0f8c5>
    "resolveJsonModule": true,
    // jsを使えるようにするための設定
    "allowJs": true,
    // ソースマップの有効か
    // <https://developer.mozilla.org/ja/docs/Tools/Debugger/How_to/Use_a_source_map>
    // <https://www.wetch.co.jp/output-source-map/>
    "sourceMap": true,
    // <https://maku.blog/p/7b9432m/>
    "strict": true,
    // trueにするとコンパイル結果を出力しなくなる。
    // tscによる型チェックだけを機能として利用したい場合（Babelなど他ツールが実際のコンパイルを行う場合）に使用する。
    // <https://qiita.com/ryokkkke/items/390647a7c26933940470#noemit>
    "noEmit": true,
    // <https://qiita.com/ryokkkke/items/390647a7c26933940470#baseurl>
    "baseUrl": ".",
    // インポートする際の記述を簡単にするための設定
    // <https://www.agent-grow.com/self20percent/2019/03/11/typescript-paths-work-careful/>
    "paths": {
      "~/*": [
        "src/*"
      ],
      "@/*": [
        "src/*"
      ]
    },
    "types": [
      "@types/node",
      "@nuxt/types",
      "@nuxtjs/axios"
    ]
  },
  "exclude": [
    "node_modules"
  ]
}

```

- commonJSとは

    > そもそも CommonJS とは何かと言うと、JavaScript の仕様を作っているプロジェクトです。
    JavaScript の仕様というと ECMAScript を連想する方も多いと思いますが、ECMAScript はブラウザ上での JavaScript の仕様と標準を作っているのに対し、CommonJS ではブラウザ上だけでなく、サーバーサイドやクライアントでのCUI、GUI で JavaScript を使う際の仕様を作成しています。

    [https://hysryt.com/archives/1542](https://hysryt.com/archives/1542)

    ようはrequireとかのあれ

    ```
    // script.js
    var math = require('./math');
    console.log(math.add(1, 3)); // 4

    ```

- ソースマップとは
  > ブラウザーが実行する JavaScript ソースは、開発者が作成した元のソースから何らかの方法で変換される場合があります。例えば:
より効率よくサーバーから提供するためにコンバインおよび ミニファイ されることがよくあります。
CoffeeScript や TypeScript のような言語からコンパイルするように、ページで実行する JavaScript が機械生成されることがあります。
このような状況では、ブラウザーがダウンロードした変換後のソースよりも、元のソースをデバッグするほうがとても容易です。ソースマップ は変換後のソースと元のソースを関連付けるファイルであり、ブラウザーが元のソースを再構成して、そのソースをデバッガーに提供できます。

- noemit
- ts導入

    [既存プロダクトに最小構成でTypeScriptを導入する | Raksul ENGINEERING](https://tech.raksul.com/2019/07/22/introduce-typescript-to-existing-product/)