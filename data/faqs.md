## What does FAQ mean
Frequently Asked Questions!
tags: faq

## How do I add a new FAQ?
Add to the page here:
link: https://github.com/dcsan/faqbot/blob/master/data/faqs.md

tags: howto

## 1.1 I can not login with my Wechat account
Wechat account that registered after 2017 will not be able to login via Web API. Learn more at https://github.com/Chatie/wechaty/issues/872

Solution: Wechaty support protocols other than Web API, such as pad. Learn more at https://github.com/Chatie/wechaty/issues/1296


## 2.1 Does wechaty support Red envelope, transfer money, moment?
Short answer: NO

Long answer:

Payment: we won't support this because this related to property security
@ someone in the room: we will support this in the future in solutions other than Web API.
Send Contact Card: we support this in ipad solution.
Send Share Card: we will support this in the future in solutions other than Web API.
Send Voice: we will support this in the future in solutions other than Web API.
Moment: we haven't decide yet whether to support this function

## 2.2 Can wechaty send url rich media message?
Not yet at this moment, will support later

Related Issue：
- Add support for send url rich media message
- can wechaty send share card msg

## 2.3 I don't know wechaty support for personal account of wechat official account
At this moment, wechaty only support personal account

Related Issue:
- Using wechaty to start a wechatOA account


