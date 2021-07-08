## Vant

​		Vant 是**有赞前端团队**开源的移动端组件库，于 2017 年开源，已持续维护 4 年时间。Vant 对内承载了有赞所有核心业务，对外服务十多万开发者，是业界主流的移动端组件库之一。

​		https://vant-contrib.gitee.io/vant/#/zh-CN/home



## 安装使用

1.可以直接通过 vue add vant指令安装配置，过程类似vue add element

2.通过npm i vant -S指令安装，安装后再main.js中进行配置

```js
import Vue from 'vue';
import Vant from 'vant';
import 'vant/lib/index.css';

Vue.use(Vant);
```

安装成功后可直接调用相应的组件



App基本架构地址：https://gitee.com/zachgmytea/briup-ej-app.git



## 项目基本结构

### src/App.vue

项目全局根组件，只显示<router-view></router-view>即可，其余路由跳转配置在Manager.vue中。

```vue
<template>
  <div id="app">
    <!-- 全局根组件 -->
    <!-- 只显示一个routerview 即可 -->
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: "app",
};
</script>

<style>
/* 获取父元素高度 */
html,body,#app{
 height: 100%;
}
</style>

```

### src/router/index.js

路由配置文件，将基本的页面路由进行配置

```js
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)
// 防止路由重复点击报错
const originalPush = VueRouter.prototype.push
VueRouter.prototype.push = function push(location) {
  return originalPush.call(this, location).catch(err => err)
}

const routes = [
  // 默认加载界面 ， 重定向页面
  {
    path: '/',
    redirect: '/login'
  },
  // 登录页面界面
  {
    path: '/login',
    name: 'Login',
    component: () => import('@/views/Login.vue')
  },
  // 注册页面路由
  {
    path: '/register',
    name: 'Register',
    component: () => import('@/views/Register.vue')
  },
  // 总路由
  {
    path: '/manager',
    name: 'manager',
    component: () => import('@/views/Manager.vue'),
  },
]

const router = new VueRouter({
  // mode: 'history',
  base: process.env.BASE_URL,
  routes
})

// 路由守卫 判断有无token
// 使用 router.beforeEach 注册一个全局前置守卫，判断用户是否登陆
router.beforeEach((to, from, next) => {
  //若要跳转的页面是登录界面
  if (to.path === '/login') {
    //直接跳转
    next();
  } else { //若想要跳转其他页面
    //获取本地存储的token值
    let token = localStorage.getItem('token');
    //若token为空则验证不成功，跳转到登录页面
    if (token === 'null' || token === '') {
      next('/login');
    } else {
      next();
    }
  }
});

export default router
```

### src/views/Manager.vue

管理者页面，在此配置App的tabbar，控制底部导航跳转

```vue
<template>
  <div class="manager">
    <!-- 用于接受管理页面，首页，订单页，我的页面 -->
    我是管理页面
  </div>
</template>

<script>
export default {
  data() {
    return {
      active: 0,
    };
  },
};
</script>

<style scoped>
</style>
```

### src/views/Login.vue

登录页面，登录页面样式以及登录操作的实现

```vue
<template>
  <div class="login">
    <!-- 头部信息展示区 -->
    <div class="header">
      <div class="title">
        易洁家政
      </div>
    </div>
    <!-- 登录区域 -->
    <div class="loginArea">
      <div class="loginForm">
        <van-form @submit="onSubmit">
          <van-field
            v-model="username"
            name="用户名"
            label="用户名"
            placeholder="用户名"
            :rules="[{ required: true, message: '请填写用户名' }]"
            size="large"
          />
          <van-field
            v-model="password"
            type="password"
            name="密码"
            label="密码"
            placeholder="密码"
            :rules="[{ required: true, message: '请填写密码' }]"
            size="large"
          />
          <div style="margin: 16px">
            <van-button color="linear-gradient(to right, #5098fa, #265aca)" round block type="info" native-type="submit">
            提交
            </van-button>
          </div>
          <div class="signUp">
            <span @click="toRegister">没有账号？点击注册</span>
          </div>
        </van-form>
      </div>
    </div>
  </div>
</template>

<script>
// 引入辅助函数
import { mapMutations } from 'vuex'
// 异步加载  引入axios
import { post_json } from '@/http/axios'
import { Toast } from 'vant';

export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    // 引入vuex中的mutations
    ...mapMutations('user',['setToken']),
    // 登录
    async onSubmit(values) {
      // 配置参数
      let params = {
        username: this.username,
        password: this.password,
      }
      // 发送登录验证请求
      let res = await post_json('/user/login', params)
      // console.log(res);
      if (res.data.status == 200) {
        // 保存token
        this.setToken({token: res.data.data.token});
        // 跳转到首页
        this.$router.push('/manager')
      }else{
        // 提示错误信息
        Toast(res.data.message);
      }
    },
    // 跳转到注册
    toRegister(){
      this.$router.push('/register')
    }
  },
};
</script>

<style scoped>
/* 整体样式 */
.login {
  width: 100%;
  height: 100%;
  background-image: linear-gradient(#5098fa, #265aca);
  overflow: hidden;
}
/* 头部样式 */
.header{
  width: 100%;
  position: absolute;
  text-align: center;
  top: 120px;
}
/* 标题样式 */
.header .title{
  font-family: 'webfont';
  font-size: 40px;
  color: white;
}
@font-face {
  font-family: 'webfont';
  font-display: swap;
  src: url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.eot'); /* IE9*/
  src: url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
  url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.woff2') format('woff2'),
  url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.woff') format('woff'), /* chrome、firefox */
  url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
  url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.svg#AlibabaPuHuiTiH') format('svg'); /* iOS 4.1- */
}
/* 中间登录输入区域 卡片样式 */
.loginArea {
  box-shadow: 0 4px 8px 0 rgba(255, 255, 255, 0.2);
  background-color: white;
  transition: 0.3s;
  width: 90%;
  border-radius: 5px;
  margin: 265px auto;
  height: 250px;
  padding: 10px;
}
.loginArea:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}
/* 输入框整体样式 */
.loginForm{
  padding-top: 20px;
}
/* 注册样式 */
.signUp{
  color: #4E95F7;
  text-align: center;
}
</style>

```

