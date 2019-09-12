# top-progress
this is a very very very light weight web progressbar at the top of the document.

这是一个非常非常轻量的网页顶部进度条。

## Usage
### 在一般html中使用
1.  add ```<script src="tp.js"></script>``` at the end of ```<body></body>```

    add```<link rel="stylesheet" href="./src/tp.style.css">```

2. add
    ```html
    <script>
        const bar = new TP(options={

        });
    </script>
    ```
    options:
     - color：进度条的颜色，默认为'lightblue'
     - width：宽度，默认为'2px'
     - speed；好像有bug，懒得改了，建议别调（类型为字符串，单位s）

3. 提供start、done、add三个函数
    - void start()：进度条滚动，若不主动执行done，则会越来越慢
    - void done()：进度条滚动到底，并且初始化
    - int add(len)：无条件增加len%，最大值为100%

4. example
    ```html
    <script src="./src/tp.js"></script>
    <script>
        const bar = new TP({
            color: '#c471f5',
            width: '2px',
            speed: '1'
        });
        function start () {
            bar.start();
        }
        function add(x) {
            bar.add(x);
        }
        function done () {
            bar.done();
        }
    </script>
    ```
### 在Vue中使用
```html
<!-- src/main.js -->
import Vue from 'vue'
import App from './App.vue'
import router from './router'
<!-- 导入tp.js -->
import TP from './plugins/tp'
<!-- 导入css -->
import './plugins/tp.style.css'

Vue.config.productionTip = false

<!-- new TP的实例为tp -->
let tp = new TP({
  color: 'red',
  width: '2px',
  speed: '1'
})

new Vue({
  router,
  render: h => h(App)
}).$mount('#app')

router.beforeEach((to, from, next) => {
  tp.start();
  next();
});

router.afterEach(() => {
  tp.done()
})
```