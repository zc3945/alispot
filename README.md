# 概述
* 目前阿里云海外节点的抢占式实例非常便宜，平均都在0.01\~0.02元/小时，外加流量费0.5\~1.0元/G，特别适合上班族尤其是程序员使用。
* 上班来了启动脚本，下班了自动释放，一点不浪费，只要不看视频，一天的成本也就2毛钱。
* 本脚本自动创建阿里云抢占式实例，启用GoogleBBR网络加速，然后自动安装启动SSR服务器。
* 使用speedtest.net实测速度，可以跑满带宽上限。
* 注意，本人仅在Windows10 x64上测试过，其它平台未测试。

# 前提
* 在阿里云有个账号
* 充值120块钱，账户余额必须在100以上才能创建抢占式实例，剩下20只要不经常看视频应该够用很久
* 在阿里云控制台"访问控制"里面，添加一个RAM用户
* 给该RAM用户添加AliyunECSFullAccess和AliyunVPCFullAccess权限
* 给该RAM用户创建一个AccessKey，然后把AccessKey ID和AccessKey Secret记住。注意：Secret只会显示一次，一定马上复制保存好！！
* node.js，我只在node12上测试过，但估计node8以上都应该没问题
* 本脚本不包含SSR客户端，请自行安装，推荐C#版本

# 安装
* 把项目克隆到本地
* 执行 `npm install`

# 配置
* 修改config.json
* 把前面保存的AccessKeyID和AccessKeySecret填入RAM配置段
* 填入服务器地域ID，推荐新加坡`ap-southeast-1`，速度快还便宜
* 推荐设置一个自动释放时间，否则1小时后可能会被自动回收
* 根据你使用的SSR客户端的配置信息，修改ssr_server配置段

# 启动
* 执行 `npm start` 然后等待即可
* 命令是按照windows配置的，linux/mac上没测过，可以试试：<br/>
  `node index.js | ./node_modules/.bin/bunyan`<br/>
   bunyan是日志过滤工具，不用也可以
* 整个脚本运行大概需要3 ~ 5分钟，最后会打印出SSR连接信息，照此修改客户端配置即可，通常就是改个IP
* 脚本最后会使用forward.js创建一个端口转发，这样SSR客户端只要把服务端IP设成localhost即可，连上一步说的IP都不用改了

# 参考
* [阿里云 OpenAPI Explorer](https://api.aliyun.com/#/)
* [ssr_py版的命令行参考](https://doubibackup.com/hi10k-7p-4.html)
* 启用BBR的shell脚本bbr.sh来自[这里](https://www.codercto.com/a/25431.html)，我这里为了实现自动化去掉了用户交互部分
* forward.js来自[这里](https://github.com/sjitech/forward.js)，因为这不是个node模块，因此直接引用源代码

