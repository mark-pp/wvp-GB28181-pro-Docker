# wvp-GB28181-pro-Docker

源项目地址为<https://github.com/648540858/wvp-GB28181-pro>，这里只是做了docker镜像和编排。

## 使用方法：

### 第一步 拉文件
```bash
git clone https://github.com/mark-pp/wvp-GB28181-pro-Docker.git
```

### 第二步 创建HTTPS测试证书
```bash
cd wvp-GB28181-pro-Docker/tools
chmod -R 777 ssl.sh
./ssl.sh
```
这里创建证书需要使用到`keytool`，请自行安装OpenJDK。

### 第三步 修改编排文件
```bash
cd ..
vim docker-compose.yml
```
这里`WVP_HOST`改成自己的公网IP地址，别的按需要修改。

### 第四步 修改ZLMediaKit config文件
```bash
cd zlmediakit/config
vim config.ini
```
这里将配置文件中的ip地址更改为自己服务器的IP地址。

### 第五步 修改最新的sql脚本
检查并修改`mvp/sql/init.sql`文件，与<https://github.com/648540858/wvp-GB28181-pro/tree/master/%E6%95%B0%E6%8D%AE%E5%BA%93>最新版本保持一致。

### 第六步 运行
```bash
cd ../../
docker-compose up -d
```

### 第七步 运行成功后替换ZLMediaKit证书
```bash
docker cp zlmediakit/resource/default.pem wvp-GB28181-pro-Docker_zlmediakit_1:/opt/media/bin
docker restart wvp-GB28181-pro-Docker_zlmediakit_1
```
