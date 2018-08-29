# VueDome vue 2.0实例（VueDome，再次梳理）
一、Vue全局AIP
  1.Vue.directive 自定义指令
  	注册或获取全局指令。
  2.Vue.extend 构造器延伸
	使用基础 Vue 构造器，创建一个“子类”。参数是一个包含组件选项的对象。
  	data 选项是特例，需要注意 - 在 Vue.extend() 中它必须是函数
  3.Vue.set(target,key,value)设置值，全局操作
  	向响应式对象中添加一个属性，并确保这个新属性同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新属性，因为 Vue 无法探测普通的新增属性 	   (比如 this.myObject.newProperty = 'hi')
  4.Vue.extend()构造器
  	用法：使用Vue构造器，创建一个“子类”，参数是一个包含组件选项的对象，其中,data选项中必须是函数
 vue单文件方式 xxx.vue
 1:准备好配置文件 package.json(包描述文件&& 封装命令npm run dev) + webpack.config.js文件（打包的配置文件）
 2:创建index.html（单页应用的页）
 3:创建main.js(入口文件) 
 4:引入vue和相关的文件xxx.vue
 5:new Vue(options)