### src/views/Register.vue

注册页面，注册页面样式以及注册操作的实现

```vue
<template>
  <div class="login">
    <!-- 头部信息展示区 -->
    <div class="header">
      <div class="title">
        易洁家政
      </div>
    </div>
    <!-- 登录区域 -->
    <div class="loginArea">
      <div class="loginForm">
        <van-form @submit="onSubmit">
          <van-field
            v-model="username"
            name="用户名"
            label="用户名"
            placeholder="用户名"
            :rules="[{ required: true, message: '请填写用户名' }]"
            size="large"
          />
          <van-field
            v-model="password"
            type="password"
            name="密码"
            label="密码"
            placeholder="密码"
            :rules="[{ required: true, message: '请填写密码' }]"
            size="large"
          />
          <van-field
            v-model="confirmPwd"
            type="password"
            name="确认密码"
            label="确认密码"
            placeholder="确认密码"
            :rules="[{ required: true, message: '请再次输入密码' }]"
            size="large"
          />
          <div style="margin: 16px">
            <van-button color="linear-gradient(to right, #5098fa, #265aca)" round block type="info" native-type="submit">
            注册
            </van-button>
          </div>
          <div class="signUp">
            <span @click="toLogin">已有账号，去登录</span>
          </div>
        </van-form>
      </div>
    </div>
  </div>
</template>

<script>
// 引入辅助函数
import { mapMutations, mapActions } from 'vuex'
// 异步加载  引入axios
import { post } from '@/http/axios'
import { Toast } from 'vant';

export default {
  data() {
    return {
      username: "",
      password: "",
      confirmPwd:''
    };
  },
  methods: {
    ...mapActions('register', ['toRegister']),
    onClickLeft() {
      this.$router.go(-1);
    },
    onSubmit(){
      if (this.password != this.confirmPwd) {
        Toast('两次密码输入不一致,请重新输入！');
      }else{
        // 获取注册参数
        let params = {
          username: this.username,
          password: this.password,
        }
        // 调用注册请求
        this.toRegister(params)
        Toast('注册成功')
        setTimeout(() => {
          this.$router.go(-1)
        }, 1500);
      }
    },
    // 跳转到登录
    toLogin(){
      this.$router.push('/login')
    }
  },
};
</script>

<style scoped>
/* 整体样式 */
.login {
  width: 100%;
  height: 100%;
  background-image: linear-gradient(#5098fa, #265aca);
  overflow: hidden;
}
/* 头部样式 */
.header{
  width: 100%;
  position: absolute;
  text-align: center;
  top: 120px;
}
/* 标题样式 */
.header .title{
  font-family: 'webfont';
  font-size: 40px;
  color: white;
}
.header .title_bottom {
  color: #fff;
  font-family: 'webfont';
  font-size: 20px;
}
@font-face {
  font-family: 'webfont';
  font-display: swap;
  src: url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.eot'); /* IE9*/
  src: url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
  url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.woff2') format('woff2'),
  url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.woff') format('woff'), /* chrome、firefox */
  url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
  url('//at.alicdn.com/t/webfont_mtjyk0oq5ef.svg#AlibabaPuHuiTiH') format('svg'); /* iOS 4.1- */
}
/* 中间登录输入区域 卡片样式 */
.loginArea {
  box-shadow: 0 4px 8px 0 rgba(255, 255, 255, 0.2);
  background-color: white;
  transition: 0.3s;
  width: 90%;
  border-radius: 5px;
  margin: 265px auto;
  height: 250px;
  padding: 10px;
}
.loginArea:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}
/* 输入框整体样式 */
.loginForm{
  padding-top: 20px;
}
/* 注册样式 */
.signUp{
  color: #4E95F7;
  text-align: center;
  font-size: 12px;
  letter-spacing: .05em;
  cursor: pointer;
}
</style>

```

