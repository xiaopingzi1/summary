## vue中常用指令
1. v-text v-html 替换标签中的全部内容  区别：v-html可以识别数据中的标签字符串
2. v-if 条件渲染 v-if的值如果为true,在页面中显示该元素,为false则隐藏
3. v-show 为true为显示隐藏。display:none和display:block
4. v-on 作用：给标签绑定事件 
> 语法：v-on:事件名="methods中的方法"   
> 简化写法 @click.修饰符 = "methods中的方法"  

5. v-for列表渲染，循环遍历标签
> 1 v-for="v in 数组" v 数组中元素 i 每个元素索引  
> 2 v-for="in 数组"  (v,i) in 数组  
> 如果Key和value的单词一样，可以简写为1个,es6中的语法  
> v-for遍历对象  
> v-for = "v in 对象" v 对象中的value值  
> v-for = "(v,x) in 对象" x 对象中的key值  
> v-for = "(v,k,i) in 对象" i 索引是自动生成，从0开始  
> 注意：在使用v-for时，通常要设置key属性值，key的值要求是唯一的，作用：可以加快vue标签的渲染速度