# ti-component
题库的通用组件，提取为依赖库并统一发布在npm

## demo

```bash
npm install
npm run storybook
open http://localhost:3002/
```

## 使用指南

### 安装

```bash
npm install --save @zhike/ti-component
```

### 安装项目依赖，如已安装可跳过

*  基础框架 [React][1] :
```bash
npm install --save react
```
*  CSS-in-JS 框架 [aphrodite][2] :
```bash
npm install --save aphrodite
```
*  题库UI组件库 [ti-UI][3] :
```bash
npm install --save @zhike/ti-ui
```

### 在页面使用需要的组件

```javascript
import React from 'react'
import { Modal } form '@zhike/ti-component'

class MyComponent extends React.Component {
  componentDidMount() {
    Modal.show('ModalAlert', {
      title: 'Alert',
      buttons: [{ title: 'OK' }],
      width: 400,
      isUnhide: true,
      component: (
        <div>Hello World!</div>
      ),
    });
  }
}

export default MyComponent
```

## 开发指南

1. 修改`package.json`文件的版本号
2. 打包到`lib`文件夹并发布

```bash
npm run build
npm publish
```

## API

### Modal组件改造：
* type, props, onShow, onHide
* type为字符串，可选值Alert/Correct。根据传入的字符串匹配Modal内的实例对象，不需要在组件中引入实例并传入Modal
* 若type为Correct， 则props需要再传入一个option对象，用于上传纠错信息时添加自定义属性
* 新增加的onShow/onHide是为了降低耦合度，在抽离的组件中减少不合理的引用
* onShow(可选)，在isReport为false的时候执行，一般情况下，传入以下方法：
```javascript
() => {
  AudioPlayer.pause();
  Header.pauseTimerForModal();
}
```
* onHide(可选)，在isReport为false，且Modal全部关闭后执行，一般情况下，传入以下方法：
```javascript
() => {
  Header.startTimerForModal();
  AudioPlayer.resume();
}
```

[1]: https://github.com/facebook/react
[2]: https://github.com/Khan/aphrodite
[3]: https://github.com/zhike-team/ti-UI
