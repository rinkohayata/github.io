---
title: "IPアドレスの固定"
date: 2022-09-19
draft: false
---

Goal: 仮想マシンのIPアドレスのネットワーク部を物理マシンのものと一致させる  
(仮想OS=Ubuntu、物理OS=Windows)

<!--more-->

### 1. WindowsでIPアドレスとデフォルトゲートウェイを確認する

cmd
```
> ipconfig
......
IPv4アドレス: 192.168.XXX.XXX
サブネットマスク: 255.255.0.0
デフォルトゲートウェイ: 192.168.XXX.1
......
```

### 2. Ubuntuでインターフェースを確認する

[Ctrl] + [Alt] + [t]
```
~$ ip a
......
2: ens33: 
......
```

### 3. Ubuntuで99_config.yamlを作成する

```
~$ cd /etc/netplan/
/e/netplan$ sudo vim 99_config.yaml
```

99_config.yaml
```
1   network:
2     version: 2
3     renderer: networkd
4     ethernets:
5       ens33:
6         dhcp4: false
7         dhcp6: false
8         addresses: [192.168.***.*/16] 
9         gateway4: 192.168.XXX.1
10        nameservers:
11          addresses: [192.168.XXX.1]      
```          
☆チェックポイント
- 「:」の後ろは半角スペース有り
- 5行目は、`2. Ubuntuでインターフェースを確認する`で表示されていたもの
- 8行目は、固定したいIPアドレス(ネットワーク部は`1. WindowsでIPアドレスとデフォルトゲートウェイを確認する`のIPアドレスに一致させる)
- 8行目の「/サブネットマスク」は省略するとエラーになる場合がある
- 8行目と11行目の「[]」も省略NG
- 9行目と11行目は、`1. WindowsでIPアドレスとデフォルトゲートウェイを確認する`のデフォルトゲートウェイ  

:wq(保存して閉じる)

### 4. Ubuntuに変更を適用させる

```
~$ sudo netplan apply
```

### 5. UbuntuのIPアドレスを変更できたか確認する

```
~$ ip a
......
inet 192.168.***.*/16
......
```

