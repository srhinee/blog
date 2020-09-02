---
title: linux笔记
date: 2019-03-22 18:38:45
categories: 
    - linux
tags: 
    - linux
cover: https://da-xi-gua-1253809426.cos.ap-beijing.myqcloud.com/blog/A2.jpg
---
###FTP
  + /etc/vsftpd.conf 是配置 不能同时配ip4和6 否则无法启动服务
  + 登录时候填该主机用户名和密码(不是root权限密码)
  + get mget put mput 相当于pull和push及多个文件操作 不支持文件夹 压缩后上传
  + lcd 操作本地目录 cd是远程
  
----

###压缩
  + tar czvf demo.tar * 打包该目录所有为demo
  + tar xzvf demo.tar 解压在当前目录
  + zip/unzip

---

###nginx
  ```
  location /little/ {
                   proxy_redirect off;
                   proxy_set_header X-Real-IP $remote_addr;
                   proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                   proxy_set_header X-Forwarded-Proto $scheme;
                   proxy_set_header Host $http_host;
                   proxy_set_header X-NginX-Proxy true;
                   proxy_set_header Connection "";
                   proxy_http_version 1.1;
                   proxy_pass http://172.17.0.5:3000;
               }
  ```
