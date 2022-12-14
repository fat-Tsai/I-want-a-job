# 记录找实习的日子

# DAY1

**后端**

每次写好一个接口，需要重新运行

**前端  CSS cursor属性**

`cursor`属性用来设置光标的类型，在鼠标悬浮在元素上时显示设置的样式

cursor的可选值

1. help 鼠标+有方向的箭头
2. wait 我们常见的加载
3. crosshair 翻译过来为 "十字准线"
4. not-allowed 意思为不允许/禁止
5. zoom-in/zoom-out 放大/缩小 
6. grab 意思为抓，就是我们常见的事件点击鼠标悬浮的样子

详情见https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor

**删除本地分支** `git branch -d 分支名`

**在Vue中使用iconfont（Web+Vue）**

1. 首先点开 iconfont 官网 https://www.iconfont.cn/
2. 找到我的项目，创建一个新项目，并选择好信息
3. 选择自己想要的图标，加入购物车
4. 点开购物车，将图标放置在项目下
5. 打开我的项目，选择下载
6. 解压缩包，除.html外，其余文件全部放置项目中
7. 在Vue中的main.js文件中引入刚刚解压缩的.css文件（这边使用的路径根据你放置的路径来）![image](https://github.com/fat-Tsai/I-want-a-job/blob/main/imgs/1/1-6.png)

8. 在页面中引用，这里使用font-class引用

```javascript
<i class="iconfont xxx"></i>
// 这里使用是 i标签，你也可以使用 span、div标签
// xxx 指的是你项目中的font-class名
```

到这里，就完成了，官网还提供了web端的其他方法和移动端的方法，链接放在这https://www.iconfont.cn/help/detail?spm=a313x.7781069.1998910419.d8cf4382a&helptype=code

**从Vuex中取数据**

我存了用户信息在Vuex中的state中的userInfo和localStorage中
尝试从state取数据，取不到再到localStorage里取

```javascript
方法一：在store中设置getters,再到页面中import、computed、{{getters中的方法名}}
getName:state=> {
  returnJSON.parse(state.userInfo).name
}

方法二：this.$store.state.你要调用的属性
注意点：如果调用的属性是 [Object Object] 记得使用JSON.parse()
```

# DAY2

**前端：如何在requet.js文件中使用路由**

我的需求是用户未登录时，访问后端没有权限，前端响应拦截器需要定向到登录页面

```javascript
// 文件位置 utils/request.js

import axios from 'axios'
import router from '@/router'  // 引入router

const request = axios.create({
	baseURL: '你要访问的网址'
})

// 添加请求拦截器
request.interceptors.request.use(config => {}, error => {})
// 添加响应拦截器
request.interceptors.response.use(res => {
	const code = res.data.code
	const msg = res.data.msg
	if(msg === 'Not login') { // 未登录状态
		router.replace('/login')  // 路由定向到登录页
	} else {
        return res.data
    }
},error => {
    return Promise.reject(error)
})

export default request
```

**管理页面是用动态组件好还是路由跳转好**

![image](https://github.com/fat-Tsai/I-want-a-job/blob/main/imgs/2/2-1.png)

```javascript
/*
	文件位置router/index.js,假设我的一级路由是first,二级路由是second1、second2
*/

import Vue from 'vue'
import Router from 'vue-router'

Vue.use(Router)  // 挂载到Vue实例

const routes = [{
	{ 
		path: '/first',
		compnent: () => import('first页面所在的路径'),
		children: [
			{
				path: '/second1',
				compnent: () => import('second1页面所在的路径'),
			},
			{
				path: '/second2',
				compnent: () => import('second2页面所在的路径'),
			}
		]
	}
}]

const router = new VueRouter({
	routes
})

export default router
```

**使用router-link会出现下划线，如何消除下划线**

![image](https://github.com/fat-Tsai/I-want-a-job/blob/main/imgs/2/2-2.png)

仔细看，会发现有一条很浅的紫色线。这一段的代码简单介绍就是一个被router-link包围的div

```
<router-link v-for="item in menuList" :key="item.id">
	<div>这里面放的子菜单，即XX管理</div>
</router-link>
```

解决方法一： 框架使用Vue，所以我在静态资源assets中放置了一个全局样式表global.css

```javascript
// 全局样式表
html,
body,
#app {
    height: 100%;
    width: 100%;
    margin: 0;
    padding: 0;
}

a {
    text-decoration: none;
}
```

解决方法二： 在页面中写 ```a { text-decoration: none; }``` 。因为router-link标签本质上也是一个a标签

![image](https://github.com/fat-Tsai/I-want-a-job/blob/main/imgs/2/2-3.png)

# DAY3

今天就来总结一下最近笔试遇到的问题吧

**二叉树的性质**

1. 在二叉树的第 i 层上最多有 $2^{i-1}$ 个节点，当 i >=1 时
2. 二叉树深度为 k，那么最多有  $2^k-1$ 个节点
3. 在完全二叉树中，具有 n 个节点的完全二叉树其深度为 $[log_2n]+1$ ，其中 $[log_2n]$ 为向下取整

**二叉树的分类**

满二叉树：每一层的节点都是满的，第 i 层的节点数为 $2^{i-1}$ 个

![image-20220924114502863](C:\Users\asus\AppData\Roaming\Typora\typora-user-images\image-20220924114502863.png)
