# Serv00 服务器状态检测工具

[![GitHub license](https://img.shields.io/github/license/lzban8/serv00-server-status)](https://github.com/lzban8/serv00-server-status/blob/main/LICENSE)
[![GitHub issues](https://img.shields.io/github/issues/lzban8/serv00-server-status)](https://github.com/lzban8/serv00-server-status/issues)
[![GitHub stars](https://img.shields.io/github/stars/lzban8/serv00-server-status)](https://github.com/lzban8/serv00-server-status/stargazers)
[![Deploy Status](https://img.shields.io/github/deployments/lzban8/serv00-server-status/github-pages)](https://github.com/lzban8/serv00-server-status/deployments)
[![Website Status](https://img.shields.io/website?url=https%3A%2F%2Flzban8.github.io%2Fserv00-server-status%2F)](https://lzban8.github.io/serv00-server-status/)

> 🔍 一个轻量级的服务器状态监控工具，支持多服务器批量检测、IP地理位置查询、网络连通性测试等功能。
> 
> 基于纯原生JavaScript开发，无需后端支持，支持深色模式，响应式设计适配移动端。

![GitHub language count](https://img.shields.io/github/languages/count/lzban8/serv00-server-status)
![GitHub top language](https://img.shields.io/github/languages/top/lzban8/serv00-server-status)
![GitHub code size in bytes](https://img.shields.io/github/languages/code-size/lzban8/serv00-server-status)
![GitHub last commit](https://img.shields.io/github/last-commit/lzban8/serv00-server-status)

**关键特性：**
- 🚀 零依赖，纯静态部署
- 🌓 自适应深色模式
- 📱 响应式设计
- 🔄 实时状态监控
- 🌍 IP地理位置查询
- 🔒 隐私安全保护

**技术标签：** `JavaScript` `HTML5` `CSS3` `RESTful API` `响应式设计` `深色模式` `服务器监控` `网络工具`

这是一个用于检测 Serv00 系列服务器可用性的网页工具。该工具提供了实时的服务器状态监控、IP 地理位置查询以及网络连通性测试功能。

## 在线演示

🚀 [立即访问在线演示](https://lzban8.github.io/serv00-server-status/)

## 功能特点

### 1. 服务器状态检测
- 支持批量检测多个 Serv00 服务器
- 显示服务器的 IP 地址和可访问状态
- 提供服务器响应时间和地理位置信息
- 支持一键复制服务器 IP 地址

### 2. 自定义域名检测
- 支持添加和检测自定义域名
- 实时显示检测结果和详细信息
- 智能识别无效域名格式

### 3. 本地网络信息
- 显示用户当前 IP 地址
- 提供 IP 地理位置信息
- 显示网络运营商信息
- 支持查看 IP 地址段和 ASN 信息

### 4. 界面特点
- 响应式设计，支持移动端访问
- 深色模式自适应
- 简洁直观的用户界面
- 实时状态更新和动态效果

## 技术实现

### 使用的技术
- 纯原生 JavaScript 实现
- 响应式 CSS 设计
- 支持深色模式（自动适配系统主题）
- RESTful API 集成

### API 服务
本工具使用 [uapis.cn](https://uapis.cn) 提供的公共 API 服务，包括：
- IP 地理位置信息查询
- 服务器 Ping 检测
- 本地网络信息获取

## 部署说明

### 环境要求
- 支持静态文件托管的 Web 服务器（如 Nginx、Apache 等）
- 支持 HTTPS（推荐，因为部分浏览器在 HTTP 环境下可能限制某些功能）
- 无需数据库支持
- 无需后端服务支持

### 部署步骤

1. **本地开发环境**
   ```bash
   # 克隆项目
   git clone https://github.com/your-username/serv00-server-status.git
   cd serv00-server-status
   
   # 使用任意 HTTP 服务器运行
   # 例如使用 Python 的简单 HTTP 服务器
   python -m http.server 8080
   # 或使用 Node.js 的 http-server
   npx http-server
   ```

2. **生产环境部署**
   
   **Nginx 配置示例：**
   ```nginx
   server {
       listen 80;
       listen [::]:80;
       server_name your-domain.com;
       
       # 启用 HTTPS 重定向（推荐）
       return 301 https://$server_name$request_uri;
   }

   server {
       listen 443 ssl http2;
       listen [::]:443 ssl http2;
       server_name your-domain.com;

       # SSL 配置
       ssl_certificate /path/to/cert.pem;
       ssl_certificate_key /path/to/key.pem;

       # 网站根目录
       root /var/www/serv00-server-status;
       index index.html;

       # 缓存配置
       location ~* \.(css|js)$ {
           expires 7d;
           add_header Cache-Control "public, no-transform";
       }

       # 安全性配置
       add_header X-Frame-Options "SAMEORIGIN" always;
       add_header X-XSS-Protection "1; mode=block" always;
       add_header X-Content-Type-Options "nosniff" always;
       add_header Referrer-Policy "no-referrer-when-downgrade" always;
   }
   ```

3. **Docker 部署**
   ```bash
   # 使用提供的 Dockerfile 构建镜像
   docker build -t serv00-status .
   
   # 运行容器
   docker run -d -p 80:80 serv00-status
   ```

### 更新维护

1. **代码更新**
   ```bash
   # 拉取最新代码
   git pull origin main
   
   # 如果使用 Docker，重新构建并启动容器
   docker build -t serv00-status .
   docker run -d -p 80:80 serv00-status
   ```