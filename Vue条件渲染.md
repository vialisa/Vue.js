# 条件渲染

* # v-if
	> 根据条件展示元素
	
	```html
	<p v-if="ok">Yes</p>
	<p v-else>No</p>
    ```
	+ template v-if
	  > 可切换多个元素
      
	  ```html
	  <template v-if="OK">
	  <h1>title</h1>
	  <p>alt</p>
	  <p>paragraph</p>
	  </template>
	  ```
	+ v-else
	  > v-else必须紧跟在 v-if 或者 v-show 元素的后面，用来添加else 块

	+ v-show 
	  > 根据条件展示元素,不支持< template >语法

	  ```html
	  <h1 v-show="OK">alisa</h1>
	  ```

    + v-if VS V-show
      * v-if  
	  > 条件第一次为真时开始编译，有缓存。v-if 有更高的切换消耗。
	  
	  * v-show 
	  > 始终被编译并保留，只是简单的切换元素的CSS的display属性。有更高的初始渲染消耗。

	  * 频繁切换使用 v-show ，运行时条件不大可能改变用 v-if


