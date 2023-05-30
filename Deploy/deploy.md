### 0: cd到/data/code/model_share下, 以下操作均在该目录下;
### 1. git pull 拉取最新代码
### 2. build 新镜像: 
   - docker build -t registry.cn-hangzhou.aliyuncs.com/jianchuang_tech/stable_deffusion_webui:dev -f Deploy/Dockerfile .
   - 如有需要保存该镜像到aliyun docker hub
     - docker push registry.cn-hangzhou.aliyuncs.com/jianchuang_tech/stable_deffusion_webui:dev
