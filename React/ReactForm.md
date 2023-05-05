## React に関してのアウトプットの場

> 今日は React Hook Form について学んだ

React Hook Form を使えば useState や useRef など煩雑なステート管理を用いずに作成できる。

### 導入メリット
* state管理などのコードの記述量を減らすことが出来る
* パッケージが軽量
* Unontrolled Componentsのパターンを採用しており、レンダリング回数を減らすことが出来る



```javascript
mport { useForm } from 'react-hook-form';

function App() {
  const { register, handleSubmit } = useForm();

  const onSubmit = (data) => console.log(data);

  return (
    <div className="App">
      <h1>ログイン</h1>
      <form onSubmit={handleSubmit(onSubmit)}>
        <div>
          <label htmlFor="email">Email</label>
          <input id="email" {...register('email')} />
        </div>
        <div>
          <label htmlFor="password">Password</label>
          <input id="password" {...register('password')} type="password" />
        </div>
        <button type="submit">ログイン</button>
      </form>
    </div>
  );
}

export default App;

```

```javascript
// registerで登録する
<input id="password" {...register("password")} type="password" />
```

```javascript
// validationはターゲットの横に書く
<input
  id="password"
  {...register("password", { required: true })}
  type="password"
/>
```



ZodとYupっていうValidationライブラリ導入することがスタンダードらしい

参考資料

- [REFFECT　React Hook form](https://reffect.co.jp/react/react-hook-form)
- [REFFECT　Zod](https://reffect.co.jp/react/zod-validation)
