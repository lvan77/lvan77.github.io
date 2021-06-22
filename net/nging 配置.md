## nginx 
[参考](https://www.zybuluo.com/phper/note/89391)
[参考2](https://www.zybuluo.com/phper/note/90310)
[参考3](https://www.zybuluo.com/phper/note/133244)

nginx 配置常用参数

```shell
# main 最外层 main 全局配置

events {                                        # 工作模式
    worker_connections  1024;                   # 最大连接数
}
http {                                          # 配置http服务器
    include       mime.types;                   # 定义mime的文件类型
    default_type  application/octet-stream;     # 默认文件类型
    sendfile        on;                         # 开启 sendfile 函数（zero copy 方式）输出文件
    keepalive_timeout  65;                      # 连接超时时间,单位秒
    
    upstream pictureserver {                    # 定义负载均衡设备的ip和状态
        server 192.168.225.133:8081 ;           # 默认权重值为一
        server 192.168.225.133:8082 weight=2;   # 值越高，负载的权重越高
        server 192.168.225.133:8083 down;       # 当前server 暂时不参与负载
        server 192.168.225.133:8084 backup;     # 当其他非backup状态的server 不能正常工作时，才请求该server，简称热备
    }
    server {                                    # 设定虚拟主机配置
        listen  80;                             # 监听的端口
        server_name  picture.itdragon.com;      # 监听的地址，多个域名用空格隔开
        location / {                            # 默认请求 ，后面 "/" 表示开启反向代理，也可以是正则表达式
           root     html;                       # 监听地址的默认网站根目录位置
           proxy_pass   http://pictureserver;   # 代理转发
           index  index.html index.htm;         # 欢迎页面
           deny 127.0.0.1;                      # 拒绝的ip
           allow 192.168.225.133;               # 允许的ip
        }
        error_page   500 502 503 504  /50x.html;# 定义错误提示页面     
        location = /50x.html {                  # 配置错误提示页面
            root   html;
        }
    }

```