## Ambari集成Bigtop编译安装
### 简介
众所周知的原因，CDH新版不再免费，HDP也不再更新。幸运的是，ambari先因无人维护而退役，后又于2022年6月火速复活。说明项目依然很有市场需求，这也是目前唯一免费开源的方案。另外，此次选用的Hadoop stack是使用Bigtop编译包取代HDP。Bigtop也是Apache开源项目，只是因为之前大家有CDH或HDP使用，所以并没有获得大家太多的关注，而现在Ambari+Bigtop成为了开源的首选方案。当然目前还没有发布稳定版本，所以不建议直接使用到生产。尽请期待，后续开发及正式版发布。
### 步骤
1. 购买一台国外按量计费的服务器
```text
编译时需要拉取jar包等，为减少人力、时间成本，建议初期体验使用国外服务器。
```
2. 拉取源码
```shell
git clone https://github.com/apache/ambari.git
```
3. 进入到编译目录
```shell
cd ambari/dev-support/docker/centos7/
```
4. 安装docker
```shell
yum install -y docker
```
5. 创建编译、集群部署基础镜像
```shell
./build-image.sh
```
6. 编译ambari并使用docker部署集群
   1. 创建ambari-rpm-build容器，用于编译及缓存maven仓库
   2. 编译ambari
   3. 配置数据库环境、部署ambari集群 

    部署成功后，网页访问IP:8080端口，账号密码admin/admin
```shell
./build-containers.sh
```
7. 修改ambari代码重新编译部署
```shell
./build-ambari.sh
```
8. 重新分发bigtop stack
```shell
./distribute-scripts.sh
```
9. 删除ambari集群
```shell
./clear-containers.sh
```
10. 删除编译环境

    注：此操作将删除构建依赖的jar，下次编译需要重新拉取。
```shell
docker rm -f ambari-rpm-build
```