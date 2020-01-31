# Vagrantとは
VagrantはMitchell Hashimoto氏によって作られた開発環境を自動で構築するコマンドラインツール。

`vagrant` コマンドを使って開発環境を構築できる。  
開発環境はVirtualBoxやVMWareといった仮想環境の上に仮想マシンを構築して，これを利用する。  
さらにChefやPuppetといったプロビジョニングツールと組み合わせることで，仮想マシン内で必要なミドルウェアのインストールや設定を自動で行うことができる。  

## プロバイダ
Vagrantでは仮想環境乗に仮想マシンを構築し、それを操作する。  
この仮想環境をプロバイダと呼ぶ。  
デフォルトではVirtualBoxを利用でき、プラグインをインストールするとVMWare FusionやAWSなどを利用できる。  

## プロビジョニング
プロビジョニングツールを使うことで起動した仮想マシンへApacheやPHP、MySQLなどのミドルウェアのインストールや設定を行うことができる。  
デフォルトでシェルスクリプト，Ansible，CFEngine，Chef(chefsolo，chefclient)，Puppet(puppetapply，puppetagent)をプロビジョニングツールとして利用することができる。  

## Boxファイル
仮想マシンを起動する際にベースとなるイメージファイルをBoxファイルと呼ぶ。  
Boxファイルは仮想環境毎に必要。  
通常BoxファイルはOSイメージから作成し、Vagrantを利用する上で最低限必要な設定(Vagrantユーザの作成，sshd起動，プロビジョニングツールインストール)のみ行っておく。  

## Vagrantfile
VagrantfileにはVagrantを使って構築する仮想マシンのスペックやプロビジョニングツールの指定等、仮想マシンの構成を記述する。  
VagrantfileはRubyで記述する。  
このファイルとプロビジョニングツールの設定ファイルがあれば、どの環境においても同じ仮想マシンを構築することができる。  

## vagrantコマンド
`vagrant` コマンドを使ってVagrantの各機能を実行する  