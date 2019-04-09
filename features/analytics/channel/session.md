# Session 规则

> 怎样的一系列行为算是一个Session？ 通常如下
>
> * iOS应用：用户屏熄、home键切换到后台、杀掉进程、跨天等视为会话结束
> * Android应用：用户杀掉进程、屏熄、按home键超过30秒、跨天等视为会话结束
> * H5/Web应用：用户从打开网页到离开视为一次会话，包括关闭整个浏览器、30分钟未进行新打开页面、触发事件等活动。如果一次访问跨天的话，会被切割成两次会话

**易观方舟根据用户实际访问的场景，抽象成以下四种规则，来判断一次访问**

| 切割规则 | 优先级 |
| :--- | :--- |
| 跨天 | 1 |
| 强制切割-帐号切换（暂未上线） | 2 |
| 强制切割-广告来源切换 | 3 |
| 新进程 | 4 |
| 可见页面间隔时间 | 5 |

**实际用户的使用场景**

| 场景 | 规则覆盖 |
| :--- | :--- |
| 直接打开A | 新进程 |
| B中的deeplink→A | 强制切割-广告来源切换 |
| 在A中→调起支付/分享→A | 可见页面间隔时间 |
| 在A→接电话→回到A | 可见页面间隔时间 |
| 在A→B中的deeplink→A | 强制切割-广告来源切换 |
| 在APC端→A移动端（跨屏） | 跨屏本身换Session |
| 帐号x使用A后退出登录，切换到帐号y | 强制切割-帐号切换 |
| 打开A一直亮着不操作 | 可见页面间隔时间 |
| 打开A一直在一个页面操作很长时间 | 可见页面间隔时间 |
| 通过消息通知打开A | 强制切割-广告来源切换 |
| 点击home键 | 可见页面间隔时间 |
| 点击两次返回 | 可见页面间隔时间 |
| 锁屏 | 可见页面间隔时间 |
| 熄屏 | 可见页面间隔时间 |
| 主动杀掉进程 | 新进程 |
| 从今天玩到明天 | 跨天 |


