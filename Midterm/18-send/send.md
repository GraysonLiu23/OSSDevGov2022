# 期中作业 -- mozilla/send

## 成员及分工
曹汇杰(52215903002)：数据处理和第二部分

牛悦安(51215903012)：第三部分和报告整理

马源航(51215903076)：第一部分和部分第二部分内容

## 一、项目的基本背景和发展历程介绍

### 基本介绍

&emsp; &emsp; Firefox Send 项目是火狐开源的临时文件分享服务平台，用户可以安全、简单的从任何浏览器共享文件。该服务平台提供了端到端的加密来保护从共享到打开文件之间的数据安全，另外还提供了可以设置的安全控件，包括：设置文件链接何时到期，下载次数，添加密码，用以增加安全性。

### 技术类型

&emsp; &emsp;该项目作为一款网页应用，主要使用Javascript来构建项目代码。

### 版本发布历史

&emsp; &emsp;共发布65个版本，最后一个版本号是“v3.0.22”，发布于2020年4月30号。

### 主要贡献者的构成（国家、区域和组织等）

&emsp; &emsp;共有241个贡献者，从commits的日期与数量来看，主要贡献者来自于[@Mozilla](https://github.com/mozilla)

![Untitled](pic/contributor.png)

### CI/CD 的使用

&emsp; &emsp;使用[Circle](https://circleci.com/)CI进行CI/CD，具体配置文件参考[yaml](https://github.com/mozilla/send/blob/master/.circleci/config.yml)

&emsp; &emsp;CircleCI配置文件由三部分组成，从配置名基本可以看出对应的执行流程

- version
- jobs
    - test
    - integration_tests
    - deploy_dev
    - deploy_vnext
    - deploy_stage
- workflows
    - test_pr
        - test
        - integration_tests
    - build_and_deploy_dev
        - deploy_dev
        - deploy_vnext
    - build_and_deploy_stage
        - test
        - integration_tests
        - deploy_stage

## 二、项目的历史轨迹分析

&emsp; &emsp;我们对项目mozilla/send创建 - 归档 期间的数据分析如下，代码详情见 send.ipynb

1. 每月新增 Star 和 Frok 的个数
    
    ![Untitled](pic/analysis1.png)
    
2. 每月打开 Issue 和 关闭 Issue 的个数
    
    ![Untitled](pic/analysis2.png)
    
3.  每月打开 PR 和**合入** PR 的个数（注意，关闭 PR 不等于合入）
        
    ![Untitled](pic/analysis3.png)
        
4.  每月在仓库中活跃（只要有日志产生就算）的不同开发者总数
        
    ![Untitled](pic/analysis4.png)
        
5.  Issue 从打开到关闭的平均时长和中位数（单位：天）
6.  PR 从打开到合入的平均时长和中位数（单位：天）
7.  Issue和PR从打开到第一次有人回复（非本人回复）的平均时长和中位数（单位：天）
    ![Untitled](pic/analysis5.png)
8.  根据你观察到的仓库的历史数据，尝试找到几个你认为关键或值得注意的时间节点
    1. 2017年5月 项目开始
    2. 2017年8月 fork，star，issue，pr等数据达到第一个峰值
    3. 2019年3月 火狐将send服务上线，fork，star等数据达到第二个峰值
    4. 2020年9月 火狐宣布下线，fork，star等数据达到最后一个峰值

## 三、洞察项目被归档的可能原因

&emsp; &emsp; 2021年5月22日，mozilla/send 项目归档，并且在2020年9月就以停止相关服务。从上述数据分析的结果中可以观察到，本项目自2019年3月，火狐将Send项目上线，至2020年9月其下线，Fork和Star一直处于稳定增加的状态，并在这两个时间点出现爆炸式的增长。同样，仓库的每月活跃数也呈现相同的状态、同时，issue和pr逐渐减少。因此，可以推断本项目的热度在其服务开放时期，一直保持稳定。但从其官方的博客中了解到，一些滥用的用户开始使用此项目来发布恶意软件并进行网络钓鱼攻击。这些恶意软件和木马病毒通常以压缩包的形式分享，部分用户看到是火狐的安全链接后，就会解压执行。据网络安全研究人员分析，由于Firefox的URL是受信任且加密的，所以这类钓鱼的邮件不会被安全系统检测到。所以，有了Firefox Send这个现成的工具，网络犯罪团队甚至不必花费自己的精力财力来搭建一个新平台，还能绕过大量安全检测。而作为一个文件临时中转站，理论上Firefox并没有审查用户文件的义务，如果真的审查了，还会引发侵犯用户隐私的问题。鉴于此两难的情况，官方团队Mozilla只能宣布永久关闭用于传输文件的Firefox Send服务，并且在一年后将此项目进行了归档。综上所述，本项目归档可能的主要原因在于，此项目的服务存在不可修复的安全问题，进而导致了项目的归档。

&emsp; &emsp; 此项目归档后，对于仅使用火狐 Send 服务的用户的影响是最严重的，他们无法再使用此服务。而对于使用此项目自己搭建传输服务的用户来说则可以继续使用，但存在潜在的安全风险。而对于开发者来说，由于原项目已经归档，无法再提交issue和pr，继续开发的难度也大大增加。

&emsp; &emsp; 开源项目如何可持续发展一直是开源项目面临的重要问题。目前，人们更关注的往往是如何将开源项目商业化变现从而更长久的发展。而从此项目中可以看到，开源项目的安全问题也是如何可持续发展的需要着重关注的问题。鉴于此项目，mozilla/send项目已经是火狐这样一个成熟的公司所开源的项目，他在上线后广受关注和好评，而且已经不需要考虑从项目中营收的相关问题。相反，仅仅由于少部分恶意用户的攻击，开发者就迫于无奈的停止服务。由于此项目的特殊性，可能已经无法通过代码的维护来解决相关的安全问题。但可以从中的吸取的教训是，在项目的开发和维护时需要时刻关注如何保证普通使用者的安全。