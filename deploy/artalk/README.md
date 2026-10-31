# Artalk 评论后端部署（comment.sayodevice.com）

把 Artalk 部署到 Linux 服务器，用 Nginx 反代提供 HTTPS，作为 docsify 文档站的评论后端。

## 文件说明
- `artalk.yml`     —— Artalk 后端配置（放 `/etc/artalk/artalk.yml`）
- `artalk.service` —— systemd 服务（放 `/etc/systemd/system/artalk.service`）
- `nginx.conf`     —— Nginx 反代配置（放 `/etc/nginx/conf.d/artalk.conf`）

## 部署步骤

### 1. 下载二进制
去 https://github.com/artalkjs/artalk/releases/latest 下载 `linux_amd64` 的 tar.gz，解压：

```bash
tar -zxvf artalk_*_linux_amd64.tar.gz
sudo mv artalk /usr/local/bin/artalk
artalk -v
```

### 2. 建用户和目录
```bash
sudo useradd --system --home /var/lib/artalk --shell /usr/sbin/nologin artalk
sudo mkdir -p /var/lib/artalk /etc/artalk
sudo chown -R artalk:artalk /var/lib/artalk
```

### 3. 放配置并创建管理员
```bash
sudo cp artalk.yml /etc/artalk/artalk.yml
sudo artalk admin -c /etc/artalk/artalk.yml   # 交互式创建管理员账号
```

### 4. 安装 systemd 服务
```bash
sudo cp artalk.service /etc/systemd/system/artalk.service
sudo systemctl daemon-reload
sudo systemctl enable --now artalk
sudo systemctl status artalk
```

### 5. Nginx 反代 + HTTPS
1. 把 `comment.sayodevice.com` 的 DNS 解析到这台服务器。
2. 签证书（Let's Encrypt）：
   ```bash
   sudo certbot certonly --nginx -d comment.sayodevice.com
   ```
   （或 `--standalone`；证书路径按实际改 `nginx.conf`）
3. 放反代配置并 reload：
   ```bash
   sudo cp nginx.conf /etc/nginx/conf.d/artalk.conf
   sudo nginx -t && sudo systemctl reload nginx
   ```

### 6. 前端
`docs/index.html` 里 `server` 已填为 `https://comment.sayodevice.com`，部署文档站后评论即生效。

## 上线后要开的项（登录 https://comment.sayodevice.com 管理后台）
- 评论审核：开启「待审核」，新评论通过后展示
- 点赞：开启 upvote
- 邮件通知：配置 SMTP（新评论/待审核提醒）
- 反垃圾：验证码 / 关键词过滤
