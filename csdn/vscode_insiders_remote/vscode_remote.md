

- vscode 
- ssh 
- rmate 

# 安装

## vscode 和插件 (客户端)

- 下载 VSCode Insiders并解压到要安装的目录

- vscode `ctrl+shift+x" 搜索 Remote - SSH 并安装,搜索 Remote VSCode 并安装,

## ssh (客户端/服务端)

### 客户端     

win10    

win+x/应用和功能/管理可选功能/添加功能/Open SSH

linux   

    sudo apt install openssh-client
    ssh-keygen

### 服务端    
    sudo apt install openssh-server


目标:客户端可以通过证书访问服务端

## rmate (服务端)

- 设置 GOPATH 环境变量,把 GOPATH 目录下的 bin (linux 下 $GOPATH/bin)也加入 PATH
- 在那装 rmate, 这里用go版本gomate go get -u -v .....,试下bash中试下 gomate 确保安装成功

# 配置

## vscode (客户端)
`ctrl+shift+p`,搜索 `remote-ssh:open configuration` 打开配置文件 config ,编辑如下

```
Host fws8uv             
    HostName 192.168.43.201
    User fws
    IdentityFile C:\\Users\\fuwens\\.ssh\\id_rsa-ssh-sfw8uv
    ForwardAgent yes
    RemoteForward -R 42698:192.168.43.201:52698
	
#注意 Host 字段是个名字,可以随意起,但最好用字母和数字,
#像 @ 就会会出问题.估计是和 ssh 命令(ssh 用户@主机)冲突
```

效果
```

    vscode                                          rmate
    ssh client                                      ssh server
    192.168.43.191:42698                            192.168.43.201:52698
    --------------------    <=================>    ---------------------
```

 
## rmate (服务端)

gomate /project_dir/rmatefile

配置了工程目录 project_dir ,vscode访问这个目录才能操作文件.

# 使用

正确安装插件后左边边栏多出 Remote SHH 按钮,能打开配置好的远程主机.




# 参考

https://code.visualstudio.com/docs/remote/remote-overview
https://linux.die.net/man/5/ssh_config
https://github.com/aurora/rmate
https://blog.csdn.net/a351945755/article/details/21785647
https://code.visualstudio.com/api/advanced-topics/remote-extension