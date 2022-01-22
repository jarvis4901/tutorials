

#Centos中通过Docker安装Jenkins

### 1.下载jenkins镜像
```
docker pull jenkins/jenkins
```

### 2.创建本地jenkins工作目录并赋权
```
mkdir -p /root/jenkins    #创建一个本地工作目录
chmod 777 /root/jenkins
```

### 3.运行容器
```

docker run -d -p 8088:8080 -p 8089:50000 -v /root/jenkins:/var/jenkins_home -v /etc/localtime:/etc/localtime --name myjenkins jenkins/jenkins

#注：将jenkins镜像中的8080、50000端口映射到8088、8089
```

### 4.验证
```
docker ps -l #查看是否启动容器成功

docker logs myjenkins #查看日志
```

### 5.jenkins镜像加速
```
cd /root/jenkins
vi hudson.model.UpdateCenter.xml

#将其中的url 替换成清华大学官方镜像：https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json
```

### 6.访问jenkins页面 ip:8088
