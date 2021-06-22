
## redis 
参考<https://www.cnblogs.com/wdliu/p/9377278.html>

```shell
redis-cli 连接命令 
quit 退出命令

```

### 查看持久话目录  
1. 首先登陆Redis
```shell
127.0.0.1:6379> config get dbfilename
1) "dbfilename"
2) "dump.rdb"
127.0.0.1:6379> config get dir
1) "dir"
2) "/www/server/redis" 

## 查看最后一次持久化信息
127.0.0.1:6379> info persistence
# Persistence
loading:0
current_cow_size:0
current_fork_perc:0.00%
current_save_keys_processed:0
current_save_keys_total:0
rdb_changes_since_last_save:0
rdb_bgsave_in_progress:0
rdb_last_save_time:1623131546
rdb_last_bgsave_status:ok
rdb_last_bgsave_time_sec:0
rdb_current_bgsave_time_sec:-1
rdb_last_cow_size:495616
aof_enabled:0
aof_rewrite_in_progress:0
aof_rewrite_scheduled:0
aof_last_rewrite_time_sec:-1
aof_current_rewrite_time_sec:-1
aof_last_bgrewrite_status:ok
aof_last_write_status:ok
aof_last_cow_size:0
module_fork_in_progress:0
module_fork_last_cow_size:0
127.0.0.1:6379>

```