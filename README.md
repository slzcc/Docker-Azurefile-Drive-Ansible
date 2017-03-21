#Docker-Azurefile-Drive-Ansible

使用 Docker Volume 创建 Azurefile 驱动的数据卷，[Azurefile 官方地址](https://github.com/Azure/azurefile-dockervolumedriver)
默认情况下需要先配置 inventory/hosts 添加主机

然后执行命令，进行服务插件的配置及安装
```
$ ansible-playbook -i inventory/hosts step.yml
```
执行后进入交互模式让你填入 Azure 存储账户认证环节，简单进行变量的介绍：
```
AZURE_STORAGE_BASE 为 Azure 地区地址，默认是中国地区，其他区域看官方介绍，在模板中有 global 地址
AZURE_STORAGE_ACCOUNT 为 Azure 存储账号名称
AZURE_STORAGE_ACCOUNT_KEY 为 Azure 存储账户授权秘钥
```
服务启动后创建 Docker Volume ，命令:
```
$ docker volume create -d azurefile --name azurefile -o share=azure-file
$ docker run -d -v azurefile:/data --name busybox busybox ls /data
```
相关介绍请转至 [Wiki 地址](https://wiki.shileizcc.com/display/DOC/Docker+Volume)。
此案例需要使用 Systemd 服务，且使用 Ubuntu 系统，如果需要使用 Redhat 系统请修改执行 Ansible Playbook 文件内的 apt 为 yum 即可。
