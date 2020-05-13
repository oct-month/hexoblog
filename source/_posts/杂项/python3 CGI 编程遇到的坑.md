---
date: 2020-01-22 11:34:18
tags:
    - 杂项
---

## python3 CGI 编程遇到的坑
当把.cgi文件放到/usr/lib/cgi-bin/目录下后，应该回到上一层目录，然后调用命令：python -m http.server --cgi 8081
来启动python3的服务，不然网页是打不开的。
然后访问的网页应该是：localhost:8081/cgi-bin/*.cgi
（8081可以自己改）
