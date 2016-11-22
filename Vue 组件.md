# 组件
  > 可扩展 HTML 元素，封装可重用的代码。

- # 使用组件

  + 全局注册
    > 初始化根实例之前注册组件

    ```Javascript
    Vue.component('my-component', {
	    // 选项
    });
    ```

  + 局部注册

  + DOM 模板解析说明
    * 特殊的 is 属性

  + 组件中，data 必须是函数 

   ```html
   <div id="demo">
       <simple-counter></simple-counter>
       <simple-counter></simple-counter>
       <simple-counter></simple-counter>
   </div>
   ```
   
   ```Javascript
   var data = {counter: 0 }
   
   Vue.component('simple-counter',{
       template:'<button v-on:click="counter += 1">{{counter}}</button>',

       data: function() {
           return {
               counter: 0 
           }
       }
   });

   var vm= new Vue({
       el:"#demo"
   });
   ```

    + 构成组件
	  * props down
	  * events up
	
- # Props

