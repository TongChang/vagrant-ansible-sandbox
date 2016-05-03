# vagrant-ansible-sandbox

これは、とんちゃんがvagrantとansibleで遊ぶためのリポジトリです。  
※ansibleじゃなくても、provisioningのsandboxにすればいいじゃんって正直思った。

おそらく、しばらく遊んだらいらない子になると思うので、いつか消えます。

## 作ったもの

* managerゲスト
  * 構成管理サーバー
    * 他のゲストをプロビジョンするサーバー
  * プロビジョニングを実装するために、vimが要る
    * .vimrcは自分のやつ
  * ansible使う想定なので、鍵が要る
    * 鍵は入れたが、ゲストには置いてない

* rpi_1ゲスト
  * とりあえずラズパイを想定
    * 仮想上で動作させるわけではないので、ハード要件はラズパイには寄せてません。

## How To Use

### setup vagrant

see [Vagrant by HashiCorp](https://www.vagrantup.com/)

### clone it to local

```
 $ git clone https://github.com/TongChang/vagrant-ansible-sandbox.git
```

### vagrant up

```
 $ cd vagrant-ansible-sandbox
 $ vagrant up
```

### ssh to manager

```
 $ vagrant ssh-config >> ~/.ssh/config
 $ ssh manager
```

### send public key to target

```
 $ scp ~/.ssh/id_rsa.pub 192.168.33.12:~/
 $ ssh 192.168.33.12
 $ cat ~/id_rsa.pub >> ~/.ssh/authorized_keys
```

### test ansible ping
```
 $ cd ~
 $ echo "192.168.33.12" > hosts
 $ ansible 192.168.33.12 -i hosts -m ping
```

and use something to you want...
