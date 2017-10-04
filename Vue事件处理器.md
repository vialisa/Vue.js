# 事件处理器

 > 用 v-on 指令监听事件来触发一些 JavaScript 代码

- 监听事件

```html
<button v-on:click= "counter += 1">增加1</button>
<p>点击了 {{ counter }} 次</p>
```

- 方法事件处理器

  > 接收一个定义的方法来调用

```html
//greet 为下面methods 对象里定义的方法名。
<button v-on:click= "greet">greet</button>
```

```JavaScript
data: {
    name:alisa
},
methods: {
    greet: function() {
        alert(name)
    }
}
```

- 内联处理器方法

```html
<button v-on:click= "say('hi')">Say Hi</button>
<button v-on:click= "say('hello')>Say Hello</button>
```

```JavaScript
methods: {
    say: function(msg) {
        alert(msg)
    }
}
```

- 事件修饰符
  > 由点表示的指令后缀来调用修饰符

  + .stop
  + .prevent
  + .captrue
  + .self

- 按键修饰符
  > 监听常见的键值

  + enter
  + tab
  + delete
  + esc
  + space
  + up
  + down
  + left
  + right

    *可以通过全局 config.keyCodes 对象自定义按键修饰符别名*
       Vue.config.keyCodes.f1 = 112
