# 计算属性 Computed

	> 模板中放入太多的逻辑会让模板过重且难以维护，所以复杂逻辑应当使用计算属性。

- ## 基础例子
	```html
		<div id="demo">
			<input type="text" v-model="message">
			<p>{{ reversedMessage }}</p>
		</div>
	```
	```javaScript
	    var vm = new Vue ({
		    el:"#demo",
		    data: {
		        message:"vialisa"
		    },
		    computed: {
		        // 声明一个计算属性 reversedMessage
		        reversedMessage: function() {
	                   return this.message.split('').reverse().join('');
		        }
	        }
	    });
	```

- ## 计算属性 VS methods
	+ 用 methods 达到同样的效果
	```html
	<p>{{ reversedMessage() }}</p>
	```
	```javascript
	methods: {
        reversedMessage: function() {
            return this.message.split('').reverse().join('');
		} 
	}
	```
	+ 计算属性只有它的相关依赖发生改变时才会重新取值。
	+ methods 调用每当重新渲染的时候总会执行函数。
	+ 计算属性默认只有getter 也可以设置一个setter 

- ## 计算属性 VS $watch
	+ $watch  当一些数据需要根据其他数据变化时使用
		```html
		<p>{{ fullName }}</p>
		<input type="text" v-model="firstName">
		<input type="text" v-model="lastName">
		```
		```javascript
		var vm = new Vue ({
             el:"#demo",
             data:{
                 firstName:"vi",
                 lastName:"alisa",
                 fullName:"vi alisa"
             },
             watch: {
                 firstName: function(val) {
                     this.fullName= val + ' ' + this.lastName;
                 },
                 lastName: function(val) {
                     this.fullName = this.firstName + ' ' + val;
                }
             }                
        });
		```
	+ 以上js代码  可用下面 computed 代替
		```javascript
		var vm = new Vue ({
             el:"#demo",
             data:{
                 firstName:"vi",
                 lastName:"alisa",
             },
             computed: {
				 fullName: function(){
                     return this.firstname + ' ' + this.lastName;
				 }
             }                
        });
		```	
	+ 也可以用 $watch 代替
		```javascript
		var vm = new Vue ({
			el:"#demo",
			data: {
				firstName:"vi",
				lastName:"alisa",
                fullName:"vi alisa"
			}
		}),
        vm.$watch('firstName',function(newVal, oldVal){
			vm.fullName = newVal + ' ' + vm.lastName; 
		}),
		vm.$watch('lastName',function(newVal, oldVal){
			vm.fullName = vm.lastName + ' ' + newVal; 
		}),
		```
- ## 观察watchers
	+ 在数据变化响应时，执行异步操作或昂贵操作时，这是很有用的。
	+ 深入理解
	  * $watch 可以和 computed 共存 
	  * $watch 可以访问 computed 内定义的属性
	  

           



  