### src/http/axios.js

项目封装axios文件，将接口地址更改为自己的可直接使用

```js
import axios from 'axios'
import router from '../router/index'
import Vue from 'vue';
import { Toast } from 'vant';
import qs from 'qs'

Vue.use(Toast);

let token = '';
// 1. 基础路径 配置为自己的服务器地址
axios.defaults.baseURL = 'http://8.134.121.225:8002/'
//配置请求头
axios.defaults.headers.post['Content-Type'] = 'application/json';

// http request拦截器 添加一个请求拦截器
axios.interceptors.request.use(function (config) {
  let token = localStorage.getItem("token")
  if (token) {
    //将token放到请求头发送给服务器,将token放在请求头中
    config.headers['Authorization'] = token
  }
  return config;
}, function (error) {
  Toast.fail('请求超时');
  // Do something with request error
  return Promise.reject(error);
});

// 添加一个响应拦截器
axios.interceptors.response.use(function (response) {
  return response;
}, function (error) {
  Toast.fail("服务器连接失败");
  return Promise.reject(error);
})

/**
  get方式请求
*/
export function get(url, params) {
  return axios({
    method: 'get',
    url,
    params, // get 请求时带的参数
    timeout: 5000
  })
}

/**
 * 提交post请求 发送的数据为查询字符串，key=val&key=val
*/
export function post(url, data) {
  return axios({
    method: "post",
    url,
    data: qs.stringify(data),
    timeout: 5000,
    headers: {
      'Content-Type': 'application/x-www-form-urlencoded'
    }
  })
}

/**
 * 提交post请求 ,查询字符串，对象中嵌套数组的格式
*/
export function post_obj_array(url, data) {
  return axios({
    method: "post",
    url,
    data: qs.stringify(data, { allowDots: true }),
    timeout: 5000
  })
}

/**
 * 提交post请求 发送的数据为查询字符串，当参数为数组的时候适用该方法
 * ids=1&ids=2
*/
export function post_array(url, data) {
  return axios({
    method: "post",
    url,
    data: qs.stringify(data, { arrayFormat: "repeat" }),
    timeout: 5000
  })
}
/**
 * 提交post请求 发送的数据为json字符串
*/
export function post_json(url, data) {
  return axios({
    method: "post",
    url,
    data,
    timeout: 5000
  })
}

export default axios
```



## 可能会用到的

#### 渐变色使用方式

##### background-image: linear-gradient(#5098fa, #265aca);

#### 卡片阴影样式

##### box-shadow: 0 0 0 0 rgba(255, 255, 255, 0.2);

渐变色网站

https://uigradients.com/#BlurryBeach

https://mycolor.space/

https://webgradients.com



## 接口

### app-顾客端

### 登录，注册，退出接口

![image-20210630212535225](/Users/Zach/Library/Application Support/typora-user-images/image-20210630212535225.png)

## 首页

##### 轮播图

![image-20210630231358660](/Users/Zach/Library/Application Support/typora-user-images/image-20210630231358660.png)

##### 栏目菜单 

![image-20210630212737007](/Users/Zach/Library/Application Support/typora-user-images/image-20210630212737007.png)

##### 产品展示

![image-20210630212839129](/Users/Zach/Library/Application Support/typora-user-images/image-20210630212839129.png)

## 服务产品页面

#### 侧边导航栏

![image-20210630212737007](/Users/Zach/Library/Application Support/typora-user-images/image-20210630212737007.png)

#### 根据点击导航栏获取产品数据

![image-20210630213547889](/Users/Zach/Library/Application Support/typora-user-images/image-20210630213547889.png)

## 订单确认页面

#### 地址相关信息

![image-20210630213834860](/Users/Zach/Library/Application Support/typora-user-images/image-20210630213834860.png)

#### 用户相关信息

![image-20210630213914004](/Users/Zach/Library/Application Support/typora-user-images/image-20210630213914004.png)

#### 提交订单

![image-20210630214025215](/Users/Zach/Library/Application Support/typora-user-images/image-20210630214025215.png)

#### 余额充值

![image-20210630214121925](/Users/Zach/Library/Application Support/typora-user-images/image-20210630214121925.png)

## 订单界面

#### 所有状态订单查询，订单详情等接口

![image-20210630233619375](/Users/Zach/Library/Application Support/typora-user-images/image-20210630233619375.png)

## 帮助页面

此页面目前只是一个假数据展示页面，可自定义



## 我的页面

#### 用户个人信息

![image-20210630213914004](/Users/Zach/Library/Application Support/typora-user-images/image-20210630213914004.png)

#### 充值

![image-20210630214121925](/Users/Zach/Library/Application Support/typora-user-images/image-20210630214121925.png)

## 常用地址页面

#### 地址查询

![image-20210630214705247](/Users/Zach/Library/Application Support/typora-user-images/image-20210630214705247.png)

#### 新增地址

![image-20210630214754646](/Users/Zach/Library/Application Support/typora-user-images/image-20210630214754646.png)