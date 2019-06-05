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

<br><br><br>
# Gitlab CI/CD

![image](https://github.com/leoa12412a/Gitlab/blob/master/git_ci_cd.png)</br></br>

## Gitlab CI ( Continuous Integration )
是GitLab 提供的持續集成服務(從8.0版本之後，GitLab CI已經集成在GitLab中了)，只要在你的倉庫根目錄下創建一個.gitlab-ci.yml 文件， 並為該項目指派一個Runner，當有合併請求或者Push操作時，你寫在.gitlab-ci.yml中的構建腳本就會開始執行。Gitlab也常常會配合Docker一起使用，以配合每種測試需要的環境。

懶人包 : Gitlab的自動化測試

## GitLab Runner
是配合GitLab CI進行構建任務的應用程序，GitLab CI負責yml文件中各種階段流程的執行，而GitLab Runner就是具體的負責執行每個階段的腳本執行，一般來說GitLab Runner需要安裝在單獨的機器上通過其提供的註冊操作跟GitLab CI進行綁定，當然，你也可以讓其和GitLab安裝在一起，只是有的情況下，你代碼的構建過程對資源消耗十分嚴重的時候，會拖累GitLab給其他用戶提供政策的Git服務。

懶人包 : 幫你跑粽動畫測試的東西，需要註冊

## GitLab CI 使用 Docker 的好處
不同的項目需要不同的工具，如 nodejs，apache ant，maven 等等，在使用像 Jenkins 這樣的工具時，我必須確保這些工具都已經安裝在伺服器上，這樣很不方便。但若然配合 Docker 來使用，開發人員可以隨便選擇 Docker Hub 上提供的任何工具，而不需要求伺服器管理員在伺服器上作任何設定或安裝。
Jenkins 也有一個管道插件，它可以與 Docker 一起使用，以達到完全相同的目的。但是需要額外的功夫來整合。若果可以的話我還是喜歡越簡單、越小設定越好。
雖然我更喜歡使用 GitLab CI，但並不意味著它可以完全取代 Jenkins。Jenkins 提供可配置的用戶界面，可以讓非開發人員例如 QA 等方便地執行部署和整合測試等特定任務。<a href="https://github.com/leoa12412a/Docker/blob/master/README.md">How to install Docker on centos</a>

懶人包 : 一般情況下用Docker比較方便

## Gitlab CI 步驟一 : 註冊一個Gitlab Runner

在Server上安裝Gitlab Runner

在Yum添加gitlab runner 
```
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-ci-multi-runner/script.rpm.sh | sudo bash
```

安裝Runner
```
yum install gitlab-ci-multi-runner
```

到Gitlab上登入管理原取得註冊Runner需要的資訊
![image](https://github.com/leoa12412a/Gitlab/blob/master/re_runner_on_web.png)</br></br>

註冊
```
sudo gitlab-runner register
```

註冊過程
```
Running in system-mode.                            

# 請輸入URL
Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com/):
http://122.147.213.58:3001/

# 請輸入註冊憑證
Please enter the gitlab-ci token for this runner:
KezEDeeRN5z8iwh_

# 請輸入Runner描述
Please enter the gitlab-ci description for this runner:
[122-147-213-58.static.sparqnet.net]: this is new runner    
 
# 請輸入此Runner可以執行哪種tag的Project
Please enter the gitlab-ci tags for this runner (comma separated):
my-tag  

# 是否可以執行沒有tag的project
Whether to run untagged builds [true/false]:
[false]: true    

# 是否只執行當前的project
Whether to lock Runner to current project [true/false]:
[false]: false  

# 為Runner選一格執行器
Please enter the executor: docker-ssh, parallels, ssh, virtualbox, docker-ssh+machine, kubernetes, docker, shell, docker+machine:
shell

```

在Project建立一個.gitlab-ci.yml並測試邏輯

![image](https://github.com/leoa12412a/Gitlab/blob/master/add_gitlab-ci.png)</br></br>

```
# 开始运行之前的操作
before_script:
  - echo 'runner begin'

# 增加名为php-syn-check的任务
php-syn-check:
  tags: # 指定使用有 my-tag 标签的runner运行该任务
    - my-tag
  script: # 任务运行的命令，原理是遍历所有php文件，依次执行 php -l进行语法检测
  - echo 'I am testing'

```

撰寫好.gitlab-ci.yml會自動執行，檢視一下剛剛編輯的結果

![image](https://github.com/leoa12412a/Gitlab/blob/master/gitlab_test.png)</br></br>

## Gitlab CD 自動部屬

gitlab CD 的自動部屬也是需要撰寫在.gitlab-ci.yml內，由於註冊的時候我們是選擇shell，所以這邊我們也使用shell檔來進行部屬，因此我們需要撰寫一個.sh的部屬方式

1.先查看執行shell檔的使用者
```
whoami
```

2.把部屬位置的給予使用者
```
chown -R gitlab-runner:gitlab-runner /var/www/html
```

3.登入gitlab-runner並建立金鑰，並將SSH公鑰存入gitlab內
```
[root@122-147-213-58 test_gitlab_ci]# sudo su - gitlab-runner

[gitlab-runner@122-147-213-58 ~]$ ssh-keygen -t rsa

```

4.撰寫Shell檔
```
cd /var/www/html/test_gitlab_ci
ll
git pull
git log
```

5.查看結果
![image](https://github.com/leoa12412a/Gitlab/blob/master/sh_isok.PNG)</br></br>
