# Vue入门
## Vue理解
  * 发明： 尤雨溪， 2014
  * vue: 渐进式框架： 
    * 核心库只保留基本的功能(最简单的功能)，可以满足基本开发
    * vue-router：扩展库。。。
## 知识点
  * 引入Vue.js
  * 创建Vue的实例对象
    * 配置对象
      - el(element)： 选择器字符串(id)，关联页面中的模板，管理页面中指定区域
      - data： 初始化Vue的数据， 数据最终供实例对象使用---- <font color=red>数据代理： Vue实例对象代理了data中的数据</font>
      - methods: 事件的回调函数： click，keyup。。。
      - computed(计算属性): 当使用的数据是根据data中的数据计算得到的---函数/对象(getter, setter存取器属性) 
      - watch: 监视数据(data中的数据)
          属性名： function(value){
            value === 监视属性最新的值
          }
   * 绑定事件：
     * v-on:事件名
     * v-on:事件名(传入的参数)
     * 简写方式：@事件名
   * 指令：
     * v-if：条件判断指令
     * v-for：
       * 遍历目标元素
       * 形式： v-for=todo in todos/  v-for=(todo, index) in todos
   * 强制数据绑定：
     * 标签中原生的属性无法直接解析变量
       * <a href='变量'>百度</a>
       * <a v-bind:href='变量'>百度</a>
       * <a :href='变量'>百度</a>
   * class与style绑定
     * 当这两个属性指定的是变量
     * :class   :style
   * 条件渲染
     * v-if/v-else(什么不用指定，和v-if的条件相反)
     * v-show
     * <font color=red>v-if: 影响DOM初始化结构</font>
     * <font color=red>v-show: display: none/去掉</font>
     * <font color=red>template：影响元素组，注意：只能v-if，template标签不会再页面添加新的DOM节点</font>
