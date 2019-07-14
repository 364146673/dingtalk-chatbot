# 钉钉群自定义机器人
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/baiyutang/dingtalk/badges/quality-score.png?b=master&s=11172c454383990e38a320295a72cbd98f426cc6)](https://scrutinizer-ci.com/g/baiyutang/dingtalk/?branch=master)

采用面向对象的开发方法

## 功能列表

- [x] 实现原始 text / markdown / link / action card 类型消息发送
- [x] 消息设置可支持链式调用
- [x] 单独设置 @ 的数据，亦可链式调用设置多个 @ 的手机号。注意：设置 @ 所有人时，@ 单独手机号会失效
- [x] 发送群可指根据配置随意指定
- [x] 机器人token均可配置
- [ ] 支持自定义的告警消息模板

## 用法

```php
// text 类型
use DingTalkRobot\At;
use DingTalkRobot\DingTalkGroup;
use DingTalkRobot\Messages\TextMessage;
use DingTalkRobot\RobotClient;

// 链式调用设置 @ 多个手机号
$at = new At();
$at->setMobile('181****3753')
    ->setMobile('181****3751');

// 链式调用设置消息内容
$message = new TextMessage();
$message->setContent('我就是我, 是不一样的烟火')
    ->setAt($at);

$client = new RobotClient();
// 可以指定群，若不设置则发送默认的群
$client->send($message, new DingTalkGroup('other'));
```
---
```php
// markdown 类型
use DingTalkRobot\DingTalkGroup;
use DingTalkRobot\Messages\MarkdownMessage;
use DingTalkRobot\RobotClient;

$markdown = new MarkdownMessage();
$markdown->setTitle('杭州天气')
    ->setText("#### 杭州天气\n" .
        "> 9度，西北风1级，空气良89，相对温度73%\n" .
        "> ![screenshot](http://tinyurl.com/y4lbucte)\n" .
        "> 10点20分发布 [天气](http://www.thinkpage.cn/)");

$client = new RobotClient();

$client->send($markdown, new DingTalkGroup());
```
> 建议：引入该sdk可以在项目中再封装一次

## 相关
* [钉钉开发文档：自定义机器人](https://open-doc.dingtalk.com/microapp/serverapi2/qf2nxq#-9)

## License
[MIT license](LICENSE)