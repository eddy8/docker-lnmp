# Docker For LNMP

## 使用
```
docker-compose up -d
```

## Docker 基本使用
查看磁盘空间占用情况。添加`-v`参数可以查看具体详情。
```
docker system df
```
清理磁盘空间。添加`-a`参数可以清理未被使用的镜像。
```
docker system prune
```
进入容器内部。
```
docker exec -it container_name sh
```
根据`Dockerfile`编译镜像
```
docker build --tag imagename:imageversion .
```
发布编译好的镜像
```
docker tag imagename:imageversion <Your Docker ID>/imagename:imageversion
docker push <Your Docker ID>/imagename:imageversion
```