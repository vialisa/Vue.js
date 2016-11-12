.# 列表渲染
- # v-for

  > 根据一组数组的选项列表进行渲染 可以用 of 代替 in 作为分隔符。

  + 基本用法

  ```html
  <ul id="example">
      <li v-for=" item in items ">
		  {{ item.massage }}
      </li>
  </ul>
  ```

  ```Javascript
  var vm= new Vue ({
      el:"#example",
      data: {
	      items: [
              { message:"CSS" },
              { message:"HTML" },
              { message:"JavaScript" }
          ]
      }		  
  });
  ```

  + v-for 支持一个可选的第二参数作为当前项的索引。

  ```html
  <ul id="example">
      <li v-for= "(item, index) in items ">
          {{ parentMessage }} - {{ index }} - {{ item.message }}
	  </li>
  </ul>
  ```
  ```Javascript
  var vm = new Vue ({
      el:"#example",
      data: {
          parentMessage:"parent",
		  items: [
              { message:"CSS" },
              { message:"HTML" },
              { message:"JavaScript" }
		  ]
      }
  });
  ```
  + 可用带有 v-for 的`<template>` 标签，来渲染多个元素块。

  ```html
  <ul>
  　　<template v-for="item in items">
  　　　　<li> {{ item.message }}</li>
  　　</template>
  </ul>
  ```

  + 对象迭代 v-for

  ```html
  <ul id= "demo">
      <li v-for="value in object">{{　value }}</li>
  </ul>
  ```

  ```Javascript
  data: {
      object: {
          name:"alisa",
          age:27
      }
  }
  ```

	+ 对象迭代 可提供第二个参数作为键名

  ```html
  <li v-for="(value,key) in object">
  {{ key }} : {{ value }}
  </li>
  ```
  ```Javascript
  data: {
	  object: {
		  name: "alisa",
		  age: 27
	  }
  }
  ```

	+ 对象迭代 可提供第三个个参数作为索引

	```html
	<li v-for= "(value,key,index) in object">
	{{ index }}. {{ key }} : {{ value }}
	</li>
	```
   
   + 整数迭代 v-for

   ```html
   <div v-for ="n in 10 ">{{ n }}</div>
   ```

   + 变异方法

     > 观察数组的变异，会触发视图的更新

	 * .push() ==》 数组末尾添加一个新元素
	 * .pop()  ==》 删除数组最后个元素
	 * .shift() ==》  删除数组第一个元素
	 * .unshift()  ==》 在数组开头添加新元素
	 * .splice()  ==》 指定位置，长度，添加/替换
	 * .sort()  ==》 排序
	 * .reverse()  ==》 将数组顺序反转



