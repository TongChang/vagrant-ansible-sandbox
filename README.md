# vagrant-ansible-sandbox

これは、とんちゃんがvagrantとansibleで遊ぶためのリポジトリです。  
※ansibleじゃなくても、provisioningのsandboxにすればいいじゃんって正直思った。

おそらく、しばらく遊んだらいらない子になると思うので、いつか消えます。

## 目指すもの

* managerゲスト
  * 構成管理サーバー
    * 他のゲストをプロビジョンするサーバー
  * プロビジョニングを実装するために、vimが要る
    * .vimrcは自分のやつでいいや
    * neobundleがいるなぁ
  * ansible使う想定なので、鍵が要る

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

and use something to you want...
