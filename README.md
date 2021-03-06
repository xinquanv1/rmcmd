## 1 RMCMD-远程控制、登录、传输便携终端管理器
> 更多远程，更多简单！

单机跑一个程序 、部署一个安装包都是非常简答的工作，可是当你的代码需要在足够多的目标机运行的时候，痛点就来了，他们有可能是：

* 目标机太多，无法不通过软件xshell这类软件记住每一个ip地址的管理信息；
* 需要将环境部署到多个主机，而有些更有可能在docker容器内；
* 希望有时通过一个命令就能很简单的远程执行一个主机甚至执行一堆主机的命令，并且不需要每次都要输入令人厌恶的IP地址或者密码；
* 远程主机信息状态统计、命令批量执行；
* 拷贝文件或者文件夹到多台主机或者反向从多台目标主机拷贝文件；

RMCMD便是我对于自己日常工作中遇到的这个问题的一个解答，我希望通过简单的yaml配置，就再也不需要输入ip地址或者密码就能方便的在一个shell终端执行之前非常痛苦的多机部署、日志拷贝、日志分析、远程状态查看等问题。

> 目标只有一个，最简单的代码实现，以及最少的配置，实现一机安装，多处控制。
>

远程控制指令演示:
```shell script
#### 01-初始命令-这里还有一个关键-首先需要进入目标容器id信息
ssh root@192.168.1.1 "docker exec -i 8bd4dd7ef18a /bin/bash -c 'cd /root/test;pwd;./testcmd'"
#### 02-远程登录简化ip如下所示
rmc cmd --index=7 --value="docker exec -i 8bd4dd7ef18a /bin/bash -c 'cd /root/test;pwd;./testcmd'"
#### 03-有可能你觉得这个命令有点长通过配置文件配置docker关键词后可以简化为
rmc dockercmd --index=7 --value="./testcmd"
#### 04-换成一次性执行100台主机
rmc dockercmd --all --value="./testcmd"
#### 这个工具的目标是--机器愈多，使用越简单！

rmc switch  --file=./file/core-example.yaml --all --roomvid=10000000 --autoadd=60
rmc switch  --file=./file/core-example.yaml --index=1 --roomvid=10000000 --autoadd=60
```


>
>
>
>
>
>