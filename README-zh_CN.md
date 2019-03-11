![ghChat](https://user-images.githubusercontent.com/24861316/54087029-11853080-438a-11e9-9607-bc48d3746a70.png)


[English](./README.md) | 简体中文

## ghChat(react版)

之所以叫ghChat，是想着以后做一些GitHub的集成，希望让这个即时通讯工具成为chat tool for github.

目前只支持github授权登录，和展示github用户公开的信息。

### 地址

[github项目地址](https://github.com/aermin/react-chat)。***可以的话给个star支持一下*** 😄


[网站线上地址，支持直接github授权登录](https://im.aermin.top)。

欢迎加入 "ghChat" 这个群交流呀，可搜索群名(不用全打)加入，也可点击机器人的邀请加入(如下图)

![image](https://user-images.githubusercontent.com/24861316/53296199-6337a200-3845-11e9-8435-3f5480cca602.png)




### 技术栈

前端React全家桶，后端node.js(koa2), 数据库MySQL, 双向通信SocKet.io, jwt鉴权等等。具体看package.json哦。

### 目前进度

- 账户

  - [x] 登录
  - [x] 注册
  - [x] 支持github授权登录 
  - [x] 退出登录

- UI
    - [x] 弹窗，提示等基础组件
    - [x] 响应式布局, 适配桌面端和移动端。以前vue-chat的实现只是移动端的布局。

- 私聊

  - [x] 私聊（外加重要的重构）：始化时请求聊天列表所有聊天对象的聊天记录（后期将请求聊天记录的限制为20条聊天内容，避免初始化时间过长），接着根据点击列表导致chatId(取自url params)的改变，重新渲染新的聊天内容。以前vue-chat的实现方式是点击进入每个聊天页面都会发1至多次请求然后渲染页面，性能较差
  - [x] 添加联系人: 搜索到该用户并发送信息后即记录为好友(关系存DB)，会展示在双方的聊天列表
  - [x] 好友资料展示
  - [ ] 删除联系人

- 群聊

  - [x] 群聊 && 重构： 本来是根据消息列表上的群和好友去遍历发HTTP请求拿数据，现在直接在后端整合好一次性用websocket发过来，减少请求次数且websocket在此情况性能更优一些； 完成群聊功能
  - [x] 建群
  - [x] 加群：搜索到该群并点击，会看到当前时间前的聊天记录，点加入按钮后即成功加入群(关系存DB)，开始受到群消息的广播，并且群会展示在聊天列表
  - [x] 群资料展示
  - [x] 退群：退群后聊天列表不再展示该群(DB中删除该关系)
  - [ ] 编辑群资料

- 查询

  - [x] 用户搜索&&群搜索： 支持前端模糊搜索和后端模糊搜索

- 丰富聊天方式

  - [x] 聊天页表： 实时按时间降序展示联系过的人和加入的群
  - [x] 发图
  - [x] 发表情
  - [x] 发文件
  - [x] 下载文件
  - [x] Enter快捷键发送信息,发送按钮灰亮
  - [x] @某人
  - [x] 图片放大查看
  - [ ] 提供在线表情库
  - [ ] 支持Markdown
  - [ ] 支持Quote

- 新消息提示

  - [x] 浏览器桌面通知（生产环境下，使用chrome的桌面通知需要你的网站是HTTPS的）
  - [x] 列表未读数字提示

- 不断的重构和性能优化

  - [x] gzip 压缩
  - [x] 聊天内容懒加载，每次获取20条数据
  - [ ] sql优化

- 其他

  - [x] 机器人智能聊天回复
  - [x] 部署SSL证书
  - [ ] 支持PWA
  - [ ] 后端用TS重写，封装成sdk
  - [ ] CI/CD

### 本地跑项目

1. 项目拉到本地
```
git clone https://github.com/aermin/react-chat.git
```


2. 在react-chat文件夹下创建一个secret.js的空白文件。

如果要使用github授权登录，使用七牛云cdn，生产环境数据库和jwt的secret的单独配置，就要填充相应的配置了。
```
module.exports = {
  client_secret: '', // github授权登录需要的  github-> settings ->  Developer settings 那边生成获取
  db: {
    host: '', // 数据库IP
    port: , // 数据库端口
    database: '', // 数据库名称
    user: '', // 数据库用户名
    password: '', // 数据库密码
  },
  secretValue: '', // json web token 的 secret
  qiniu: { // 七牛云配置
    accessKey: '',
    secretKey: '',
    bucket: ''
  }
};
```

3. 下载前端的npm包
```
cd react-chat
```

```
npm i
```

4. 下载后端的npm包
```
cd cd react-chat/server 
```

```
npm i
```

5. 初始化数据库
```
//需要先在本地建一个名为ghchat的mysql数据库
配置如下看react-chat/server/config.js

npm run init_sql    //然后查看下数据库是否init成功
```

6. 跑起前端和后端的代码
```
npm run start
```

```
cd ..      // 返回到react-chat/目录
```

```
npm run start
```

ps: 本地发图片和发文件和github登录无法使用，需要自己去github和七牛云申请一些东西

### 文档

这边开坑了一篇[ghChat开发历程](https://github.com/aermin/blog/issues/60) ，将不断地更新总结做这个全栈项目时会遇到的问题，知识点，和坑。

### 项目展示：

github对gif图有限制，我就直接截图了，具体详情建议直接[线上体验](https://im.aermin.top)。

![image](https://user-images.githubusercontent.com/24861316/53351929-e1d33300-395c-11e9-84a9-0a9fd793b5a1.png)

![image](https://user-images.githubusercontent.com/24861316/53295822-b3f7cc80-383e-11e9-83b4-82a12bd4a24f.png)

![image](https://user-images.githubusercontent.com/24861316/53296063-eb687800-3842-11e9-9da3-ab1c312c673d.png)

![image](https://user-images.githubusercontent.com/24861316/53296160-afcead80-3844-11e9-9827-4b03303fcd3d.png)

![image](https://user-images.githubusercontent.com/24861316/53351432-4346d200-395c-11e9-936e-e08d887f1355.png)
