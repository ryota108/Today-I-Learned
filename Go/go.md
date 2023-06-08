# Go に関して学んだ内容を書く場所

### hello world するには

```go
 package  main
 import "fmt" // printするために必要

 func main () {
  fmt.PrintIn("Hello world")
 }

 // main関数はデフォルトで呼ばれる
```

### print 関数の区別

`Print()` <br>

- フォーマット指定なしで、引数の値を標準出力に出力します。
- 引数をスペースで区切って連続して表示します。
- 改行は行われず、出力の最後にカーソルが残ります。

`Println()`

- 引数の値を標準出力に出力します。
- 引数をスペースで区切って連続して表示します。
- 改行が自動的に行われ、出力の最後にカーソルが移動します。
  <br>

`Printf()`

- フォーマット指定子を使用して、引数の値を指定された書式で標準出力に出力します。
- 書式指定子 % を使用して、変数を埋め込むことができます。
- 引数を指定された書式に従って整形し、スペースで区切って連続して表示します。
- 改行は行われず、出力の最後にカーソルが残ります。

### 配列とスライスの違い

Go言語において、スライス（slice）と配列（array）はデータのコレクションを表現するための異なるデータ構造です。以下にそれぞれの特徴と違いを説明します。

**配列（Array）**:
- 配列は要素の固定長の連続した領域を表現します。
- 宣言時に要素の型と長さを指定する必要があります。例えば、`var arr [5]int`という宣言は、整数型の要素を5つ持つ配列を宣言しています。
- 配列の要素は0から始まるインデックスを使ってアクセスします。例えば、`arr[0]`は配列の最初の要素を表します。
- 配列の長さは宣言時に指定された固定値です。そのため、後から要素数を変更することはできません。

```go
package main

import "fmt"

func main() {
	// 宣言方法1: 要素数を指定して宣言
	var arr1 [5]int
	arr1[0] = 1
	arr1[1] = 2
	arr1[2] = 3
	arr1[3] = 4
	arr1[4] = 5

	// 宣言方法2: 初期値を指定して宣言
	arr2 := [3]string{"apple", "banana", "orange"}

	// 宣言方法3: 要素数を自動推論
	arr3 := [...]int{1, 2, 3, 4, 5}

	// 要素の追加方法: インデックスを指定して代入
	arr1[3] = 10

	// 配列の要素を表示
	fmt.Println(arr1) // Output: [1 2 3 10 5]
	fmt.Println(arr2) // Output: [apple banana orange]
	fmt.Println(arr3) // Output: [1 2 3 4 5]
}
```

**スライス（Slice）**:
- スライスは、可変長の要素の可変領域を表現します。
- スライスは動的な配列と見なすことができ、配列よりも柔軟なデータ構造です。
- スライスは配列や他のスライスの一部分を参照することもできます。この場合、元の配列やスライスの一部を指すポインタと長さ情報を持ちます。
- 宣言時に長さを指定せず、`[]`内に要素の型を指定して宣言します。例えば、`var slice []int`という宣言は、整数型の要素を持つスライスを宣言しています。
- スライスの長さは実行時に動的に変更できます。`append`関数を使用して要素を追加することができます。

```go
package main

import "fmt"

func main() {
	// 宣言方法1: make関数を使用して宣言
	slice1 := make([]int, 0)

	// 宣言方法2: リテラル表記で宣言
	slice2 := []string{"apple", "banana", "orange"}

	// 宣言方法3: nilスライスを宣言
	var slice3 []float64

	// 要素の追加方法: append関数を使用
	slice1 = append(slice1, 1)
	slice1 = append(slice1, 2, 3, 4, 5)

	// スライスの要素を表示
	fmt.Println(slice1) // Output: [1 2 3 4 5]
	fmt.Println(slice2) // Output: [apple banana orange]
	fmt.Println(slice3) // Output: []
}
```


スライスは配列のような固定長の連続領域を保持しているわけではなく、内部的にはデータへのポインタ、長さ、容量の情報を持っています。そのため、スライスは柔軟性と効率性の両方を提供し、Go言語で頻繁に使用されるデータ構造です。配列は要素数が固定されている場合に使用され、サイズが静的であることがわかっている場合に適しています。


### struct と Map の違い

`struct（構造体)`:
struct は、関連する異なるデータ型のフィールド（属性）をグループ化するために使用されます。それぞれのフィールドは名前と型を持ち、異なるデータ要素を含むことができます。struct は、データのまとまりを表現するために使用され、異なるフィールドを 1 つのオブジェクトとして扱うことができます。

例えば、Person（人物）という struct があり、そのフィールドには name（名前）や age（年齢）などが含まれる場合、Person オブジェクトはそれらのフィールドの値を持つことができます。

```go
package main

import "fmt"

// Person struct（構造体）
type Person struct {
	Name string
	Age  int
}

func main() {
	// Personオブジェクトの作成
	p := Person{Name: "Alice", Age: 25}

	// フィールドへのアクセスと表示
	fmt.Println("Name:", p.Name)
	fmt.Println("Age:", p.Age)
}
```

