
---
title: 小程序比赛
date: 2019-03-22 18:38:45
categories: 
    - 比赛
tags: 
    - 比赛
cover: https://da-xi-gua-1253809426.cos.ap-beijing.myqcloud.com/blog/biSai.jpg

---




## 0. 任务分工及项目介绍
 <i class="icon-star" style="color:green">美工</i> <i class="icon-star" style="color:red">前端</i> <i class="icon-star" style="color:blue">后端</i>
 
*  该版本小程序为东软实验室小程序的完善版本，由于东软实验室的一些不可抗力（无法与学校开发部门联动）导致该版本小程序核心功能不完善（预定和通过教务获取学生信息），故在此小程序的基础上添加新功能和完善核心功能，该版本不同于东软小程序最大两点有：
    * 该版本是通用版本，不拘泥于东软提供的实验室数据和服务 见1.通用模块
    * 该版本是东软小程序的业务完善版本 见2.业务模块 
***
## 1. 通用模块

* 小程序前端 <i class="icon-star" style="color:red"></i> <i class="icon-star" style="color:green"></i>
    * 登录 用户填写学号和密码 选取学校后方可登录 
    > 用户进入小程序后先看到小程序**启动页**  随后显示登录界面 填写学号密码后选取学校  
    > ps. 启动页类似app启动页 随后进入登录页面 表单有三项 学号密码和学校 其中学校为下拉框 选取学校后登录页背景跟随变化
        

**登录界面背景**跟随选取学校变动 随后进入业务模块  


* 小程序后台 <i class="icon-star" style="color:red"></i> <i class="icon-star" style="color:blue"></i>
    * 初始化学校信息和学生信息 导入导出学生信息
    > 后台跟随前台逻辑 首先是学校的初始化 管理员登入填写该学校的名字和宣传图等基本信息 然后导入或添加学生信息(账号列表) **操作包括导入导出及增删改 后期可能需要设置接入接口 与各学校教务真实数据联动** 
## 2. 业务模块
* 前端 <i class="icon-star" style="color:red"></i> <i class="icon-star" style="color:green"></i>
    1. - [ ] 新闻条目渲染  
    2. - [x] 实验室轮播图
    3. - [x] 实验室信息渲染 
    4. - [ ] 设备条目渲染
    5. - [x] **实验室预定** *用户进入某个实验室页面 点击预定按钮 转入实验室座位页面 选取座位和时间后提交后台* 
    6. - [x] 我的预订记录 
    7. - [x] 实验室信息查询 *根据实验室关键字或列表中选取实验室 查看该实验室当前预定情况*
    8. - [x] 主题设置
    9. - [x] 切换学校及切换账号等账号设置
    
> ps. √是需要实现的任务 其余可能是待定 

* 后台 <i class="icon-star" style="color:red"></i><i class="icon-star" style="color:blue"></i>
    1. - [ ] 新闻条目导入及管理
    2. - [x] 实验室基本信息导入及管理
    3. - [x] **实验室座位设置** *实验室预定模块 初始化实验室座位信息 接收前端预定信息 编排实验室预定场景并记录*
    4. - [ ] 设备基本信息导入及管理
    5. - [x] 操作记录统计 *记录用户操作信息 日后生成用户行为信息报表*
## 3. 开发计划
```gantt
title 项目开发流程
dateFormat  YYYY-MM-DD
section 项目确定
需求分析       :a1,now,7d
项目对接       :a3,after a2,7d
section 项目实施
UI美工      :a2,after a1 , 14d
前端        :after a1, 21d
后台        :after a1, 21d
测试        :after a3, 7d
section 发布验收
发布: 2d
验收: 3d
```
> ps. x轴单位为一周 也就是说需求分析是7天 剩下以此类推 从4月初为项目实施阶段  共计一个月

