## ログ方式

Spring Bootのデフォルトロガーを利用する  
Spring BootのデフォルトロガーはLogback  
starter-webの依存関係を含めると自動的にLogbackが組み込まれる  

### ログの拡張  

Logbackの設定内で環境変数などを利用する場合はLogbackのデフォルトではなく、  
Springの拡張設定を適用する  
Springの拡張設定はLogbackの設定ファイルをresources直下にlogback-spring.xmlファイルを配備する  
  
### ログ設定

#### 実行モードごとの変数

SpringProfileでロガー用の実行モードごとの変数を設定する  
|実行モード|変数値|
|--|--|
|dev|DEV_MODE|
|prod|PROD_MODE|

#### ログパターン

Java側のログパターンは下記を設定する

```
|DEFAULT_PATTERN|
%clr(%d{yyyy-MM-dd HH:mm:ss.SSS}){faint} %clr(%-5level) : ${PID:- } %clr(---){faint} %clr([%15.15t]){faint} %clr(%-40.40logger{39}){cyan} %clr(:){faint} %msg %n

|APPLOG_PATTERN|
[APP_LOG] %clr(%-13([${mode}])) %clr(%-5level) : %msg %n
```

#### ログ出力

コンソールとファイル出力を行う  
コンソール出力はDEFAULT_PATTERNによる出力を行う  
ファイル出力はAPPLOG_PATTERNによる出力を行う  
ファイルの出力パスはC:/home/pmmaster/logs以下に出力する  

|プロジェクト|ログファイル|
|--|--|
|pmmaster-api|pmmaster-api.app.log|

#### ローリング

ファイル出力するログはローリング設定を行う  
ローリングは時間設定により行い、日付でローリングする  
ローリングファイルは通常のログと同じディレクトリに「ファイル名.ログタイプ.%d{yyyy-MM-dd}.log」形式で出力する  
