



## nginx指定配置文件启动

```shell
/usr/local/nginx/sbin/nginx   -c   /usr/local/nginx/conf/nginx.conf
```

杀掉NGINX进程

```shell
sudo killall nginx
sudo nginx
```

## 测试

只浏览不下载

```shell
  location / {
        add_header Content-Type text/plain;        
        return 200 "I'm test"; #测试用
    }
```



```shell
    location / {
        root /home/wwwroot/;
        index index.html;
        #新增配置
        add_header Content-Type text/plain;        
        return 200 "I'm test";
    }
```

只下载不浏览

```shell
  if ($request_filename ~* ^.*?\.(filename)$){
        add_header Content-Disposition attachment;
    }
```

nginx一般默认是下载
