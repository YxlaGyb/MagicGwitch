---
title: Windows Git GPG 密钥访问锁与超时问题
published: 2025-09-21
description: 这篇文章演示如何在博客文章中嵌入视频。
tags: [Git, GPG, Windows]
draft: false
---

在准备开开心心提交代码的时候，诶？！提交不了？

尝试查看 GPG 密钥，发现连接超时？正在等待锁？

```
$ gpg --list-secret-keys --keyid-format LONG
gpg: Note: database_open 134217901 waiting for lock (held by 185) ...
gpg: Note: database_open 134217901 waiting for lock (held by 185) ...
gpg: Note: database_open 134217901 waiting for lock (held by 185) ...
gpg: Note: database_open 134217901 waiting for lock (held by 185) ...
gpg: Note: database_open 134217901 waiting for lock (held by 185) ...
gpg: keydb_search_first failed: Connection timed out
```

使用 `ps aux | grep gpg` 命令查看有没有 GPG 进程在运行，发现没有

研究了亿小会，找到了个解决方法，

前往路径 `C:\Users\[你的Windows账号]\.gnupg\` 找一下有没有 `pubring.db.lock`

如果有你直接把 `pubring.db.lock` 删除掉即可，我反正是恢复了
