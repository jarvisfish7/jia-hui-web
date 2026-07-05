# Docker 部署说明

本文档说明如何使用 Docker 部署 `jia-hui-web`，并区分开发环境、测试环境和现网环境。

## 环境划分

项目现在按 Vite 的 `mode` 区分三套环境：

| 环境 | mode | 环境文件 | 说明 |
| --- | --- | --- | --- |
| 开发环境 | `development` | `.env.development` | 本地开发调试 |
| 测试环境 | `test` | `.env.test` | 测试服务器或预发布验证 |
| 现网环境 | `production` | `.env.production` | 正式线上部署 |

环境变量必须以 `VITE_` 开头，前端代码才能读取，例如：

```env
VITE_APP_ENV=production
VITE_APP_TITLE=广州佳汇企业管理有限公司
VITE_API_BASE_URL=
```

## 本地开发环境

```bash
npm install
npm run dev
```

默认访问：

```text
http://localhost:5173
```

如需验证不同 mode 的构建：

```bash
npm run build:dev
npm run build:test
npm run build:prod
```

## Docker 镜像结构

Docker 使用多阶段构建：

1. `node:20-alpine` 安装依赖，并按指定 `BUILD_MODE` 执行 Vite 构建。
2. `nginx:1.27-alpine` 托管构建后的 `dist` 静态文件。
3. Nginx 监听容器内 `80` 端口，并支持 Vue 单页应用路由回退。

## 测试环境部署

测试环境使用 `.env.test`，默认映射服务器 `8081` 端口：

```bash
docker compose -f docker-compose.yml -f docker-compose.test.yml up -d --build
```

访问：

```text
http://服务器IP:8081
```

查看日志：

```bash
docker compose -f docker-compose.yml -f docker-compose.test.yml logs -f
```

停止测试环境：

```bash
docker compose -f docker-compose.yml -f docker-compose.test.yml down
```

## 现网环境部署

现网环境使用 `.env.production`，默认映射服务器 `8080` 端口：

```bash
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d --build
```

访问：

```text
http://服务器IP:8080
```

如果要直接使用标准 HTTP 端口，可以把 `docker-compose.prod.yml` 中的端口改成：

```yaml
ports:
  - "80:80"
```

## 单独使用 Docker Build

测试环境镜像：

```bash
docker build --build-arg BUILD_MODE=test -t jia-hui-web:test .
docker run -d --name jia-hui-web-test -p 8081:80 jia-hui-web:test
```

现网环境镜像：

```bash
docker build --build-arg BUILD_MODE=production -t jia-hui-web:prod .
docker run -d --name jia-hui-web-prod -p 8080:80 --restart unless-stopped jia-hui-web:prod
```

## 更新发布

测试环境更新：

```bash
git pull
docker compose -f docker-compose.yml -f docker-compose.test.yml up -d --build
```

现网环境更新：

```bash
git pull
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d --build
```

## 常用维护命令

查看容器：

```bash
docker ps
```

重启服务：

```bash
docker compose restart
```

清理旧镜像：

```bash
docker image prune
```

## Nginx 配置说明

`nginx.conf` 包含以下关键配置：

- `/` 使用 `try_files $uri $uri/ /index.html`，支持 Vue 单页应用刷新和直接访问子路径。
- 静态资源设置 30 天缓存，并启用 `immutable`。
- `index.html` 设置 `no-cache`，确保新版本发布后入口文件能及时更新。


## 服务器已有部署脚本
bash deploy.sh prod


# 设置 HTTP 代理
git config --global http.proxy http://127.0.0.1:7897
# 设置 HTTPS 代理
git config --global https://127.0.0.1:7897
