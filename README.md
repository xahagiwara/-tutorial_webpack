# jsメモ
## WebPack
* ウェブコンテンツを構成するファイルをまとめて、リクエスト数を減らすことのできるモジュールバンドラー。

### webpack.config.js
* エントリーポイントの設定
    ```
    module.exports = {
      entry: `./src/index.js`
  };
    ```
* 出力ファイルの設定
    ```
    module.exports = {
      output: {
        path: `${__dirname}/dist`,
        filename: "main.js"
      }
    };
    ```
* 開発、本番環境の切り替え
    ```
    module.exports = {
      mode: 'production'
    };
    ```
* JS、json以外を読み込ませる
    ```
    module:{
        rules:[
            {
                test: /\.css$/,
                use:[
                    'style-loader',
                    'css-loader'
                ]
            }
        ]
    }
    ```
* プラグイン
    ```
    const MiniCssExtractPlugin = require('mini-css-extract-plugin');
    module:{
        plugins: [
            new MiniCssExtractPlugin({filename: 'style/[name].css'}),
        ],
    }
    ```
    
* CSSを圧縮
    * 必要プラグイン
    ```
    npm i -D optimize-css-assets-webpack-plugin
    npm i -D terser-webpack-plugin
    ```
    ```
    const OptimizeCSSAssetsPlugin = require("optimize-css-assets-webpack-plugin");
    const TerserPlugin = require('terser-webpack-plugin');
    
    module.exports = {
        module:{
            rules:[
                {
                    test: /\.css$/,
                    use:[
                        MiniCssExtractPlugin.loader,
                        'css-loader'
                    ]
                }
            ]
        },
        plugins: [
            new MiniCssExtractPlugin({filename: 'style/[name].css'}),
        ],
        optimization: {
            minimizer: [new TerserPlugin({}), new OptimizeCSSAssetsPlugin({})],
        },
    }
    ```
    ただし、modeをproductionに設定しないと圧縮されない

    
### webpack系列のコマンド
* Node.jsでwebサーバを立てる時
    ```
    npm run start
    npx webpack-dev-server
    ```
* ソースマップのみを生成する
    ```
    npx webpack --watch
    ```

## Node.js
* JSをブラウザ環境外（PCやサーバなど）で動かすJavaScript環境
### 即時関数
* 定義すると即時に実行
    ```  var sum = (function (a,b){
    var result = a + b;
    return result;
  })(1,2);
  console.log(sum);
  ```
* 即時関数を使うことにより、変数の汚染を気にすることなく連結を行うことができる。



