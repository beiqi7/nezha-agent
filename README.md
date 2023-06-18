# 容器化的 nezha-agent
[Github主页](https://github.com/Redamancy2319/dockerized-nezha-agent)  
[Dockerhub主页](https://hub.docker.com/r/redamancy2319/nezha-agent)  
因为官方并不提供docker版本的Agent，现学了一点docker和shell写出的小玩具  
由于Docker的特性，***系统版本不能被正确读取，网页终端和定时任务功能无效***  
已在主流Linux系统(Debian11，CentOS7)经过测试，仍有问题可以提出Issue  
***
## 使用教程
#### 一键命令(需要预装Docker环境)
```shell
docker run -d -e panel_domain='<面板域名>' -e port='<面板端口>' -e secret='<节点密钥>' -v /mnt:/mnt/host:ro --net='host' --name='<容器名>' redamancy2319/nezha-agent:latest
```
多开可重复执行上方命令，替换为不同面板的参数
#### 在容器云上手动安装  
##### 必须添加的环境变量  
| 变量名       | 值                  |
| ------------ | ------------------- |
| panel_domain | 面板域名(未接入CDN) |
| secret       | 节点密钥            |  
##### 可选添加的环境变量(不添加则使用默认值)  

| 变量名 | 值                         | 默认值                    |
| ------ | -------------------------- | ------------------------- |
| port   | 面板端口                   | 5555                      |
| args   | nezha-agent 支持的额外参数 | --disable-command-execute |
#### 修改nezha-agent设置  
如果读取网速或硬盘大小出错，可以执行下面命令修改设置  
方向键上下移动光标，方向键左全不选，方向键右全选，空格键单选，回车键确认  
```shell
docker exec -it <容器名> nezha-agent --edit-agent-config
```
网络接口在大部分情况下只需要单独选择eth0，硬盘分区应选择/mnt/host目录
每次修改后都需要重启nezha-agent  
```shell
docker exec -it <容器名> pkill nezha-agent
```
***
## nezha-agent 支持的额外参数    
| 参数                      | 说明                     |
| ------------------------- | ------------------------ |
| -d, --debug               | 开启调试信息             |
| --disable-auto-update     | 禁用自动升级             |
| --disable-command-execute | 禁止在此机器上执行命令   |
| --disable-force-update    | 禁用强制升级             |
| --report-delay int        | 系统状态上报间隔 (默认1) |
| --skip-conn               | 不监控连接数             |
| --skip-procs              | 不监控进程数             |
| --tls                     | 启用SSL/TLS加密          |
***
## 哪吒监控源项目
[官方使用指南](https://nezha.wiki/)
[哪吒监控Github主页](https://github.com/naiba/nezha)
