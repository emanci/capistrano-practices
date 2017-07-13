## FAQ

#### 用户验证错误
SSHKit::Runner::ExecuteError: Exception while executing as user@127.0.0.1: git exit status: 128
git stdout: Nothing written
git stderr: Permission denied (publickey,password).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

SSHKit::Command::Failed: git exit status: 128
git stdout: Nothing written
git stderr: Permission denied (publickey,password).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

Tasks: TOP => deploy:check => git:check
(See full trace by running task with --trace)
The deploy has failed with an error: Exception while executing as user@127.0.0.1: git exit status: 128
git stdout: Nothing written
git stderr: Permission denied (publickey,password).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.


** DEPLOY FAILED
** Refer to log/capistrano.log for details. Here are the last 20 lines:

###### 解决方案
Mac OSX 通过 Homebrew 进行安装
```code
brew install ssh-copy-id
```
将私钥加入 ssh-agent 管理
```code
ssh-add id_rsa      # (id_rsa 指的是私钥名称)
```
