#Docker-Azurefile-Drive-Ansible
使用 Docker Volume 创建 Azurefile 驱动的数据卷，[Azurefile 官方地址](https://github.com/Azure/azurefile-dockervolumedriver)
默认情况下需要先配置 inventory/hosts 添加主机

然后执行命令，进行服务插件的配置及安装
```
$ ansible-playbook -i inventory/hosts step.yml
```
服务启动后创建 Docker Volume ，命令:
```
$ docker volume create -d azurefile --name azurefile -o share=azure-file
$ docker run -d -v azurefile:/data --name busybox busybox ls /data
```
相关介绍 [文章](https://wiki.shileizcc.com/display/DOC/Docker+Volume)
