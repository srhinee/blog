---
title: docker 笔记
date: 2019-04-02 18:38:45
categories: 
    - docker
tags: 
    - docker
cover: https://da-xi-gua-1253809426.cos.ap-beijing.myqcloud.com/blog/A1.jpg
---
#dcoker
 - cp 相互拷贝文件 后面被前面覆盖 
    + 在run指定挂载前 确定容器目录为空 不然会覆盖掉容器 
    + 例如挂载配置文件前确保宿主有文件 否则报错
 - inspect 查看容器参数 
   + 两个容器链接时候查看IP地址 
   + 用link替代更好 否则重启ip变更 
 - -add-host=hostname:ip 给容器添加宿主机host 要不然呢 localhost都是指向本机 确定不了宿主机ip
   + 同理 容器之间指向 也是由link来确定host 可在/etc/hosts中查看修改
   + alias hostip="ifconfig en0 | grep inet | grep -v inet6 | cut -d ' ' -f2"  && docker run --add-host=docker:$(hostip) -p 3001:3000 -v node start.js
    
   
>##运行代码
关于python java node等语言运行已有项目需要dockerfile来构建一层特有的images来确定初始工作
1. 每个镜像对应一个项目符合规范 封装性良好 无缝移植
2. ~~要么封装一个公共环境镜像 运行本机项目 /
封装不来哦--本事不够 *直接跑run 带参数这种?有待尝试*  因为没必要 一个image对应一个死程序 何必在一个确认行为的程序上再运行别的程序呢~~
3. dockerfile是不依赖于运行环境的 就是说不能指定 挂载目录 映射端口等与宿主机关联的行为
4. 指令解析
    + valume 指定挂载点(镜像内部) 可用于同镜像下多容器共享目录 --volumes-from 在run时指定现有的一个容器可共享 
    不同于 run -v(指定宿主机与容器目录) 虽然持久化储存都要保存在宿主机上 若每次运行新容器后删除 会在宿主机留下目录碎片
    run --rm 用后即删 和rm -v name 删除容器且删除持久储存目录可避免
    + expose 指定端口 只是告诉需要暴露的端口 run时 -P可以自动映射出暴露的端口  
5. build -f 指定dockerfile路径 -t 指定镜像名
6. 运行容器时候也可以指定运行指令 不过和dockerfile中的指令不一样 
7. arg和env 编译传参/运行传参 都需要默认值 但是貌似通用镜像根据env传参执行不同行为有点不现实
python还有可能(没有依赖情况) 
run时候跟的指令不过是由镜像系统(linux)来执行 没有执行环境(workdir)
>小相册 dockerfile 对应1 打包整个项目
```dockerfile
  FROM node
  MAINTAINER samsara
  
  # 给镜像创建一层工作目录 用来执行项目
  RUN mkdir -p /home/Service
  WORKDIR /home/Service
  #build时如果在同目录会把自己也复制进去
  COPY . /home/Service
  RUN npm install --registry https://registry.npm.taobao.org
  EXPOSE 3000
  #run时触发
  ENTRYPOINT [ "node", "app.js"]
```
生成images直接run -P就可以 项目已经打包 

>###nginx
  ```docker
    跑起来拿设置
    docker run --rm -p 80:80 --name mynginx -d nginx
    进入查找config
    docker exec -it mynginx /bin/bash
    这个log文件不推荐复制 重定向到了标准输出和错误
    docker cp mynginx:/var/log/nginx/ $PWD/log
    复制容器配置到目录
    docker cp mynginx:/etc/nginx/ $PWD/set 
    docker cp mynginx:/usr/share/nginx/html/ $PWD/static
    正真运行 可选link或add-host
    docker run --name nginx -d -p 80:80 -v $PWD/log:/var/log/nginx  -v $PWD/set:/etc/nginx  -v $PWD/static:/usr/share/nginx/html nginx
  ```