## 3.1 What is a Puppet in Wechaty
The term Puppet in Wechaty is an Abstract Class for implementing protocol plugins. The plugins are the component that helps Wechaty to control the Wechat(that's the reason we call it puppet).

The plugins are named XXXPuppet, like PuppetPuppeteer is using the chrome puppeteer to control the WeChat Web API via a chrome browser, PuppetPadchat is using the WebSocket protocol to connect with a Protocol Server for controlling the iPad Wechat program.

## 3.2 Wechaty & Queue
In order not blocked by wechat, we add queue in wechaty, see more: rx-queue

## 3.3 What's the difference between wechaty and wechat4u?
Wechaty can implement many wechat protocol plughins. The plugins are the component that helps Wechaty to control the Wechat. Wechaty provide same API in web, ipad, ios solutions. wechat4u is SPACELAN write as a web solution on github. Wechaty can use wechaty API call wechat 4u API

Is this right: wechaty has All api in wechat4u, but wechat 4u don't have all api wechaty has.

No, wechaty use wechaty itself API for wechat4u. They are totally 2 different project and no one contains another.

## 3.4 I found there is a default.memory-card.json in the root directory, what does this do?
The default.memory-card.json stores the bot's login information, which can be used to save bot's personal information, so the bot can auto login to Wechat after the first time.

## 3.5 If the default.memory-card.json stores my bot's personal information, what if I want to start multiple bots? Are they gonna share the same file?
If you want to fire up multiple bots on one machine, you can setup the name for the memory-card, so you will have multiple memory-card.json files, To setup the name, you need to setup the profile for your bot, you have two options to do this:

1. Set the profile with option of the constructor, like this
const bot = Wechaty.instance({ profile: 'your-cute-bot-name' })
2. Set the environment variable for WECHATY_PROFILE during the start
WECHATY_PROFILE="your-cute-bot-name" node bot.js
Then you will see a file called your-cute-bot-name.memory-card.json file in the root folder.

## 3.6 Why wechaty.on(event, listener) return Wechaty
This is for chaining.

Method chaining, also known as named parameter idiom, is a common syntax for invoking multiple method calls in object-oriented programming languages. Each method returns an object, allowing the calls to be chained together in a single statement without requiring variables to store the intermediate results. More info in wiki

Wechaty class support method chaining, you could write code like this:

const { Wechaty } = require('wechaty')
const bot = new Wechaty()
.on('scan', (qrcode, status) =>  {})
.on('login', user => {})
.on('message', message => {})
.start()
 Add a custom footer



## What's the easiest way to start using Wechaty?

1. Clone our Starter Project at <https://github.com/Chatie/wechaty-getting-started>
2. Run `npm install`
3. Run `npm start`
4. Our demo example will be runned out-of-the-box
5. Modify our demo example to implement your own bot logic

tags: getting-started

## Why are the entire project writing in English?

First, it's the author's choice: he wants to practice English by writing more.

Second, according to [PEP8 from Python](https://www.python.org/dev/peps/pep-0008/#comments):
> ... coders from non-English speaking countries: please write ... in English, unless you are 120% sure that the code will never be read by people who don't speak your language.

tags: en, english

## Why doesn't the entire project use the semicolon?

It's just author's favorite.

And I'm also supporting to not use semicolons, because of:
1. <http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding>
1. <http://inimino.org/~inimino/blog/javascript_semicolons>
1. <https://www.youtube.com/watch?v=gsfbh17Ax9I>

So I would like to suggest all my friends not to use the semicolon, which is a _JS Standard Code Style_.

[![JS Standard Coding Style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://standardjs.com/rules.html#semicolons)

> No semicolons.

Related PR:
* [#362](https://github.com/Chatie/wechaty/pull/362/files/3c3c9ef92b05149ab5813248d454943102ccdcd3..fe29a6c154bc64a603d934c7954c538c38e2ea60#r111056262)

tags: code-style

## How to Understand the Wechaty Semantic Versioning?

### Short answer:

Even Minor Number is for Production.

### Long Answer:

Wechaty is following the Semantic Versioning 2.0 <http://semver.org/> and will use the MINOR version to indicated the release is for **Production** or NOT.

Numbering rule:
1. even numbers, such as 0.8, 0.12, is for production use.
1. odd numbers, such as 0.11 or 0.13, is development releases.

According to [#905](https://github.com/Chatie/wechaty/issues/905) [#1158](https://github.com/Chatie/wechaty/issues/1158), when the **minor version number** in SemVer is odd, it means it comes from a developing branch, and it will not be ready for Production.

**even** Examples: (for Production)
* 0.**16**.1
* 0.**16**.2
* 1.**0**.1
* 1.**0**.2

**odd** Examples: (for Development)
* 0.**15**.1
* 0.**15**.2
* 1.**1**.1
* 1.**1**.2

At the same time, we publish all the version to NPM when the code base passed the Automatic Testing by Travis CI.

We should only publish to NPM via CI/CD for the STABLE/PROD version for the master branch, which means we should limit it to the version number is even.

### See Also

* https://stackoverflow.com/q/43210945/1123955
* https://docs.npmjs.com/misc/config#environment-variables

Copy from **Linux Kernel Version Numbering** - http://www.linfo.org/kernel_version_numbering.html :

> The second number denotes the major revision of the kernel version. It was formerly the case that even numbers indicated a stable release, that is, one that was deemed fit for production use (i.e., use in a non-experimental environment), such as 1.2, 2.4 or 2.6. Likewise, odd numbers, such as 1.1 or 2.5, have historically represented development releases. They were for testing new features and device drivers until they became sufficiently stable to be included in a stable release. However, this has changed starting with the Linux 2.6.x series, and new feature development now takes place in the same revision number.

## Why login via scanning the QRcode instead of just username and password?

> I see in the code the ability to log in via username and password, so probably I can create an account from scratch and do not need to scan the QR .... but why not?

Yes, you are right.

Some of the puppet(Wechaty Puppet, specifically) has the ability to login via username and password, as you see in the code. However, I have no plan to add an API to enable login via username and password yet, because of the following three reasons:

1. some of the puppets do not have the ability to do that, for example, PuppetWechat4u, which is using the Web API;
1. when you log in by scan QR Code, you can keep your session on your phone, which means you can use WeChat at the same time when your Bot is online; If you login in by username/password, then all other login sessions will be terminated, only your Bot can use WeChat.
1. as you have already seen, we are using a Protocol Server to control the iPad WeChat. If you want to use username/password to log in, then you will have to send that sensitive information to a 3rd party server, which will not be comfortable for most people.

tags: login

## How to send the message without onMessage?

Send message to one room
```ts
const room = await wechaty.Room.find('room name')
room.say('hello room')
```

Send message to one contact
```ts
const contact = await wechaty.Contact.find('contact name')
contact.say('hello room')
```
See more example at https://github.com/Chatie/wechaty/wiki/Example

Related issues:
* [#446](https://github.com/Chatie/wechaty/issues/446) how to send mesage without onMessage
* [#200](https://github.com/Chatie/wechaty/issues/200) [new feature] Forward Message
* [#89](https://github.com/Chatie/wechaty/issues/89) Wechaty.send() error when send message to the room
* [#41](https://github.com/Chatie/wechaty/issues/41) [New Feature] send message by branding new method: say()


## Get ERROR: can not found bot file: xxx.js when using docker to start wechaty.

First, please make sure you have the file `xxx.js`, if you get an error again, please check `SELinux` settings for your Linux:

**SELinux** is setting to enforcing mode by default with `CentOS/RHEL` installation. (`Ubuntu` default installation had never seen this.)

_SELinux is another user access control system. By setting user/role/type attribute for folder and files, it define how processes interact with files, as well as how processes interact with each other. Using `getenforce` and `sestatus` to check the SELinux status._

Add :Z label to allow docker to modify the selinux label: (check with ```ls -laZ```)
```shell
docker run -ti --rm --volume="$(pwd)":/bot:Z zixia/wechaty xxx.js
```
(Note: It will lost their last selinux label, that may raise another 'Permission Denied' from program which using this folder.)

**Another method**, disable SELinux (Not recommended)
What you need to do is to run:
```shell
setenforce 0
```

**Related documents:**
* [Docker: Configure the selinux label](https://docs.docker.com/storage/bind-mounts/#configure-the-selinux-label)
* [RHEL: SELinux Introduction](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/selinux_users_and_administrators_guide/chap-security-enhanced_linux-introduction)

**Related blog:**
* [Find if permission denied errors are caused by SELinux](https://www.mysysadmintips.com/linux/servers/587-find-if-permission-denied-error-is-caused-by-selinux)

**Related issues:**
* [#66](https://github.com/Chatie/wechaty/issues/66#issuecomment-374086724) Dockerize Wechaty for easy start

tags: troubleshooting

## 我的微信号无法登陆
从2017年6月下旬开始，使用基于web版微信接入方案存在大概率的被限制登陆的可能性。 主要表现为：无法登陆Web 微信，但不影响手机等其他平台。 验证是否被限制登陆： https://wx.qq.com 上扫码查看是否能登陆。 更多内容详见：

Can not login with error message: 当前登录环境异常。为了你的帐号安全，暂时不能登录web微信。
[RUMOR] wechat will close webapi for wechat
New account login issue
wechaty-puppet-puppeteer
解决方案：我们提供了非web 版本的解决方案，正在进行alpha 测试，点击申请测试token，技术细节及实现请查看wechaty-puppet-padchat

more: https://github.com/wechaty/wechaty-getting-started/wiki/FAQ-ZH#11-%E6%88%91%E7%9A%84%E5%BE%AE%E4%BF%A1%E5%8F%B7%E6%97%A0%E6%B3%95%E7%99%BB%E9%99%86

## 支持 红包、转账、朋友圈… 吗？
以下功能目前 均不支持

支付相关 - 红包、转账、收款 等都不支持 在群聊中@他人 - 是的，Web 微信中被人@后也不会提醒 发送名片 发送分享链接 发送语音消息 - 后续会支持 朋友圈相关 - 后续会支持

## wechaty 是否可以发送卡片消息，然后点击跳转到网页
现阶段还不可以，后续会在非web 解决方案中陆续支持

相关Issue：

Add support for send url rich media message
can wechaty send share card msg

## wechaty 是支持个人号还是公众号？
现阶段，wechaty 只支持个人号

相关Issue:

Using wechaty to start a wechatOA account

## wechaty & 队列的最佳实践
为了防止微信封号，wechaty 内置了队列，详细可见：rx-queue

## wechaty 和 wechat4u 项目，有什么区别？
wechaty 可以实现多个微信接入的方案，对外提供统一的接口，包括web，ipad，ios等等，其中wechat4u 是SPACELAN写的基于web 实现微信接入的，wechaty 可以实现用wechaty 的接口，调用wechat4u的api。

这么理解：wechat4u有的，wechaty都有，反之不一定有，对么？

这个也不是完全确定的，因为wechaty 只是基于wechaty 暴露出来的接口为wechat4u 进行了封装

## 我发现在根目录下有一个default.memory-card.json 的文件，这个文件是干什么的？
default.memory-card.json 会用来存储登陆信息，机器人可以通过这个文件实现自动登陆。

## 既然default.memory-card.json 存储了机器人的登陆信息，如果我想启动多个机器人，如何防止每次启动的时候加载不同的信息呢？
如果你想在一个机器上启动多个机器人，你可以通过设置 profile 的值设置不同的机器人登陆信息，对应的你得到多个*.memory-card.json文件。有两种方法可以设置profile

1. wechaty 初始化的时候设置profile

> const bot = Wechaty.instance({ profile: 'your-cute-bot-name' })

2. 通过设置WECHATY_PROFILE 环境变量传递profile

> WECHATY_PROFILE="your-cute-bot-name" node bot.js

这样，你就可以在根目录下看到your-cute-bot-name.memory-card.json的文件了。



## qrcode
each MiniProgram has it's own QR code. you can also generate three different types of custom QRs
https://github.com/MiniProgDevs/faqbot/wiki/Faqs#qrcode

tags: mp, qrcode

## parametric QR code 
You can generate QR codes with parameters...
https://github.com/MiniProgDevs/faqbot/wiki/Faqs#parametric QR code
