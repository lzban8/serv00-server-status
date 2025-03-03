# Serv00 服务器状态检测工具

这是一个用于检测 Serv00 系列服务器可用性的网页工具。该工具提供了实时的服务器状态监控、IP 地理位置查询以及网络连通性测试功能。

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

2. **配置更新**
   - 修改服务器列表：编辑 `index.html` 中的 `servers` 数组
   - 调整 API 配置：根据需要修改 API 地址和参数
   - 更新界面主题：修改 CSS 样式定义

### 性能优化建议

1. **CDN 加速**
   - 建议将网站部署到 CDN
   - 适当配置缓存策略
   - 启用 HTTP/2 支持

2. **安全性配置**
   - 启用 HTTPS
   - 配置适当的 CSP (Content Security Policy)
   - 启用 HSTS
   - 定期更新 SSL 证书

3. **监控告警**
   - 配置网站可用性监控
   - 设置错误日志告警
   - 监控 API 调用限制

## 使用说明

### 基本功能
1. **检测所有服务器**
   - 点击"检测所有服务器"按钮
   - 等待检测完成，查看结果

2. **检测被阻止的服务器**
   - 点击"仅检测被阻止的服务器"按钮
   - 系统将只检测之前显示为"被阻止"状态的服务器

3. **添加自定义域名**
   - 在输入框中输入要检测的域名
   - 点击"检测"按钮或按回车键
   - 系统会将新域名添加到列表并立即进行检测

### 查看详细信息
- 点击 IP 地址可以快速复制
- 查看服务器的响应时间和地理位置信息
- 观察详细的错误信息（如果有）

## 注意事项

1. **API 限制**
   - 由于使用免费 API 服务，可能存在访问限制
   - 建议适当控制检测频率
   - 如遇到 API 访问失败，请稍后重试

2. **网络要求**
   - 确保设备有稳定的网络连接
   - 部分功能可能受到网络环境影响

3. **兼容性**
   - 支持所有现代浏览器
   - 自适应深色/浅色模式
   - 支持移动端访问

## 隐私说明

- 本工具不会保存任何用户数据
- 所有检测均为实时进行
- IP 信息仅用于显示，不会被存储或共享

## 免责声明

本工具仅供网络连通性测试使用，API 数据由第三方服务提供，不对数据准确性做保证。使用本工具时请遵守相关法律法规和服务条款。 