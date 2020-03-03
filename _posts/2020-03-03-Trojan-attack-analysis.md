---
published: ture
layout: post
title: "挖矿木马植入服务器分析"
author: Yu
categories:
tags:
- 木马
- 挖矿
---

用了这么多年 linux，第一次遇到了挖矿木马植入攻击[^1]。记录一下分析和解决过程。

#### 事情经过

昨天用 top 命令服务器 cpu 使用情况，突然发现一个用户占用了 8 个 cpu 跑了一个`cron`，并且运行时间越来越长。

![top_screenshot](https://i.imgur.com/8bioErQ.png)

这个用户一般情况下是不会去使用服务器的，所以我立马引起警觉，联系当事人，询问情况。

很显然该用户没有做任何操作。

由于这个服务器本身的一些原因，暂时无法解决的安全问题，这次并没有查出入侵的原因是管理员用户弱密码攻击，还是运行的某些服务有漏洞。

#### 删除木马程序

首先要做的是关掉这个`cron`程序。

```bash
ps -aux | grep cron
kill -9 进程号

#如果没有其他cron job运行，可以直接杀掉crontab

pkill -9 crontab
```

接下来删除这个 cron 定时任务。

```bash
crontab -r 用户名
```


之后开始查找木马文件，进入该用户目录，发下了隐藏的文件夹`.bashtemp`。


```bash
.
├── a
│   ├── a
│   ├── anacron
│   ├── bash.pid
│   ├── cron
│   ├── dir.dir
│   ├── init0
│   ├── run
│   ├── stop
│   └── upd
├── b
│   ├── a
│   ├── dir.dir
│   ├── run
│   ├── stop
│   └── sync
├── cron.d
└── dir2.dir
```

看到`cron.d`是执行的定时任务。`/home/用户名/.bashtemp/b/sync`是所执行的程序。

```bash
0 0 */3 * * /home/用户名/.bashtemp/a/upd>/dev/null 2>&1
@reboot /home/用户名/.bashtemp/a/upd>/dev/null 2>&1
5 8 * * 0 /home/用户名/.bashtemp/b/sync>/dev/null 2>&1
@reboot /home/用户名/.bashtemp/b/sync>/dev/null 2>&1  
0 0 */3 * * /tmp/.X19-unix/.rsync/c/aptitude>/dev/null 2>&1
```

`.bashtemp/b/sync`是一段 shell 脚本，用来运行`.bashtemp/b/run`里面的内容，`run`里是恶意挖矿脚本以及添加黑客的 rsa 公钥加到`/root/.ssh/authorized_keys`的程序，具体内容和详细分析参见参考资料4[^4]。

密钥长这个模样:

```bash
AAAAB3NzaC1yc2EAAAABJQAAAQEArDp4cun2lhr4KUhBGE7VvAcwdli2a8dbnrTOrbMz1+5O73fcBOx8NVbUT0bUanUV9tJ2/9p7+vD0EpZ3Tz/+0kX34uAx1RV/75GVOmNx+9EuWOnvNoaJe0QXxziIg9eLBHpgLMuakb5+BgTFB+rKJAw9u9FSTDengvS8hX1kNFS4Mjux0hJOK8rvcEmPecjdySYMb66nylAKGwCEE6WEQHmd1mUPgHwGQ0hWCwsQk13yCGPK5w6hYp5zYkFnvlC8hGmd4Ww+u97k6pfTGTUbJk14ujvcD9iUKQTTWYYjIIu5PmUux5bsZ0R4WFwdIe6+i6rBLAsPKgAySVKPRK+oRw== mdrfckr
```

用这个公钥在网上一搜，可以发现不少中招的信息。

通过上面的定时人物，还可以发现在`/tmp`文件夹下有一个隐藏的文件夹`.X19-unix`, 里面有一个dota3的压缩包和隐藏的`.rsync`文件夹，压缩包查看内容后发现是整套木马程序(`.rsync`里的内容)。

```bash
.
├── dota3.tar.gz
└── .rsync
    ├── 1
    ├── a
    │   ├── a
    │   ├── anacron
    │   ├── cron
    │   ├── init0
    │   ├── run
    │   └── stop
    ├── b
    │   ├── a
    │   ├── run
    │   └── stop
    ├── c
    │   ├── 1
    │   ├── aptitude
    │   ├── dir.dir
    │   ├── go
    │   ├── golan
    │   ├── lib
    │   │   ├── 32
    │   │   │   ├── libc.so.6
    │   │   │   ├── libdl.so.2
    │   │   │   ├── libnss_dns.so.2
    │   │   │   ├── libnss_files.so.2
    │   │   │   ├── libpthread.so.0
    │   │   │   ├── libresolv-2.23.so
    │   │   │   ├── libresolv.so.2
    │   │   │   └── tsm
    │   │   └── 64
    │   │       ├── libc.so.6
    │   │       ├── libdl.so.2
    │   │       ├── libnss_dns.so.2
    │   │       ├── libnss_files.so.2
    │   │       ├── libpthread.so.0
    │   │       ├── libresolv-2.23.so
    │   │       ├── libresolv.so.2
    │   │       └── tsm
    │   ├── n
    │   ├── run
    │   ├── scan.log
    │   ├── slow
    │   ├── start
    │   ├── stop
    │   ├── tsm
    │   ├── tsm32
    │   ├── tsm64
    │   ├── v
    │   └── watchdog
    ├── dir.dir
    ├── init
    ├── init2
    ├── initall  <---安装木马程序到服务器
    └── .out
```

上面的程序，会安装木马到指定的用户目录下，并改写 root 目录下的 ssh 公钥。所以如果只删除了用户目录的可以程序，并不能解决问题。

### 如何防范这种事情再次发生？

1. 安装 fail2ban[^7] 禁止多次尝试用户名密码撞库的 ip
2. 禁止通过 ssh 方式用 root 账号登录服务器（即，只让用管理员账号登录）
3. 关闭常用的 22 端口


参考资料：

[^1] [Analysis Report cron](https://www.joesandbox.com/analysis/202041/0/html)
[2] [Dota3: Is your Internet of Things device moonlighting?](https://blogs.juniper.net/en-us/threat-research/dota3-is-your-internet-of-things-device-moonlighting)
[3] [Strange Cron Job takes up 100% of CPU Ubuntu 18 LTS Server](https://askubuntu.com/questions/1161003/strange-cron-job-takes-up-100-of-cpu-ubuntu-18-lts-server)
[4] [分享一次惨痛亲身经历之es服务服务器被入侵植入挖矿木马溯源分析](http://m.lanhusoft.com/Article/745.html)
[5] [Outlaw Hacking Group’s Botnet Observed Spreading Miner, Perl-Based Backdoor](https://blog.trendmicro.com/trendlabs-security-intelligence/outlaw-hacking-groups-botnet-observed-spreading-miner-perl-based-backdoor/)
[6] [How To Protect SSH With Fail2Ban on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-centos-7)
