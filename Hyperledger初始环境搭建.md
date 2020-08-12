## Hyperledger fabric 环境搭建总结



* 该环境搭建由于国内墙的原因以及下载速度关系十分艰辛，主要结合[Hyperledger1.4中的binary手动下载][https://www.cnblogs.com/zongmin/p/11635686.html] 以及[Hyperledger2.0前置环境条件搭建][https://www.cnblogs.com/always-kaixuan/p/12398251.html] 以及[Hyperledger fabric 发行版2.2的官方文档][https://hyperledger-fabric.readthedocs.io/en/release-2.2/test_network.html] 最终成功搭建了Hyperledger fabric v2.2以及fabric-ca1.4.8的环境，并成功跑通了test-network中的例子。
* git, curl, wget安装
```bash
sudo apt-get install git || sudo apt-get install curl ||sudo apt-get install wget
```
* docker安装
参考[官方文档][https://docs.docker.com/install/linux/docker-ce/ubuntu] 中的说明安装即可，若觉得速度慢可以配置apt镜像
docker安装完成之后配置docker[阿里云镜像][https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors]

* docker-compose安装
由于docker-compose速度太慢，通过pip来安装要快很多
① sudo apt install python-pip   #首先安装pip
② sudo pip install docker-compose
③ docker-compose --version   #查看版本

* golang安装
1. 根据[golang中文社区][http://docscn.studygolang.com/doc/install] 文档以及 [golang标准工作区搭建][http://docscn.studygolang.com/doc/code.html] 对本地golang环境进行配置
2. 通过[golang包管理镜像站][https://goproxy.cn/] 中的说明对本地的golang进行goproxy配置，否则在使用go工具时会没有反应

* fabric, fabric-sample仓库拉取，二进制数据下载，以及docker镜像拉取
1. 自己从GitHub上拉取fabric和fabric-samples的镜像。然后切换到自己想要的版本。
2. 然后在fabric/core/scripts中找到bootstrap.sh的文档，在最后输出出来需要下载的fabric, fabric-ca的二进制下载链接，然后打开用浏览器下载，将下载到的两个压缩包解压之后的bin文件下的文件放到一起，然后把两个文件夹都放到fabric-samples的路径下，并将bin目录添加到$PATH中。这里可以参考[手动下载二进制代码][https://www.cnblogs.com/zongmin/p/11635686.html] 。
3. 最后通过`bash bootstrap.sh -d` 来自动拉取docker镜像

* testnetwork测试（[根据官网提供的教程][https://hyperledger-fabric.readthedocs.io/en/release-2.2/test_network.html] ）
