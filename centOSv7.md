# How to Install and use centOS v7

## <font color="red">How to setup CentOS v7 in VirtualBox</font>

1. Install [VirtualBox][1]
1. Install `Minimal ISO` from [CentOS v7][2]
1. Create new VM in VirtualBox app 
1. Decide name, select `Linux` Type and select `RedHat(64-bit)` version
1. Decide memory size, check `create a virual Hard Disk now`, check
   `VDI` and check `Dynamically allocated`
1. set storage size
1. install CentOS 7 in next page
1. select language
1. click `インストール先` and check `ATA VBOX HARDDISK` and click `完了`
1. select `ネットワークとホスト` and change `オフ` to `オン` and click `インストールの開始`
1. create root and user
1. finally click `再起動` and login

## <font color="red">Structure of root directory </font>

[detail][3]
| directory | content                  |
|-----------|--------------------------|
| bin       | バイナリコマンド群                |
| boot      | ブートローダ用のファイル群            |
| dev       | デバイスドライバ用ファイル群           |
| etc       | システム、OS、デーモンなどの設定ファイル群   |
| home      | ユーザのホームディレクトリ（ワークスペース）   |
| lib       | bin/sbinのコマンド実行に必要なファイル群 |
| media     | 取り換え可能メディア用のマウントポイント     |
| mnt       | ファイルシステムを一時的にマウントするポイント  |
| proc      | システム情報を含む仮想ディレクトリ（）      |
| root      | ルートユーザのホームディレクトリ         |
| sbin      | システムコマンド群                |
| sys       | システム情報を含む仮想ディレクトリ（カーネル）  |
| tmp       | 一時ファイル用                  |
| usr       | プログラムなどを置く場所             |
| var       | 値が常に変動するデータを置く場所         |
| srv       | FTPやwwwなのでデータファイルの置き場所   |
| opt       | 追加アプリケーション用              |

[1]: https://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html?ssSourceSiteId=otnjp
[2]: https://www.centos.org/download/
[3]: http://mrs.suzu841.com/tebiki/linux/centos/directory/
