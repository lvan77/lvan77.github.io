     server {
        listen 80 ;
        # listen 443 ssl;
        server_name  xinyi.shkdl.cn;

        gzip on;
        gzip_buffers 32 4K;
        gzip_comp_level 6;
        gzip_min_length 100;
        gzip_types application/javascript text/css text/xml;
        gzip_disable "MSIE [1-6]\.";
        #配置禁用gzip条件，支持正则。此处表示ie6及以下不启用gzip（因为ie低版本不支持）
        gzip_vary on;
        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        access_log /www/wwwlogs/nginx/xinyi.access.log;
        error_log /www/wwwlogs/nginx/xinyi.error.log;

	client_max_body_size 500m;

        location / {
            root   /www/server/xinyi/mall-admin-web/dist;
            index  index.html index.htm;
            try_files $uri $uri/ /index.html;
        }

        location /api-admin/ {
	    proxy_connect_timeout 300;
            proxy_read_timeout 300;
            proxy_send_timeout 300;

            #proxy_set_header  Host  $http_host:$server_port;
            proxy_set_header  Host  $host;
            proxy_set_header  X-Real-IP  $remote_addr;
            proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto  $scheme;
            proxy_set_header X-Forwarded-Port    $server_port;
            proxy_pass  http://127.0.0.1:8080/;
            client_max_body_size 500m;
        }

        location ~^/api-admin/swagger/(.*)
        {
            proxy_redirect off;
            #proxy_set_header Host $host;
            proxy_set_header Host $host:$server_port; #添加:$server_port
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_pass http://127.0.0.1:8080/$1;
        }

        location /api-portal/ {
	    proxy_connect_timeout 300;
            proxy_read_timeout 300;
            proxy_send_timeout 300;

            #proxy_set_header  Host  $http_host:$server_port;
            proxy_set_header  Host  $host;
            proxy_set_header  X-Real-IP  $remote_addr;
            proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto  $scheme;
            proxy_set_header X-Forwarded-Port    $server_port;
            proxy_pass  http://127.0.0.1:8085/;
            client_max_body_size 500m;
        }

        location ~^/api-portal/swagger/(.*)
        {
            proxy_redirect off;
            #proxy_set_header Host $host;
            proxy_set_header Host $host:$server_port; #添加:$server_port
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_pass http://127.0.0.1:8085/$1;
        }

        location ~^/rabbitmq/(.*)
        {
            proxy_redirect off;
            #proxy_set_header Host $host;
            proxy_set_header Host $host:$server_port; #添加:$server_port
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_pass http://127.0.0.1:15672/$1;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /usr/share/nginx/html;
        }

    }