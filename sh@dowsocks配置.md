安装 shadowsocks
```
$ sudo pip install shadowsocks
```
看到 Successfully installed shadowsocks-2.8.2 则代表安装成功

Ubuntu18.04中安装shadowsocks和privoxy全局代理

配置 shadowsocks

运行：
```
$ sudo gedit /etc/shadowsocks.json
```
在 shadowsocks.json 文件中写入：
```
{ 

"server":"代理服务器ip”,

"server_port":代理服务器端口,

"password":"代理服务器访问密码”,  

"local_address":"127.0.0.1”, 

"local_port":1080, 

"timeout":600, 

"method":"aes-256-cfb" // 代理服务器访问数据加密方式，根据自己配置ss 服务端时的配置自行填写

}
```
 

启动 shadowsocks
```
$ sudo sslocal -c /etc/shadowsocks.json -d -start
```
