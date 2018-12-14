# How to use virtual box

## <font color="Red">how to `ping` command from host to VM

</font>

`ping` command succeed from gestOS to hostOS, but fail in reverse case.  
this disconnection is default specification.  
below procedure can do above process.  
this procedure adopt that replace access to host(inclucding port) with access to VM(including port)

1. Open VM settings
1. Select network tab
1. Click advanced arrow
1. Click `port forwarding`
1. Verify `protcol`
1. Write `Host IP` corresponding to host IP address
1. Verify temporary host port in `Host Port`
1. Write `Guest IP` corresponding to guest IP address
1. Verify real guest port
1. Run `Test-NetConnection -ComputerName {Host IP} -Port {Host Port}`
   to check above process succeed

## <font color="Red">How to ssh connection to VM using Teraterm</font>

### <font color="orange">Summary</font>

1. do below procedure on root user
1. install package  
1. configure firewall

### <font color="orange"> server side</font>

1. Run `yum -y install openssh-server`
1. Run `vi /etc/ssh/sshd_config` to open sshd_config file
1. Commentout `Port`, set `PermitRootLogin` no, set `PasswordAuthentication` yes
1. Run `systemctl start sshd.service` and `systemctl status sshd.service`
1. Run `firewall-cmd --list-all` to check port for ssh is open
1. if ssh don't exist in services, Run `firewall-cmd --permanent --add-service=ssh`
1. Run `useradd {usernamme}`, `passwd {username}` and decide password

### <font color="orange"> client side</font>

1. Run `yum -y install openssh-clients`
1. ssh {username}@{server's IP address}
1. if [{username}@localhost], preparation finish

### <font color="orange">How to set up Firewall (In my case, ESET's firewall )</font>

1. open firewall setup page
1. decide name, check `双方向`, check TCP/UDP
1. in `ローカル`, set `ポート` 22
1. in `リモート`, set `ポート` 22 and set `IP` Host IP address

### <font color="orange">setup in virtualbox side</font>

1. select settings, network, adaptar.
1. select advanced and open `Port Forwarding`
1. decide Name, check TCP, write `Host port` and write 22 in `Guest Port` (`Host Ip` and `Guest IP` are empty)
1. push `OK`
