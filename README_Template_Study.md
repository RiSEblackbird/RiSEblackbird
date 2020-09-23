# 

(This repository is my own self-study document
)

## リポジトリの目的

- ````の基礎学習
  - とりあえず組んで動かす
- 学習記録/自分用資料まとめ

## 主なリファレンス

- メインチュートリアル
  - **[]()**
  - **[]()**

### **Flask**について

- GitHub : https://github.com/pallets/flask
- Official : https://flask.palletsprojects.com/en/1.1.x/

- Goコマンド
  - 原文 : https://golang.org/cmd/go/
  - 日訳 : https://godoc.org/github.com/gophersjp/go/src/cmd/go

- 文法 (The Go Programming Language Specification)
  - 原文 : https://golang.org/ref/spec

### **Python**について

- GitHub : https://github.com/python
- Official : https://www.python.org/
- Documentation :
  - General : https://www.python.org/doc/
  - Language : https://docs.python.org/ja/3/reference/index.html

## 工程(参考先より適宜変更)

### パッケージ管理

- [GOMODULE--Goのパッケージ管理 - Qiita](https://qiita.com/Syoitu/items/f221b52231703cebe8ff)
- ``$ go mod init _Gin_API_Sample``

### パッケージ導入

- ``$ go get -u github.com/gin-gonic/gin``
- ``$ go get github.com/go-sql-driver/mysql``
  - **go-sql-driver/mysql** : https://github.com/go-sql-driver/mysql
- ``$ go get xorm.io/xorm``
  - **xorm / xorm** : https://gitea.com/xorm/xorm
  - [旧] go-xorm/xorm : https://github.com/go-xorm/xorm
    - Go向けのORMツール
- ``$ go get go.uber.org/zap``
  - **uber-go/zap** : https://github.com/uber-go/zap
    - 高速で動作するロギングツール

### APIの作成

- ``main.go``
  - import
    - ``"_Gin_API_Sample/controller"``, ``"_Gin_API_Sample/middleware"``, ``"github.com/gin-gonic/gin"``
  - デフォルトのミドルウェアでginルーターを作成する

## Tips

### import文について

- Import declarations : https://golang.org/ref/spec#Import_declarations
  - "_"(unserscore)
    - パッケージの副作用 (初期化) のみを目的としてインポートする場合に空白識別子を前方に付して記述する

      ~~~go
      import _ "lib/math"
      ~~~

### ポインタ関連

- [Pointers - A Tour of Go](https://go-tour-jp.appspot.com/moretypes/1)
- [Go's Declaration Syntax - The Go Blog](https://blog.golang.org/declaration-syntax)
- [Goで学ぶポインタとアドレス - Qiita](https://qiita.com/Sekky0905/items/447efa04a95e3fec217f)

## 階層

~~~txt
_Gin_API_Sample
├── controller
│   └── book.go
├── middleware
│   └── bookMiddleware.go
├── .gitignore               // standard gitignore file
├── go.mod
├── go.sum
├── main.go
└── README.md                // simple readme file

### ├── │ └──
~~~

## Error

### DbEngineのメソッド名誤り (CLEAR!)

~~~error
$ go run main.go
# _Gin_API_Sample/service
service/book.go:27:20: DbEngine.Id undefined (type *xorm.Engine has no field or method Id, but does have ID)
service/book.go:36:20: DbEngine.Id undefined (type *xorm.Engine has no field or method Id, but does have ID)
~~~

- 要因&対処
  - https://gitea.com/xorm/xorm#notice
    - v1.0.0にて関数名が``Sql`` -> ``SQL``, ``Id`` -> ``ID``と変更された
