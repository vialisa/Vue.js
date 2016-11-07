# Vue.js 简介

- ## 兼容性
	> Vue.js 不支持 IE8 及其以下版本, Vue.js 支持所有兼容ECMAScript 5 的浏览器。

- ## 目标
	> 通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件 

- ## 声明式渲染
	> 核心是允许采用简洁的模板语法来声明式的将数据渲染进DOM的系统

	+ 绑定插入的文本内容

		```html
		<div id="demo">{{ message }}</div>
		```
		```javascript
		var vm = new Vue ({
			el:"#demo",
			data: {
		  	 message:"alisa"
			}
		});
		```

	+ 绑定 DOM 元素属性
		```html
		<div id="demo">
	    	<span v-bind:title= "message">vivi alisa</span>
		</div>
		```
		```javascript
		var vm = new Vue ({
			el:"#demo",
			data: {
		   		message:"lee"
			}
		});
		```

- ## 条件与循环
	+ v-if : 控制一个元素的显示
		```html
		<div id="demo">
		<p v-if="seen">false or true</p>
		</div>
		```
		```javascript
		var vm = new Vue ({
	        el:"#demo",
		    data: {
		       seen:true
		    }
		});

	+ v-for 绑定数据到数据来渲染一个列表
		```html
		<div id="demo">
		<ol>
		<li v-for="item in items">{{ item.message }}</li>
		</ol>
		```

		```javascript
		var vm =  new Vue({
		     el:"#demo",
		     data: {
                items: [
                    { message: "item" }
                    { message: "items" }
                    { message: "item.message" }
                ]
             }
		});
		```
		*vm.items.push(message:"new item") 列表新增一项*
- ## 处理用户输入
	+ v-on 可以绑定一个监听事件，用于调用 Vue 实例中定义的方法。
		```html
		<div id="demo">
            <p>{{ msg }}</p>
 	        <button v-on:click="reversedMsg"></button>
		</div>
		```

		```javascript
		var vm = new Vue({
		    el:"#demo",
		    data: {
		        msg:"vialisa"
		    },
		    methods: {
		        reversedMsg: function() {
                    this.msg = this.msg.split('').reverse().join('');	       
                }
            }
		});
		```

	+ v-model 可在表单输入和应用状态中做双向数据绑定
		```html
		<div id="demo">
		    <p>{{ msg }}</p>
		    <input type="text" v-model= "msg">
		</div>
		```
		```javaScript
		var vm = new Vue({
		    el:"#demo",
			data: {
			    msg:"alisa"
			}
		});


- ## 构造器
	> 每个 Vue.js 都是通过构造函数 Vue 创建一个Vue 根的实例启动的
  ```javascript
  var vm = new Vue({
	  //选项对象
  })
  ```
	+ 选项对象可包含数据、模板、挂载元素、方法、生命周期钩子等选项
	+ 所有的Vue.js 组件其实都是被扩展的 Vue 实例。	

- ## 属性与方法
	+ 每个Vue 实例都会代理其 data 对象性里所有的属性
		```javascript
		var data = { a: 1 }
		var vm = new Vue ({
	    	data:data
		})

		vm.a === data.a
		```
	+ $watch 一个实例方法
		```javascript
		$watch('a',function(newVal,oldVal){
			//回调将在 vm.a 改变后调用
		})
		```
- ## 实例生命周期
	+ 钩子的 this 只用调用它的 Vue 实例