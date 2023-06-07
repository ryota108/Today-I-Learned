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

