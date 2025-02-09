# Nginx API 网关配置说明

## 部署说明
1. 确保 nginx/nginx.conf 文件存在于项目根目录
2. 使用以下命令启动服务：
   ```bash
   docker compose up -d
   ```

## 访问方式
- API 通过 http://localhost 访问
- Nginx 会自动将请求转发到 Vapor 应用

## 注意事项
- 生产环境部署时建议：
  - 配置 SSL/TLS
  - 添加适当的安全头
  - 根据实际需求调整 worker_processes 和 worker_connections
  - 配置访问日志和错误日志

## 环境配置说明

### 环境变量设置
1. 在开发环境中：
   - 复制 `.env.example` 到 `.env`
   - 根据本地开发环境修改配置值

2. 在生产环境中：
   - 不要使用 `.env` 文件
   - 使用系统环境变量或容器编排工具（如 Docker Compose）设置环境变量
   - 确保所有敏感信息使用安全的密钥管理系统

### 安全建议
- 不要在版本控制中提交 `.env` 文件
- 定期轮换数据库密码和其他敏感凭证
- 在生产环境使用强密码和长密钥
- 限制数据库用户权限至最小必要权限

### 配置检查清单
- [ ] 确保数据库连接使用 TLS
- [ ] 验证日志级别在生产环境设置适当
- [ ] 检查所有密码和密钥的强度
- [ ] 确认环境特定的配置已正确设置

## Nginx 公网访问配置说明

### 安全注意事项
1. 生产环境配置：
   - 必须配置 SSL/TLS 证书（HTTPS）
   - 建议使用具体域名而不是通配符
   - 考虑配置 rate limiting 防止 DDoS 攻击
   - 建议使用 WAF（Web Application Firewall）

2. 防火墙配置：
   - 只开放必要端口（80/443）
   - 配置 UFW 或其他防火墙规则
   ```bash
   sudo ufw allow 80/tcp
   sudo ufw allow 443/tcp
   ```

3. 监控建议：
   - 定期检查访问日志
   - 设置异常访问告警
   - 监控服务器资源使用情况

4. 性能优化：
   - 根据服务器配置调整 worker_processes
   - 配置 gzip 压缩
   - 配置浏览器缓存
   - 考虑使用 CDN 