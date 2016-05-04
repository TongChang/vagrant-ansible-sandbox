# vagrant-sandbox

これは、とんちゃんがvagrantでVMを作って遊ぶためのリポジトリです。  

おそらく、しばらく遊んだらいらない子になると思うので、いつか消えます。

## 作ったもの

* managerゲスト
  * 構成管理サーバー
    * 他のゲストをプロビジョンするサーバー
  * プロビジョニングを実装するために、vimが要る
    * .vimrcは自分のやつ
  * ansible使う想定なので、鍵が要る
    * 秘密鍵と公開鍵を用意しておく

* rpi_1ゲスト
  * とりあえずラズパイを想定
    * 仮想上で動作させるわけではないので、ハード要件はラズパイには寄せてません。
  * 公開鍵をmanagerゲストからもらっておく

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

### test ansible ping
```
 $ cd ~
 $ echo "192.168.33.12" > hosts
 $ ansible 192.168.33.12 -i hosts -m ping
```

and use something to you want...
