[返回](ProxyBalancer.md)

通过http\_upstream实现loadbalance
```
http {
    upstream cluster{
        server 10.0.22.21:5555;
        server 10.0.22.22:5555;
    }
    server {
        listen 80;
        server_name localhost;
        location / {
        	proxy_pass http://cluster;
	}
}
```

如果在多个应用上配置，也很方便
```
http {
    upstream wiki_cluster{
        server 10.0.22.21:5555;
        server 10.0.22.22:5555;
    }
    upstream blog_cluster{
        server 10.0.22.23:5555;
        server 10.0.22.24:5555;
    }
    server {
        listen 80;
        server_name localhost;
        
        location /wiki {
        	proxy_pass http://wiki_cluster;
	}
        location /blog {
        	proxy_pass http://blog_cluster;
	}
}
```
或者另一种方式，将不同的应用以CGI方式发布到不同端口。


另外，作为proxy使用时，fcgi方式的配置
```
        location / {
            # host and port to fastcgi server
            fastcgi_pass 127.0.0.1:8888;
            fastcgi_param PATH_INFO $fastcgi_script_name;
            fastcgi_param REQUEST_METHOD $request_method;
            fastcgi_param QUERY_STRING $query_string;
            fastcgi_param CONTENT_TYPE $content_type;
            fastcgi_param CONTENT_LENGTH $content_length;
            fastcgi_pass_header Authorization;
            fastcgi_intercept_errors off;
        }
```