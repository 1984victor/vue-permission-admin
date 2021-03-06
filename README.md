
## 简介

vue-permission-admin 是一个后台前端权限管理解决方案，最大特点是权限控制到按钮级别，权限配置方便简单，非开发人员也可以配置。它使用了最新的前端技术栈，动态路由，权限配置，权限验证，它可以帮助你快速搭建后台权限管理。

前端基于: [vue-element-admin](https://panjiachen.github.io/vue-element-admin?_blank)

预览：[Preview](https://zhenglinping.github.io/vue-permission-admin?_blank)

服务端: koa2+mongodb

环境准备


[nodejs](http://nodejs.cn/download/) |
[mongodb](https://www.runoob.com/mongodb/mongodb-window-install.html) |
[redis](https://www.runoob.com/redis/redis-install.html)




## 功能

```
- 登录 / 注销

- 系统配置
  - 用户管理
  - 角色管理
  - 权限列表
  - 按钮配置

- 多环境发布
  - dev sit stage prod

- 全局功能
  - 国际化多语言
  - 多种动态换肤
  - 动态侧边栏（支持多级路由嵌套）
  - 动态面包屑
  - 快捷导航(标签页)
  - Svg Sprite 图标
  - Screenfull全屏
  - 自适应收缩侧边栏


```

## 开发

```bash
# 克隆项目
git clone https://github.com/ZhengLinPing/vue-permission-admin.git

# 进入项目目录
cd vue-permission-admin

# 安装依赖
npm install

# 建议不要直接使用 cnpm 安装依赖，会有各种诡异的 bug。可以通过如下操作解决 npm 下载速度慢的问题
npm install --registry=https://registry.npm.taobao.org

# 启动前端服务
npm run dev


#用本地mock数据可以忽略下面操作 

# 导入数据

先把项目根目录的dbs中的数据导入数据库,在mongodb安装目录的bin目录执行

mongorestore -d koa <path>

# 进入后端服务目录
cd server

# 安装依赖
npm install

# 启动后端服务
npm run dev
```

浏览器访问 http://localhost:9527

## 发布

```bash
# 构建测试环境
npm run build:stage

# 构建生产环境
npm run build:prod
```

## 其它

```bash
# 预览发布环境效果
npm run preview

# 预览发布环境效果 + 静态资源分析
npm run preview -- --report

# 代码格式检查
npm run lint

# 代码格式检查并自动修复
npm run lint -- --fix
```

## 后端权限控制
有人疑问怎么与后端配合控制权限，后端怎么控制接口权限，下面是我用js的描述后端控制接口访问权限的思路,参考一下

```bash

# 用户登录后把用户信息会存到redis，同时把premissions数据洗一下，便于查询

 premissions={
    "user":["query","detail","add","update"],
    "page2":["query","detail"]
  }

# 定义两个常量，与后台配置的"权限"与"按钮"的唯一识别码对应起来
const API_CODE = {
  "LIST":'query',
  "ADD":'add',
  "UPDATE":'update'
}
const MENU_CODE = {
  "USER":'user',
  "ROLE":'role'
}


# 判断权限
const hasPrem = function (token,urlCode,APICode) {
  return loginUser[token].premissions[urlCode].includes(APICode)
}

# 接口方法,例如：用户管理
const urlCode=MENU_CODE.USER 
const user={
    list:function(){
        if(hasPrem(token,urlCode,API_CODE.LIST)){
            return data
        }else{
            return "没有查询权限"
        }
    },
    add:function(){
        if(hasPrem(token,urlCode,API_CODE.ADD)){
            return data
        }else{
            return "没有新增权限"
        }
    }
  
}



```



