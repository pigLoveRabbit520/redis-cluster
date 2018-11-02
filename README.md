# 使用
1. `docker-compose up -d`启动所有容器
2. `docker-compose exec cli bash`进入cli容器，然后执行命令`redis-cli --cluster create 10.0.0.2:6379 10.0.0.3:6379 10.0.0.4:6379 10.0.0.5:6379 10.0.0.6:6379 10.0.0.7:6379 --cluster-replicas 1`，创建集群
3. `docker-compose exec redis1 redis-cli cluster nodes`查看集群状态


# 说明
* cli容器使用的镜像其实是`redis:5.0`，启动这个容器的目的是为了使用`redis-cli --cluster`，redis5以下，cli不支持`--cluster`选项，cli目录下的二进制文件**app**其实是一个C语言写的无限循环
* 如果不使用静态ip，可以用`--net=host`，配置文件中改不一样的端口，cluster也可以启动。原因是Redis在docker这种模式下`addresses are NAT-ted or because ports are forwarded`。

# 架构图
![cluster](http://dl2.iteye.com/upload/attachment/0127/3625/bd9c5a2f-5d7d-3460-8642-37b143343b2e.jpg)