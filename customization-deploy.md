## Capistrano 部署 PHP 项目（自定义任务）

版本说明，这里使用的是 Capistrano v3，安装或者简单的部署，可以参考 [Capistrano 部署项目（PHP）](https://github.com/emanci/deploy-practices/blob/master/capistrano.md)

#### Capistrano 发布流程
我们想要在 Capistrano 发布流程中添加自定义的任务，那么我们需要先知道这些流程是什么，
当我们运行cap production deploy 时，它会按顺序调用以下任务：
```code
deploy:starting    - start a deployment, make sure everything is ready
deploy:started     - started hook (for custom tasks)
deploy:updating    - update server(s) with a new release
deploy:updated     - updated hook
deploy:publishing  - publish the new release
deploy:published   - published hook
deploy:finishing   - finish the deployment, clean up everything
deploy:finished    - finished hook
```
更多 Flow 介绍，见[这里](http://capistranorb.com/documentation/getting-started/flow)

#### 编写第一个自定义任务
deploy.rb 我们认为是用来配置共用变量和对一些共用 Task 的定义，当然也可以将自定义任务单独拆分出来，放入 tasks 目录中，tasks 目录中的文件都是以 rake 为后缀名的文件。
这里，我以写在 deploy.rb 中为例，简单介绍一下如何自定义 Task
```code
namespace :fuck_you do
  desc "funk you"
  task :fuck do
    puts "Fuck you"
  end

  after 'deploy:started', 'fuck_you:fuck'
end
```

The console will output 'Fuck you'

#### 如何把自定义任务放入 Capistrano 预设任务流
上面已经介绍了，系统默认包含的那些 Task 是按照设定的顺序执行的，因此，在每个 Task 之前和之后都可以通过 before, after 添加自定义的 Task，将自定义的流程加入到部署的默认流程当中。
比如，上面的自定义任务中，
```code
after 'deploy:started', 'fuck_you:fuck'
```
这里我使用了 after，将自定义任务 fuck 放入了 started 之后执行。

```code
未完待续...
```

#### 参考：
 - [capistrano](http://capistranorb.com)
 - [capistrano github](https://github.com/capistrano/capistrano)
 - [capistrano-handbook](https://github.com/leehambley/capistrano-handbook)
