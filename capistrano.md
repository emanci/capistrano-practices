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
另外, 还有两个比较重要的配置项
```code
# linked_dirs
append :linked_dirs, "tmp/sockets"
# or
set :linked_dirs, fetch(:linked_dirs, []).push('public/images', 'logs', 'tmp/pids')
# linked_files
append :linked_files, "config/database.yml"
# or
set :linked_files, fetch(:linked_files, []).push('.env')
```
Capistrano 每次部署会更新所有的文件和文件夹，但是有时候有些东西我并不想让它每次都更新。又比如生产环境的很多配置, 比如数据库配置或者其他一些敏感信息的配置是不会加入到版本库中，因此在生产环境配置后无需更改。那么我们就可以使用 linked_dirs 和 linked_files 这两个配置项。所不同的是，linked_dirs 是针对文件夹，而 linked_files 是针对某个文件或某些文件，这就保证了每次部署这些文件/文件夹都不会被更新。

##### 配置 production.rb
```code
role :web, %w{deployer@127.0.0.1}
```

#### 执行部署命令
```code
cap production deploy
```

经过多次部署后, 服务器会生成一个这样的目录结构:  

<img src="https://github.com/emanci/deploy-practices/blob/master/server-directory.png" width = "240" alt="structure" align=center />  

*  current 是指当前版本, link 到 releases 下的指定版本目录(默认为最新的 releases)
*  releases 每次部署都会产成一个目录存放项目源码, 目录个数由 :keep_releases 变量来控制
*  repo 项目的 .git 目录
*  shared 是项目中共享的内容, 不会随部署而改变

好了, Just enjoy it.
