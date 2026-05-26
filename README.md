# minikube-springboot-demo
Minikube 一键部署 SpringBoot+MySQL+Redis 的 K8s 模板

## 前置条件
- Minikube v1.38.1
- Docker v29.2.1

## 部署步骤
1. 启动Minikube
   ```bash
   minikube start
   ```
2.使用 Minikube 的 Docker daemon（最关键的一步，90% 的人会忘）
临时把你本地电脑上的docker命令，重定向到 Minikube 虚拟机内部的 Docker 引擎上。
  ```bash
   eval $(minikube docker-env)
  ```
如果需要切回本地dockers：eval $(minikube docker-env -u)

3.构建 SpringBoot 镜像（在你的项目根目录执行）
```bash
docker build -t springboot-app:latest .
```

4.部署所有服务
```
kubectl apply -f mysql.yaml
kubectl apply -f redis.yaml
kubectl apply -f springboot.yaml
```



### 注意
1. **必须执行`eval $(minikube docker-env)`**，否则Minikube找不到你本地构建的镜像
2. **不要用`latest`标签加`imagePullPolicy: Always`**，本地镜像会被强制拉取失败
3. **不要用`localhost`访问服务**，必须用`minikube service <service-name>`命令



本项目采用 MIT 许可证，你可以自由使用、修改和分发。
