### TODO
- [x] 微信支付SDK使用开源版本的
- [x] Nginx需要把真实客户端IP转发进来
- [ ] 抽象出第一个微服务 fitter-lottery-service.为什么要先抽象出这个服务，因为这个最简单
    - [x] consul安装
    - [x] 书写服务
    - [x] lottery-service 实验成功
    - [ ] lottery-service 搭建完成，剔除app中所有

- [x] 使用docker搭建mongodb集群
- [ ] acme.sh 配合 letsencrypt 配置泛域名
    - 配置出 *.3dfitter.cn的泛域名 全站https化
- [ ] Nginx 设置用户认证
- [ ] mongo 数据备份
- [ ] 搭建ngrok实现内网穿透
- [ ] 全部docker容器化

### 之后的操作
- [ ] 前端持续集成 jenkins
- [ ] 后端服务报警系统 sentry