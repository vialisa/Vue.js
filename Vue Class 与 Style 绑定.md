# Class 与 Style 绑定
	
> 用v-bind 做处理， 表达式的结果类型可以是字符串，对象或数组。

- # 绑定 HTML Class
	+ 对象语法
	  * 可以传给 v-bind:class 一个对象，对象里可以有多个属性。
		*当属性名里含有短杠  - ，属性名要加引号。*
		```HTML
		<div v-bind:class = "{ active:isA, 'txt-t':isT }">alisa</div>
		```
		```JavaScript
		data:{
			isA:true,
			isT:false
		}
		```
	  * 可以直接绑定数据里的一个对象
		```HTML
		<div v-bind:class =" objectClass ">alisa</div>
		```
		```JavaScript
		data: {
			objectClass: {
				active: true,
				'txt-t': false
			}
		}
		```

	  * 可以与普通 Class 属性共存

      * 可以绑定返回对象的计算属性
	    ```HTML
	    <div v-bind:class =" objectClass ">alisa</div>
	    ```
		``` JavaScript
		data: {
            isA: true,
            isT: null
		}
		computed: {
            objectClass: function(){
                return {
		            active: this.isA && !this.isT,
                    'txt-t': this.isT && this.isT.type === "fatal"		    
                }
            }
		}
		```

	+ 数组语法
		* 传一个数组

			```HTML
			<div v-bind:class = " [ isA, isT ] ">alisa</div>
			```
			```JavaScript
          data: {
                isA:'active',
                isT: 'txt-t'
			}
			```
	  * 可以用三元表达式
   ` 条件 ? 语句1 : 语句2`
        ```HTML
        <div v-bind:class=" [ isA ? activeClass : '', isT ] ">alisa</div>
        ```

	  * 可以在数组语法里使用对象语法
        ```html
        <div c-bind:class="[ {active: isA}, isT ]">alisa</div>        
        ```
	  * 数组语法里可使用多个数据对象，也可与数组混用。
	  `v-bind:class = "[ {active:isA} , isT ]" `
- # 绑定内联样式
  + 对象语法
    > CSS 属性名可以用驼峰式 或 短横分隔符。

	```HTML
	<div v-bind:style=" { color:activeColor, fontSize:fongSize + 'px' }">alisadiv> 
	```
	```JavaScript
	data: {
        activeColor:'red',
        fontSize:30
	}
	```

  + 绑定一个样式对象

  	```HTML
	<div v-bind:style=" styleObject ">alisa</div>
	```
	```JavaScript
	data:{
        styleObject: {
            color:'red',
            'font-size':30+ 'px'
        }
	}
	```
   + 数组语法
     > 可以将多个样式对象应用到一个元素上。

	 ```html
	 <div v-bind:style="[ styleObject1 , styleObject2 ]">vi</div>
	 ```
	 ```JavaScript
	 data: {
         styleObject1: {
             color:'red',
             fontSize:30+'px'
		 },
         styleObject2: {
             'background-color':'#ccc'
         }
	 }
	 ```

	+ 自动添加前缀
	  > v-bind:style 使用需要特定前缀的CSS 属性时，Vue.js会自动检测添加前缀









