

# Centos中通过Docker安装Jenkins

### 1.下载jenkins镜像
```
docker pull jenkins/jenkins
```

### 2.创建本地jenkins工作目录
```
mkdir -p /root/jenkins    #创建一个本地工作目录
chown -R root:root /root/jenkins
chmod 777 /root/jenkins
```

### 3.运行容器
```
docker run -d -p 8088:8080 -p 8089:50000  -v /root/jenkins:/var/jenkins_home  -v /usr/local/bin/docker:/usr/bin/docker -u 0 -P --name myjenkins jenkins/jenkins
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



---


#### 附：jenkin 前端构建流程

##### 1.判断packege.json文件是否有修改，有则重新安装依赖 没有修改则不用重新安装依赖
```
echo $PATH
node -v
npm -v
#判断package.json md5文件是否存在
if [! -f "package.json.md5" ];then 
    echo "package.json md5值不存在,需要重新安装依赖"    
    #npm install cnpm  --registry https://registry.npm.taobao.org
    rm -rf ./node_modules
    cnpm install 
    echo "依赖安装完成!"
    #把文件的md5值写入到目标文件中
    md5sum package.json>package.json.md5
    echo "package.json md5值已记录"
else  
    echo "package.json md5值已经存在 进行对比..."
fi
 
#检查md5sum是否有变更
if(md5sum -c --status package.json.md5);then
    echo "md5值一致"
else 
    echo "md5值不一致，需要重新安装依赖"
    # 用cnpm安装依赖
    #npm install cnpm  --registry https://registry.npm.taobao.org
    rm -rf ./node_modules
    cnpm install
    echo "依赖安装完成!"
    md5sum package.json>package.json.md5
    echo "package.json md5值已记录"
fi
```

##### 2.build
```
rm -rf ./dist/*

echo "开始打包..."
npm run build
echo "打包完成"
```

##### 3.打包好的静态文件移动至nginx指定资源目录
```
docker exec test /bin/bash -c 'rm -rf /usr/share/nginx/html/*' 
docker cp ./dist test:/usr/share/nginx/html/
docker exec test /bin/bash -c 'mv /usr/share/nginx/html/dist/* /usr/share/nginx/html/' 
```
> 视nginx环境及配置而定 这里是docker环境下的nginx