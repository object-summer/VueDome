# VueDome vue 2.0实例（VueDome，再次梳理）
#### Vue全局AIP
  1.Vue.directive 自定义指令
  	注册或获取全局指令。
  2.Vue.extend 构造器延伸
	使用基础 Vue 构造器，创建一个“子类”。参数是一个包含组件选项的对象。
  	data 选项是特例，需要注意 - 在 Vue.extend() 中它必须是函数
  3.Vue.set(target,key,value)设置值，全局操作
  	向响应式对象中添加一个属性，并确保这个新属性同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新属性，因为 Vue 无法探测普通的新增属性 	   (比如 this.myObject.newProperty = 'hi')
  4.Vue.extend()构造器
  	用法：使用Vue构造器，创建一个“子类”，参数是一个包含组件选项的对象，其中,data选项中必须是函数
 #### vue单文件方式 xxx.vue
 1:准备好配置文件 package.json(包描述文件&& 封装命令npm run dev) + webpack.config.js文件（打包的配置文件）
 2:创建index.html（单页应用的页）
 3:创建main.js(入口文件) 
 4:引入vue和相关的文件xxx.vue
 5:new Vue(options)
 6:options（选项）: 
    - data
    - methods
    - components（组件内声明子组件)
    - props
 7:实例:
    - 在组件内（xxx.vue）中的this
    - new Vue()
    - 事件
        + this.$on(事件名,回调函数(参数))
        + this.$emit(事件名,数据)
        + this.$once(事件名,回调函数(参数)) 就触发一次
        + this.$off(事件名); 取消事件
 8:全局
    - Vue.component('组件名',组件对象)  在哪里都可以使用
 9: 组件传值
    - 父传子: 属性作为参数
        + 常量 title="xxx"   子组件声明接收参数 props:['xxx']
        + 变量 :title="num"  子组件声明接收参数 props:['xxx']
    - 子传父: vuebus（只能是同一辆车）
        + 先停车到父组件，On一下
        + 再开车到子组件，如果需要的话，emit一下，触发上述时间的回调函数
#### mint-ui组件库
 饿了么出品,element-ui 在PC端使用的
 移动端版本 mint-ui
 https://mint-ui.github.io/#!/zh-cn
 注意:
    - 如果是全部安装的方式
        + 1:在template中可以直接使用组件标签
        + 2:在script中必须要声明，也就是引入组件对象（按需加载）
 #### vue-router
 前端路由 核心就是锚点值的改变，根据不同的值，渲染指定DOM位置的不同数据
 ui-router:锚点值改变，如何获取模板？ajax、
 vue中，模板数据不是通过ajax请求来，而是调用函数获取到模板内容
 核心：锚点值改变
 以后看到vue开头，就知道必须Vue.use
 vue的核心插件:
    - vue-router 路由
    - vuex 管理全局共享数据
 使用方式
    - 1:下载 `npm i vue-router -S`
    - 2:在main.js中引入 `import VueRouter from 'vue-router';`
    - 3:安装插件 `Vue.use(VueRouter);`
    - 4:创建路由对象并配置路由规则
        + `let router = new VueRouter({ routes:[ {path:'/home',component:Home}  ]   });`
    - 5:将其路由对象传递给Vue的实例，options中
        + options中加入 `router:router`
    - 6:在app.vue中留坑 ` <router-view></router-view>`
 #### 命名路由
 需求，通过a标签点击，做页面数据的跳转
 使用router-link标签
    - 1:去哪里 `<router-link to="/beijing">去北京</router-link>`
    - 2:去哪里 `<router-link :to="{name:'bj'}">去北京</router-link>`
        + 更利于维护，如果修改了path，只修改路由配置中的path，该a标签会根据修改后的值生成href属性
#### 参数router-link
 在vue-router中，有两大对象被挂载到了实例this
 $route(只读、具备信息的对象)、$router(具备功能函数)
 查询字符串
    - 1:去哪里 `<router-link :to="{name:'detail',query:{id:1}  } ">xxx</router-link>`
    - 2:导航(查询字符串path不用改) `{ name:'detail' , path:'/detail',组件}`
    - 3:去了干嘛,获取路由参数(要注意是query还是params和对应id名)
        + `this.$route.query.id`
 path方式
    - 1:去哪里 `<router-link :to="{name:'detail',params:{name:1}  } ">xxx</router-link>`
    - 2:导航(path方式需要在路由规则上加上/:xxx) 
    - `{ name:'detail' , path:'/detail/:name',组件}`
    - 3:去了干嘛,获取路由参数(要注意是query还是params和对应name名)
        + `this.$route.params.name`
#### 编程导航
* 不能保证用户一定会点击某些按钮
* 并且当前操作，除了路由跳转以外，还有一些别的附加操作
* this.$router.go 根据浏览器记录 前进1 后退-1
* this.$router.push(直接跳转到某个页面显示)
    - push参数: 字符串 /xxx
    - 对象 :  `{name:'xxx',query:{id:1},params:{name:2}  }`
#### 获取DOM元素
* 救命稻草, 前端框架就是为了减少DOM操作，但是特定情况下，也给你留了后门
* 在指定的元素上，添加ref="名称A"
* 在获取的地方加入 this.$refs.名称A  
    - 如果ref放在了原生DOM元素上，获取的数据就是原生DOM对象
        + 可以直接操作
    - 如果ref放在了组件对象上，获取的就是组件对象
        + 1:获取到DOM对象,通过this.$refs.sub.$el,进行操作
    - 对应的事件
        + created 完成了数据的初始化，此时还未生成DOM，无法操作DOM
        + mounted 将数据已经装载到了DOM之上,可以操作DOM
#### 多视图
* 以前可以一次放一个坑对应一个路由和显示一个组件
    - 一次行为 = 一个坑 + 一个路由 + 一个组件
    - 一次行为 = 多个坑 + 一个路由 + 多个组件
* components 多视图 是一个对象 对象内多个key和value
    - key对应视图的name属性
    - value 就是要显示的组件对象
* 多个视图`<router-view></router-view>` -> name就是default
* `<router-view name='xxx'></router-view>` -> name就是xxx
### 嵌套路由
* 用单页去实现多页应用，复杂的嵌套路由
* 开发中一般会需要使用
* 视图包含视图
* 路由父子级关系路由
#### vue-resource(了解)
* 可以安装插件，早期vue团队开发的插件
* 停止维护了，作者推荐使用axios
* options预检请求，是当浏览器发现跨域 + application/json的请求，就会自动发起
* 并且发起的时候携带了一个content-type的头
