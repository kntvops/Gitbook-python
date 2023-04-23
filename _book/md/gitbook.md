## gitbook安装

- 1. 安装 [Node.js](https://mirrors.tuna.tsinghua.edu.cn/nodejs-release/v6.14.1/node-v6.14.1-x64.msi)

```
$ node -v
v6.14.1
$ npm -v
3.10.10

```

- 2. 安装 gitbook

```
$ npm install -g gitbook-cli
$ gitbook -V # 第一次执行此命令时自动安装gitbook库，以后就直接使用
CLI version: 2.3.2
GitBook version: 3.2.3

# 如安装不成功，卸载可用
npm uninstall -g gitbook
```

## gitbook使用

- 新建目录，终端进入新建目录
- 创建gitbook文档：`gitbook init`（新建目录后只能执行一次，第一次执行命令会联网下载gitbook）
- 预览：`gitbook serve`，关闭预览`ctrl+c`
  生成HTML文档：`gitbook build --gitbook=2.6.7`（第一次执行会联网下载包）之所以不用gitbook build是因为最新版gitbook生成的HTML文档静态情况下链接不能点击跳转


