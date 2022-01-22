

# Centos中通过Docker安装Jenkins

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

MIIEogIBAAKCAQEApP6s3wR7kN4pRPOFl0VdTXYQKv15a7REJKNASiWhMogFL3Od
xhhAkdnR0Sfq9zHANGLa2zuL6xYlpur4A10EFtVKaZsyhpxUu+FHCtxNnFeV+Hyx
TVTOsio1dKWmQcdpLTLGzIFH4HNEpM6rqjkeIr42qYeSe1ROI2tKs1BBC9FHOe+w
jBHCIhoblXp7fakrOWledsZjT9fqGgrYOcTv3kvttMCYb0EVuRzorAmNE7ZK7tmc
+1heJcYP8UrEkRPgCqH//XLreYQ37djlXzggqC8nRWz9fc4utf6luEn9KqXSNxy/
fiG9mvdzh0fCyOfnblWjVBU60VczoiHwnQDOgQIDAQABAoIBAG7bUkkxmNg3/GCA
gjSl/U9rUOehkPBFmTdInIx1Bf6Ol3VPaCVN7CxSvn+aI2vc+Hf6J3P/aT4Vjky9
ONABshqpSir0hJke9muZrALnDBpMWs4u8W202n+ojmwGVFOD6O3eXOXQwvtSVz+o
QHzJja7oQI/dMBU/CpUPpIwgEuQdrzouPrECXl+IQymaxtSDZUgimBetL8QdGBfE
lh1YMfyI9FMjezSFSaAnakLnFhB8tee3d/oVykwTk2Zp0Yq9bmRM0io2nKsoI7u9
BG9M46u7p0b85vVe9lUZWobc7snuZiJ32kw05zq9A7opiyPDvq6hTViIKgvhYWu3
fHZZDzECgYEA1IXKwF2FX9rd6jAuoFXt7K8oUeHTxPfFjUOJvRLRxNmhnjTxjHfi
cdzsAhMoiAi6CqdqcRw1WJWzrqiAq8SwN+5jCdQijI0o0u5QOlMPfQQT5Y9Dvg/D
WPDcVckgSZyiymGqeg4oLys+ZuacQd3A3C2s+3e/SZT1noXPqGZubQ0CgYEAxr/D
bHlavkbZBEl6P3KfrqIdX8yeh9k+eI2eSUv+Zf7FOTnYrCSTOamL7ORGwwMS9SUA
rPhaSqA9o0zjDNAXxKJu+yTE0oPX0pPqaLuzCxC36PizAyx/bVj/r/K/UnV59qwR
yVLXMbVCs1IK0El8/i5Q+MdGbAAQ7PH91Fg8kkUCgYByEybTvt9apna7wAUnFzjQ
9Owll5w+e+jUfM4waSukCFWSQETv62HnUHh2XKZC7rw9/8NI16Vi2WhLdjMrADa+
rv0GR5IL87FYF4eE5xTHPCsZ656nJHrtAMykV4M3QBa5n1cMkRDM0N98CIkTad6d
0P6rNIm/C3AUGStv7xuS+QKBgEqC9kcisAyKDy52Rain1onoKU8TLZQMtEkJ/v/H
x9aBT3uG3l6bT77ce6MSah0Od/sEJl6ytVcpADLKzoytL1v+8dCiFlA+MZm27rjZ
NeS+HdTv+F0GP7fFGAbk4SmO9WyvUfPCZP8zz4/fAELaakv5HU5Hl3VCCRZsGxeT
BRJpAoGAe3e46yjJZxP6wrV2pX6oyEB+PLwj/06Yf2tNTDtvKHzSVvzAQj/IeRL/
R1gSAkNhbOhdOLISK96lyM0GmzLRo8u6WdTWB6lWii65w90QAMXbOm4GmGtwv6qj
ndIGhl/zNgzjf1OaIfY/afyOagZRb+ZZiSPFCU4sag7Eczd4Osw=

### 6.访问jenkins页面 ip:8088
