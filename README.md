# xtunnel
//导入的某大牛的开源项目，感谢开源，作者名当时没记，请作者联系下

XTunnel服务端Windows版

下载地址
http://fs.d1sm.net/xtunnel/xtunnel_server_windows.zip

说明
1.Windows版服务端运行需要java环境和winpcap.
2.Windows版配置文件位于cnf目录下,参数和linux版一样,但是需要在cnf目录下手动新建/编辑文件,文件名为listen_port,web_port,password,文件内容为设置值,password可增加多行,代表多个密码.

XTunnel服务端Linux版,支持Centos,Ubuntu,Debian

一键安装
rm -f install_xt.sh
wget  http://fs.d1sm.net/xtunnel/install_xt.sh
chmod +x install_xt.sh
./install_xt.sh 2>&1 | tee install.log

debian,ubuntu下如果执行脚本出错,请切换到dash,
切换方法: sudo dpkg-reconfigure dash 选no

更新
执行一键安装会自动完成更新.

绑定域名
单端口映射映射可以不绑定域名,网站映射必须绑定域名.
绑定命令
mkdir -p /xtunnel/cnf/ ; echo 域名 > /xtunnel/cnf/domain_name ; sh /xtunnel/restart.sh
登录域名控制面板,增加记录,假设域名为nwct.biz,服务器ip为9.9.9.9,需增加泛域名解析*.nwct.biz .

如果域名已有其他用途,为了避免冲突,可绑定二级域名,比如tunnel.nwct.biz,并增加泛域名解析*.tunnel.nwct.biz


卸载
sh /xtunnel/stop.sh ; rm -rf /xtunnel

启动
sh /xtunnel/start.sh

停止
sh /xtunnel/stop.sh

重新启动
sh /xtunnel/restart.sh

日志
tail -f /xtunnel/server.log

设置服务端口
默认tcp 180.
mkdir -p /xtunnel/cnf/ ; echo 180 > /xtunnel/cnf/listen_port ; sh /xtunnel/restart.sh

设置网站映射端口
默认tcp 80
mkdir -p /xtunnel/cnf/ ; echo 80> /xtunnel/cnf/web_port ; sh /xtunnel/restart.sh

设置密码,默认无密码,可添加多个密码
mkdir -p /xtunnel/cnf/ ; echo pass >> /xtunnel/cnf/password ; sh /xtunnel/restart.sh

删除,修改密码
编辑密码文件/xtunnel/cnf/password,
一行代表一个密码,删除或修改相应行.
vi /xtunnel/cnf/password
修改后重启服务端生效
sh /xtunnel/restart.sh

查看密码
cat /xtunnel/cnf/password

取消密码
rm -rf /xtunnelocks/cnf/password
sh /xtunnel/restart.sh

设置开机启动
chmod +x /etc/rc.local
vi /etc/rc.local
加入
sh /xtunnel/start.sh

每天晚上3点自动重启
crontab -e
加入
0 3 * * *  sh /xtunnel/restart.sh
//////////////////////////////////////////////////////////////

网站映射教程
假设映射网站位于本机,ip为127.0.0.1,端口为8080.

1.运行客户端,并登录穿透服务器.


2.添加映射,映射类型选网站映射,内网ip为网站服务器的ip,内网端口为网站端口,域名前缀为系统分配的网站二级域名前缀.


3.添加完成后,映射列表出现刚才添加的映射,右键选择复制外网地址,并在浏览器中打开,内网网站映射成功.


单端口映射教程
单端口映射会为映射分配一个外网端口,访问时需要加端口号.
假设映射网站位于本机,ip为127.0.0.1,端口为8080.

1.运行客户端,并登录穿透服务器.


2.添加映射,映射类型选单端口映射,内网ip为网站服务器的ip,内网端口为网站端口.


3.添加完成后,映射列表出现刚才添加的映射,右键选择复制外网地址,并在浏览器中打开,单端口映射成功.
