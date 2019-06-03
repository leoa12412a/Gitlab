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
![image](https://github.com/leoa12412a/Gitlab/blob/master/lab_url.png)</br></br>

* 啟動gitlab

```
# gitlab-ctl reconfigure
```

![image](https://github.com/leoa12412a/Gitlab/blob/master/gitlab_start.PNG)</br></br>

* 如果出現以下錯誤，表示需更改server編碼

![image](https://github.com/leoa12412a/Gitlab/blob/master/error.PNG)</br></br>

```
export LC_CTYPE=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```

## 3. 管理介面

* 輸入IP ( 如果有輸入port記得加入port ex:192.168.30.1:3000 )

第一次登入先設定密碼 帳號為root

![image](https://github.com/leoa12412a/Gitlab/blob/master/gitlab_first_password.PNG)</br></br>


# Gitlab管理

## 1. Gitlab中文化設定

gitlab有內建的語言選項，並且持續翻譯中，原本爬文尋找中文化的修改方式，但是版本是在V9.XXX與這次所安裝的11.10.4相差甚遠，因此推斷9.X後版本官方將語言選項列入標準的gitlab內。

中文化設定步驟

![image](https://github.com/leoa12412a/Gitlab/blob/master/gitlab_ch.png)</br></br>


## 2. 建立新的專案

* 新的空白頁
* 從模組建立
* 匯入

![image](https://github.com/leoa12412a/Gitlab/blob/master/gitlab_new.PNG)</br></br>
![image](https://github.com/leoa12412a/Gitlab/blob/master/gitlab_new1.PNG)</br></br>
![image](https://github.com/leoa12412a/Gitlab/blob/master/gitlab_new2.PNG)</br></br>


## 3. 設置SSH Key

![image](https://github.com/leoa12412a/Gitlab/blob/master/gitlab_ssh.PNG)</br></br>


# Gitlab CI/CD

## Gitlab CI ( Continuous Integration )
是GitLab 提供的持續集成服務(從8.0版本之後，GitLab CI已經集成在GitLab中了)，只要在你的倉庫根目錄下創建一個.gitlab-ci.yml 文件， 並為該項目指派一個Runner，當有合併請求或者Push操作時，你寫在.gitlab-ci.yml中的構建腳本就會開始執行。

## GitLab Runner
是配合GitLab CI進行構建任務的應用程序，GitLab CI負責yml文件中各種階段流程的執行，而GitLab Runner就是具體的負責執行每個階段的腳本執行，一般來說GitLab Runner需要安裝在單獨的機器上通過其提供的註冊操作跟GitLab CI進行綁定，當然，你也可以讓其和GitLab安裝在一起，只是有的情況下，你代碼的構建過程對資源消耗十分嚴重的時候，會拖累GitLab給其他用戶提供政策的Git服務。


<a href="https://github.com/leoa12412a/Docker/blob/master/README.md">How to install Docker on centos</a>
