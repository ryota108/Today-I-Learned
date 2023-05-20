## TypeScript についての学びの場

### 各タイプに関して

Children の型定義について
Children は ReactNode を用いる

```TypeScript
type Props {
 children:ReactNode
}
```

Props に型付けする方法

```typeScript
type Props = {
  flag:boolean
}

// ③ props に直接型注釈を指定するパターン
const SampleComponent3 = (props: Props) => {
  return (<div>{props.flag ? <h1>Ok</h1>: <h1>No</h1>}</div>)
}

// ④ React.VFC<P>のジェネリック型<P>として型を指定するパターン
const SampleComponent4: React.VFC<Props> = (props) => {
   return (<div>{props.flag ? <h1>Ok</h1>: <h1>No</h1>}</div>)
}


```
