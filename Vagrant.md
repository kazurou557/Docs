# How to use Vagrant

Vagrant is manage tool for virtualbox

## How to install and initialize Vagrant box

Vagrant box is image file for VM.

1. Run `vagrant box add {VM name} {url}`  
   Search url from [Vagrant][1]
1. Run `vagrant init {VM name}
1. Run `vagrant up` to start vagrant VM
   ID:   vagrant
   pass: vagrant

## How to write Vagrant box

```bash
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  #上で決めたVM name
  config.vm.box = "{VN name}"

  #IPアドレス
  config.vm.network "private_network", ip: "192.168.33.10"

  #メモリ割り当て（環境に合わせる）
  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

end
```

## How to share file between Host and VM

1. add below content in box file
   file name is thing to want to share

```bash
    config.vm.synced_folder "../{file name}", "/var/www/html/{file name}"
```

1. Run `vagrant reload` to load box file content

## How to ssh VM

The ssh in vagrant is easy  
Just run `vagrant ssh`

[1]:http://www.vagrantbox.es/