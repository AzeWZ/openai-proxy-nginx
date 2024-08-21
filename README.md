Forward requests based on Nginx, with support for SSE (Server-Sent Events).
基于Nginx进行请求转发，支持SSE。

1. Nginx.conf 

```
            # 代理地址
            proxy_pass  https://api.openai.com/;
            # ssl支持
            proxy_ssl_server_name on;
            # 更新Host 
            proxy_set_header Host api.openai.com;
            # 如果转发侧直接设置api-key。修改为正确的key，并移除#
            # proxy_set_header Authorization "Bearer sk-XXX"
            chunked_transfer_encoding off;
            proxy_buffering off;
            proxy_cache off;

```

2. docker 启动
```
docker run -itd -p 80:80 -v $PWD/nginx.conf:/etc/nginx/nginx.conf --name my-nginx nginx
```

3. docker-compose 启动
```
docker-compose up -d 
```
4. 使用
openai.api_base = "your_proxy_url" 

5. 云服务器注意修改开发和端口 80 443