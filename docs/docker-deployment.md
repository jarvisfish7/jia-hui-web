# Docker 部署说明

本文档说明如何使用 Docker 构建和部署 `jia-hui-web` 前端项目。

## 部署结构

项目采用多阶段镜像构建：

1. `node:20-alpine` 安装依赖并执行 `npm run build`。
2. `nginx:1.27-alpine` 托管 `dist` 静态文件。
3. Nginx 监听容器内 `80` 端口，并对单页应用路由回退到 `index.html`。

## 本地构建镜像

```bash
docker build -t jia-hui-web:latest .
```

## 本地运行容器

```bash
docker run -d --name jia-hui-web -p 8080:80 --restart unless-stopped jia-hui-web:latest
```

访问：

```text
http://localhost:8080
```

## 使用 Docker Compose

启动：

```bash
docker compose up -d --build
```

查看日志：

```bash
docker compose logs -f
```

停止：

```bash
docker compose down
```

## 服务器部署流程

1. 将项目代码推送到服务器或 CI/CD 环境。
2. 在项目根目录执行：

```bash
docker compose up -d --build
```

3. 确认容器状态：

```bash
docker ps
```

4. 浏览器访问服务器地址：

```text
http://服务器IP:8080
```

如果需要使用标准 HTTP 端口，可以把 `docker-compose.yml` 中的端口改为：

```yaml
ports:
  - "80:80"
```

## Nginx 配置说明

`nginx.conf` 包含以下关键配置：

- `/` 使用 `try_files $uri $uri/ /index.html`，支持 Vue 单页应用刷新和直接访问子路径。
- 静态资源设置 30 天缓存，并启用 `immutable`。
- `index.html` 设置 `no-cache`，确保新版本发布后入口文件能及时更新。

## 常用维护命令

重新构建并发布：

```bash
docker compose up -d --build
```

重启服务：

```bash
docker compose restart
```

删除旧镜像缓存：

```bash
docker image prune
```
