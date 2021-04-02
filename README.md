# SubManage Ansible
## About
サブスクリプションサービスマネジメントサービス[SubManage](https://github.com/sirogane1013/submanage-core)の構成管理用リポジトリです。

## Requirements
### Ansible Server
- Ubuntu 20.04 LTS
- ansible 2.9.6

### Web Server
- Ubuntu 20.04 LTS

### DB Server
- CentOS 8

## How to Release
### Common
1. `Ansible Server`の公開鍵を`WebServer`, `DBServer`に転送
```
ssh-copy-id -i /root/.ssh/id_rsa.pub [USER]@[ADDRESS]
```
2. `inventory.example`を`inventory`にリネームし、[webservers], [dbservers]をそれぞれ追記
```
mv inventory.example inventory
vim inventory
```
```
[webservers]
# 192.168.1.1
192.168.1.2
192.168.1.3

[dbservers]
# 192.168.1.2
192.168.1.4
192.168.1.5
```
3. `group_vars/*.example`をリネームし、変数を適当に設定
```
mv all.example all
vim all
mv dbservers.example dbservers
vim dbservers
mv webservers.example webservers
vim webservers
```

### Web Server
1. 初期設定
```
ansible-playbook -i ./inventory ./webservers.yml 
```
2. アプリケーションのビルド
```
ansible-playbook -i ./inventory ./deploy.yml 
```

## DB Server
1. 初期設定
```
ansible-playbook -i ./inventory ./dbservers.yml 
```
2. 各サーバーでレプリケーションの設定