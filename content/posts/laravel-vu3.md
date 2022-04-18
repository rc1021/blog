---
title: "Laravel + Vue3 環境安裝"
date: 2022-04-18T14:05:28+08:00
tags: ['laravel', 'vue3']
draft: false
showToc: true
TocOpen: true
hidemeta: false
comments: false
# description: "短描述"
# hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
---

雖然不是新聞了，但還是分享一下這簡單的步驟，拋磚引玉。
目前 Laravel8 | 9 還只支援 Vue 2，如果要整合 Vue 3 可參考這篇，只要 3 個步驟簡單又不出錯。
1. 首先建立 Laravel 專案，並利用 `laravel/ui` 初始化 vue2 環境
```
composer create-project laravel/laravel demo-app "8.6.11"
cd demo-app
composer require laravel/ui --dev 
php artisan ui vue
```
其中 `php artisan ui vue` 會建立 `vue` 相關目錄和變更一些檔案
```
demo-app
 |- resources
 |  |- js
 |  |   |- components
 |  |      |- ExampleComponent.vue
 |  |- app.js
 |- package.json    // 加入 vue, vue-loader, vue-template-compiler
 |- webpack.mix.js  // 加入 .vue()
```
2. 升級 vue3 版本
```
npm install -D vue@next 
npm install -D @vue/compiler-sfc
npm install vue-loader@^16.2.0 --save-dev --legacy-peer-deps
npm run dev
```
注意：執行 `npm run dev` 雖然不會發生錯誤，但前台載入 `app.js` 會發生錯誤，原因是 vue2 和 vue3 框架載入和應用方式的差異導致錯誤，請變更 `resources/js/app.js` 檔案。
3. 變更 resources/js/app.js 以符合 vue3 規格
```
// ...
// window.Vue = require('vue').default;
// 改為
window.Vue = require('vue');
```
```
// const app = new Vue({
//     el: '#app',
// });
// 改為
Vue.createApp({
    components: {
        'example-component': require('./components/ExampleComponent.vue').default
    }
}).mount('#app')
```
修改完成後執行 `npm run dev` 即可。

恭喜你又學會了一個技巧

---

## 聽說：劃線筆記

來源 吳軍。硅谷來信3。第37封信：憑一己之力能做多少事?

如果有一個適合自己的目標，而且真心願意做那件事情，堅持做下去，比起完全依賴外界資源來驅動自己做事，結果會大不相同。
