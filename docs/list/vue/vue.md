## vue中常用指令
1. v-text v-html 替换标签中的全部内容  区别：v-html可以识别数据中的标签字符串
2. v-if 条件渲染 v-if的值如果为true,在页面中显示该元素,为false则隐藏
3. v-show 为true为显示隐藏。display:none和display:block
4. v-on 作用：给标签绑定事件 
> 语法：v-on:事件名="methods中的方法"   
> 简化写法 @click.修饰符 = "methods中的方法"