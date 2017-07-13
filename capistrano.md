## Capistrano 部署 PHP 项目

#### 实践环境:
Aws EC2 Ubuntu x86_64

#### 开始之前

 - 已经成功搭建 PHP 环境
 - 已经成功安装 Git

#### 创建部署用户和组
```code
sudo adduser deployer
```
注意：这里使用的是 adduser, 而不是 useradd. 使用 adduser, 系统会为我们:
 1. 建立一个新目录作为家目录
 2. 建立同名新组
 3. 把用户的主要组设为该组
 4. 建立新用户的密码
 5. etc

#### 安装 Capistrano
```code
gem install capistrano
```

#### 发起 Capistrano
```code
cap install
```
该命令会帮助我们创建一些文件, 它看起来像这样:  

<img src="https://github.com/emanci/deploy-practices/blob/master/capistrano-structure.png" width = "240" alt="structure" align=center />  

##### 配置 deploy.rb
如果要想更好的使用, 可能需要一定的 Ruby 和 Rake 的知识, 但是这里我们就简单的实践, 因此你按照我的配置就能成功.
```code
set :application, "capDemo"
set :repo_url, "git@127.0.0.1:/var/git/demo.git"
set :branch, 'master'
set :deploy_to, "/var/www/html/capDemo"
set :keep_releases, 5
```

##### 配置 production.rb
```code
role :web, %w{deployer@127.0.0.1}
```

#### 执行部署命令
```code
cap production deploy
```
好了, enjoy it.

