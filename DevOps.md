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