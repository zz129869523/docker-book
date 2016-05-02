# 6.1. Docker Hub

##Docker Hub
---
###Docker Hub
---

目前 Docker 官方維護了一個公共倉庫 [Docker Hub](https://hub.docker.com/)  ,這裡有非常多的的Image。只要是你要的需求，基本上都可以Docker Hub中直接下載Image來實作

**登錄**
可以透過執行 ```docker login ```命令來輸入使用者名稱、密碼和電子信箱來完成註冊和登錄。

**基本操作**

使用者無需登錄即可透過``` docker search``` 命令來查詢官方倉庫中的映像檔，並利用 ```docker pull``` 命令來將它下載到本地。

```
$ sudo docker search ubuntu
//顯示
NAME                              DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ubuntu                            Ubuntu is a Debian-based Linux operating s...   3778      [OK]       
ubuntu-upstart                    Upstart is an event-based replacement for ...   61        [OK]       
torusware/speedus-ubuntu          Always updated official Ubuntu docker imag...   25                   [OK]
rastasheep/ubuntu-sshd            Dockerized SSH service, built on top of of...   24                   [OK]
ubuntu-debootstrap                debootstrap --variant=minbase --components...   23        [OK]       
```
這邊顯示非常多的搜尋結果，有名字，描述，★，是否為官方建立，是否自動建立，官方的Image代表是由官方所建立維護的，automated資源允許User驗證Image的來源和內容。

根據是否是官方提供，可將Image資源分為兩類。

一種是類似 ubuntu 這樣的基礎Image，被稱為基礎或根Image。這些基礎Image是由 Docker 公司建立、驗證、支援、提供。這類的Image往往使用單個單詞作為名字。

另一種類型例如wolibohebadon/ca22006 映像檔，它是由 Docker 的使用者建立並維護的，往往帶有使用者名稱。可以透過user_name/ 來指定使用某個使用者提供的Image，比如 wolibohebadon 使用者。

另外，在查詢的時候透過 ```-s N``` 參數可以指定僅顯示評價為``` N``` 星以上的映像檔。

這邊下載官方 ubuntu的Image 到本機

```
$ sudo docker pull ubuntu
Using default tag: latest
latest: Pulling from library/ubuntu
72b39c1d4615: Pull complete 
46a2d5ede4a6: Pull complete 
d7caf6e91ad4: Pull complete 
c7ac9f284354: Pull complete 
a3ed95caeb02: Pull complete 
```
有```pull```就會有```push```，也可以將改好的Image push到Docker Hub。

---