在解决禁止ip直接访问网站的问题的时候，受到群友启发，发现还有个可以禁止ip直接访问网站的办法，那就是网站黑白名单。

Nginx配置黑名单
创建黑名单其实很简单，只需要使用allow或者deny关键字就可以了。

其中，allow关键字用来允许访问某ip,其中allow all，表示允许所有的ip
其中，deny关键字用来拒绝访问某ip，其中deny all，表示拒绝所有的ip进行访

```
server{
    listen:80;
    server_name localhost;
    deny 192.168.1.10;  #拒绝访问192.168.1.10的ip地址
    allow 192.168.1.9;  #允许访问192.168.1.9的ip地址
}
```

当然如上我所需要的，是禁止通过IP访问某个网站，那么只要使用如下代码所示：

```
server{
    listen: 80;
    server_name www.yechuchen.cn;
    allow all;#允许访问所有的ip
    deny 12.345.56.678;#但不允许访问域名所绑定的ip
}
```

而要做出网站黑名单，就有可能要屏蔽一堆ip，但是如果将其放在nginx.conf文件夹下，既不美观，也不利于管理，因此需要单独写出一个blacklist.conf，然后在nginx.conf中引用它。

blacklist.conf

```
allow all;
deny 123.45.678.91;
deny 12.345.67.8;
...
```

nginx.conf

```
server{
    listen:80;
    server_name www.yechuchen.cn;
    include blacklist.conf; #引用blacklist.conf
}
```

Nginx配置白名单
配置白名单和配置黑名单其实差不多，只是把allow和deny反过来罢了，因此这里不细写了，直接贴一个代码

whitelist.conf

```
deny all; # 禁止访问所有ip
allow 192.168.1.10; # 允许访问指定ip
allow 192.168.1.9; # 允许访问指定ip
...
```

nginx.conf

```
server{
    listen:80;
    server_name www.yechuchen.cn;
    include whitelist.conf; #引用whitelistlist.conf
}
```

黑名单作用范围
HTTP范围黑名单
总入口黑名单


```
http{
    include blacklist.conf;
    ...
    server{
        ...
    }
}
```

如上所示，在http里配置的则是http范围的黑名单了。

SERVER范围黑名单
分域名黑名单

```
http{
    ...
    server{
        include blacklist.conf;
        ...
    }
}
```

如上所示，在server配置的是server范围的黑名单。

Location范围黑名单
分域名黑名单

```
http{
    ...
    server{
        ...
        location /{
            include blacklist.conf;
            ...
        }
    }
}
```

如上，这是location范围的黑名单。
从上面不同范围的黑名单可以看出来，不同的范围对应的效果不一样。在Http范围的黑名单中，访问该服务器的所有服务都要被黑名单过滤。在Server范围黑名单中，只有访问该http服务器的当前server服务时，才会被黑名单过滤。而Location范围呢，自然便是针对当前转发才会被黑名单过滤了。

