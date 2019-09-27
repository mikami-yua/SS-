# SS-
使用chacha20加密方式，并解决使用这种加密方式可能遇到的问题。操作系统Ubuntu。本地与服务器端的连接采用putty。


进入ubantu系统后：
0、更新软件源
sudo apt-get update
1、安装pip3
sudo apt-get install python3-pip

2、先用python3安装shadowsocks：
sudo pip3 install shadowsocks

3、编辑配置文件
sudo vim /etc/shadowsocks.json
i进入编辑
{
"server":"ip",
"server_port":8888,
"local_address":"127.0.0.1",
"local_port":1080,
"password":"888888",
"timeout":500,
"method":"chacha20",
"fast_open":false
}
按esc退出编辑 按‘:wq’保存退出。这里需要做出一些更改。
"server":"ip"中的ip改为服务器的ip
"server_port":8888其中的8888可以改为自己喜欢的数字，这是服务器的端口号
"password":"888888"这是连接的密码可以设置为自己喜欢的数字
其他选项不建议更改


4、启动服务（以后台方式启动）
sudo ssserver -c /etc/shadowsocks.json -d start

如果使用之前版本的Ubuntu操作系统可能会遇到libsodium not found问题，可以返回服务器提供商的服务器选择页面重新选择操作系统，重复上面的操作。也可以按照下面的方法解决。按照下面的方法不需要做任何额外的操作，只需要继续输入下面的指令即可。
如果你没有遇到任何问题，搭建已经完成。

libsodium not found问题
1. 安装依赖
sudo apt-get update
sudo apt-get install build-essential wget -y
2. 下载 libsodium 最新版本
wget https://download.libsodium.org/libsodium/releases/LATEST.tar.gz
3. 解压
tar xzvf LATEST.tar.gz
4. 生成配置文件
cd libsodium*
./configure
5. 编译并安装
make -j8 && make install
6. 添加运行库位置并加载运行库：
echo /usr/local/lib > /etc/ld.so.conf.d/usr_local_lib.conf
ldconfig
7.再尝试启动服务
cd ..
启动服务（以后台方式启动）
sudo ssserver -c /etc/shadowsocks.json -d start

up实测数次可以解决问题
如果你执行了所有步骤依然不能上网冲浪，请留言，我看到了会和你一起思考并尽力提供帮助
                 
	      
