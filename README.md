> 接口支持实时返回推广状态,方便业务逻辑

## 设置

建议登录后台设置`callback`网址

## 直链推广

您的推广链接形式如下:
```
https://zfbao.club/fa/?tg_user=admin&hours=置顶小时&zhufu=祝福语&author=付款人&tg_type=推广渠道

tg_user:推广人
tg_type:推广渠道,随意定义
hours:置顶小时=元
zhufu:祝福语
author:付款人
```

其中的各种参数都可自定义,具体参数可参考: [这里](https://zfbao.club/fa/)


## 直接post

还可将以上参数直接post到这个页面`https://zfbao.club/fa/pay.php`

## 回调接收:

付款成功后,如果定义了`tg_callback`网址,系统会将结果post到该页面
post内容如下:
```
Array
(
    [content] => 祝福内容
    [author] => 付款人
    [hours] => 1.05  (置顶小时=付款金额)
    [tg_user] => 推广人
    [tg_type] => 推广渠道,提前定义的
    [tg_callback] => 回调网址
    [paid] => 1 (1付款成功,不成功不回调)
)
```
接收demo
```
<?php
if ($_SERVER['REQUEST_METHOD'] != 'POST') {
	exit();
}
$author = $_POST['author'];
$hours = $_POST['hours'];
$tg_user = $_POST['tg_user'];
$paid = $_POST['paid'];
$tg_type = $_POST['tg_type'];
$tg_callback = $_POST['tg_callback']; //这个登录后台设置
$my_callback=???; //这个写到自己的代码里,用于校验是否一致
if(tg_callback == $my_callback){
//业务逻辑
}
```
