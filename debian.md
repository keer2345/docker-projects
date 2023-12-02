# Debian
## [Debian系统新建用户，赋予其ROOT权限；Debian系统删除用户](https://blog.csdn.net/weixin_38735917/article/details/133304287)

### Debian系统中添加用户
1. 使用超级管理员账户(`root`)登录，不是超级管理员用户身份的使用 `su` 命令切换到（root）身份。
2. 输入命令 `apt-get install sudo`, "Enter"键后，系统即开始安装sudo
```sh
root@hadoop01:/home/hongpon316# apt-get install sudo
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
sudo is already the newest version (1.9.5p2-3+deb11u1).
0 upgraded, 0 newly installed, 0 to remove and 4 not upgraded.
root@hadoop01:/home/hongpon316#
```
3. 新建名称为 hadoop 的用户
- 方式① ：在root权限下，useradd只是创建了一个用户名，如 （useradd +用户名 ），它并没有在/home目录下创建同名文件夹，也没有创建密码，因此利用这个用户登录系统，是登录不了的，为了避免这样的情况出现，可以用 （useradd -m +用户名）的方式创建，它会在/home目录下创建同名文件夹，然后利用（ passwd + 用户名）为指定的用户名设置密码。
- 方式② ：可以直接利用adduser创建新用户（adduser +用户名）这样在/home目录下会自动创建同名文件夹。




此处选择方式① useradd -m hadoop -s /bin/bash 的新建名为 hadoop 的用户，加上命令/bin/bash就会创建同名文件。

```sh
useradd -m hadoop -s /bin/bash
```

4. 设置登录密码
```sh
passwd hadoop
```

5. 将hadoop加入到sudo组里面
```sh
usermod -aG sudo hadoop
```
用于将用户 "hadoop" 添加到 sudo 组中，以便赋予其 sudo 特权，执行该命令后，用户 "hadoop" 将能够使用 sudo 命令获取 root 权限。

先使用命令之前先查看 cat /etc/sudoers中是否有 hadoop 

6. 验证用户 hadoop的权限
```sh
sudo -l -U test
```

切换到用户 hadoop
```sh
su - hadoop
```

7. 查看hadoop用户所拥有的权限
```sh
hadoop@hadoop01:~$ id hadoop 
uid=1001(hadoop) gid=1001(hadoop) groups=1001(hadoop),27(sudo)
```

### Debian系统中删除用户
```sh
# 查看系统中的所有用户
cat /etc/passwd

# 只查看系统中的所有用户的用户名
awk -F: '{print $1}' /etc/passwd
```

删除系统中的名为hadoop的用户
- ① 如果只想删除用户，但保留其相关的用户目录和文件，可以使用 `userdel` 命令。

- ② 如果想在删除用户的同时删除其相关的用户目录和文件，可以使用 `userdel -r` 命令选项。

一般采用这种方式②删除用户。

```sh
userdel -r hadoop
```

### 回收用户 "hadoop" 的 root 权限 
删除用户之前，如果你给用户分配了 root 权限（通过将其添加到 sudo 组），你可以在删除用户之后通过将其从 sudo 组中移除来回收这些特权。以下是在 Debian 系统中回收用户 "hadoop" 的 root 权限的步骤：
```sh
deluser hadoop sudo
```
注意，这只会回收用户 "hadoop" 在 sudo 组中的特权，而不会删除用户本身。如果你想完全删除用户 "hadoop"，可以使用 userdel 命令，如前面所述。

## Debian 12 上安装 Docker
### Docker
- https://www.jianshu.com/p/3085326d9502
- https://computingforgeeks.com/how-to-install-docker-on-debian-12-bookworm/


控制命令：
- 启动命令： `/etc/init.d/docker start`
- 运行状态： `/etc/init.d/docker status`
- 停止命令： `/etc/init.d/docker stop`
- 重启命令： `/etc/init.d/docker restart`

```sh
# 1、更新系统
apt -y update && sudo apt -y upgrade

# 2、添加Docker的官方稳定存储库
# 为了能够安装 Docker 和所有必需的软件包，我们需要将官方存储库添加到我们的 Debian 12 系统中。我们将从安装所需的软件包开始：

apt install lsb-release gnupg2 apt-transport-https ca-certificates curl software-properties-common -y



# 导入 Docker 存储库的 GPG 密钥：

curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/debian.gpg


# 现在添加 Docker 稳定存储库：

add-apt-repository "deb [arch=$(dpkg --print-architecture)] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

# 3、Debian 12 安装Docker CE（Bookworm）
# 添加存储库后，您可以使用以下命令在 Debian 12 (Bookworm) 上继续安装 Docker：

apt update
apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin

sudo usermod -aG docker $USER
sudo systemctl start docker && sudo systemctl enable docker
sudo systemctl status docker
sudo docker version
sudo docker info
sudo docker login
```
### Docker-compose
```
sudo apt install docker-compose -y
docker-compose --version
```
