好的，帮你把这份开发日志结构化梳理一下：

---

## 项目概况

全人力开发 PPT 生成网站（Banana Slides），技术栈：Vite + Python + Docker，前后端全栈。

---

## 今日完成的工作

### 1. Docker 部署流程梳理
- 搞清楚了 Docker 内服务的代码部署和启动流程
- 解决了容器名冲突问题：`docker ps -a` 查看容器，`docker rm -f <container_id>` 删除同名容器后重新 `docker compose up`
- 确认了 `.env` 文件修改不需要重新 build

### 2. 数据库认知
- 项目使用 SQLite（文件型数据库），部署简单
- 把 `.db` 文件放进 Docker / 服务器上即可，本机和线上运行方式一致

### 3. 新功能开发
- 账户登录系统
- 积分体系：新用户登录赠送 1 积分，1 积分可生成 1 张 PPT
- 积分购买功能（跳转 Stripe 支付）
- 首页添加 PPT 预览入口，展示更多预览 PPT，提升用户预期
- 预览详情页：只读模式，不能触发编辑和图片生成

---

## 遗留问题

### Stripe Webhook 回调问题
- 现状：Stripe 支付后的 Webhook 回调更新有问题
- 原因：线上正式 Webhook 要求 HTTPS 链接，当前服务没有
- 计划方案：用之前 smart-downloader（download pilot）的页面做中转，该页面已有 HTTPS 链接，通过它转发 Webhook 请求到当前服务

---

## 关键经验记录

| 场景 | 命令 / 要点 |
|---|---|
| 容器名冲突 | `docker rm -f <container_id>` 后重新 up |
| 修改环境变量 | 改 `.env` 不需要重新 build |
| SQLite 部署 | `.db` 文件随 Docker 部署即可 |
| Stripe Webhook | 需要 HTTPS，可用已有 HTTPS 站点做中转 |