### pyenv 简介

pyenv 是 Python 版本管理工具。 pyenv 可以改变全局的 Python 版本，在系统中安装多个版本的 Python， 设置目录级别的 Python 版本，还能创建和管理 virtual python environments。

#### 安装 pyenv

-  安装git：`~]# yum install -y git`
- 安装依赖：`~]# yum install zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel xz xz-devel libffi-devel findutils`
- 添加python用户：`~]# useradd python`
- 安装pyenv： `~]$ curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash`
- 添加环境变量`vim ~/.bashrc`

```
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

#### Pyenv 使用

- 安装指定版本：`pyenv install 3.6.8`
- 离线安装
```
~]$ mkdir .pyenv/cache
~]$ mv Python-3.6.8.tgz  Python-3.6.8.tar.xz  Python-3.6.8.tar.gz .pyenv/cache
~]$ pyenv install 3.6.8
```
- 查看当前的版本：`pyenv version`
- 列出所有的版本：`pyenv versions`
- 设置当前目录及子目录的版本：`pyenv local 3.6.8`

####  Virtualenv

使用插件 virtualenv 创建独立空间，实现模块/包之间的隔离
- 创建虚拟环境：`pyenv virtualenv 3.6.8 py368`
- 使用虚拟环境：`pyenv local py368`