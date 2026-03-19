
## 6dy

声明: 此库所有内容仅用于个人学习！！！

### [TG CHANEL](https://t.me/dylan_jdpro)


国内机（带加速，也不太稳）：

```
ql repo https://js.googo.win/https://github.com/6dylan6/jdpro.git "jd_|jx_|jddj_" "backUp" "^jd[^_]|USER|JD|function|sendNotify|utils"

```


国外机（国外ip有限制可能有些任务不能正常运行）：

```
ql repo https://github.com/6dylan6/jdpro.git "jd_|jx_|jddj_" "backUp" "^jd[^_]|USER|JD|function|sendNotify|utils"

```



## 使用

1、部署青龙登陆，版本不用追新，稳定才好，推荐部署到内网（不要外网访问，2.20.2以下版本面板会被免密登录偷家，如果必须外网就用最新版本吧）。

2、到订阅管理创建订阅并运行；正确配置[参考](https://github.com/6dylan6/jdpro/issues/22)

3、订阅执行完，到定时任务搜索依赖安装（jd_indeps)任务执行；

4、到环境变量，创建变量，名称: JD_COOKIE,值：抓的CK（要安全就手抓），多个每行建一个，不要全写在一个；

5、配置通知，通知的key填写到配置管理config.sh文件；


<details>
<summary>笔记</summary>
<pre><code>

1、任务并发和分组

并发配置方法：

在任务后面加conc JD_COOKIE

如 task XXXXX.js conc JD_COOKIE

任务分组运行方法：

在任务后面加desi JD_COOKIE 需要运行的ck序号

如 task XXXX.js desi JD_COOKIE 1-10  前10个一组运行，2 8 9就是第2/8/9序号的ck执行，以此类推。

2、通知支持一对一推送和显示备注（需用本库sendnotify文件），还有分组通知等用法参考[notify.md](./notify.md)

备注显示变量如下

export NOTIFY_SHOWNAMETYPE="1"    不做任何变动

export NOTIFY_SHOWNAMETYPE="2"    效果是 :  账号名称：别名(备注)	

export NOTIFY_SHOWNAMETYPE="3"    效果是 :  账号名称：pin(备注)

export NOTIFY_SHOWNAMETYPE="4"    效果是 :  账号名称：备注

3、因为青龙有随机延时（可以在配置文件设置为0，默认300秒），所以涉及准点运行的任务，最后加now，如果是desi或conc不用加也会准时跑。

4、脚本的通知，需把通知key变量在config.sh文件配置。

5、建议调整任务运行超时时间，青龙默认1小时有些跑不完就被强制结束，config.sh里配置。CommandTimeoutTime="3h"  即改为3小时，根据自己ck数量调整。

6、ck掉线，不是常用地ip，短时间内连续获得豆可能就会会触发风控掉线


## 通用环境变量（到配置管理-config.sh里添加变量,export xxx='xxx'格式)

AUTOCFG='true' 自动配置sendNotify文件到deps目录 

代理API模式（API代理是通过url接得到随机可用代理ip，格式是：xxx.xxx.xxx.xxx:xxxx）

DY_PROXY='URL1#URL2' 多个#分割

PERMIT_API='test' 需要走API代理的js关键词，多个&分割，可不设置，支持的js都会走

DY_PROXY_RENUM='5'  获取IP失败重试次数

DY_PROXY_REDELAY='3' 获取失败重试间隔 单位秒



代理池模式（就是一个代理服务器的地址）

DP_POOL='http://xxx' 代理池url

PERMIT_JS='farm&plant&opencard' 需要走代理池的js关键词，多个&分割（可不设置，如果不设置就是所有的js都会走）



BANPIN 禁止某pin执行任务

ALLOWPIN 只执行某pin执行任务

多个任务同pin：任务1|任务2@pin1,pin2  

多个任务不同pin：任务1@pin,pin2&任务2@pin2,pin3

不指定任务只写pin：全部任务

示例 

export BANPIN='draw@pin1,pin2'

export ALLOWPIN='draw@pin1,pin2'

## 支持的通知方式

server酱，go-cqhttp，pushdeer，Bark App，tg bot，钉钉bot，企业微信bot，企业微信应用消息，飞书，iGot，push plus，WxPusher，gotify

请在配置管理config文件里填写对应key
