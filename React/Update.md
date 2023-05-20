## React の最新情報のキャッチアップの場

### React18 はそもそも破壊的変更のため確実にキャッチアップする必要がある。

**Root に関して**

index.js において、ReactDOM の表示方法が違う
createRoot を用いて使用している

```javascript
//　React18 createRootにすると18の機能が使えるようになる
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);

//React17
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementByID("root")
);
```

**Automatic batching** <br/><br/>
**バッチングとは？**

> バッチングとは React がパフォーマンスのために複数のステート更新をグループ化して、単一の再レンダーにまとめることを指します。

つまり、set 関数などをハンドル内で呼んだとしてもその都度レンダリング走るのではなく、ある程度自動的にまとめてくれること<br/>

**例**

```javascript
const [state1, setState1] = useState(false);
const [state2, setState2] = useState("");
const [state3, setState3] = useState(0);
-----------------中略--------------------
const onClickHandler = () => {
  //set関数が３回も呼ばれているがその都度レンダリングが走るわけではなく、まとめて一回のみ走るようにしてくれる（バッチング）
  setState1(true);
  setState2("OK");
  setState3(1000);
};
```

上記の機能自体は前の React17 でもあったが、今回の変更点は**イベントハンドラ以外**にもバッチ処理がされるようになることである。

### 以前はイベントハンドラ以外はバッチ処理されていなかった

> 自動バッチング以前は、React のイベントハンドラ内での更新のみバッチ処理されていました。promise や setTimeout、ネイティブのイベントハンドラやその他あらゆるイベント内で起きる更新はデフォルトではバッチ処理されていませんでした。

### どういうメリットがあるの？

そのため、以前は何回も処理が走ってしまっていたりかなり効率の悪いコードになっていた可能性があるが今回の改訂のおかげでパフォーマンスが向上された。

_ちなみに、このアップデートに関しては特にこちら側が設定することなく勝手に最適化してくれるが一応知っておいた方がいい_

## Transition について

今回のアップデートで大きく変わった内容にもなるので注視する必要があるのがこの Transition である。

#### どういう内容？

> トランジション（transition; 段階的推移）とは React における新たな概念であり、緊急性の高い更新 (urgent update) と高くない更新 (non-urgent update) を区別するためのものです。

新しく生まれた概念、機能であり UX の向上に役立つ機能である。

**端的にいうとどういうこと？**
今まで均一的な更新だったのが、**優先順位**をつけて更新できるようになった！
