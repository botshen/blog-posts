## 测试 React 应用

## 使用 create-react-app 

除了 Jest 之外，我们还需要另一个测试库，它将帮助我们以测试目的渲染组件。 

目前最好的选择是[react-testing-library](https://github.com/testing-library/react-testing-library) ，这个库在最近几年迅速流行起来。

```bash
npm install --save-dev @testing-library/react @testing-library/jest-dom
```

## 依赖项

```json
  "dependencies": {
    "@testing-library/jest-dom": "^5.14.1",
    "@testing-library/react": "^11.2.7",
    "@testing-library/user-event": "^12.8.3",
    "react": "^17.0.2",
    "react-dom": "^17.0.2",
    "react-scripts": "4.0.3",
    "web-vitals": "^1.1.2"
  }
```

## 测试命令

使用`"test": "react-scripts test --detectOpenHandles=true"`进行测试

有一些选项可以进行操作：

```shell
Watch Usage
 › Press a to run all tests.
 › Press f to run only failed tests.
 › Press q to quit watch mode.
 › Press p to filter by a filename regex pattern.
 › Press t to filter by a test name regex pattern.
 › Press Enter to trigger a test run.
```

## 测试文件名约定

要么已test结尾，要么已spec结尾：`App.test.js/App.spec.js`

## 目录约定

我们习惯将测试文件放在和开发文件放在一起，例如：

```shell
├── App.js
├── index.css
├── index.js
├── pages
│   ├── SignUpPage.js      // 页面文件
│   └── SignUpPage.spec.js // 测试文件
├── reportWebVitals.js
└── setupTests.js
```

## 第一个测试例子

我们采用 TDD 测试驱动开发来进行开发，所以我们应该先写测试再来写页面

让我们先看一个最简答的例子：

```js
//SignUpPage.spec.js
import SignUpPage from './SignUpPage';
import { render, screen } from '@testing-library/react';

it('has header', () => {
  render(<SignUpPage />);
  const header = screen.queryByRole('heading', { name: 'Sign Up' });
  expect(header).toBeInTheDocument();
});

```

这个例子中，我们首先引用了组件，使用`@testing-library/react`库来进行渲染组件和查找引用

it函数接收两个参数，第一个是测试的描述，第二个是测试的具体实现

首先render(<SignUpPage />);来渲染一个组件，然后使用screen.queryByRole()函数获取引用

这里的heading就是标题对应的HTML元素是标签，这里最开始还不太理解，后面查了官方文档才知道


```js
getByRole('heading', {level: 1})
// <h1>Heading Level One</h1>

getAllByRole('heading', {level: 2})
// [
//   <h2>First Heading Level Two</h2>,
//   <div role="heading" aria-level="2">Second Heading Level Two</div>
// ]
```

通过上面的2个例子知道了对关系，下面的写法是不推荐的，相当于强行顶一个等级为2的heading元素。

最后就是`expect(header).toBeInTheDocument();`这个方法了，他就是jest库为我们提供的断言方法，来判断header的引用是否出现在文档中。

这就是单元测试最简答的例子，通过testing-library 库来对组件进行渲染和获取引用等操作，使用 jest 来提供断言才测试是否通过测试用例。

