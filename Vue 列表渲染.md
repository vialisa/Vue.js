# 列表渲染
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
