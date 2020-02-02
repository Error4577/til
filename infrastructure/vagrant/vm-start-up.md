# 仮想マシンの起動
仮想マシンを起動するには`vagrant up`コマンドを使用する。  
VirtualBoxのウィンドウが自動で立ち上げるようにVagrantfile内の下記箇所のコメントアウトを外しておく  

```ruby
config.vm.provider "virtualbox" do |vb|
  # Display the VirtualBox GUI when booting the machine
  vb.gui = true

  # Customize the amount of memory on the VM:
  vb.memory = "1024"
end
```

Vagrantfileと同じディレクトリで下記コマンドを実行する

```
$ vagrant up
```

実行後しばらくするとVirtualBoxのウィンドウが表示され、CentOSのブート処理が実行される。  
しばらく待機するとログインプロンプトが表示される 

```
user: vagrant
passwd: vagrant
```
でログインできる

## 仮想マシンへSSHログイン
仮想マシンへはSSHでログインすることができる  
Vagrantには専用の`vagrant ssh`コマンドが用意されている。  
接続先のホストやポート、ユーザー名を指定しなくても簡単に仮想マシンにSSH接続が可能。  
(仮想マシンにてsshdが起動している必要はある。)  

```
$ vagrant ssh
Last login: Sun Feb  2 11:04:24 2020 from 10.0.2.2
[vagrant@vagrant-centos64 ~]$ 
```

## 仮想マシンの状態を確認
仮想マシンが起動しているかどうかは`vagrant status`コマンドで確認することができる。

```
$ vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
```


## 仮想マシンを停止
起動した仮想マシンを停止する(電源オフ状態)には`vagrant halt`コマンドを使用する。

```
$ vagrant halt
==> default: Attempting graceful shutdown of VM...

$ vagrant status
Current machine states:

default                   poweroff (virtualbox)

The VM is powered off. To restart the VM, simply run `vagrant up`
```


## 仮想マシンを削除
仮想マシンを削除するには`vagrant destroy`コマンドを使用する。

```
$ vagrant destroy
    default: Are you sure you want to destroy the 'default' VM? [y/N] y
==> default: Destroying VM and associated drives...

$ vagrant status
Current machine states:

default                   not created (virtualbox)

The environment has not yet been created. Run `vagrant up` to
create the environment. If a machine is not created, only the
default provider will be shown. So if a provider is not listed,
then the machine is not created for that environment.
```
