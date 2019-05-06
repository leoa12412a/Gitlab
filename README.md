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

* 安裝郵件伺服器：Postfix

Postfix : 是一種MailServer是開放性的Source code

```
###安裝郵件伺服器：Postfix
#　sudo yum install postfix

###加載 Postfix 服務
#　sudo systemctl enable postfix

###啟用 Postfix 服務
#　sudo systemctl start postfix
```

* 取得 GitLab 套件

使用 curl 指令由網路上取得 gitlab-ce 套件，並交給 bash 執行。 gitlab-ee(官方版:要錢)  gitlab-ce(社區版:免費)

```
###官網指令碼（gitlab-ee）
#　curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.rpm.sh | sudo bash

###調整指令碼（gitlab-ce）
#　curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
```
## 2 安裝gitlab

* gitlab-ee(官方版:要錢)  gitlab-ce(社區版:免費)

```
###官網指令碼（gitlab-ee）
#　curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.rpm.sh | sudo bash

###調整指令碼（gitlab-ce）
#　curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
```
## 3 設定並啟動

* vi /etc/gitlab/gitlab.rb 設定gitlab的domain name和port

```
external_url 'http://192.168.0.1'
```

