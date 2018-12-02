# How to use virtual box

## how to `ping` command from host to VM

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

## How to ssh connection to VM using Teraterm

Summary
  do below procedure on root user
  install package  
  configure firewall

### server side

1. Run `yum -y install openssh-server`
1. Run `vi /etc/ssh/sshd_config` to open sshd_config file
1. Commentout `Port`, set `PermitRootLogin` no, set `PasswordAuthentication` yes
1. Run `systemctl start sshd.service` and `systemctl status sshd.service`
1. Run `firewall-cmd --list-all` to check port for ssh is open
1. if ssh don't exist in services, Run `firewall-cmd --permanent --add-service=ssh`
1. Run `useradd {usernamme}`, `passwd {username}` and decide password

### client side

1. Run `yum -y install openssh-clients`
1. ssh {username}@{server's IP address}
1. if [{username}@localhost], preparation finish

### How to set up Firewall

1. open firewall setup page
1. decide name, check `双方向`, check TCP/UDP
1. in `ローカル`, set `ポート` 22
1. in `リモート`, set `ポート` 22 and set `IP` Host IP address