仮想環境の導入
===

環境によって開発環境の導入手順などが大きく異なってしまうので、環境を統一するために仮想環境を導入する。

仮想環境であれば、WindowsであってもMacOSであっても同様の環境を再構築することができる。

## 導入手順
### 1. VirtualBox インストール
[Downloadページ](https://www.virtualbox.org/wiki/Downloads)から自分のPCのOSにあったソフトをダウンロード

### 2. Vagrantのインストール
[Downloadページ](https://www.vagrantup.com/downloads)から自分のPCにあったソフトをダウンロード

インストールが完了していれば、コマンドプロンプトを開いて`vagrant --version`とすればvagrantのバージョンが確認できる。

### 3. VagrantでUbuntu18.04を立ち上げる(Windows)
1. コマンドプロンプトを立ち上げる
2. `mkdir myvagrant`
3. `cd myvagrant`
4. `vagrant init`
5. Vagrantfileを以下の内容に書き換える

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # ubuntu18.04を起動する
  config.vm.box = "ubuntu/bionic64"
  # 起動するIPアドレスを指定
  config.vm.network "private_network", ip: "192.168.33.20"
  # 起動するマシンのポートを開放する
  config.vm.network "forwarded_port", guest: 3000, host: 3000

  # 起動するマシンに指定したメモリを割り当てる
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end
end
```

6. `vagrant up`で起動

ここまででとりあえずUbuntuが起動する

### 4. Ubuntuにアクセスする(Windows)

上記まででUbuntuが起動しているはずなので次はそれにアクセスする手順。

1. コマンドプロンプトを立ち上げる
2. `cd myvagrant`
3. `vagrant status`で起動しているか確認。
  - runnnig: 起動中
  - poweroff: 停止中
4. 起動中なら`vagrant ssh`でアクセスできる。
