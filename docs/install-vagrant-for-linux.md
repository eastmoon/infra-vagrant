# Vagrant 安裝

此安裝操作使用 Ubuntu 18.04 環境

1. 安裝 VirtualBox

```
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib"
sudo apt-get update -y && \
sudo apt-get install -y virtualbox-6.1
```

2. 安裝 Vagrant

```
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update -y && \
sudo apt-get install -y vagrant
```

3. 重啟電腦，並於 Terminal 測試 Vagrant 命令

```
// 列出說明
vagrant --help
// 列出版本
vagrant --version
```

4. 安裝 SSH 工具

Ubuntu 18.04 作業系統預設有安裝 SSH 功能。

5. 安裝 Vagrant Plugin

+ 安裝 ```vagrant scp``` 指令，提供 SSH Copy 的方式複製資料
```
vagrant plugin install vagrant-scp
```

+ 安裝 VirtualBox Guest Additions
在多數情況下，使用 Guest Additions 可以開通諸多硬體功能接通，對此，若有需要則需安裝可自動更新 Guest Additions 的套件 [Vagrant-vbguest](https://github.com/dotless-de/vagrant-vbguest)。
```
vagrant plugin install vagrant-vbguest
```
