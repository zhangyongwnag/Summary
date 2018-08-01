# 1. 说明
	官方提供的用来实现SPA的vue插件
	github: https://github.com/vuejs/vue-router
	中文文档: http://router.vuejs.org/zh-cn/
	下载: npm install vue-router --save
  
# 2. 相关API说明
## 1). VueRouter(): 用于创建路由器的构建函数
    new VueRouter({
      // 多个配置项
    })

## 2). 路由配置
    routes: [
      { // 一般路由
        path: '/about',
        component: about
      },
      { // 自动跳转路由
        path: '/', 
        redirect: '/about'
      }
    ]

## 3). 注册路由器
	import router from './router'
	new Vue({
		router
	})

## 4). 使用路由组件标签:
	1. router-link: 用来生成路由链接
		<router-link to="/xxx">Go to XXX</router-link>
	2. <router-view>: 用来显示当前路由组件界面
		<router-view></router-view>
      
# 3. 简单路由
## 1). 路由组件:
	home.vue
	about.vue

## 2). 应用组件: App.vue
    <div>
      <!--路由链接-->
      <router-link to="/about">About</router-link>
      <router-link to="/home">Home</router-link>
      <!--用于渲染当前路由组件-->
      <router-view></router-view>  
    </div>

## 3). 路由器模块: src/router/index.js
	export default new VueRouter({
      routes: [
        {
          path: '/',
          redirect: '/about'
        },
        {
          path: '/about',
          component: about
        },
        {
          path: '/home',
          component: home
        }
      ]
    })

## 4). 入口js: main.js
	import Vue from 'vue'
    import router from './router'
    // 创建vue配置路由器
    new Vue({
      el: '#app',
      router,
      render: h => h(app)
    })

## 5). 优化路由器配置
    linkActiveClass: 'active', // 指定选中的路由链接的class

## 6. 总结: 编写使用路由的3步
	1). 定义路由组件
	2). 注册路由
	3). 使用路由
		<router-link>
		<router-view>
    
# 4. 嵌套路由
## 1). 配置嵌套路由
    path: '/home',
    component: home,
    children: [
      {
        path: 'news',
        component: news
      },
      {
        path: 'message',
        component: message
      }
    ]

## 2). 路由链接
    <router-link to="/home/news">News</router-link>
    <router-link to="/home/message">Message</router-link>

# 5. 向路由组件传递数据
## 1). 方式1: 路由路径携带参数
	1.配置路由
      children: [
        {
          path: 'mdetail/:id',
          component: messageDetail
        }
      ]
    2.路由路径
      <router-link :to="'/home/message/mdetail/'+m.id">{{m.title}}</router-link>
    3.路由组件中读取请求参数
      this.$route.params.id

## 2). 方式2: <router-view>属性携带数据
    <router-view :msg="msg"></router-view>

# 6. 缓存路由组件: <keep-alive>
    <keep-alive>
      <router-view></router-view>
    </keep-alive>
    
# 7. 路由的编程式导航
	this.$router.push(path): 相当于点击路由链接(可以返回到当前路由界面)
	this.$router.replace(path): 用新路由替换当前路由(不可以返回到当前路由界面)
	this.$router.back(): 请求(返回)上一个记录路由
	this.$router.go(-1): 请求(返回)上一个记录路由
	this.$router.go(1): 请求下一个记录路由

	路由跳转:
		<a href="#/xxx">
		
	页面跳转:
		<a href="/xxx">
		window.location = '/xxx'
    
    传递路由参数
        this.$router.push({path: `/home/message/detail/${id}`})

# 7. 简化路由路径(使用history模块)
## 1) 配置
    mode: 'history'
## 2) 结果
    路由路径不再携带#
## 3) 基本原理
    hash: 利用window监视history的hash值的变化来实现路径跳转
    history: 利用 history.pushState API 来完成路由跳转  
## 4). 问题: 直接在子路由路径上刷新, 样式不正常
    原因: 在index.html中引入全局样式的路径, 使用的相对路径
          <link rel="stylesheet" href="./static/css/bootstrap.css">
    解决: 必须以/开头(代表项目的根路径)
          <link rel="stylesheet" href="/static/css/bootstrap.css">
## 5). 配置404界面
    方式一: 后台配置404页面
    方式二: 前端配置404组件
        {
          path: '*',
          component: NotFound
        }

## 8. 监视路由参数变化
    watch: {
      '$route' (to, from) {
        // 对路由变化作出响应...
      }
    }

# 9. 路由总结
## 1). 分类 
	后台路由
	前台路由
## 2). 是什么
	一句话: 就是一个映射关系(key:value)
	后台路由: path: callback
	前台路由: path: component