安装 shadowsocks
```
$ sudo pip install shadowsocks
```
```
root@XS103852412:~# cat shadowsocks.json 
{
"server":"0.0.0.0",
"server_port":10666,
"password":"xxxx",
"local_address":"127.0.0.1",
"local_port":1080,
"timeout":600,
"method":"aes-256-cfb"
}
```
```
root@XS103852412:~# ssserver -c shadowsocks.json
INFO: loading config from shadowsocks.json
2020-03-28 21:24:10 INFO     loading libcrypto from libcrypto.so.1.0.0
2020-03-28 21:24:10 INFO     starting server at 0.0.0.0:10666
```
