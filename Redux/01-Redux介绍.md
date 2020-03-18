Redux是JavaScript应用的状态容器，以期状态可预测。  
它能帮助你的应用有更好的一致性，可以在不同的环境（客户端，服务器，本地化）中运行，也更容易测试。同时，它也提供了很好的编程体验，比如在线编辑测试。  
你可以与React一起使用Redux，或者其它图形框架。
## 安装
Redux可作为一个捆绑模组包来通过NPM进行安装：
```
# NPM
npm install redux

# Yarn
yarn add redux
```
它也能过通过预编译的UMD包来获取，UMD包可以在`<script>`标签中直接使用。通过`window.Redux`全局对象来使用Redux。
## 安装补充包
通常你也需要**绑定React**和**开发者工具**。
```
npm install react-redux
npm install --save-dev redux-devtools
```
之后介绍基础教程。
