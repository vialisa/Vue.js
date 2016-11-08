# 模板语法
  > 基于 HTML 的模板语法，允许开发者声明的式的将DOM 绑定至底层 Vue 实例的数据。


  - # 插值
 
	+ v-once  指令 ： 一次性地插值，当数据改变时，插值处的内容不会更新

	+ 文本插值 :
		> 使用 Mustache 语法（双大括号）。

	 	```html
	 	<p>{{ msg }}</p>
	 	```

	+ 纯 HTML 插值 : v-html
		```html
	 	<p v-html="msg"></p>
	 	```

	+ 属性插值 ：v-bind
		``` html
		<div v-bind:id="dynamocId"></div>
		```

	+ 使用 JavaScript 表达式
		> 所有的数据绑定，Vue.js 都提供了完全的JavaScript的支持
		
		* 每个绑定都只能含有单个表达式

	+ 过滤器
		> 允许自定义过滤器 ，应添加在 mustache 插值的尾部，由管道符指示

		```html
		{{ message | capitalize }}
		```
		
		* 过滤器函数总接受第一个表达式的值作为第一个参数
		* 过滤器可以串联
		* 过滤器是 JavaScript 函数

 - # 指令 Directives
	> 指令属性的值预期是单一 JavaScript表达式,当其表达式的值改变时，相应的将某些行为应用到DOM上。
    
	
 
	+ 参数
	    > 一些指令能接受一个参数，在指令后以冒号指明。

	      * v-bind 指令用来更新 HTML 属性
	      
		```html
		<a v-bind:href="url">alisa</a>
		```
		
	      * v-on  用于监听 DOM 事件
	      
		```html
		<a href="" v-on:click="doSomething">alisa</a>
		```

	 + 修饰符  Modifiers
		> 半角句号 . 指明的特殊后缀,指出一个指定应该以特殊方式绑定。
		
	 + 缩写
	    * v-bind 为 :
	    * v-on   为 @

