# 表单控件绑定

- 基础用法
  > v-model 在表单控件元素上创建双向数据绑定。

  *v-model选择实例数据作为具体的值。*

  + 文本

    ```html
	<input type="text" v-model= "message" placeholder= "edit me">
	<p> Message is: {{ message }} </p>
	```

  + 多行文本
  	> 在文本域插值不会生效

    ```html
    <textarea v-model= "message" placeholder= "add multiple lines"></textarea>
    <p>Message is : {{ message }}</p>
    ```

  + 复选框

    * 单个勾选框，逻辑值

	```html
	<input type="checkbox" id="checkbox" v-model= "checked">
	<label for="checkbox"> {{ checked }}</label>
	```

	 * 多个勾选框，绑定到同一个数组

	 ```html
	 <input type= "checkbox" id= "cici" v-model= "checkedNames" value= "cici">
	 <label for="cici"> Cici </label>
	 <input type= "checkbox" id="vivi" v-model= "checkedNames" value= "vivi">
	 <label for="vivi"> Vivi </label>
	 <input type= "checkbox" id="alisa" v-model= "checkedNames" value= "alisa">
	 <label for="alisa"> Alisa </label>

	 <p>Checked Names : {{ checkedNames }} </p>
     ```

  + 单选按钮
    
	```html
	<input type="radio" id="vivi" v-model= "radioName" value="vivi">
	<label for= "vivi"> Vivi </label>
	<input type="radio" id="cici" v-model= "radioName" value="cici">
	<label for="cici"> Cici </label>

	<p>Radio name: {{ radioName }} </p>
	```

  + 选择列表

    * 单选列表

    ```html
	<select v-model= "selecked">
	    <option> Vivi </option>
        <option> Cici </option>
        <option> ViCi </option>
	</select>
	<p>Selecked : {{ selecked }} </p>
	```

	* 多选列表
	  > 绑定到一个数组

	```html 
	<select v-model= "selecked" multiple>
        <option>A</option>
        <option>B</option>
        <option>C</option>
	</select>
	<p>Selecked : {{ selecked }}</p>
	```

	* 动态选项，用v-for 渲染

	```html
	<select v-model="selecked">
	    <option v-for="option in options" v-bind:value="option.value">
		{{ option.text }}
		</option>
	</select>
	<p> Selecked: {{ selecked }}</p>
	```

	```Javascript
	data: {
		selecked: 'A',
		options: [
			{ text: "Alisa", value: "A"},
			{ text: "Cici", value: "B"},
			{ text: "Vivi", value: "C" }
		]
	}
    ```

- 绑定 Value

  + 对于单选按钮，勾选框，选择列表选项，v-model 绑定的value 通常是静态字符串。
  + 绑定 value 到Vue实例的一个动态属性可用 v-bind 实现，属性的值可以不是字符串。

- 修饰符

  + .lazy   - 转变为在 change 事件中同步
  + .number  - 自动将用户的输入值转为 Number 类型
  + .trim   - 自动过滤用户输入的首尾空格









