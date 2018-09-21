## Vue笔记


### 指令
----
1. v-html
2. v-bind
3. v-if （低频切换）
4. v-else
5. v-show （高频切换）
6. v-on
7. v-for
8. key （管理复用）
9. v-once
10. v-model （文本输入与显示的双向绑定）
11. is （指定当前元素匹配的组件名称，用于table等特殊元素对子元素有限制的情况）



### 属性
----
1. el
2. data （必须是函数，保证复用组件时，数据的独立性）
3. methods
4. computed (有缓存)
5. watch
6. created


### 事件修饰符
----
```html
<!-- 示例 -->
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```
- .stop: 阻止单击事件继续传播。
- .prevent: 提交事件不再重载页面。
- .capture: 添加事件监听器时使用事件捕获模式。
- .self: 只当在 event.target 是当前元素自身时触发处理函数。
- .once: 点击事件将只会触发一次。
- .passive: 告诉浏览器你不想阻止事件的默认行为。
- .native: 绑定原生事件。

`注：修饰符可串联使用，但顺序很重要。`


### 按键修饰符
----
```html
<!-- 示例 -->
<!-- 只有按下 "enter" 键时调用 `vm.submit()` -->
<input v-on:keyup.enter="submit">
```

### 系统修饰符
----
```html
<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>

<!--.exact 修饰符允许你控制由精确的系统修饰符组合触发的事件。-->
<!-- 没有任何系统修饰符被按下的时候才触发 -->
<button @click.exact="onClick">A</button>
```

### 鼠标按钮修饰符
----
- left
- right
- middle

### 输入修饰符
----
- lazy
- number
- trim
```html
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg" >
<!-- 自动将用户的输入值转为数值类型 -->
<input v-model.number="age" type="number">
<!-- 自动过滤用户输入的首尾空白字符 -->
<input v-model.trim="msg">
```

### 组件基础
----
- prop : 向子组件传递数据。
- $emit : 向父组件传递消息，参数为 `方法名，参数`
```html
<button v-on:click="$emit('enlarge-text','params')">
  字体放大
</button>
<!--用 v-on 在父组件上监听这个事件-->
<blog-post
  ...
  v-on:enlarge-text="postFontSize += 0.1"
></blog-post>
```

- $listener : 
- $attrs
- .sync
- \<slot> ， \<slot-scope>
- \<keep-alive>
- \<router-view/>
- \<router-link/>