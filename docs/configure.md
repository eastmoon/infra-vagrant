# 設定

Vagrant 專案是以檔案夾為基礎，每個虛擬機對應一個專案目錄，當開發者執行 ```vagrant init``` 可以初始化其目錄並得到基礎的 [Vagrantfile](https://www.vagrantup.com/docs/vagrantfile)，而開發者可透過設定此檔來改變啟動的虛擬機狀態

## 腳本版本指定

```
Vagrant.configure("2") do |config|
```

在設定是指此 Vagrantfile 使用版本 2 的解析，在理想情況上並不需要特別改變，除版本增加的新語法外；而主要會使用語法是以 [config.vm](https://www.vagrantup.com/docs/vagrantfile/machine_settings) 所指定的功能來延伸。

## 映像檔

```
config.vm.box = "custom-osx"
```

此設定指定本虛擬機使用的映像檔名稱，若本機不存在該映像檔會自行前往 [Vagrant Cloud](https://app.vagrantup.com/boxes/search) 中搜尋；而若屬於自定義而壓制出的 box 檔，則需使用 ```vagrant box``` 將映像檔自行匯入。

## 硬碟容量

```
config.vm.disk :disk, size: "100GB", primary: true
```

此設定可指定虛擬機的主硬碟容量，在預設情況下僅有 20G，使用此方式可以擴大其容量；但對 VirtualBox，請於腳本版本指定前設定如下環境變數。

```
ENV['VAGRANT_EXPERIMENTAL'] = "disks"
```

## CPU、RAM

```
config.vm.provider "virtualbox" do |vb|
  # Customize the amount of cpu on the VM:
  vb.customize ["modifyvm", :id, "--cpus", "2"]
  # Customize the amount of memory on the VM:
  vb.memory = "8192"
end
```

此設定是針對目標虛擬化技術提供額外設定，此處使用目標是 ```virtualbox```，而詳細設定可以參考 [Virtualbox VBoxManage](https://www.virtualbox.org/manual/ch08.html) 設定，亦可特別設定如下指令來關閉內部虛擬化服務 VT-x。

```
config.vm.provider "virtualbox" do |vb|
  # Enable VT-x
  vb.customize ["modifyvm", :id, "--hwvirtex", "on"]
  vb.customize ["modifyvm", :id, "--nested-hw-virt", "off"]
end
```

## 轉發通訊埠 ( forwarded port )

```
config.vm.network "forwarded_port", guest: 80, host: 8080
config.vm.network "forwarded_port", guest: 443, host: 8081
```

使用 Vagrant 標準會啟用 SSH 通訊，但倘若該虛擬機有額外通訊埠，則可透過上述設定轉換到 HOST 主機的通訊埠上。

## 網路介面

```
config.vm.network "private_network", ip: "192.168.0.50", mac: "5CA1AB1E0001", virtualbox__intnet: "inet1"
```

由於 ```forwarded_port``` 是將虛擬機的通訊埠轉接到 HOST 主機上，因此虛擬機啟動時有預設建立一個網路介面，例如 ```eth0```，但倘若要建立虛擬機間的區域網路並指定給特定網路介面，則須設定如上；雖然 Vagrant 可以設定介面，但對應到 Virtualbox 時，需額外設定 ```virtualbox__intnet: "inet1"``` 來建立一個對應的虛擬網路。

## 初始化腳本

```
config.vm.provision "shell", inline: <<-SHELL
  apt-get update
  apt-get install -y apache2
SHELL
```

此設定是指當虛擬機建立時 ( 第一次 UP 時 )，會執行此處設定的腳本，以完成虛擬機的初始化；倘若腳本複雜，可指定外不腳本檔來執行。

```
config.vm.provision "shell", path: "install.sh"
```
