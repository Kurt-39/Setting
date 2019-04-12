# Nginx遇到的常见问题

## 1.404 bad request

**一般原因**:请求的Header过大

**解决方法**：配置nginx.conf相关设置

```conf
client_header_buffer_size 16k;
large_client_header_buffers 4 64k;
```
##  2.413 Request Entity Too Large

**一般原因**:一般出现在上传文件
**解决方法**：配置nginx.conf相关设置

```conf
client_max_body_size 10m;
```

##499 Client Closed Request
**一般原因**:客户端在为等到服务器相应返回前就关闭了客户端描述符。一般出现在客户端设置超时后，主动关闭socket.
**解决方法**：根据实际Nginx后端服务器的处理时间修改客户端超时时间。

##500 Internal Server Rrror
**一般原因**：脚本错误，（php语法错误、lua语法错误）
      访问量过大，系统资源限制，不能打开过多文件
      磁盘空间不足。（access log开启可能导致磁盘满溢 关闭）
**解决方法**：语法错误查看nginx_err_log php_err_log。
      文件访问量：
      1.修改nginx配置文件
      2.在配制类中添加:
```conf
worker_rlimit_nofile 65535;
```
3.修改/etc/security/limits.conf
```conf
* soft nofile 65535
* hard nofile 65535
```