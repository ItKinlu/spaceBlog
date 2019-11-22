# 使用 PM2 管理 gunicorn 程序

## 配置实例

> 注意：`gunicorn` 会自己管理进程，自动生成子进程，所以 `pm2` 不能开启 `cluster` 模式

```json
{
  "server": [
    {
      "exec_interpreter": "bash",
      "script": "gunicorn-start.sh",
      "args": [],
      "exec_mode": "fork",
      "error_file": "./logs/pm2-err.log", // 错误日志路径
      "out_file": "./logs/pm2-out.log", // 普通日志路径
      "log_date_format": "YYYY-MM-DD HH:mm:ss.SSS"
    }
  ]
}
```