`map（マップ）`:
map は、キーと値のペアを関連付けるために使用されるデータ構造です。キーは一意であり、値を取得するためのインデックスとして機能します。map は連想配列やハッシュマップとも呼ばれ、データを高速に検索するために使用されます。キーと値のペアは追加、削除、更新することができ、キーに基づいて値を検索することができます。

例えば、studentGrades（生徒の成績）という map があり、キーには生徒の名前を、値には成績を関連付けることができます。これにより、生徒の名前を使用して成績を取得したり更新したりすることができます。

```go
package main

import "fmt"

func main() {
	// mapの作成と初期化
	studentGrades := map[string]int{
		"Alice":  85,
		"Bob":    92,
		"Charlie": 78,
	}

	// mapへの要素の追加
	studentGrades["Dave"] = 79

	// mapの要素の取得
	aliceGrade := studentGrades["Alice"]
	fmt.Println("Alice's grade:", aliceGrade)

	// mapの要素の更新
	studentGrades["Bob"] = 95

	// mapの要素の削除
	delete(studentGrades, "Charlie")

	// mapの要素数の取得
	fmt.Println("Number of students:", len(studentGrades))

	// mapのイテレーション
	for name, grade := range studentGrades {
		fmt.Println(name, ":", grade)
	}
}
```

`structとmapの比較`:

- struct は異なるデータ型のフィールドをグループ化するために使用され、固定されたフィールドのセットを持ちます。一方、map はキーと値のペアを関連付けるために使用され、動的にキーと値のペアを追加、削除、更新することができます。

- struct はフィールドに名前と型があり、struct のインスタンスはフィールドごとに個別にアクセスすることができます。一方、map はキーを使用して値を取得しますが、特定のキーに基づいてアクセスするためにはイテレーションが必要です。

- struct は一連の関連するデータを表現するために使用され、個々のフィールドに対して型の安全性を提供します。一方、map はキーと値のペアを格納し、キーを使用して値を照会することができますが、フィールドの型安全性は提供しません。

### API の作り方

```go
package main

import (
	//JSONのエンコードとデコードをサポート
	"encoding/json"
	//ログ出力を提供
	"log"
	//HTTP関連の機能
	"net/http"
)

type Response struct {
	//JSONのキーとして message を使用することを示す。
	Message string `json:"message"`
}

func main() {
	// routing設定
	http.HandleFunc("/api", handleAPIRequest)
　　// serverの起動
   //エラー発生=>log.Fatal を使用してエラーメッセージを表示
	log.Fatal(http.ListenAndServe(":8080", nil))
}
  //http.ResponseWriter は HTTP レスポンスを書き込むためのインターフェース
  //http.Request は受信したリクエストに関する情報を保持
func handleAPIRequest(w http.ResponseWriter, r *http.Request) {
	response := Response{Message: "Hello, World!"}
	json.NewEncoder(w).Encode(response)
}

```
### Goのフレームワークの違い

1. ``Gin``: Ginは非常に軽量で高速なWebフレームワークです。シンプルなルーティングやミドルウェアのサポート、JSONのシリアル化とデシリアル化、HTTPリクエストのバインディングなどの機能を提供しています。Ginはシンプルなデザインと高速なパフォーマンスを重視しており、API開発やマイクロサービス向けに人気です。

2. ``Echo``: Echoは高速なパフォーマンスとシンプルなAPI設計に焦点を当てたWebフレームワークです。ルーティング、ミドルウェア、コンテキストの管理、バリデーションなどの機能を提供しています。Echoは柔軟な構造と優れたパフォーマンスを持ち、RESTful APIやWebアプリケーションの開発に適しています。

3. ``Fiber``: FiberはGinの影響を受けたWebフレームワークで、高速なルーティングとハンドラ処理を特徴としています。Goroutineの効率的な利用、低メモリ使用量、ルーティンググループ、ミドルウェア、バリデーションなどの機能を提供しています。Fiberは高速なWebアプリケーションの構築に適しており、Goのコンテキストと非同期処理を活用しています。

4. ``Revel``: Revelは全体的なフルスタックWebフレームワークで、高生産性と堅牢性を重視しています。MVCアーキテクチャのサポート、ルーティング、テンプレートエンジン、データバリデーション、セッション管理などの機能を提供しています。Revelは初心者にも親しみやすいフレームワークであり、大規模なWebアプリケーションの開発に適しています。


### Ginを用いてダミーAPI開発する方法


```go
package main

import (
	"net/http"
    //ginをインポート　
	"github.com/gin-gonic/gin"
)

type Response struct {
	ID    string `json:"id"`
	Title string `json:"title"`
}

func main() {
	r := gin.Default()
	//動的に変化するパス、この場合IDの前には:を打つ
	r.GET("/restaurants/:id", restaurantHandle)
	r.Run(":8080")
}

func restaurantHandle(c *gin.Context) {
	//実際はダミーデータではなくSQLから取得する
	m := map[string]string{
		"original1": "東京ラーメン",
		"original2": "モンスターズバスターキッチン",
	}
	//下記コードid以下を取得　例/restaurants/aaa => aaa
	id := c.Param("id")
	response := Response{ID: id, Title: m[id]}
	c.JSON(http.StatusOK, response)
}

```
### 注意点
* go get "github.com/gin-gonic/gin"しないとエラーがでる
* 動的に取得したいParamの前にはコロンをつける

