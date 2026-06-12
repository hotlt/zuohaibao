# 部署说明

本项目是纯静态前端应用，线上域名为：

```text
https://huabu.xin/
```

当前使用目录路由：

```text
/          首页
/canvas    无限画布
/generate  海豹生图
```

因此服务器需要把不存在的路径回退到 `index.html`，否则直接访问 `/canvas` 或 `/generate` 会返回 404。

## 本地构建

在项目目录执行：

```bash
npm install
npm run build
```

构建产物在：

```text
dist/
```

上传 `dist/` 目录里的内容到站点根目录。注意是上传 `dist` 里面的文件，不是上传 `dist` 文件夹本身。

站点根目录最终应类似：

```text
index.html
favicon.svg
icons.svg
assets/
```

## Caddy 配置

假设静态文件目录是：

```text
/www/wwwroot/huabu.xin
```

Caddyfile 示例：

```caddyfile
huabu.xin {
    root * /www/wwwroot/huabu.xin
    encode zstd gzip

    try_files {path} {path}/ /index.html
    file_server
}
```

如果同时使用 `www.huabu.xin`：

```caddyfile
huabu.xin, www.huabu.xin {
    root * /www/wwwroot/huabu.xin
    encode zstd gzip

    try_files {path} {path}/ /index.html
    file_server
}
```

重载 Caddy：

```bash
caddy reload --config /etc/caddy/Caddyfile
```

## 验证

部署后打开：

```text
https://huabu.xin/
https://huabu.xin/canvas
https://huabu.xin/generate
```

如果首页正常，但 `/canvas` 或 `/generate` 404，说明 Caddy 的 `try_files {path} {path}/ /index.html` 没有生效。

如果页面能打开但不能生图，通常是模型 API 不允许 `https://huabu.xin` 跨域请求，需要在 API 服务侧开启 CORS。
