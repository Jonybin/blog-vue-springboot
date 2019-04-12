
Vue + SpringBoot实现的博客系统

# 写在前面

声明：本系统是从 <a href="https://github.com/shimh-develop/blog-vue-springboot"> shimh大神</a> fork 下来的开源项目。作用于毕业设计。在此基础上，进行设计开发。旨在打造一个类似简书，csdn这种。分享类博客系统。

关于更多信息，请访问大神源码。进行fork，stars.


# 技术

## 前端  blog-app

- Vue
- Vue-router
- Vuex
- ElementUI
- mavon-editor
- lodash
- axios
- Webpack

## 后端  blog-api

- SpringBoot
- Shiro
- Jpa
- Redis
- Fastjson
- Druid
- MySQL
- Maven

# 实现功能

## 整体

- 用户：登录 注册 退出
- 首页：文章列表、最热标签、最新文章、最热文章
- 文章分类-标签：列表、详情
- 文章归档
- 文章：写文章、文章详情
- 评论：文章添加评论 对评论回复
- 文章列表滑动分页

## 后端
- 用户、文章、文章分类、标签和评论 增删改查api接口
- 基于token权限控制
- Redis存储Session
- 全局异常处理
- 操作日志记录

# 待实现功能
- 评论的分页 点赞
- 留言板
- 第三方登录
- ......

# 运行

将项目clone到本地

## 方式一  直接运行SpringBoot项目（已将打包的静态文件放到了 resources/static下）
1. 将blog-api导入到IDE工具中

<font color="red" size="3"> 注意：</font> </br>

a：注意自己的jdk版本号，是不是跟pom.xml指定的版本号一致。
该项目下的jdk版本号为：1.8
```
<java.version>1.8</java.version>
```
b：数据库版本问题
同样是pom.xml配置
```
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>8.0.15</version>
    </dependency> 
```
我这里把数据库配置改成自己电脑配置的mysql版本号。

2. resources/sql/blog-schema.sql、blog-data.sql导入MySQL数据库
3. 打开Redis数据库
4. resources/application.properties 修改MySQL、Redis连接
5. Runas运行,访问：http://localhost:8888

## 方式二  前后分离（开发方式）
1. 按方式一运行blog-api，提供api数据接口
2. 打开命令行
	> cd blog-app

	> npm install

	> npm run dev

3. 访问：http://localhost:8080
4. 修改blog-app/src 下的文件进行开发
5. npm run build 生成最终静态文件




