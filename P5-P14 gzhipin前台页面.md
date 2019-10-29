## P5 项目准备：API接口

### 1. 接口的4个组成部分

###### 接口文档就是这个格式

* url
* 请求方式：post/get 
* 请求参数的格式（类型）
* （服务器返回的）响应数据的格式

### 2. 测试接口、对接口、调接口、联调

###### 这四者是类似的



## P6 项目准备：其他

1. 熟悉一个项目的开发流程
2. 学会**模块化、组件化、工程化**的开发模式
3. create-react-app脚手架初始化react项目
4. node + express（后台路由） + mongoose（操作mongodb数据库） + mongodb 搭建后台开发
5. socket.io 实现实时通信
6. blueimp-md5 对密码进行MD5加密处理
7. js-cookies 操作浏览器端 cookie数据



##  P7 创建项目并运行

### 1. 编码测试

> npm start

### 2. 打包发布

> npm run build  //构建一个包，但没有运行打包后的项目
>
> npm install -g serve  //下载serve服务器，用来运行 打包后的项目
>
> serve build  //进入打包后生成文件夹中，运行打包后的项目

* 访问：5000端口



## P8 项目(前端)源码目录设计

######  在WebStorm中，使用命令行窗口*终止批处理*命令的*快捷键*：Ctrl+C.

<img src="../../前端/我的学习笔记/React项目：硅谷直聘/通用图示（结构、导图）/项目(前端)源码目录设计.png" alt="项目(前端)源码目录设计" style="zoom:67%;" />

## P9 引入antd-mobile

### 1. 踩过的坑

1. antd-mobile中的按需加载

   * config-overrides.js 中的配置，{injectBabelPlugin} 已经失效

     * The "injectBabelPlugin" helper has been deprecated as of v2.0.

     > 解决方法：主要步骤——参照此链接
     >
     > https://github.com/yaoningvital/blog/issues/69
     >
     > ——在不弹出隐藏的配置文件的前提下，怎样实现 antd 的按需加载。
     >
     > > 注：
     > >
     > > 1. libraryName要改成 'antd-mobile'
     > > 2. style: 'css' 改为 style: true。注：true 没有单引号！！
     > >    - 目的是：use less for customized theme

     >解决 **关键字require** 提示报错：Unresolved function or method for require()
     >
     >![解决require提示报错：Unresolved function or method for require()](../../前端/我的学习笔记/React项目：硅谷直聘/解决踩过的坑/解决require提示报错：Unresolved function or method for require().png)

2. 自定义主题

   * 参考antd-mobile中，自定义主题的代码

     > ##### 在项目的根目录处新建config-overrides.js文件（见下图），并把以下代码复制进config-overrides.js中：
     >
     > <img src="../../前端/我的学习笔记/React项目：硅谷直聘/解决踩过的坑/在项目根目录下，新建此文件config-overrides.js.png" alt="在项目根目录下，新建此文件config-overrides.js" style="zoom: 80%;" />
     >
     > ```javascript
     > /* config-overrides.js中，要复制进来的代码
     > *
     > * 主要参考了 antd-mobile中，自定义主题的代码，网址如下：
     > * https://ant.design/docs/react/use-with-create-react-app-cn
     > * 在此网页的：
     > * 	大标题“在 create-react-app 中使用” - “自定义主题” 部分
     > *
     > * */
     > 
     > // addLessLoader 自定义主题的关键字
     > const {override, fixBabelImports,addLessLoader} = require('customize-cra');
     > 
     > module.exports = override(
     >     fixBabelImports('import', {
     >         libraryName: 'antd-mobile',
     >         libraryDirectory: 'es',
     >         /* 原本是style : 'css'，
     >         * 改为 style : true。注意这里的 true 没有单引号！
     >         * 注意这里的 true 没有单引号！
     >         * 注意这里的 true 没有单引号！
     >         *  */
     >         style: true
     >     }),
     >     addLessLoader({
     >             javascriptEnabled: true,
     >             modifyVars: {
     >                 "@brand-primary": "#1cae82",
     >                 "@brand-primary-tap": "#1DA57A"
     >             }
     >     }),
     > );
     > ```
     >
     > 



## P10 引入路由

### 1. 前端路由结构图

<img src="../../前端/我的学习笔记/React项目：硅谷直聘/通用图示（结构、导图）/前端路由结构图.png" alt="前端路由结构图" style="zoom: 67%;" />

### 2. 编码过程

1. 下载路由包：npm install --save react-router-dom
2. 一般情况下，多数路由组件都会与redux交互，所以**将路由组件放在 containers 目录下**

---

1. 定义一级路由组件：注册、登陆、主界面，并在 index.js 中 映射这三个路由组件

   > ```javascript
   > //index.js ——P10版本
   > ReactDOM.render(
   >     /* 注意：路由Main没有指定路径 path
   >     * 问：什么时候 去请求Main组件呢？
   >     * 答：当需要加载 Main下的二级路由组件(如 老板界面、大神界面……)时，
   >     * 需要这样做：先请求(加载)Main组件，然后再加载 Main下的二级路由组件
   >     *  */
   >     ( <HashRouter>
   >         <Switch>
   >             <Route path='/register' component={Register}/>
   >             <Route path='/login' component={Login} />
   >             <Route component={Main} /> {/*默认组件*/}
   >         </Switch>
   >     </HashRouter> ),
   >     document.getElementById('root') );
   > ```



## P11 引入redux

1. 下载相关依赖
   * npm install --save redux react-redux redux-thunk
   * npm install --save-dev redux-devtools-extension

> 详情见代码文件



## P12 register组件：静态组件

> 在gzhipin-client_final目录下的cmd中，npm run 运行此项目：gzhipin-client_final（前台页面），观察它的源码，并试着仿写之

---

> > 在console中奇怪的报错：SyntaxError Unexpected token
> >
> > * 原因：启用某些油猴插件所致
> > * 解决：根据报错信息，关掉相应插件即可
>
> ![在console中奇怪的报错：SyntaxError Unexpected token——启用油猴插件所致，关掉某些插件即可](../../前端/我的学习笔记/React项目：硅谷直聘/解决踩过的坑/在console中奇怪的报错：SyntaxError Unexpected token——启用油猴插件所致，关掉某些插件即可.png)
>
> 
>
> > 解决：根据报错信息，关掉相应插件即可（无报错信息了）
>
> ![解决在console中奇怪的报错：根据报错信息，关掉油猴的相关脚本即可](../../前端/我的学习笔记/React项目：硅谷直聘/解决踩过的坑/解决在console中奇怪的报错：根据报错信息，关掉油猴的相关脚本即可.png)
> 



## P13 register组件：收集表单数据

> 当 route 匹配到 URL 时会渲染一个 route 的组件，路由会在渲染时将以下属性注入组件的props中：
>
> - history
> - location
> - params



## P14 login组件——与Register组件类似，删减部分即可



