# PostgreSQL 配置文件自动生成器

一个用于自动生成 PostgreSQL 优化配置的 Python 脚本，根据服务器硬件规格和工作负载类型生成最佳实践配置。

## 功能特点

- 自动检测服务器 CPU 核心数和内存容量
- 根据负载类型（OLTP/OLAP）优化配置参数
- 支持不同存储类型（SSD/NVMe/HDD）的参数调整
- 针对虚拟机环境进行特殊优化
- 支持主备架构配置，包括物理流复制和逻辑复制
- 提供操作系统级别调优建议
- 需要使用Python3运行小版本不限
  
## 使用方法

1. 下载脚本到本地服务器
   ```bash
   wget https://example.com/pg_auto_conf_v2.py
   chmod +x pg_auto_conf_v2.py
   运行脚本
bash
python pg_auto_conf_v2.py

按照提示回答问题，包括：
服务器性能自动检测
负载类型选择
autovacuum 策略选择
服务器环境（物理机 / 虚拟机）
存储类型
高可用性配置
数据丢失容忍度
副本数量等
生成配置后，可选择直接应用或仅输出配置参数
配置示例
以下是脚本生成的典型配置参数示例（基于 2 核 CPU、1GB 内存、OLTP 负载、HDD 存储的虚拟机）：

plaintext
shared_buffers = 256MB
effective_cache_size = 768MB
work_mem = 64MB
maintenance_work_mem = 20MB
wal_buffers = 32MB
wal_level = 'physical streaming'
max_wal_size = 2GB
min_wal_size = 1GB
checkpoint_completion_target = 0.9
checkpoint_timeout = 5min
max_connections = 200
max_worker_processes = 4
max_parallel_workers = 2
max_parallel_workers_per_gather = 2
effective_io_concurrency = 2
random_page_cost = 4.0
seq_page_cost = 1.0
autovacuum = on
log_min_duration_statement = 500ms
listen_addresses = '*'
port = 5432
hot_standby = on
max_wal_senders = 5
archive_mode = on
synchronous_commit = off

操作系统调优建议
脚本还会提供操作系统级别的优化建议，包括：
禁用透明大页 (THP)
禁用 TCP 时间戳
禁用 atime
启用大页
优化磁盘布局
使用连接池（如 PgBouncer）

注意事项
生成的配置仅供参考，建议根据实际工作负载进行测试和调整
生产环境中应用配置前，请备份原配置文件
对于特殊工作负载，可使用脚本的 "微调模式" 进行更细致的参数调整
配置变更后需要重启 PostgreSQL 服务才能生效

许可证
MIT License
   
