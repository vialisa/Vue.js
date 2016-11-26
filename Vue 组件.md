# 组件
  > 可扩展 HTML 元素，封装可重用的代码。

- # 组件

  + 全局注册
    > 初始化根实例之前注册组件

    ```Javascript
    Vue.component('my-component', {
	    // option
    });
    ```

  + 局部注册
    > 通过实例选项 components 注册

  + DOM 模板解析说明
    * 特殊的 is 属性
    * ` <ul>/<ol>/<tabel>/<select> `

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
       template:'<button v-on:click="counter += 1">counter</button>

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
    * 父组件通过 props 向下传递数据给子组件
    * 子组件通过 events 给父组件发送消息

- # Props

  + 组件实例的作用域是独立的
  +
     ```html
     <child message="vialisa"></child>
     ```

     ```JavaScript
     Vue.component('child',{
         props:['message'],
         template:"<span>{{ message }}</span>"
     });
     ```

  + camelCase  /  kebab-case (非字符串模板时)
    * HTML 特性不区分大小写
    * camelCase  in JavaScript
    * kebab-case in HTML
      > myMessage  -  my-message

  + 动态 props
    > 用v-bind 绑定动态props 到父组件的数据`<my-component v-bind:message="parentMsg"></my-component>`

  + 字面量语法  vs  动态语法
    > 使用 v-bind 动态语法传递数值

  + 单向数据流
    > 父组件的属性变化时传递到子组件

  + 属性校验
    ```
    Vue.component('example',{
      props:{
        //基本类型验证（null任何类型）
        propA:Number,
        //多类型验证
        propB:[Number,String]
        //必须是字符串属性
        propC:{
          type:String,
        required:true
        },
        //数值类型，默认值
        propD:{
          type:Number,
          default:100
        },
        //对象/数组的默认值由函数返回
        propE:{
          type:Object,
          default:function(){
            return { message:'vivi'}
          },
          //自定义函数验证
          propF:{
            validator:function(value){
              return value< 10
            }
          }
        }
    })
    ```

- # 自定义事件
  > 子组件向父组件通信

  + v-on
    * $on(eventName)  -  监听事件
    * $emit(eventName)  -  触发事件  可传参
      > 父组件模板中使用 v-on 来监听子组件分发的事件

        ```html
        <div id="demo">
            <p>{{counter}}</p>
            <child-com @outer="changer">{{message}}</child-com>
            <child-com @outer="changer">{{message}}</child-com>
        </div>
        ```

        ```JavaScript
        new Vue({
          el:"#demo",
          data: {
            counter:0
          },
          methods:{
              changer:function(){
                counter += 1;
              }
          },
          components:{
            childCom:{
              template:"<button @click="inner">{{msg}}</button>",
              data:function(){
                return {msg:0}
              },
              methods:{
                  inner:function(){
                    this.msg += 1;
                    this.$emit('outer')
                  }
              }
            }
          }
        });
        ```

    * 组件上绑定原生事件
       `<my-com @click.native="deSomething"></my-com>`

  + 表单控件上使用自定义事件

    * v-mode / :value / @input / $events.target.value
    * 货币输入控件例子:
       ```html
       <div id="demo">
          <p>{{message}}</p>
          <input-com v-model="message"></input-com>
       </div>
      ```

      ```JavaScript
      new Vue({
        el: "#demo",
        data: {
          message:10
        },
        components: {
          inputCom:{
            template: '<input type="text" @input="changer" :value="value">',
            props: ['value'],
            methods: {
                changer:function($events){
                    var value = $events.target.value;
                    //小数点后限制两位
                    var outerVal = value.trim().slice(0, value.indexOf('.')+3);
                    $events.target.value = outerVal;
                    this.$emit('input',Number(outerVal));
                }
            }
          }
        }
      });
      ```


  + 非父子组件通信
    > 可把一个 Vue 实例作为事件中心


- # 使用插槽分发内容 ` <slot> `

  + 编译作用域
    * 父组件模板中的内容在父组件作用域内编译
    * 子组件模板中的内容在子组件作用域内编译
    * 分发内容会在父组件的作用域内编译

  + 单个插槽
    * 子组件包含`<slot>`,否则父组件模板的内容被丢弃。
    * `<slot>` 内为替换内容，父组件内容为空或没有内容插入时显示。
    * 子组件模板的内容要全部放在一个容器内。

  + 具名插槽 name属性
    > 定义内容分发的方式

    * 匿名插槽为默认插槽

      ```html
      //父组件模板
      <com-slot>
          <p slot="two">由name为two替换</p>
          <p slot="one">顺序按子组件模板内容</p>
          <p>由匿名插槽替换</p>
      </com-slot>
      ```

      ```html
      // 子组件comSlot模板
      <div>
          <p>子组件模板内容p元素</p>
          <slot name="one">替换内容</slot>
          <slot name="tow">替换内容</slot>
          <slot>匿名插槽</slot>
      </div>
      ```

- # 动态组件
  > 要绑定is属性

    + 点击切换组件demo
    ```html
    <div id="example-18">
      <button @click="firstMethod">{{msgfirst}}</button>
      <button @click="middleMethod">{{msgmiddle}}</button>
      <button @click="lastMethod">{{msglast}}</button>

      <div v-bind:is="changerCom"></div>

    </div>
    ```
    ```JavaScript
    <script>
      new Vue({
        el:"#example-18",
        data: {
            msgfirst:"first",
            msgmiddle:"middle",
            msglast:"last",
            changerCom:"first-com"
        },
        methods:{
            firstMethod:function() {
            this.changerCom = "first-com"
            },
        middleMethod:function() {
            this.changerCom = "middle-com"
            },
        lastMethod:function() {
            this.changerCom = "last-com"
            }
      },
      components: {
        'first-com': {
          template:"<div>This is first component<div>"
        },
        'middle-com': {
          template:"<div>This is middle component</div>"
        },
        'last-com': {
          template:"<div>This is last component</div>"}
      }
    });
    </script>
    ```

    + 可直接绑定到组件对象
      ```JavaScript
      var first = {
      template:"<div>component</div>"
      }

      new Vue({
          el:"#demo",
          data:{
          changerCom:first
          }
      });
      ```

    + keep-alive
      > 组件缓存

      ```html
      <keep-alive>将组件模板包裹在内</alive>
      ```

- # 杂项

  + 编写可复用的组件（属性/事件/插槽）
    * 外部环境通过属性将数据传递给组件
    * 组件通过事件对外部环境产生影响
    * 外部环境通过 slot 将部分内容和组件组合

  + 子组件索引
    > 可在 JavaScript 中直接访问子组件

    ```html
    <div id="parent">
      <child-refs ref="profile"></child-refs>
    </div>
    ```

    ```JavaScript
    var prant = new Vue({el:"#parent"});
    var child = parent.$refs.profile
    ```

  + 组件命名约定
    * 注册组件时驼峰/短横分隔
    * HTML 模板必须是短横分隔命名（字符串模板除外）



