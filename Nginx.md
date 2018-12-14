# Nginx

## <font color="Red">Install Nginx</font>

Start CentOS using Oracle VM VirtualBox Manager.

for a while, run command on root user.

1. Login root user, Run `su`
1. Run `rpm -ivh http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm` to install release package
1. Run `yum install nginx` to install Nginx
1. Run below command to install modules  
   `yum groupinstall "Development Tools"` to install fundamental develop environment
   `yum install pcre pcre-devel` to install Perl interchageable regular expression library
   `yum install zlib zlib-devel` to install library for compression transport
   `yum install openssl openssl-devel` to install library for HTTPS
1. Run `curl -O http://nginx.org/download/nginx-{version}.tar.gz`  
   refer to http://nginx.org/download
1. Run `taf xvfz nginx-{version}.tar.gz`
1. cd ng-{version}
1. Run `./configure`
1. Run `sudo make`
1. Run `sudo make install`

## <font color="Red">Operate Nginx</font>

In /usr/local/nginx/sbin/, run following command

`./nginx` to start nginx server
`nginx -s stop` to stop nginx  
`nginx -s quit` to stop after response  
`nginx -s reopen` to reopen log file
`nginx -s reload` to reload config file

## <font color="Red">setup port for nginx</font>

setup firewall in VM

1. Run `sudo vi /etc/sysconfig/iptables` and copy the following

```bash
# (1) ポリシーの設定 OUTPUTのみACCEPTにする
*filter
:INPUT   DROP   [0:0]
:FORWARD DROP   [0:0]
:OUTPUT  ACCEPT [0:0]

# (2) ループバック(自分自身からの通信)を許可する
-A INPUT -i lo -j ACCEPT

# (3) データを持たないパケットの接続を破棄する
-A INPUT -p tcp --tcp-flags ALL NONE -j DROP

# (4) SYNflood攻撃と思われる接続を破棄する
-A INPUT -p tcp ! --syn -m state --state NEW -j DROP

# (5) ステルススキャンと思われる接続を破棄する
-A INPUT -p tcp --tcp-flags ALL ALL -j DROP

# (6) icmp(ping)の設定
# hashlimitを使う
# -m hashlimit                   hashlimitモジュールを使用する
# —hashlimit-name t_icmp  記録するファイル名
# —hashlimit 1/m               リミット時には1分間に1パケットを上限とする
# —hashlimit-burst 10        規定時間内に10パケット受信すればリミットを有効にする
# —hashlimit-mode srcip    ソースIPを元にアクセスを制限する
# —hashlimit-htable-expire 120000   リミットの有効期間。単位はms
-A INPUT -p icmp --icmp-type echo-request -m hashlimit --hashlimit-name t_icmp --hashlimit 1/m --hashlimit-burst 10 --hashlimit-mode srcip --hashlimit-htable-expire 120000 -j ACCEPT

# (7) 確立済みの通信は、ポート番号に関係なく許可する
-A INPUT -p tcp -m state --state ESTABLISHED,RELATED -j ACCEPT

# (8) 任意へのDNSアクセスの戻りパケットを受け付ける
-A INPUT -p udp --sport 53 -j ACCEPT

# (9) SSHを許可する設定
# hashlimitを使う
# -m hashlimit                   hashlimitモジュールを使用する
# —hashlimit-name t_sshd 記録するファイル名
# —hashlimit 1/m              リミット時には1分間に1パケットを上限とする
# —hashlimit-burst 10       規定時間内に10パケット受信すればリミットを有効にする
# —hashlimit-mode srcip   ソースIPを元にアクセスを制限する
# —hashlimit-htable-expire 120000   リミットの有効期間。単位はms
-A INPUT -p tcp -m state --syn --state NEW --dport 22 -m hashlimit --hashlimit-name t_sshd --hashlimit 1/m --hashlimit-burst 10 --hashlimit-mode srcip --hashlimit-htable-expire 120000 -j ACCEPT

# (10) 個別に許可するプロトコルとポートをここに書き込む。
# この例では、HTTP(TCP 80)とHTTPS(TCP 443)を許可している。
-A INPUT -p tcp --dport 80   -j ACCEPT
-A INPUT -p tcp --dport 443  -j ACCEPT

COMMIT
```

1. Run `yum install iptables-services`
1. Run `systemctl status firewalld`
1. Run `systemcrl -stop firewall`
1. Run `systemctl disable firewall`
1. Run `systemctl enable iptables`
1. Run `systemctl start iptables`
1. Run `systemcrl status iptables`

## <font color="Red">Deal with error</font>

### <font color="orange">ErrorCode nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use) </font>

examine port status using lsof command

1. Run `sudo yum install lsof`
1. Run `sudo lsof -i:80`
1. Run `sudo servide nginx status`  
   if nginx is stop, Run `sudo kill {pid}`
1. Run `sudo service nginx start` to start nginx
