
## DY

>加密js审查，无重复，默认无加购，内部互助(可选模式);

 
>欢迎大家issue、pr，会一一回复！


### 上车注意安全，不用不明js，app，exe！

### 防走失[TG频道](https://t.me/dylan_jdpro)

### 一键部署（2.11.3版本青龙，默认国内机拉库命令，建好后根据自己情况调整）

使用root用户运行下面一串命令，支持Centos/Ubuntu系统

```
curl -sSL https://js.dayplus.xyz/https://raw.githubusercontent.com/6dylan6/jdpro/main/docker/ql1key.sh -o install.sh && bash install.sh
```

## 拉库指令

【注意】2.11.1前版本青龙config.sh配置把GithubProxyUrl="https://ghproxy.com/ （差不在多19行）" 修改为GithubProxyUrl=""，否则拉取失败，以上版本无需配置。

2.13版本以上拉库方式变了，到订阅管理添加订阅，请看配置[截图](https://github.com/6dylan6/jdpro/issues/251)

国内机用下面指令（带代理）：

```
ql repo https://ghproxy.com/https://github.com/6dylan6/jdpro.git "jd_|jx_|jddj_" "backUp" "^jd[^_]|USER|JD|function|sendNotify"

```
如默认代理ghproxy.com 拉不动，换备用的 js.dayplus.xyz

国外机用下面指令（无需代理）：

```
ql repo https://github.com/6dylan6/jdpro.git "jd_|jx_|jddj_" "backUp" "^jd[^_]|USER|JD|function|sendNotify"

```

Gitee版不能正常拉取，已停止维护！（20220711）


任务定时建议 50 7-23/2 * * *  


线报监控类脚本已移除，需要的到 https://github.com/6dylan6/jdm.git

自动评价 需要的到 https://github.com/6dylan6/auto_comment.git


## 使用流程

1、青龙部署。

2、修改青龙config.sh配置，差不多在17行（特别注意，没有修改此配置，任务拉不全，一键部署忽略此处）

RepoFileExtensions="js py"修改为 RepoFileExtensions="js py sh ts" 保存

3、新建拉库任务，并执行，刷新浏览器即可看到添加的任务。

4、添加CK环境变量，多CK不要写在一起，每个都新建JD_COOKIE变量；



<details>
<summary>使用技巧与问题解答</summary>
<pre><code>

1、涉及兑换或需要抢的可以配置任务并发，就是全部一起跑。

并发配置方法：

在任务后面加conc JD_COOKIE

如 task XXXXX.js conc JD_COOKIE

任务分组运行方法：

在任务后面加desi JD_COOKIE 需要运行的ck序号

如 task XXXX.js desi JD_COOKIE 1-10  前10个一组运行，2 8 9就是第2/8/9序号的ck执行，以此类推。

2、极速版签到建议并发，号多跑很久的，一个号要30多分钟。。

task 6dylan6_jdpro_jd_speed_sign.js conc JD_COOKIE （具体任务路径不同版本不一样，按自己的写）

3、保价建议并发，否则可能前几个号正常跑，后面会报频繁！

task 6dylan6_jdpro_jd_price.js conc JD_COOKIE

4、通知支持一对一推送和显示备注，还有分组通知等用法参考[notify.md](./notify.md)

备注显示变量如下

export NOTIFY_SHOWNAMETYPE="1"    不做任何变动

export NOTIFY_SHOWNAMETYPE="2"    效果是 :  账号名称：别名(备注)	

export NOTIFY_SHOWNAMETYPE="3"    效果是 :  账号名称：pin(备注)

export NOTIFY_SHOWNAMETYPE="4"    效果是 :  账号名称：备注

5、因为青龙有随机延时（可以在配置文件设置为0，默认300秒），所以涉及准点运行的任务，最后加now，如果是desi或conc不用加也会准时跑。

6、青龙系统通知（新增删除任务、登录等通知），需把通知变量写到config.sh文件，在环境变量里只发脚本运行通知哈。

7、如果通知文件发现和库里的不一致，那是被青龙自带的覆盖了，手动拷贝一份到deps目录下。

8、建议调整任务运行超时时间，青龙默认1小时有些脚本跑不完就被强制kill，config.sh里配置。CommandTimeoutTime="3h"  即改为3小时，根据自己的号数量调整。
</code></pre>
</details>

## 加密脚本说明

<details>
<summary>加密脚本，不放心可禁用</summary>
<pre><code>
加密的会在任务后添加加密标识
开卡系列都加密 
</code></pre>
</details>

## 互助模式使用说明

集成互助研究院taskbefore,code模块，可实现临时禁止某些CK参加所有活动或某些活动功能，实现重组CK顺序功能，包括随机、优先、轮换、组队、分段等功能

常用变量举例：

Recombin_CK_Mode="1"  全部顺序随机

Recombin_CK_Mode="2" Recombin_CK_ARG1="15" 假设有100个CK，前15个CK按正常顺序靠前，其余CK随机乱序

Recombin_CK_Mode="3" Recombin_CK_ARG1="5" Recombin_CK_ARG2="5"  假设有100个CK，希望前5个账号始终保持在前部，剩余95个账号按照轮换模式每天轮换5个

其他用法具体参考[文档](https://docs.qq.com/doc/DTXh6QUVjRXJ1TFdN)


## 部分脚本环境变量

[Wskey转换环境变量](https://github.com/Zy143L/wskey)

|             Name             |             归属             |  属性  | 说明                                                         |
| :--------------------------: | :--------------------------: | :----: | ------------------------------------------------------------ |
|     `PET_NOTIFY_CONTROL`     |     东东萌宠<br>推送开关     | 非必须 | 控制京东萌宠是否静默运行,<br>`false`为否(发送推送通知消息),`true`为是(即：不发送推送通知消息) |
|    `FRUIT_NOTIFY_CONTROL`    |     东东农场<br>推送开关     | 非必须 | 控制京东农场是否静默运行,<br>`false`为否(发送推送通知消息),`true`为是(即：不发送推送通知消息) |
|    `NOTIFY_AUTOCHECKCK`    |       自动禁用失效CK开关  | 非必须 | 有CK失效自动禁用并通知，true为自动禁用，false不自动禁用，默认false |
|       `JOY_FEED_COUNT`       |        宠汪汪喂食数量        | 非必须 | 控制`jd_joy_feedPets.js`脚本喂食数量,可以填的数字10,20,40,80,其他数字不可. |
|       `NOTIFY_SKIP_LIST`       |        控制关闭某些标题的通知  | 非必须 | 通知标题在此变量里面存在(&隔开),则屏蔽不发送通知.例 : export NOTIFY_SKIP_LIST="临期京豆换喜豆&京东资产统计" |
|      `FRUIT_BEAN_CARD`       |    农场<br>使用水滴换豆卡    | 非必须 | 农场使用水滴换豆卡(如果出现限时活动时100g水换20豆,此时比浇水划算,推荐换豆),<br>`true`表示换豆(不浇水),`false`表示不换豆(继续浇水),脚本默认是浇水 |
|       `JD_UNSUB`             |      批量取消商品与店铺关注开关      | 非必须 | 控制jd_unsubscribe.js运行，默认为true取关，false不取关 |
|       `JD_CART_REMOVE`       |      清空购物车      | 非必须 | 控制jd_clean_car.js运行 ，默认false不清空，true清空 |
|   `WSKEY_DISCHECK`           |     wskey转换     | 非必须 | 默认为false检查，设置true为不检查直接转换 |
|   `DPSTOKEN`           |     店铺签到     | 非必须 | 多个&隔开 |




