# Gitlab 安裝教學

## 1. 安裝和設定所有需要的原件

* 使用 yum 指令安裝 curl、policycoreutils-python 與 openssh-server 三個套件。

```
#　sudo yum install -y curl policycoreutils-python openssh-server
```

* 啟用 OpenSSH 服務

```
###加載 OpenSSH 服務
#　sudo systemctl enable sshd

###啟用 OpenSSH 服務
#　sudo systemctl start sshd
```

* 設定防火牆組態

```
###設定防火牆組態，開啟 http 服務端口
#　sudo firewall-cmd --permanent --add-service=http

###重新載入防火牆組態設定
#　sudo systemctl reload firewalld
```
