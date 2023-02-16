# Vue3 + Vite

## 第三方的组件使用

1、安装

```
npm install element-plus --save
```

2、导入到项目中去使用

```js
import { createApp } from "vue";
import ElementPlus from "element-plus";
import "element-plus/dist/index.css";
import App from "./App.vue";
const app = createApp(App);
app.use(ElementPlus);
app.mount("#app");
```
