# Docker官方安装包

2024年6月以来，大量Docker镜像网站停服，Docker无法下载安装<br>
本仓库致力于解决国内网络原因无法使用Docker的问题。<br>

### 特点：
- 使用Github Action将官网的安装脚本/安装包定时下载到本项目Release，供国内使用<br>
- 官方安装包，安全可靠<br>
- 每天定时同步，保证最新<br>

作者：[JamesCVBN](https://github.com/jamescvbn)、[技术爬爬虾](https://github.com/tech-shrimp/me)<br>
转载请注明作者<br>

# 1. Docker安装
## 1.1 Linux
一键安装命令
```
sudo curl -fsSL https://github.com/jamescvbn/docker_installer/releases/download/latest/linux.sh| bash -s docker --mirror Aliyun
```

启动docker
```
sudo service docker start
```

## 1.2 Windows
任务栏搜索功能，启用"适用于Linux的Windows子系统" + "虚拟机平台" <br>
![](images/windows功能.png)

管理员权限打开命令提示符，安装wsl2<br>
```
wsl --set-default-version 2
wsl --update --web-download
```
等待wsl安装成功
![](images/wsl2成功.png)
下载Windows版本安装包，进入此项目的Release<br>
https://github.com/jamescvbn/docker_installer/releases

下载Windows版本安装包
![](images/windows安装包.png)
双击安装即可

>可选:
如果想自己指定安装目录，可以使用命令行的方式
参数 --installation-dir=D:\Docker可以指定安装位置


```
start /w "" "Docker Desktop Installer.exe" install --installation-dir=D:\Docker
```

## 1.3 Mac
进入此项目的Release，下载Mac系统的安装包<br>
https://github.com/jamescvbn/docker_installer/releases
![](images/mac安装包.png)
注意区分CPU架构类型 Intel芯片选择x86_64, 苹果芯片选择arm64<br>
下载好双击安装即可

# 2. Pull镜像

### 方案一 使用Cloudflare worker 自建镜像加速或使用现有镜像站
https://github.com/jamescvbn/CF-Workers-docker.io

当前可用镜像站包括https://docker.m.daocloud.io、https://docker.1panel.live。若失效，可根据[第三方 DockerHub 镜像服务](https://github.com/jamescvbn/CF-Workers-docker.io?tab=readme-ov-file#%E7%AC%AC%E4%B8%89%E6%96%B9-dockerhub-%E9%95%9C%E5%83%8F%E6%9C%8D%E5%8A%A1)替换。


#### Linux配置镜像站
```
sudo vi /etc/docker/daemon.json
```
输入下列内容，最后按ESC，输入 :wq! 保存退出。
```
{
  "registry-mirrors": [
    "https://docker.m.daocloud.io",
    "https://docker.1panel.live"
  ]
}
```
重启docker
```
sudo service docker restart
```

### Windows/Mac配置镜像站
Setting->Docker Engine->添加上换源的那一段，如下图
![](images/win加速.png)

### 方案二 离线镜像
使用Github Action下载docker离线镜像
https://github.com/wukongdaily/DockerTarBuilder

### 方案三 使用一键脚本
bash -c "$(curl -sSLf https://xy.ggbond.org/xy/docker_pull.sh)" -s 完整镜像名

# 3. 去哪里找镜像

https://docker.fxxk.dedyn.io/