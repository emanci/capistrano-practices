## Capistrano 部署 PHP 项目（自定义任务）

版本说明，这里使用的是 Capistrano v3

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

因此，可以使用 before/after 把自定义的流程加入到部署的默认流程当中。


```code
未完待续...
```

#### 参考：
[capistrano-handbook](https://github.com/leehambley/capistrano-handbook)
