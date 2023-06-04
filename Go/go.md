# Go に関して学んだ内容を書く場所


### hello worldするには
```go:
 package  main
 import "fmt" // printするために必要

 func main () {
  fmt.PrintIn("Hello world")
 }

 // main関数はデフォルトで呼ばれる
```

### print関数のあれこれ

``Print()`` <br>
* フォーマット指定なしで、引数の値を標準出力に出力します。
* 引数をスペースで区切って連続して表示します。
* 改行は行われず、出力の最後にカーソルが残ります。

``Println()``
* 引数の値を標準出力に出力します。
* 引数をスペースで区切って連続して表示します。
* 改行が自動的に行われ、出力の最後にカーソルが移動します。
<br>

``Printf()``
* フォーマット指定子を使用して、引数の値を指定された書式で標準出力に出力します。
* 書式指定子 % を使用して、変数を埋め込むことができます。
* 引数を指定された書式に従って整形し、スペースで区切って連続して表示します。
* 改行は行われず、出力の最後にカーソルが残ります。