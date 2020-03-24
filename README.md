# 1 电商后台管理系统的技术选择

## 前端项目技术栈

- Vue
- Vue-router
- Element-ui
- Axios
- Echarts



# 2 项目初始化

## 2.1 通过可视化面板创建项目

win+r=>cmd=>vue ui

![TIM截图20200322210635.png](https://i.loli.net/2020/03/24/bjFOwiRaKoGeCmU.png)

![TIM截图20200321130200.png](https://i.loli.net/2020/03/24/jsCXi5ZxAL1gNhq.png)

## 2.2 选择项目的存储目录

![TIM截图20200321130336.png](https://i.loli.net/2020/03/24/7Bhr18TRiSFtcOk.png)

## 2.3 项目名称

![TIM截图20200321130452.png](https://i.loli.net/2020/03/24/qI52h3JiLyueQrf.png)

## 2.4 手动配置项目

![TIM截图20200321130616.png](https://i.loli.net/2020/03/24/RzwPOHS39uIgxv5.png)

## 2.5 安装Babel、Router、Linter/Formatter

![TIM截图20200321130815.png](https://i.loli.net/2020/03/24/jmbON2EnJG6IUKf.png)

## 2.6 最后一个配置

![TIM截图20200321130929.png](https://i.loli.net/2020/03/24/kUO5wHMXW3Ybqcf.png)

## 2.7 创建项目

**保存为新预设**

![TIM图片20200321131159.png](https://i.loli.net/2020/03/24/pGrBELdahCOZJwt.png)

## 2.8 配置Element-ui 组件库

### 选择插件=>添加插件

![TIM截图20200321131338.png](https://i.loli.net/2020/03/24/d1zneaACNThxIPW.png)

### 搜索vue-cli-plugin-element 选中并安装

![TIM截图20200321131620.png](https://i.loli.net/2020/03/24/kFWQj6uyTweYKG5.png)

### 配置插件

**设置为按需导入并点击完成安装**

![TIM截图20200321131812.png](https://i.loli.net/2020/03/24/RbyPrlkB58tKpDY.png)

## 2.9 配置axios库

### 侧边栏选中依赖=>安装依赖=>运行时依赖

![TIM截图20200321132047.png](https://i.loli.net/2020/03/24/JGFdMxuCpivUDLe.png)

### 搜索axios并安装

![TIM截图20200321132238.png](https://i.loli.net/2020/03/24/oBsWYH1TrjGxngz.png)

## 2.10 安装less依赖

- 依赖=> 开发依赖=>less-loader


- 依赖=> 开发依赖=>less

# 3 在gitee中创建git仓库

> 新建仓库=>仓库名称=>仓库介绍=>取消勾选Readme文件初始化仓库

```
git init
git add .
git commit -m "init project"
git remote add origin https://gitee.com/tzforevereer/prison_roll_call.git
git push -u origin master
```

# 4 数据库导入

> mydb.sql

# 5 修改默认页面

## 1 打开src/main.js

> main.js为入口文件

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router'
import './plugins/element.js'

Vue.config.productionTip = false


new Vue({
  router,
  render: h => h(App)
}).$mount('#app')

```

## 2 App.vue

> 将根组件的内容进行操作梳理(template中留下根节点，script中留下默认导出，去掉组件，style中去掉所有样式)

```vue
<template>
  <div id="app">
      <!--路由占位符-->
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>
</style>
```

## 3 router.js(路由)

```js
import Vue from 'vue'
import Router from 'vue-router'

Vue.use(Router)

export default new Router({
  routes: [
    
  ]
})
```

## 4 删除不用的内容

- 删除views文件

- 删除HelloWorld.vue

# 6 引入axios

> 在main.js中

```
import axios from 'axios'


// 配置请求的根路径
axios.defaults.baseURL = 'http://127.0.0.1:8888/api/private/v1/'

Vue.prototype.$http = axios
```
# 7  配置 弹框提示

Element 注册了一个`$message`方法用于调用，Message 可以接收一个字符串作为参数，它会被显示为正文内容。

```js
import {Message} from 'element-ui'

// 进行全局挂载
Vue.prototype.$message = Message;
```
# 8 登录组件

>1.在assets文件夹下面添加css文件夹，创建global.css文件,添加全局样式

```less
/* 全局样式表 */
html,body,#app{
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0; 
}
```

>2.在main.js中导入global.css，使得全局样式生效

```js
// 导入全局css
import './assets/css/global.css'
```

> 3. 编写Login.vue

```vue
<template>
  <div class="login_container">
     <!--根元素需要设置撑满全屏（height:100%）-->
    <div class="login_box">
      <!--头像区域-->
      <div class="avatar_box">
        <img src="../assets/logo.png" alt="">
      </div>
      <!--登录表单区域-->
      <el-form ref="loginFormRef" :rules="loginFormRules" :model="loginForm"  label-width="0px" class="login_form">
        <!--用户名-->
        <el-form-item prop="username">
          <el-input v-model="loginForm.username" prefix-icon="el-icon-s-custom"></el-input>
        </el-form-item>
        <!--密码-->
        <el-form-item prop="password">
          <el-input v-model="loginForm.password" prefix-icon="el-icon-lock" type="password"></el-input>
        </el-form-item>
        <el-form-item class="btns">
          <el-button type="primary" @click="login">登录</el-button>
          <el-button type="info" @click="resetLoginForm">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      // 这是登录表单的数据绑定对象
      loginForm: {
        username: '',
        password: ''
      },
      // 表单的验证规则对象
      loginFormRules: {
        // 验证用户名是否合法
        username: [
          { required: true, message: '请输入用户名称', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
        ],
        // 验证密码是否合法
        password: [
          { required: true, message: '请输入登录密码', trigger: 'blur' },
          { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    // 点击重置按钮，重置登录表单
    resetLoginForm () {
      this.$refs.loginFormRef.resetFields()
    },
    login () {
      // 点击登录的时候先调用validate方法验证表单内容是否有误
      this.$refs.loginFormRef.validate(async (valid) => {
        if (!valid) return
        const { data: res } = await this.$http.post('login', this.loginForm)
        if (res.meta.status !== 200) return this.$message.error('登录失败！')
        this.$message.success('登录成功')
        // 1.登录成功之后的token,保存到客户端的 sessionStorage 中
        //  1.1 项目中除了登录之外的其他API接口，必须在登录之后才能访问
        //  1.2 token 只应在当前网站打开期间生效，必须讲 token 保存在 sessionStorage中
        window.sessionStorage.setItem('token', res.data.token)
        // 2. 通过编程式导航跳转到后台主页，路由地址是 /home
        this.$router.push('/home')
      })
    }
  }

}
</script>
<style lang="less" scoped>
.login_container{
  background-color: #2b4d6b;
  height: 100%;
}
.login_box{
  width: 450px;
  height: 300px;
  background-color: #fff;
  border-radius: 3px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%,-50%);
}

.avatar_box{
  height: 130px;
  width: 130px;
  border: 1px solid #eee;
  border-radius: 50%;
  padding: 10px;
  box-shadow: 0 0 10px #ddd;
  position: absolute;
  left: 50%;
  transform: translate(-50%,-50%);
  background-color: #fff;
  img{
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background-color: #eee;
  }
}

.btns{
  display: flex;
  justify-content: flex-end;
}

.login_form{
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}
</style>

```

> 4. 添加路由规则

```
const router = new Router({
  routes: [
    { path: '/', redirect: '/login' },
    { path: '/login', component: Login },
  ]
})
```

> 5. element-ui 组件按需导入

```js
import {
  Button, Form, FormItem, Input
} from 'element-ui'

Vue.use(Button)
Vue.use(Form)
Vue.use(FormItem)
Vue.use(Input)
```

# 9 携带Token令牌

> 登录成功之后，将服务器颁发的token令牌保存到客户端的 sessionStorage 

- 项目中除了登录之外的其他API接口，必须在登录之后才能访问
- token 只应在当前网站打开期间生效，必须讲 token 保存在 sessionStorage中

- sessionStorage是会话存储机制、localStorage是持久化存储机制

```js
window.sessionStorage.setItem('token', res.data.token)
```

> 通过编程式导航跳转到后台主页，路由地址是 /home

```js
 this.$router.push('/home')
```

# 10 路由导航首位控制访问权限

如果用户没有登录，但是直接通过URL访问特定页面，需要重新导航到登录页面

在router/index.js 

>更改代码格式

```js
const router = new Router({
  routes: [
    { path:'/', redirect:'/login'},
    { path:'/login' , component:Login },
    { path:'/home' , component:Home}
  ]
})

export default router 
```

> 添加路由导航首位

```js
// 挂载路由导航守卫
router.beforeEach((to, from, next) => {
  // to 将要访问的路径
  // from 带表从哪一个路径跳转而来
  // next 是一个函数，表示放行
  //  next() 放行  next('login') 强制跳转
  if (to.path === '/login') return next()
  // 获取token
  const tokenStr = window.sessionStorage.getItem('token')
  if (!tokenStr) return next('/login')
  next()
})
```

# 11 退出功能

> 基于token的方式退出比较简单，只需要销毁本地的token即可，这样后续的请求就不会携带token,必须重新登录生成一个新的token之后才可以访问

```
    logout () {
      // 清空token
      window.sessionStorage.clear()
      // 跳转到登录页
      this.$router.push('/login')
    },
```

# 12 主页布局

## Home.vue基本布局

```vue
<el-container class="home-container">
  <!-- 头部区域 -->
  <el-header>Header<el-button type="info" @click="logout"> 退出 </el-button></el-header>
  <!-- 页面主体区域 -->
  <el-container>
    <!-- 侧边栏 -->
    <el-aside width="200px">Aside</el-aside>
    <!-- 主体结构 -->
    <el-main>Main</el-main>
  </el-container>
</el-container>
```

默认情况下，跟element-ui组件同名的类名可以帮助我们快速的给对应的组件添加样式，如：

```
.home-container {
  height: 100%;
}
.el-header{
  background-color:#373D41;
}
.el-aside{
  background-color:#333744;
}
.el-main{
  background-color:#eaedf1;
}
```

## 顶部布局

```vue
      <!--头部区域-->
      <el-header>
        <div>
          <span>电商后台管理系统</span>
        </div>
        <el-button  type="info" @click="logout">退出</el-button>
      </el-header>
```

## 侧边栏布局

```vue
        <!--侧边栏-->
        <el-aside :width="isCollapse ? '64px' : '200px'">
          <div class="toggle-button" @click="toggleCollapse">|||
          </div>
          <!--侧边栏菜单区域-->
          <el-menu background-color="#333744" text-color="#fff" active-text-color="#409EFF" unique-opened :collapse="isCollapse" :collapse-transition='false' router :default-active="activePath">
            <!--一级菜单-->
            <el-submenu :index="item.id + ''" v-for="item in menulist" :key='item.id'>
              <!--一级菜单的模板区域-->
              <template slot="title">
                <!-- 图标 -->
                <i :class="iconsObj[item.id]"></i>
                <!-- 文本 -->
                <span>{{item.authName}}</span>
              </template>
              <!-- 二级菜单 -->
              <el-menu-item :index="'/' + subItem.path" v-for="subItem in item.children" :key="subItem.id" @click="saveNavState('/' + subItem.path)">
                <template slot="title">
                <!-- 图标 -->
                <i class="el-icon-menu"></i>
                <!-- 文本 -->
                <span>{{subItem.authName}}</span>
              </template>
              </el-menu-item>
            </el-submenu>
          </el-menu>
        </el-aside>
```

解析：

- :index="item.id + ''"    index仅接受字符串，所以需要将id转换为字符串
- unique-opened="true" 保持左侧菜单每次只能打开一个

## 设置图标

在数据中添加一个iconsObj

将图标类名进行数据绑定，绑定iconsObj中的数据

```
iconsObj: {
        '125':'iconfont icon-user',
        '103':'iconfont icon-tijikongjian',
        '101':'iconfont icon-shangpin',
        '102':'iconfont icon-danju',
        '145':'iconfont icon-baobiao'
      }
```



# 13 请求数据的注意事项

需要授权的API，必须在请求头中使用`Authorization`字段提供token令牌

- 通过添加axios请求拦截器来添加token，以保证拥有获取数据的权限
- 在main.js中添加代码，在将axios挂载到vue原型之前添加下面的代码

```js
//请求在到达服务器之前，先会调用use中的这个回调函数来添加请求头信息
axios.interceptors.request.use(config=>{
  //为请求头对象，添加token验证的Authorization字段
  config.headers.Authorization = window.sessionStorage.getItem("token")
  return config
})
```

# 14 菜单栏隐藏展开

在菜单栏上方添加一个div

```vue
        <!-- 侧边栏,宽度根据是否折叠进行设置 -->
        <el-aside :width="isCollapse ? '64px':'200px'">
          <!-- 伸缩侧边栏按钮 -->
          <div class="toggle-button" @click="toggleCollapse">|||</div>
          <!-- 侧边栏菜单，:collapse="isCollapse"（设置折叠菜单为绑定的 isCollapse 值），:collapse-transition="false"（关闭默认的折叠动画） -->
          <el-menu
          :collapse="isCollapse"
          :collapse-transition="false"
          ......
```

```js
    // 点击按钮，切换菜单的折叠与展开
    toggleCollapse () {
      this.isCollapse = !this.isCollapse
    },
```

```less
.toggle-button{
  background-color: #4A5064;
  font-size: 10px;
  line-height: 24px;
  color: #fff;
  text-align: center;
  letter-spacing: 0.2em;
  cursor: pointer;
}
```



# 15 首页路由的重定向

Welcome.vue

```vue
<template>
  <div>
    <h3>Welcome</h3>
  </div>
</template>

```

编写路由

在router/index.js中导入子级路由组件，并设置路由规则以及子级路由的默认重定向

```js
routes: [
    { path: '/login', component: Login },
    { path: '/', redirect: '/login' },
    {
      path: '/home',
      component: Home,
      redirect: '/welcome',
      children: [
        { path: '/welcome', component: Welcome }
    ]

```

# 16 左侧菜单改造为路由链接

将二级菜单改为路由链接

- 将el-menu的router属性设置为true就可以了，此时当我们点击二级菜单的时候，就会根据菜单的index

- 使用index id来作为跳转的路径不合适，我们可以重新绑定index的值为  :index="'/'+subItem.path"

```
<el-menu-item :index="'/' + subItem.path" v-for="subItem in item.children" :key="subItem.id" @click="saveNavState('/' + subItem.path)">
</el-menu-item>
```

# 17 二级菜单高亮

通过设置el-menu的default-active属性来设置当前激活菜单的index

但是default-active属性也不能写死，固定为某个菜单值
所以我们可以先给所有的二级菜单添加点击事件,并将path值作为方法的参数

```vue
<el-menu-item :index="'/' + subItem.path" @click="saveNavState('/' + subItem.path)">
```

在saveNavState方法中将path保存到sessionStorage中

```js
 // 保存链接的激活状态
    saveNavState (activePath) {
      window.sessionStorage.setItem('activePath', activePath)
      this.activePath = activePath
    }
```

```js
  created () {
    this.getMenuList()
    this.activePath = window.sessionStorage.getItem('activePath')
  },
```

# 18 面板屑

通过设置 `separator-class` 可使用相应的 `iconfont` 作为分隔符，注意这将使 `separator` 设置失效

```vue
<el-breadcrumb separator-class="el-icon-arrow-right">
  <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
  <el-breadcrumb-item>活动管理</el-breadcrumb-item>
  <el-breadcrumb-item>活动列表</el-breadcrumb-item>
  <el-breadcrumb-item>活动详情</el-breadcrumb-item>
</el-breadcrumb>
```

## Breadcrumb Item Attributes

| 参数    | 说明                                                         | 类型          | 可选值 | 默认值 |
| :------ | :----------------------------------------------------------- | :------------ | :----- | :----- |
| to      | 路由跳转对象，同 `vue-router` 的 `to`                        | string/object | —      | —      |
| replace | 在使用 to 进行路由跳转时，启用 replace 将不会向 history 添加新记录 | boolean       | —      | false  |

# 19 卡片视图

```vue
<el-card></el-card>
```

# 20 搜索

```vue
<el-input placeholder="请输入内容" v-model="input3" class="input-with-select">
    <el-button slot="append" icon="el-icon-search"></el-button>
  </el-input>
```

## 实现搜索功能

添加数据绑定，添加搜索按钮的点击事件(当用户点击搜索按钮的时候，调用getUserList方法根据文本框内容重新请求用户列表数据)
当我们在输入框中输入内容并点击搜索之后，会按照搜索关键字搜索，我们希望能够提供一个X删除搜索关键字并重新获取所有的用户列表数据，只需要给文本框添加clearable属性并添加clear事件，在clear事件中重新请求数据即可

```vue
<el-col :span="7">
    <el-input placeholder="请输入内容" v-model="queryInfo.query" clearable @clear="getUserList">
        <el-button slot="append" icon="el-icon-search" @click="getUserList"></el-button>
    </el-input>
</el-col>
```

# 21 栅格布局

Row 组件 提供 `gutter` 属性来指定每一栏之间的间隔，默认间隔为 0。

```vue
<el-row :gutter="20">
  <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
  <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
  <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
  <el-col :span="6"><div class="grid-content bg-purple"></div></el-col>
</el-row>
```

# 22 table表格

```vue
 <el-table :data="userList" border stripe>
        <el-table-column label="姓名" prop="username">
        </el-table-column>
        <el-table-column label="邮箱" prop="email">
        </el-table-column>
        <el-table-column label="电话" prop="mobile">
        </el-table-column>
        <el-table-column label="角色" prop="role_name">
        </el-table-column>
        <el-table-column label="状态" prop="mg_state">
        </el-table-column>
        <el-table-column label="操作" >
        </el-table-column>
      </el-table>
```

# 23 文字提示

```vue
            <el-tooltip  effect="dark" content="分配角色" placement="top" :enterable="false">
              <el-button type="warning" icon="el-icon-setting" size="mini"></el-button>
            </el-tooltip>
```

# 24 分页

```vue
<!-- 分页导航区域 
@size-change(pagesize改变时触发) 
@current-change(页码发生改变时触发)
:current-page(设置当前页码)
:page-size(设置每页的数据条数)
:total(设置总页数) -->
<el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="queryInfo.pagenum"
      :page-sizes="[1, 2, 5, 10]"
      :page-size="queryInfo.pagesize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total">
    </el-pagination>
```

解析：

- @size-change 绑定方法，每页显示多少条信息
- @current-change  绑定当前页变动时候触发的事件
- :current-page：绑定当前页数
- :page-sizes 显示每页显示多少数据的选项数组
- :pagesize 绑定当前每页显示多少条数据
- layout布局，选择显示什么功能
  - total 显示总共多少条信息
  - sizes 显示选项可以每条显示多少条信息
  - prev，next 上一页下一页
  - jumper 页面跳转
- :total 绑定总数

函数定义：

```js
handleSizeChange(newSize) {
  //pagesize改变时触发，当pagesize发生改变的时候，我们应该
  //以最新的pagesize来请求数据并展示数据
  //   console.log(newSize)
  this.queryInfo.pagesize = newSize;
  //重新按照pagesize发送请求，请求最新的数据
  this.getUserList();  
},
handleCurrentChange( current ) {
  //页码发生改变时触发当current发生改变的时候，我们应该
  //以最新的current页码来请求数据并展示数据
  //   console.log(current)
  this.queryInfo.pagenum = current;
  //重新按照pagenum发送请求，请求最新的数据
  this.getUserList();  
}
```

# 25 Switch开关

绑定`v-model`到一个`Boolean`类型的变量。可以使用`active-color`属性与`inactive-color`属性来设置开关的背景色。

```vue
<el-switch v-model="scope.row.mg_state" @change="userStateChanged(scope.row)"></el-switch>
```

发起状态更改的请求

```js
async userStateChanged(row) {
  //发送请求进行状态修改
  const { data: res } = await this.$http.put(
    `users/${row.id}/state/${row.mg_state}`
  )
  //如果返回状态为异常状态则报错并返回
  if (res.meta.status !== 200) {
    row.mg_state = !row.mg_state
    return this.$message.error('修改状态失败')
  }
  this.$message.success('更新状态成功')
},
```

# 26  Dialog组件

```vue
<!-- 对话框组件  :visible.sync(设置是否显示对话框) width(设置对话框的宽度)
:before-close(在对话框关闭前触发的事件) -->
<el-dialog title="添加用户" :visible.sync="addDialogVisible" width="50%">
    <!-- 对话框主体区域 -->
    <el-form :model="addForm" :rules="addFormRules" ref="addFormRef" label-width="70px">
        <el-form-item label="用户名" prop="username">
            <el-input v-model="addForm.username"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="password">
            <el-input v-model="addForm.password"></el-input>
        </el-form-item>
        <el-form-item label="邮箱" prop="email">
            <el-input v-model="addForm.email"></el-input>
        </el-form-item>
        <el-form-item label="电话" prop="mobile">
            <el-input v-model="addForm.mobile"></el-input>
        </el-form-item>
    </el-form>
    <!-- 对话框底部区域 -->
    <span slot="footer" class="dialog-footer">
        <el-button @click="addDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="addDialogVisible = false">确 定</el-button>
    </span>
</el-dialog>
```

## 添加数据绑定和校验规则

```js
data() {
  //验证邮箱的规则
  var checkEmail = (rule, value, cb) => {
    const regEmail = /^\w+@\w+(\.\w+)+$/
    if (regEmail.test(value)) {
      return cb()
    }
    //返回一个错误提示
    cb(new Error('请输入合法的邮箱'))
  }
  //验证手机号码的规则
  var checkMobile = (rule, value, cb) => {
    const regMobile = /^1[34578]\d{9}$/
    if (regMobile.test(value)) {
      return cb()
    }
    //返回一个错误提示
    cb(new Error('请输入合法的手机号码'))
  }
  return {
    //获取查询用户信息的参数
    queryInfo: {
      // 查询的条件
      query: '',
      // 当前的页数，即页码
      pagenum: 1,
      // 每页显示的数据条数
      pagesize: 2
    },
    //保存请求回来的用户列表数据
    userList: [],
    total: 0,
    //是否显示添加用户弹出窗
    addDialogVisible: false,
    // 添加用户的表单数据
    addForm: {
      username: '',
      password: '',
      email: '',
      mobile: ''
    },
    // 添加表单的验证规则对象
    addFormRules: {
      username: [
        { required: true, message: '请输入用户名称', trigger: 'blur' },
        {
          min: 3,
          max: 10,
          message: '用户名在3~10个字符之间',
          trigger: 'blur'
        }
      ],
      password: [
        { required: true, message: '请输入密码', trigger: 'blur' },
        {
          min: 6,
          max: 15,
          message: '用户名在6~15个字符之间',
          trigger: 'blur'
        }
      ],
      email: [
          { required: true, message: '请输入邮箱', trigger: 'blur' },
          { validator:checkEmail, message: '邮箱格式不正确，请重新输入', trigger: 'blur'}
      ],
      mobile: [
          { required: true, message: '请输入手机号码', trigger: 'blur' },
          { validator:checkMobile, message: '手机号码不正确，请重新输入', trigger: 'blur'}
      ]
    }
  }
}
```

## 关闭对话框，重置表单

给el-dialog添加@close事件，在事件中添加重置表单的代码

```js
methods:{
  ....
  addDialogClosed(){
      //对话框关闭之后，重置表达
      this.$refs.addFormRef.resetFields();
  }
}
```

# 27 删除组件

## 引入MessageBox组件

```
Vue.prototype.$confirm = MessageBox.confirm
```

## 添加事件

```js
async removeUserById(id){
    //弹出确定取消框，是否删除用户
    const confirmResult = await this.$confirm('请问是否要永久删除该用户','删除提示',{
    confirmButtonText:'确认删除',
    cancelButtonText:'取消',
    type:'warning'
    }).catch(err=>err)
    //如果用户点击确认，则confirmResult 为'confirm'
    //如果用户点击取消, 则confirmResult获取的就是catch的错误消息'cancel'
    if(confirmResult != "confirm"){
        return this.$message.info("已经取消删除")
    }
    //发送请求根据id完成删除操作
    const {data:res} = await this.$http.delete('users/'+id)
    //判断如果删除失败，就做提示
    if (res.meta.status !== 200) return this.$message.error('删除用户失败')
    //修改成功的提示
    this.$message.success('删除用户成功')
    //重新请求最新的数据
    this.getUserList()
}
```

# 28 tag组件

通过作用域插槽的形式来自定义他的输出格式

v-if判断输出等级

```vue
<el-table-column label="权限等级" prop="level">
        <template slot-scope="scope">
          <el-tag v-if="scope.row.level === '0'">一级</el-tag>
          <el-tag type="success" v-else-if="scope.row.level === '1'">二级</el-tag>
          <el-tag type="warning" v-else>三级</el-tag>
        </template>
      </el-table-column>
```

# 29 Tree树形控件

使用elelment ui 中的Tree 树形组件

```vue
<el-tree :data="rightList" :props="treeProps"></el-tree>
```

勾选的节点即为权限的id值

默认展开所有结点

将已有权限自动勾选

# 30 级联选择器

控制级联选择框选择范围

# 31 文本框自动获取焦点

```js
 // 点击按钮，展示文本输入框
    showInput (row) {
      row.inputVisible = true
      // 获取文本框dom对象 获得焦点
      // nextTick 当页面上元素被重新渲染后，才会执行回调
      this.$nextTick(_ => {
        this.$refs.saveTagInput.$refs.input.focus()
      })
    }
```



# 32 文本不合法，自动不保存

```js
    // 文本框失去焦点，或摁下了enter都会 触发
    handleInputConfirm (row) {
      if (row.inputValue.trim().length === 0) {
        row.inputValue = ''
        row.inputVisible = false
        return
      }
      // 如果没有return 则做后续处理
```

# 33 处理时间格式问题

1.在main.js中添加过滤器

```js
Vue.filter('dateFormat', function (originVal) {
  const dt = new Date(originVal)
  const y = dt.getFullYear()
  const m = (dt.getMonth() + 1 + '').padStart(2, '0')
  const d = (dt.getDate() + '').padStart(2, '0')
  const hh = (dt.getHours() + '').padStart(2, '0')
  const mm = (dt.getMinutes() + '').padStart(2, '0')
  const ss = (dt.getSeconds() + '').padStart(2, '0')
  return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
})
```

2 渲染表格数据

```vue
<el-table-column  label="创建日期" prop="add_time" width="140px">
<template slot-scope="scope">
{{scope.row.add_time | dateFormat}}
</template>
</el-table-column>
```

# 34 步骤条

# 35 tab栏组件

# 36 图片上传组件

图片的上传、移除、预览

# 37 echarts 插件

# 38 Form表单

- 由输入框、选择器、单选框、多选框等控件组成，用以收集、校验、提交数据

- 在 Form 组件中，每一个表单域由一个 Form-Item 组件构成，表单域中可以放置各种类型的表单控件，包括 Input、Select、Checkbox、Radio、Switch、DatePicker、TimePicker

## 简单代码示例

```vue
<el-form ref="loginFormRef" :rules="loginFormRules" :model="loginForm"  label-width="0px">
<el-form-item label="名称">
    <el-input v-model="loginForm.name"></el-input>
  </el-form-item>
</el-form>
```

## 表单验证

通过 `rules` 属性传入约定的验证规则，并将 Form-Item 的 `prop` 属性设置为需校验的字段名

```js
// 表单的验证规则对象
loginFormRules: {
  // 验证用户名是否合法
  username: [
    { required: true, message: '请输入用户名称', trigger: 'blur' },
    { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
  ],
  // 验证密码是否合法
  password: [
   	{ required: true, message: '请输入登录密码', trigger: 'blur' },
    { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
  ]
}
```

## 预验证

返回true/false

```js
// 点击登录的时候先调用validate方法验证表单内容是否有误
      this.$refs.loginFormRef.validate(async (valid) => {
        if (!valid) return
        const { data: res } = await this.$http.post('login', this.loginForm)
        if (res.meta.status !== 200) return this.$message.error('登录失败！')
        this.$message.success('登录成功')
```



## 属性

### Form Attributes

| 参数        | 说明                                                         | 类型    | 可选值 | 默认值 |
| :---------- | :----------------------------------------------------------- | :------ | :----- | :----- |
| disabled    | 是否禁用该表单内的所有组件。若设置为 true，则表单内组件上的 disabled 属性不再生效 | boolean | —      | false  |
| model       | 表单数据对象                                                 | object  | —      | —      |
| rules       | 表单验证规则                                                 | object  | —      | —      |
| label-width | 表单域标签的宽度，例如 '50px'。作为 Form 直接子元素的 form-item 会继承该值。支持 `auto`。 | string  | —      | —      |

### Form-Item Attributes

| 参数        | 说明                                                         | 类型    | 可选值                            | 默认值 |
| :---------- | :----------------------------------------------------------- | :------ | :-------------------------------- | :----- |
| prop        | 表单域 model 字段，在使用 validate、resetFields 方法的情况下，该属性是必填的 | string  | 传入 Form 组件的 `model` 中的字段 | —      |
| label       | 标签文本                                                     | string  | —                                 | —      |
| label-width | 表单域标签的的宽度，例如 '50px'。支持 `auto`。               | string  | —                                 | —      |
| required    | 是否必填，如不设置，则会根据校验规则自动生成                 | boolean | —                                 | false  |
| rules       | 表单验证规则                                                 | object  | —                                 | —      |

### Form Methods

| 方法名      | 说明                                                         | 参数                                          |
| :---------- | :----------------------------------------------------------- | :-------------------------------------------- |
| validate    | 对整个表单进行校验的方法，参数为一个回调函数。该回调函数会在校验结束后被调用，并传入两个参数：是否校验成功和未通过校验的字段。若不传入回调函数，则会返回一个 promise | Function(callback: Function(boolean, object)) |
| resetFields | 对整个表单进行重置，将所有字段值重置为初始值并移除校验结果   | —                                             |

### Form Events

| 事件名称 | 说明                   | 回调参数                                                   |
| :------- | :--------------------- | :--------------------------------------------------------- |
| validate | 任一表单项被校验后触发 | 被校验的表单项 prop 值，校验是否通过，错误消息（如果存在） |

# 39 NavMenu导航菜单

为网站提供导航功能的菜单。

## 代码示例

```vue
<template>
    <el-container class="home-container">
      <!-- 头部区域 -->
      <el-header>
        <div>
          <!-- 顶部标题 -->
          <span>电商后台管理系统</span>
        </div>
        <el-button type="info" @click="logout"> 退出 </el-button>
      </el-header>
      <!-- 页面主体区域 -->
      <el-container>
        <!-- 侧边栏 -->
        <el-aside width="200px">
          <!-- 侧边栏菜单 -->
          <el-menu
            background-color="#333744"
            text-color="#fff"
            active-text-color="#ffd04b">
            <!-- 一级菜单 -->
            <el-submenu index="1">
              <!-- 一级菜单模板 -->
              <template slot="title">
                <!-- 图标 -->
                <i class="el-icon-location"></i>
                <!-- 文本 -->
                <span>导航一</span>
              </template>
              <!-- 二级子菜单 -->
              <el-menu-item index="1-4-1">
                <!-- 二级菜单模板 -->
                <template slot="title">
                  <!-- 图标 -->
                  <i class="el-icon-location"></i>
                  <!-- 文本 -->
                  <span>子菜单一</span>
                </template>
              </el-menu-item>
            </el-submenu>
            
          </el-menu>
        </el-aside>
        <!-- 主体结构 -->
        <el-main>Main</el-main>
      </el-container>
    </el-container>
</template>
```

**解析**:

- unique-opened 每次只能展开唯一的一项

## Menu Attribute

| 参数                | 说明                                                         | 类型    | 可选值                | 默认值   |
| :------------------ | :----------------------------------------------------------- | :------ | :-------------------- | :------- |
| mode                | 模式                                                         | string  | horizontal / vertical | vertical |
| collapse            | 是否水平折叠收起菜单（仅在 mode 为 vertical 时可用）         | boolean | —                     | false    |
| background-color    | 菜单的背景色（仅支持 hex 格式）                              | string  | —                     | #ffffff  |
| text-color          | 菜单的文字颜色（仅支持 hex 格式）                            | string  | —                     | #303133  |
| active-text-color   | 当前激活菜单的文字颜色（仅支持 hex 格式）                    | string  | —                     | #409EFF  |
| default-active      | 当前激活菜单的 index                                         | string  | —                     | —        |
| router              | 是否使用 vue-router 的模式，启用该模式会在激活导航时以 index 作为 path 进行路由跳转 | boolean | —                     | false    |
| collapse-transition | 是否开启折叠动画                                             | boolean | —                     | true     |

## SubMenu Attribute

| 参数     | 说明     | 类型        | 可选值 | 默认值 |
| :------- | :------- | :---------- | :----- | :----- |
| index    | 唯一标志 | string/null | —      | null   |
| disabled | 是否禁用 | boolean     | —      | false  |

## Menu-Item Attribute

| 参数     | 说明                | 类型    | 可选值 | 默认值 |
| :------- | :------------------ | :------ | :----- | :----- |
| index    | 唯一标志            | string  | —      | —      |
| route    | Vue Router 路径对象 | Object  | —      | —      |
| disabled | 是否禁用            | boolean | —      | false  |

## Menu-Group Attribute

| 参数  | 说明     | 类型   | 可选值 | 默认值 |
| :---- | :------- | :----- | :----- | :----- |
| title | 分组标题 | string | —      | —      |

# 40 Axios请求

# 41 提交到git

```
git branch //查看当前分支
git status //查看当前状态
git checkout -b xxx	//新增子分支
git add .
git commit -m "xxxx描述"
git push -u origin xxx 首次提交到云端
git push // 非首次
git checkout master //切换到主分支
git merge xxx //将xxx子分支合并到主分支
git push
```


