# infra-vagrant

Vagrant 是基於 Infrastructure as Code (IaC) 概念的虛擬環境操作工具，其操作裝置可以是 VirtualBox、VMWave 等。

+ [Vagrant](https://www.vagrantup.com/)
    - [VirtualBox](https://www.virtualbox.org/)
    - [VirtualBox](https://www.vmware.com/tw.html)

## 操作

操作範例使用 Vagrant + VirtualBox 為範本

+ [基礎操作](./docs/readme.md)
+ 安裝
    - [Windows](./docs/vagrant-for-windows.md)
    - Linux
+ 設定
    - 映像檔
    - 硬碟容量
    - CPU、RAM
    - 轉發通訊埠 ( forwarded port )
    - 網路介面
    - 初始化腳本
+ [技術議題](./docs/issue.md)

## 實務範例參考

+ [OSX](./Vagrantfile/OSX)
+ [Ubuntu with Docker](./Vagrantfile/Ubuntu-Docker)
+ ~~[Ubuntu with Nvidia-Docker](./Vagrantfile/Ubuntu-Nvidia-Docker)~~
