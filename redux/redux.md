## Redux

### 在講Redux之前, 要先提到`Flux`

## Flux

- Flux 是 Facebook 為了搭配 React 而提出的一套 Dataflow 設計模式，用來解決前端狀態資料的管理，社群有相當多基於此概念的實作品
- 採用單向資料流 ( One-way Dataflow) 的概念
- Facebook 官方最早有推出一套同名的 Flux 實作品，不過現在已逐漸被 Redux 取代其地位


#### 如果不使用 Flux...

- Component 之間沒有共用的狀態資料儲存地
- 你的 React Component 所有的狀態都儲存在各自的 this.state 當中，這導致不同 Component 之間想互相通知 State 的改變的話，需要層層的傳遞 callback，前端狀態管理異常複雜

#### 回到Redux

- Redux 是 JavaScript 的狀態容器，提供可預測化的狀態管理
- 由 Flux 演變而來，但避開了 Flux 的複雜性，非常單純易用
- 由 React 社群大神 Dan Abramov 所發明，日前他被 Facebook 招募，Redux 也納入 Facebook 官方項目，成為前端狀態管理的主流解決方案
- 跟 React 沒有相依關係，可以單獨使用或搭配其他前端框架使用
- [Redux DevTools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=zh-TW)

#### Redux 三大原則

- 單一資料來源 :
```
整個前端應用的 State 都被儲存在一顆 Object Tree 當中，成為唯一的 Store
在 React 中，所有  Component 都共用這個 Store
```
- State 是唯讀的 :
```
唯一改變 State 的方法就是呼叫 Action，Action 負責定義發生的事件的種類
```
- 使用純函數來執行 State 的修改 :
```
為了描述這個 Action 實際上要如何改變 State Tree，我們需要定義 Reducer
```

Redux 的 One-way Dataflow
![data_flow](https://github.com/zzpengg/hellojs-gitbook/blob/master/redux/img/data_flow.png?raw=true)

### Action

##### Action 負責定義應用程式發生的事件種類與資料傳遞形式，是純 JS 物件

```
const ADD_TODO = 'ADD_TODO';

{
  type: ADD_TODO,
  text: 'Build my first Redux app'
}
```

### Action Creator

##### Action Creator 就是產生 Action 物件的函數

```
function addTodo(text) {
  return { type: ADD_TODO, text}
}
```

### Reducer

- Action 只是描述了有事情發生，並沒有指明要如何更新 State，而 Reducer 正是要負責做這件事
- Reducer 是一個純函數，接收完整的舊的 State 和當前 Action，回傳完整的新的 State
- 你不應該直接修改傳入的舊 State，而是應該回傳一個更新狀態的新 State
- Reducer function 的名稱，就會是 State 中此子物件的 key 名稱


```
export function todos(state = [], action) {
  switch (action.type) {
    case ADD_TODO:
      return [
        ...state,
        {
          text: action.text,
          completed: false
        }
      ];
    case TOGGLE_TODO:
      return [
        ...state.slice(0, action.index),
        Object.assign({}, state[action.index], {
          completed: !state[action.index].completed
        }),
        ...state.slice(action.index+1, state.length)
      ];
    default:
      return state;
  }
}
```

### combineReducers

##### 用來建立 Store 的 Reducer 只能有一個，因此如果你因為程式碼可維護性而分開寫了很多個 Reducer 的話，可以使用 combindReducer 方法將其合併成一個大 Reducer


```
import { combineReducers } from 'redux';
import { todos } from 'reducers/TodoReducers';

const AppReducers = combineReducers({
  todos,
  reducer2,
  reducer3,
})

export default AppReducers;
```

### Store

##### 儲存與維持 State 資料
- createStore 方法：傳入主要的 Reducer 以建立 Store


```
import { createStore } from 'redux'
import AppReducers from 'reducers/AppReducers'

let store = createStore(AppReducers);
```

##### 提供 dispatch 方法，來發起一個 Action 以更新 State

```
import { addTodo, toggleTodo} from 'action/TodoActions';
dispatch(addTodo('i am a todo item'));
dispatch(toggleTodo(0));
```
