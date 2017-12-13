#### 管理员sig

在腾讯云后台设置了管理员账号，用于发送云通信，发送通讯需要管理员账号拥有userSig，并且userSig的有效期为180天

因此制作了一个定时任务php代码，代码位置为:php项目根路径/cron/createSig.php

包括cron下的其他定时类，都需要在linux下设置crontab，具体设置方法为，命令行输入:

> ```
> crontab -e
> ```

然后会弹出一个vi界面可以输入内容，把下面内容贴上去（具体要看当前项目路径）

> ```
> * * * * * /usr/bin/php /usr/share/nginx/html/zhibo/cron/ClearInactiveLive.php
> * * * * * sleep 30; /usr/bin/php /usr/share/nginx/html/zhibo/cron/ClearInactiveLive.php
>
> * * * * * /usr/bin/php /usr/share/nginx/html/zhibo/cron/ClearDeathRoomMember.php
> * * * * * sleep 15; /usr/bin/php /usr/share/nginx/html/zhibo/cron/ClearDeathRoomMember.php
> * * * * * sleep 30; /usr/bin/php /usr/share/nginx/html/zhibo/cron/ClearDeathRoomMember.php
> * * * * * sleep 45; /usr/bin/php /usr/share/nginx/html/zhibo/cron/ClearDeathRoomMember.php
>
> * * 1 * * /usr/bin/php /usr/share/nginx/html/zhibo/cron/createSig.php
> ```

![](/assets/cron.png)

crontab为linux下定时任务 但是最小时间是1分钟因此设置30秒或者设置15秒需要做特殊操作，如上图，sleep 15 就可以在15S的时候运行，sleep 30 可以在30S的时候运行，以此类推

