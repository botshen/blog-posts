## Mobx 基本使用

# 安装依赖
```bash
"mobx": "^6.5.0",
"mobx-react-lite": "^3.3.0",
```

# 初始化state
```JavaScript
import { computed, makeAutoObservable } from "mobx";

class CounterStore {
  count = 3;
  list = [1, 2, 3, 4, 5];

  constructor() {
    // 所有的变为响应式
    makeAutoObservable(this, {
      // 标记计算属性
      filterList: computed
    });
  }
  get filterList() {
    return this.list.filter(item => item > this.count);
  }
  // 定义action
  increment = () => {
    this.count++;
  }
  // 定义action
  decrement = () => {
    this.count--;
  }
  // 定义action
  addList = () => {
    this.list.push(999);
  }

}

// 导出实例
const counterStore = new CounterStore();
export { counterStore };

```

# 使用action以及computed
```JavaScript
import './App.css'
// 引用Store
import { counterStore } from './store'
// 用来包裹App组件连接
import { observer } from 'mobx-react-lite'

function App() {


  return (
    <div className="App">
      <header className="App-header">
        {counterStore.list.map(item => (<span key={item}>{item}</span>))}
        {counterStore.filterList.map(item => (<span key={item}>{item}</span>))}
        <p>
          // 通过counterStore.xxx来执行action等数据
          <button type="button" onClick={counterStore.increment}>
            加一
          </button>
          <button type="button" onClick={counterStore.decrement}>
            减一
          </button>
          <button type='button' onClick={counterStore.addList}>
            add
          </button>
          <p> count is: {counterStore.count}</p>
        </p>

        <p>
        </p>
      </header>
    </div>
  )
}

// 进行连接
export default observer(App)

```

# 模块化

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650173493978/xUFPWERL7.png)
拆分不同模块再统一到index.js,使用React的useContext机制导出useStore方法
index.ts中导出useStore在所有组件中使用

![image (1).png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650173521940/R2F6pm5NN.png)
使用useContext创建上下文
ts 临时解决的
```JavaScript
import listStore from "./List.store";
import counterStore from "./counter.Store.ts";
import React from "react";

class RootStore {
  listStore: typeof listStore;
  counterStore: typeof counterStore;
  constructor() {
    this.listStore = listStore;
    this.counterStore = counterStore;
  }

}

const rootStore = new RootStore();
const context = React.createContext(rootStore);

const useStore = () => React.useContext(context);

export { useStore };

```

List.store中导出实例
```JSON
import { computed, makeAutoObservable } from "mobx";

class ListStore {

  list = ['vue', 'react'];

  constructor() {
    makeAutoObservable(this);
  }


  addList = () => {
    this.list.push('angular');
  }


}
const listStore = new ListStore();
export default listStore;

```

全局使用
counterStore可以解构到某个store这一层
```Plain Text
import './App.css'

import { observer } from 'mobx-react-lite'
import { useStore } from './store/index'

function App() {
  const { counterStore } = useStore()
  return (
    <div className="App">
      <header className="App-header">
        {counterStore.count}
        <button onClick={counterStore.increment}>+1</button>
      </header>
    </div>
  )
}

export default observer(App)

```

