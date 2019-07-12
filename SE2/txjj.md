# 影院管理系统(TMS)软件体系结构文档

## 1. 文档修改历史

| 修改人员 | 日期      | 修改原因               | 版本号 |
| :------: | --------- | ---------------------- | ------ |
|   安皓   | 2019.4.12 | 草稿                   | 1.0    |
|   安皓   | 2019.4.20 | 增加部分业务逻辑层规范 | 1.0.1  |
|   范也 | 2019.4.20 | 增加界面和数据层规范 | 1.0.2  |
## 2. 目录

<!-- TOC -->

- [影院管理系统(TMS)软件体系结构文档](#影院管理系统tms软件体系结构文档)
    - [1. 文档修改历史](#1-文档修改历史)
    - [2. 目录](#2-目录)
    - [3. 引言](#3-引言)
        - [3.1 编制目的](#31-编制目的)
        - [3.2 词汇表](#32-词汇表)
        - [3.3 参考资料](#33-参考资料)
    - [4. 产品概述](#4-产品概述)
    - [5. 逻辑视图](#5-逻辑视图)
    - [6. 组合视图](#6-组合视图)
        - [6.1 开发包图](#61-开发包图)
        - [6.2 运行时进程](#62-运行时进程)
        - [6.3 物理部署](#63-物理部署)
    - [7. 架构设计](#7-架构设计)
        - [7.1 模块职责](#71-模块职责)
        - [7.2 用户界面层分解](#72-用户界面层分解)
            - [7.2.1 职责](#721-职责)
            - [7.2.2 接口规范](#722-接口规范)
            - [7.2.3 需要的服务接口](#723-需要的服务接口)
        - [7.3 业务逻辑层分解](#73-业务逻辑层分解)
            - [7.3.1 职责](#731-职责)
            - [7.3.2 接口规范](#732-接口规范)
        - [7.4 数据层分解](#74-数据层分解)
            - [7.4.1 职责](#741-职责)
            - [7.4.2 接口规范](#742-接口规范)
        - [7.5 信息视角](#75-信息视角)
            - [7.5.1 数据持久化对象](#751-数据持久化对象)
            - [7.5.2 TXT持久化格式](#752-txt持久化格式)
            - [7.5.3 数据库表](#753-数据库表)

<!-- /TOC -->



## 3. 引言

### 3.1 编制目的

​	本报告详细完成对影院管理系统需求阶段1和2的概要设计，达到详细指导设计和开发的目的，同时实现和测试人员及用户的沟通。

​	本报告面向开发人员、测试人员和最终用户而编写，是了解系统的导航。

### 3.2 词汇表

| 词汇名称 | 词汇含义                                 | 备注 |
| :------: | ---------------------------------------- | ---- |
|   TMS    | Theater Management System ，影院管理系统 | 无   |



### 3.3 参考资料

1. 《软件工程与计算(卷二)——软件开发的技术基础》
2. 《影院管理系统用例文档》
3. 《影院管理系统需求规格说明》

## 4. 产品概述

​	参考影院管理系统用例文档和影院管理系统软件需求规格说明文档中对产品的概要描述。

## 5. 逻辑视图

- 处理静态设计模型

  - 影院管理系统中，选择了分层的体系结构风格，将系统分为三层(展示层、业务逻辑层和数据层)，较好地实现了对于该系统的整个抽象。展示层包含对静态网页、静态网页渲染的实现及向业务逻辑层发送请求，业务逻辑层包含对于业务逻辑的实现、处理展示层发送的请求和向数据层发送请求，数据层负责访问数据、数据的持久化和处理业务逻辑层发送的请求。

- 示意图

[![体系结构风格包图.png](https://i.loli.net/2019/04/12/5cb07da0e9836.png)](https://i.loli.net/2019/04/12/5cb07da0e9836.png)

[![软件体系结构逻辑设计方案 (1).png](https://i.loli.net/2019/04/20/5cbab0f3a5791.png)](https://i.loli.net/2019/04/20/5cbab0f3a5791.png)

  

## 6. 组合视图

### 6.1 开发包图

- 表示软件组件在开发时环境中的静态组织
  - 描述开发包以及相互间的依赖
  
  - 绘制开发包图
    
    [![体系结构 (2) (1).png](https://i.loli.net/2019/04/20/5cbabbf1da38e.png)](https://i.loli.net/2019/04/20/5cbabbf1da38e.png)
    
    - 开发包图类似上述示意图画法

<<<<<<< HEAD

| 开发包 | 依赖的其他开发包               |
| :----: | ------------------------------ |
| mainui | userui、manageui、vo、loginui、clientui  |                               |
| mainui  |  loginui,  purchaseui, movieui, discountui, searchui |
| manageui | managerblservice, vo |
| manageblservice |  |
| managebl | managerblservice, movielistbl, managedataservice  |
| managedata | managedataservice, databaseutility |
| managedataservice | javaRMI, po |
| loginui | loginblservice, staffui, audienceui, administerui, managerui, audienceui, vo |
| loginblservice |  |
| loginbl | loginblservice, userbl,  |
| loginbl | loginblservice, userbl, |
| audienceui | audienceblservice, vo |
| audienceblservice |  |
| audiencebl | audienceblservice, movielikebl, searchbl, purchasebl, audiencedataservice |
| audiencedata | audiencedataservice, databaseutility |
| audiencedataservice | javaRMI, po |
| purchaseui | purchaseblservice, vo |
| mainui | vipui、purchaseui、audienceui、movielikeui、movieui、staffui、searchui、admininstratorui、loginui、VO|
| vipui | vipblservice, VO |
| vipblservice |  |
| vipbl | vipblservice, audiencebl, vipdataservice  |
| vipdata | vipdataservice, datautility |
| vipdataservice | PO |
| purchaseui | purchaseblservice |
| purchaseblservice |  |
| purchasebl | vipbl,discountbl,purchaseblservice,purchasedataservice |
| purchasedata | purchasedataservice,datautility |
| purchasedataservice |  |
| audienceui | audienceblservice, VO |
| audienceblservice |  |
| audiencebl | audienceblservice,purchasebl,movielike,userbl,searchbl |
| movielikeui | movielikeblservice,VO |
| movielikeblservice |  |
| movielikebl | movielikeblservice, movielikedataservice |
| movielikedata | movielikedataservice, datautility |
| movielikedataservice | PO |
| movieui | movieblservice, VO |
| movieblservice |  |
| moviebl | moviedataservice,movielikebl,movieblservice |
| moviedata | datautility,moviedataservice |
| moviedataservice | PO |
| staffui | staffblservice, VO |
| staffblservice |  |
| staffbl | staffblservice,userbl, arrangebl,statisticsbl |
| searchui | searchblservice |
| searchblservice |  |
| searchbl | searchblservice, movielistbl |
| admininstratorui | admininstratorblservice, VO |
| admininstratorblservice |  |
| adminbl | admininstratorblservice, userbl,movielikebl, managebl |
| loginui | loginblservice |
| loginblservice |  |
| loginbl | loginblservice, userbl |
| discountbl | staffbl,  discountdataservice,PO |
| discountdata | discountdataservice, datautility |
| discountdataservice | PO |
| movielistbl | moviebl,movielistdataservice,VO,PO |
| movielistdataservice | moviedata |
| userbl | userdataservice,VO,PO |
| userdataservice | PO |
| userdata | userdataservice,datautility |
| arrangebl | movielistbl |
| managebl | movielistbl |
| staticsbl | movielistbl |
| databaseservice | database |
| database | datautility |
| VO |  |
| PO |  |
| datautility | JDBC |


### 6.2 运行时进程

- 表示软件在运行时进程间的交互，描述系统的动态结构

  - 绘制进程图

- 示意图：
[![未命名文件.png](https://i.loli.net/2019/04/20/5cba96acc5e47.png)](https://i.loli.net/2019/04/20/5cba96acc5e47.png)

### 6.3 物理部署

- 处理如何将软件组件映射到硬件基础设施
  - 绘制部署图
- 示意图

[![5ae5be27e4b039625af793c0.png](https://i.loli.net/2019/04/19/5cb96d2e0e4fa.png)](https://i.loli.net/2019/04/19/5cb96d2e0e4fa.png)

## 7. 架构设计

- 描述功能分解和如何在不同的层中安排软件模块
  - 描述架构中的对象，包含架构图
  - 描述组件接口信息
    - 包括：语法、前置条件、后置条件

### 7.1 模块职责

- 模块视图
- 各层职责

|     层     | 职责     |
| :--------: | -------- |
| 用户界面层 | 展示界面 |

- 层之间调用接口

| 接口 | 服务调用方   | 服务提供方       |
| :--: | ------------ | ---------------- |
|      | 客户端展示层 | 客户端业务逻辑层 |



### 7.2 用户界面层分解
根据需求，系统提供14个界面：登陆界面、观众界面、vip充值界面、搜索界面、主界面、电影详情界面、员工界面、设置优惠界面、统计界面、统计想看界面、经理界面、上架电影界面、电影详情管理界面、购票界面

界面跳转如图所示
[![未命名文件 (2).png](https://i.loli.net/2019/04/20/5cbaa7c208219.png)](https://i.loli.net/2019/04/20/5cbaa7c208219.png)
<center><b>用户界面跳转</b></center>

#### 7.2.1 职责
界面实现采用HTML技术，为每个界面构建一个html文档，包括对应的css和js文件。利用ajax技术与逻辑层进行通信。

<center><b>用户界面类</b></center>

[![未命名文件 (4).png](https://i.loli.net/2019/04/20/5cbab14c12561.png)](https://i.loli.net/2019/04/20/5cbab14c12561.png)


#### 7.2.2 接口规范


<center><b>用户界面层模块的接口规范</b></center>
因为应用html、 css 、js技术，所以界面层模块不需要调用，不需要前置条件。用户打开任何一个界面的地址，界面自动显示。
<hr/>

<table border="1">
  <tr>
    <td rowspan="3">Loginui</td>
    <td>语法</td>
    <td>无</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>无</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>显示登录界面</td>
  </tr>

  <tr>
    <td rowspan="3">mainui</td>
    <td>语法</td>
    <td>无</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>用户已经登录</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>显示主界面</td>
  </tr>

  <tr>
    <td rowspan="3">staffui</td>
    <td>语法</td>
    <td>无</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>用户已登录</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>显示员工界面</td>
  </tr>

  <tr>
    <td rowspan="3">administratorui</td>
    <td>语法</td>
    <td>无</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>用户已登录</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>显示经理界面</td>
  </tr>

  <tr>
    <td rowspan="3">audienceui</td>
    <td>语法</td>
    <td>无</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>用户已登录</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>显示观众界面</td>
  </tr>
  <tr>
    <td rowspan="3">searchui</td>
    <td>语法</td>
    <td>无</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>用户已经登录</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>显示搜索界面</td>
  </tr>
    <tr>
    <td rowspan="3">movieui</td>
    <td>语法</td>
    <td>无</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>用户已经登录</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>显示电影详情界面</td>
  </tr>
    <tr>
    <td rowspan="3">vipui</td>
    <td>语法</td>
    <td>无</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>用户已经登陆</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>显示vip充值界面</td>
  </tr>
      <tr>
    <td rowspan="3">purchaseui</td>
    <td>语法</td>
    <td>无</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>用户已经登录</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>显示购票界面</td>
  </tr>
</table>

#### 7.2.3 需要的服务接口

|         服务名         | 服务                   |
| :--------------------: | ---------------------- |
| blservice.*blservice | 每个界面都有对应的业务逻辑接口 |


### 7.3 业务逻辑层分解

​	业务逻辑层包括多个针对界面的业务逻辑处理对象。比如，search对象负责处理搜索界面的相关逻辑，login对象用于处理登录注册界面的相关逻辑。业务逻辑层的设计如图所示。

[![业务逻辑层设计.png](https://i.loli.net/2019/04/19/5cb980cc44c5b.png)](https://i.loli.net/2019/04/19/5cb980cc44c5b.png)

#### 7.3.1 职责
<center>业务逻辑层模块的职责</center>

| 模块 | 职责             |
| -------- | :----- |
|   userbl   | 负责实现对应用户界面所需要的服务 |
|   adminbl   | 负责实现管理员界面所需要的服务 |
|   audiencebl   | 负责实现观众界面所需要的服务 |
|   staffbl   | 负责实现影院员工界面所需要的服务 |
|   vipbl   | 负责实现vip界面所需要的服务 |
|   moviebl   | 负责实现电影详情界面所需要的服务 |
|   movielikel   | 负责实现想看电影的相关逻辑 |
|   movielistbl   | 负责实现想看电影列表界面所需要的服务 |
|   managebl   | 负责实现上架电影的相关逻辑 |
|   statisticsbl   | 负责实现查看统计数据的相关逻辑 |
|   arrangebl   | 负责实现排片界面所需要的服务 |
|   loginbl   | 负责实现登录、注册界面所需要的服务 |
|   searchbl   | 负责实现搜索的相关逻辑 |
|   discountbl   | 负责实现优惠活动界面所需要的服务 |
|   purchasebl   | 负责实现购买电影票界面所需要的服务 |


#### 7.3.2 接口规范

<center><b>loginbl模块的接口规范</b></center>

<hr/>

<center><b>提供的服务</b></center>

<hr/>

<table border="1">
  <tr>
    <td rowspan="3">Login.check</td>
    <td>语法</td>
    <td>public ResultMessage check(long id,String password)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>id,password符合数据格式要求</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>查找是否存在相应的User，根据输入的password返回登录验证的结果</td>
  </tr>
  <tr>
    <td rowspan="3">Login.Register</td>
    <td>语法</td>
    <td>public ResultMessage register(String userid,String password)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>id,password符合数据格式要求</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>查找是否已经存在user，根据其结果返回注册验证的结果</td>
  </tr>
</table>


<hr/>

<center><b>需要的服务（需要接口）</b></center>

<hr/>



| 服务名 |    服务     |
| :----: | ---------- |
| UserDataService.insert(UserPO PO) | 在数据库中插入UserPO对象 |
| UserDataService.find(UserPO PO) | 在数据库中查找UserPO对象 |

<hr/>

<center><b>movielikebl模块的接口规范</b></center>

<hr/>

<center><b>提供的服务</b></center>



<table border="1">
  <tr>
    <td rowspan="3">Movielike.like</td>
    <td>语法</td>
    <td>public ResultMessage like(String id,boolean isLike)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>用户登录</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>根据用户当前是否已经标记电影为想看，返回想看的验证结果，该电影的想看人数增加</td>
  </tr>

  <tr>
    <td rowspan="3">Movielike.getInfo</td>
    <td>语法</td>
    <td>public Chart getInfo(String id,boolean isLike)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>用户是管理员类型</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>返回想看电影的统计表</td>
  </tr>
</table>



<hr/>

<center><b>需要的服务（需要接口）</b></center>



| 服务名 |    服务     |
| :----: | ---------- |
| MovieDataService.AddLike(long id) | 电影的想看人数增加 |
| MovieDataService.deleteLike(long id) | 电影的想看人数减少 |
| MovieDataService.findLike(long id) | 在数据库中查找电影的想看人数 |
| MovieDataService.AddLike(long id) | 电影的想看人数增加 |
| Database.getMovieLikeDatabase | 得到MovieLike数据库中的服务引用 |
| MovieLikeDataService.Like(MoviePO PO) | 在数据库中插入MoviePO对象 |
| MovieLikeDataService.dislike(MoviePO PO) | 在数据库中删除MoviePO对象 |

<hr/>

<center><b>userbl模块的接口规范</b></center>

<hr/>

<center><b>提供的服务</b></center>



<table border="1">
  <tr>
    <td rowspan="3">User.distinguish</td>
    <td>语法</td>
    <td>public User distinguish(long id)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>无</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>根据用户id，返回用户的具体类型，包括影院员工、观众、管理员</td>
  </tr>
</table>





<hr/>

<center><b>需要的服务（需要接口）</b></center>



| 服务名 |    服务     |
| :----: | ---------- |
| Database.getUserDatabase | 得到User数据库中的服务引用 |
| UserDataService.find(long id) | 在数据库中查找用户 |

<hr/>

<center><b>statisticsbl</b>模块的接口规范</center>
<hr/>

<center><b>提供的服务</b></center>



<table border="1">
  <tr>
    <td rowspan="3">Statistic.getMovieData</td>
    <td>语法</td>
    <td>public String getMovieData(DataType data)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>影院员工已经登录</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>根据data类型，返回用户查看的数据，包括近期最受欢迎电影、上座率、客单价、票房和排片率</td>
  </tr>
</table>







<hr/>

<center><b>需要的服务（需要接口）</b></center>



| 服务名 |    服务     |
| :----: | ---------- |
| MovieDataService.findPopularMovie() | 在数据库中查找最受欢迎电影 |
| MovieDataService.findOccupancy(long id) | 在数据库中查找电影上座率 |
| MovieDataService.findPerSale(long id) | 在数据库中查找电影客单价 |
| MovieDataService.findBoxOffice(long id) | 在数据库中查找电影票房 |
| MovieDataService.findScreenings(long id) | 在数据库中查找电影排片率 |

<hr/>

<center><b>audiencebl模块的接口规范</b></center>
<hr/>

<center><b>提供的服务</b></center>



<table border="1">
  <tr>
    <td rowspan="3">Statistic.getAudienceID</td>
    <td>语法</td>
    <td>public long getAudienceID()</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>无</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>根据用户ID，判断用户是否是VIP</td>
  </tr>
</table>







<hr/>

<center><b>需要的服务（需要接口）</b></center>



| 服务名 |    服务     |
| :----: | ---------- |
| Database.getUserData | 得到User数据库的服务的引用 |
| UserDataService.find(UserPO PO) | 在数据库中查找用户id并返回 |


<hr/>

<center><b>Adminbl模块的接口规范</b></center>
<hr/>

<center><b>提供的服务</b></center>



<table border="1">
  <tr>
    <td rowspan="3">Admin.login</td>
    <td>语法</td>
    <td>public ResultMessage login(long id, String password)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>password符合输入规则</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>查找是否存在对应的Admin,根据输入的password返回登陆验证结果</td>
  </tr>
  <tr>
    <td rowspan="3">Admin.shelfmovie</td>
    <td>语法</td>
    <td>public ResultMessage shelfmovie(String id)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>存在该id对应的未上架的电影对象</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>将该id对应的电影标记为上架</td>
  </tr>
  <tr>
    <td rowspan="3">Admin.unshelfmovie</td>
    <td>语法</td>
    <td>public ResultMessage unshelfmovie(String id)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>存在该id对应的已上架的电影对象</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>取消该id对应的电影的上架标记</td>
  </tr>
  <tr>
    <td rowspan="3">Admin.addmovie</td>
    <td>语法</td>
    <td>public ResultMessage addmovie(MovieVO vo)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>启动一个增加电影的任务</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>根据vo生成新的电影对象</td>
  </tr>
  <tr>
    <td rowspan="3">Admin.deletemovie</td>
    <td>语法</td>
    <td>pulic ResultMessage deletemovie(String id)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>存在该id对应的电影对象</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>删除该id对应的电影的对象、数据库数据及movielist的引用</td>
  </tr>
  <tr>
    <td rowspan="3">Admin.revisemovie</td>
    <td>语法</td>
    <td>public ResultMessage revisemovie(ReviseVo vo)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>存在对应的电影对象</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>根据vo修改电影对象的属性</td>
  </tr>
</table>







<hr/>

<center><b>需要的服务（需要接口）</b></center>



| 服务名 |    服务     |
| :----: | ---------- |
| User.login | 登陆 |
| Manage.shelf | 上架电影 |
| Manage.unshelf|下架电影|
| Manage.add|增加电影|
| Manage.delete|删除电影|
| Manage.revise|修改电影详情|


<hr/>

<center><b>Managebl模块的接口规范</b></center>
<hr/>

<center><b>提供的服务</b></center>



<table border="1">
  <tr>
    <td rowspan="3">Manage.shelf</td>
    <td>语法</td>
    <td>public ResultMessage shelf(String id)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>存在该id对应的未上架的电影对象</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>将该id对应的电影标记为上架</td>
  </tr>
  <tr>
    <td rowspan="3">Manage.unshelf</td>
    <td>语法</td>
    <td>public ResultMessage unshelf(String id)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>存在该id对应的已上架的电影对象</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>取消该id对应的电影的上架标记</td>
  </tr>
  <tr>
    <td rowspan="3">Manage.addmovie</td>
    <td>语法</td>
    <td>public ResultMessage add(MovieVO vo)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>启动一个增加电影的任务</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>根据vo生成新的电影对象</td>
  </tr>
  <tr>
    <td rowspan="3">Manage.delete</td>
    <td>语法</td>
    <td>pulic ResultMessage delete(String id)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>存在该id对应的电影对象</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>删除该id对应的电影的对象、数据库数据及movielist的引用</td>
  </tr>
  <tr>
    <td rowspan="3">Manage.revise</td>
    <td>语法</td>
    <td>public ResultMessage revise(ReviseVo vo)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>存在对应的电影对象</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>根据vo修改电影对象的属性</td>
  </tr>
</table>







<hr/>

<center><b>需要的服务（需要接口）</b></center>



| 服务名 |    服务     |
| :----: | ---------- |
| Movielist.add|增加电影|
| Movielist.delete|删除电影|
| Movielist.revise|修改电影属性|


<hr/>

<center><b>Arrangebl模块的接口规范</b></center>
<hr/>

<center><b>提供的服务</b></center>



<table border="1">
  <tr>
    <td rowspan="3">Arrange.arrange</td>
    <td>语法</td>
    <td>public ResultMessage arrange(ArrangeVO vo)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>存在已上架的电影对象</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>确定电影的上映时间列表及对应的地点列表</td>
  </tr>
 <tr>
    <td rowspan="3">Arrange.revise</td>
    <td>语法</td>
    <td>public ResultMessage revise(ReviseVO vo)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>电影已有场次时间安排，且需做个别调整</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>修改电影的上映时间和地点</td>
  </tr>
   <tr>
    <td rowspan="3">Arrange.show</td>
    <td>语法</td>
    <td>public ResultMessage show(String id)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>电影的上映时间场次已安排</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>展示排片列表</td>
  </tr>
</table>





<hr/>

<center><b>需要的服务（需要接口）</b></center>



| 服务名 |    服务     |
| :----: | ---------- |
| Movielist.getmoviebyid| 根据id获取电影对象 |
| DatabaseFaory.getArrangeDatabase| 得到Arrange数据库的服务的引用|
| MoviellistDataService.insert(ArrangePO po)| 在数据库中插入ArrangePO对象 |
| MovielistDataService.revise(RevisePO po) | 根据RevisePO修改数据库中相应的排片信息|


<hr/>

<center><b>Staffbl模块的接口规范</b></center>
<hr/>

<center><b>提供的服务</b></center>



<table border="1">
  <tr>
    <td rowspan="3">Staff.login</td>
    <td>语法</td>
    <td>public ResultMessage login(long id, String password)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td> password符合输入规则</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td> 查找是否存在对应的Staff,根据输入的password返回登陆验证结果</td>
  </tr>
  <tr>
    <td rowspan="3">Staff.arrangemovie</td>
    <td>语法</td>
    <td>public ResultMessage arrangemovie(ArrangeVO vo)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>存在已上架的电影对象</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>确定电影的上映时间列表及对应的地点列表</td>
  </tr>
 <tr>
    <td rowspan="3">Staff.revisearrange</td>
    <td>语法</td>
    <td>public ResultMessage revisearrange(ReviseVO vo)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>电影已有场次时间安排，且需做个别调整</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>修改电影的上映时间和地点</td>
  </tr>
   <tr>
    <td rowspan="3">Staff.showarrange</td>
    <td>语法</td>
    <td>public ResultMessage showarrange(String id)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>电影的上映时间场次已安排</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>展示排片列表</td>
  </tr>
</table>







<hr/>

<center><b>需要的服务（需要接口）</b></center>



| 服务名 |    服务     |
| :----: | ---------- |
| User.login       | 登陆 |
| Arrange.arrange  | 设置电影的上映时间列表及对应的地点列表 |
| Arrange.revise   | 修改电影的上映时间及场次 |
| Statistic.movielikestatistic| 统计影片销想看人数 |
| Statistic.purchasestatistic| 统计影片销售情况 |


<hr/>

<center><b>模块的接口规范</b></center>
<hr/>

<center><b>提供的服务</b></center>



<table border="1">
  <tr>
    <td rowspan="3">Purchase.purchase</td>
    <td>语法</td>
    <td>public ResultMessage purchase(PurchaseVO vo,long id)</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>观众选中电影并点击购买</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>根据观众id和电影生成订单</td>
  </tr>
  <tr>
    <td rowspan="3">Purchase.pay</td>
    <td>语法</td>
    <td>public ResultMessage pay()</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>观众选择付款</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>订单生效</td>
  </tr>
  <tr>
    <td rowspan="3">Purchase.show</td>
    <td>语法</td>
    <td>public ResultMessage show()</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>观众查看账单</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>显示账单详情</td>
  </tr>
</table>







<hr/>

<center><b>需要的服务（需要接口）</b></center>



| 服务名 |    服务     |
| :----: | ---------- |
| Moviebl.getprice | 获取电影的价格属性 |
| Moviebl.getid| 获取电影名称 |
| Discountbl.getstrategy | 获取折扣方案 |
| Vipbl.getpricestraegy | 获取会员价 |
| DatabaseFaory.getPurchaseDatabase | 得到Purchase数据库的服务的引用 |
| PurchaseDataService.insert(PurchasePo po)| 在数据库中插入PurchasePo对象 |



<hr/>




### 7.4 数据层分解
数据层主要给业务逻辑层提供数据访问服务，包括对与持久化数据的增删改查。"\*"业务由  "\*"DataService接口提供服务。由于持久化数据的保存可能存在多种形式：Txt文件、序列化文件、数据库等，所示抽象了数据服务。数据层模块具体描述如图所示：

<center>数据层模块的描述</center>
<hr>

[![未命名文件 (5).png](https://i.loli.net/2019/04/20/5cbab785ebe21.png)](https://i.loli.net/2019/04/20/5cbab785ebe21.png)

- 由于对于每一个dataservice服务，都有对应的txt、mysql、序列化实现。所以在这里用“ * ”代替dataservice服务名称。希望真诚而善良的男女对此表示理解。

数据层主要给业务逻辑层提供数据访问服务，包括对于持久化数据的增、删、改、查。业务逻辑需要的服务由对应的DataService接口提供（比如，movielikebl需要的服务由movielikedataservice接口提供），由于持久化数据的保存可能存在多种形式：xlsx文件和数据库等，下图所示抽象了数据服务。

#### 7.4.1 职责

<center><b>数据层模块职责<b></center>
<hr>

|模块|职责|
|-|-|
|*dataservice|持久化数据库的接口，提供集体介入、集体保存、增删改查服务|
|*dataserviceTxtfileImpl|基于txt的持久化数据库的接口，提供集体介入、集体保存、增删改查服务|
|*dataserviceSerializableFileImpl|基于序列化文件的持久化数据库的接口，提供集体介入、集体保存、增删改查服务|
|*dataserviceMysqlImpl|基于mysql的持久化数据库的接口，提供集体介入、集体保存、增删改查服务|

*可以替换为vip,discount,purchase,movie,user,movielike,database

#### 7.4.2 接口规范

<center><b>数据层模块的接口规范<b></center>
<hr>

<table border="1">
  <tr>
    <td rowspan="3">*DataService.find</td>
    <td>语法</td>
    <td>public *PO find(long id) throws RemoteException</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>无</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>根据用户ID查找并返回相应的PO结果</td>
  </tr>
      <tr>
    <td rowspan="3">*DataService.insert</td>
    <td>语法</td>
    <td>public *PO insert(*PO po) throws RemoteException</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>同样的ID的po在Mapper中不存在</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>在数据库中加入一个po记录</td>
  </tr>
    <tr>
    <td rowspan="3">*DataService.delete</td>
    <td>语法</td>
    <td>public *PO delete(*PO po) throws RemoteException</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>在数据库中存在相同id的PO</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>删除一个PO</td>
  </tr>
  <tr>
    <td rowspan="3">*DataService.update</td>
    <td>语法</td>
    <td>public *PO update(*PO po) throws RemoteException</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>在数据库中存在相同id的PO</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>更新一个PO</td>
  </tr>
  <tr>
    <td rowspan="3">*DataService.init</td>
    <td>语法</td>
    <td>public *PO init() throws RemoteException</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>无</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>初始化持久化数据库</td>
  </tr>
   <tr>
    <td rowspan="3">*DataService.finish</td>
    <td>语法</td>
    <td>public *PO finish() throws RemoteException</td>
  </tr>
  <tr>
    <td>前置条件</td>
    <td>无</td>
  </tr>
  <tr>
    <td>后置条件</td>
    <td>结束持久化数据库使用</td>
  </tr>
  
</table>

*可以替换为vip,discount,purchase,movie,user,movielike,database

### 7.5 信息视角
|对象|属性|
|-|-|
| UserPO | 用户名、密码、用户类型 |
| vipPO | 用户的账户余额|
| purchasePO| 用户购买记录：购买的电影、价格、时间、折扣、场次、座位 |
| moviePO| 一部电影的详情、想看人数、导演、标签、演员、公司、排片信息、价格、封面|
|  | |
| | |
#### 7.5.1 数据持久化对象

#### 7.5.2 TXT持久化格式

#### 7.5.3 数据库表
- 描述数据持久化对象(PO)
  - 属性及其定义
  - 类型