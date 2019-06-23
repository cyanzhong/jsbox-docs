# 原生 SDK

在这一章我们主要介绍 JSBox 对 iOS 原生 SDK 的封装，通过这些接口我们可以用 JavaScript 代码调用原生接口，从而实现强大的扩展功能。

iOS 的原生 SDK 是非常多的，目前 JSBox 第一版只实现了其中最重要的一些 SDK，以下是一个简短的介绍。

# $message

用于发送短信和邮件，相比于 `$system.sms` 和 `$system.mailto` 而言有更灵活的参数。

# $calendar

用于对系统日历进行读取和存储的接口。

# $reminder

用于对系统提醒事项进行读取和存储的接口。

# $contact

用于对系统联系人进行读取和存储的接口。

# $location

用于获取用户地理位置和罗盘数据等信息的接口。

# $motion

用于获取设备加速度等传感器数据的接口。

# $spotlight

用于更新 spotlight 索引的接口。

# $push

用于安排本机推送提醒的接口。

# $safari

通过 Safari View Controller 打开网页，获得比 WebView 更好的体验。

> 以上只是一个简短的介绍，在后面可以查询各个接口如何使用。