# 快速入门

欢迎来到 React 文档！本章节将介绍你每天都会使用的 80% 的 React 概念。

> ## 你将会学习到
> * 如何创建和嵌套组件
> * 如何添加标签和样式
> * 如何显示数据
> * 如何渲染条件和列表
> * 如何对事件做出响应并更新界面
> * 如何在组件间共享数据


## 创建和嵌套组件

React 应用程序是由 **组件** 组成的。一个组件是 UI（用户界面）的一部分，它拥有自己的逻辑和外观。组件可以小到一个按钮，也可以大到整个页面。

React 组件是返回标签的 JavaScript 函数：

```javascript
function MyButton() {
  return (
    <button>我是一个按钮</button>
  );
}
```

至此，你已经声明了 `MyButton`，现在把它嵌套到另一个组件中：

```javascript
export default function MyApp() {
  return (
    <div>
      <h1>欢迎来到我的应用</h1>
      <MyButton />
    </div>
  );
}
```

你可能已经注意到 <MyButton /> 是以大写字母开头的。你可以据此识别 React 组件。React 组件必须以大写字母开头，而 HTML 标签则必须是小写字母。

来看下效果：

```javascript
function MyButton() {
  return (
    <button>
      我是一个按钮
    </button>
  );
}

export default function MyApp() {
  return (
    <div>
      <h1>欢迎来到我的应用</h1>
      <MyButton />
    </div>
  );
}

```

`export default` 关键字指定了文件中的主要组件。如果你对 JavaScript 某些语法不熟悉，可以参考 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/export) 和 [javascript.info](https://zh.javascript.info/import-export)。



## 组件间共享数据 
在前面的示例中，每个 `MyButton` 都有自己独立的 `count`，当每个按钮被点击时，只有被点击按钮的 `count` 才会发生改变：


此刻，当你点击任何一个按钮时，`MyApp` 中的 `count` 都将改变，同时会改变 `MyButton` 中的两个 `count`。具体代码如下：

首先，将 `MyButton` 的 `state` 上移到 `MyApp` 中：

```javascript
export default function MyApp() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <div>
      <h1>独立更新的计数器</h1>
      <MyButton />
      <MyButton />
    </div>
  );
}

function MyButton() {
  // ... 我们正在从这里移动代码...
}
```

使用这种方式传递的信息被称作 `prop`。此时 `MyApp` 组件包含了 `count state` 以及 `handleClick` 事件处理函数，并将它们作为 `prop` 传递给 了每个按钮。

最后，改变 `MyButton` 以 读取 从父组件传递来的 `prop`：

```javascript
function MyButton({ count, onClick }) {
  return (
    <button onClick={onClick}>
      点了 {count} 次
    </button>
  );
}
```
