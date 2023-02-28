# **data-sealing demo**

简体中文 | [English](README_en.md)

## 介绍
**data-sealing demo** 展示使用TEE安全存储对文件进行加密保存的CA和TA的代码示例

## 使用依赖

1. 确保环境上已安装机密计算SDK，需要同时安装相同版本的 `kunpeng-sc-1.3.0` 和 `kunpeng-sc-devel-1.3.0`，下载地址[机密计算SDK](https://mirrors.huaweicloud.com/kunpeng/archive/Kunpeng_SDK/itrustee/)
2. 确保tzdriver正常加载，执行 `lsmod | grep tzdriver` 查看
3. 确保守护进程正常启动，执行 `ps -ef | grep teecd` 查看

## 使用教程

1. 获取代码

   ```shell
   git clone https://github.com/kunpengcompute/devkitdemo.git
   ```

2. 切入到项目根路径

   ```shell
   cd ./devkitdemo/sc-sdk/examples/data-sealing/
   ```

3. 修改TA/cloud/config_cloud.ini中的开发者私钥和config的绝对路径

   ```shell
   vim TA/cloud/config_cloud.ini
   # 修改signKey为private_key.pem绝对路径
   # secSignKey = /usr/local/kunpeng-sc-devel/examples/data-sealing/TA/cloud/TA_cert/private_key.pem
   # 修改configPath为config绝对路径
   # configPath = /usr/local/kunpeng-sc-devel/examples/data-sealing/TA/cloud/signed_config/config
   ```

4. 将 ./TA/ 目录下的manifest.txt 文件替换成,申请开发者证书时使用的manifest.txt文件

5. 安装TA demo

   ```shell
   cd ./TA/
   chmod +x ./install.sh
   ./install.sh
   ```

6. 将../CA/data_sealing_ca.h中的DATA_SEALING_TA_UUID修改为开发者申请证书的uuid

   ```shell
   vim ../CA/data_sealing_ca.h
   # #define DATA_SEALING_TA_UUID        "7824610d-0e54-4448-a905-86fffeeff327"    //开发者证书UUID[需根据实际情况进行修改]
   ```

7. 安装CA demo

   ```shell
   cd ../CA/
   chmod +x ./install.sh
   ./install.sh
   ```

8. 运行demo

   ```shell
   /vendor/bin/data-sealing
   ```
