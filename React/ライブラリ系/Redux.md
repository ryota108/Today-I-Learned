## Redux の備忘録、学びのアウトプットの場

**基本的な書き方**

> 初期設定編

1. store を作る

```javascript
import { createStore } from "redux";

const store = createStore();

export default store;
```

Redux のストアは一つしか存在しない

2. Reducer を作る

```javascript
const initialState = {
  auth: false,
};

const reducer = (state = initialState) => {
  return state;
};
```

3. Provider の設定

```javascript
import store from "./store/index";
import { Provider } from "react-redux";

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);
```
