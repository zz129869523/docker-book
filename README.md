#Docker 簡介

---

- Docker 是什麼？
- 為什麼要用Docker？ 
- 好處是什麼？


##Docker 是什麼？

Docker's Birthday : 2013/3/13

Docker 是一個開源專案，Docker 專案的目標是實作輕量級的作業系統虛擬化解決方案。 Docker 的基礎是 Linux 容器（LXC）等技術。

什麼是(LXC)呢？其名稱來自Linux軟體容器（Linux Containers）的縮寫，一種作業系統層虛擬化（Operating system–level virtualization）技術為Linux內核容器功能的一個使用者介面。它將應用軟體系統打包成一個軟體容器(Container)，內含應用軟體本身的程式碼，以及所需要的作業系統核心和函式庫。透過統一的命名空間和共用API來分配不同軟體容器的可用硬體資源，創造出應用程式的獨立沙箱執行環境，使得Linux使用者可以容易的建立和管理系統或應用容器。

在 LXC 的基礎上 Docker 進行了進一步的封裝，使用者不需要管理容器，讓操作更為輕便。使用者操作 Docker 的容器就像操作一個快速輕量級的虛擬機一樣簡單。


---

##為什麼要用Docker


作為一種快速興起的虛擬化方式，Docker 跟以往的虛擬化方式相比有很多的優勢。

- Docker容器的啟動是以秒來計算，這跟傳統的虛擬機比起來要快得多

- Docker對系統資源的使用率很高，一台主機上可以同時執行數千個 Docker 容器。

- 容器除了執行其中應用外，基本上只消耗一點額外的系統資源，使得應用的效能很高，而且系統資源消耗更少。傳統虛擬機方式執行5個不同的應用就要啟動5個虛擬機，而 Docker只需要啟動5個隔離的應用即可。

簡單而具體來說，Docker 在以下幾個方面具有較大的優勢。



- 輕鬆的遷移與擴展
  - Docker 容器幾乎可以在任意的平台上執行，包括實體機器、虛擬機、公有雲、私有雲、個人電腦、伺服器等。 這種兼容性可以讓使用者透過Dockerhub把一個應用程式從一個平台直接搬遷到另外一個。
- 有效率的虛擬化
  - Docker 容器的執行不需要額外的虛擬化支援，它是核心層級的虛擬化，因此可以實作更高的效能和效率。
- 快速的交付與部署
  - 對開發人員來說，希望的就是一次建立或設定，可以在任意地方正常執行，開發者可以使用一個標準的映像檔來建立一套開發容器，而且過程可以整個顯示，讓其他人也能夠知道應用程式是如何去建立和工作，容器是以秒開啟的，節省更多時間，能有更多時間來測試
- 簡單的管理
  - 使用 Docker，只需要小小的修改，就可以替代以往大量的更新工作。所有的修改都以增量的方式被分發和更新，從而實作自動化並且有效率的管理。



| 特性 | 容器 | 虛擬機 |
| ----- | ----- | ----- 
| 啟動 | 秒 | 分鐘 
| 硬體容量| 一般為MB | 一般為GB 
| 效能| 接近原生 | 慢 
|系統支援量 | 一台支援上千個 | 一般幾十個

---

#基本概念

---

Docker有3個基本概念

- 映像檔(Image)
- 容器(Container)
- 倉儲(Repository)

這3個就是Docker的整個架構

##映像檔

Docker Image 就是一個唯讀的模板。

- 例如一個映像檔可以包含一個ubuntu的作業環境，僅僅需要下簡單的指令就能夠直接RUN起來，而且僅安裝了Apache或使用者需要應用程式

- Image也可以用來建立Docker容器

- Docker 提供了一個很簡單的方法建立或更新映像檔，User可以直接從別人那邊用類似GitHub的方式將別人的Image拿來使用


---

##容器

---

Docker是利用容器來執行你要的需求or應用

- 容器是從映像檔建立的執行實例。它可以被啟動、開始、停止、刪除。每個容器都是互相隔離的、保證安全的平台。

- 可以把容器看做是一個簡易版的 Linux 環境（包括root權限、程式、使用者空間和網路空間等）和其中執行的應用程式。

P.S.：映像檔是唯讀的，容器在啟動的時候會建立一層可寫層作為最上層。

---

##倉儲

---

倉儲是集中存放映像檔檔案的場所。有時候會把倉儲和倉儲註冊伺服器（Registry）混為一談，並不嚴格區分。實際上，倉儲註冊伺服器上往往存放著多個倉儲，每個倉儲中又包含了多個映像檔，每個映像檔也有不同的標籤（tag），用來辨別你的映像檔。

- 倉儲分為公開倉庫（Public）和私有倉儲（Private）兩種形式。

- 最大的公開倉庫是 Docker Hub，存放了非常多的映像檔供User download。 大陸的公開倉庫包括 Docker Pool 等，可以提供大陸使用者更穩定快速的存取。然後User還可以在自己的Docker Hub內建立一個私有倉儲(Private)。

- User建立了自己的Image之後就可以使用 push 命令將它上傳到公有或者私有倉儲，當我要在另外一台機器上使用這個Image時候，只需要從倉儲上 pull 下來就可以使用。

P.S.：Docker 倉儲的概念跟 Git 類似，註冊伺服器可以把他想成跟GitHub一樣是一個分享自己Image的地方。

---

#安裝Docker服務

---

官方網站上有很多環境的安裝指南，先介紹Ubuntu就好，因為我比較常用

- https://docs.docker.com/engine/installation/#installation

---

##Ubuntu安裝Docker

---

Docker 支援這些 Ubuntu 版本號:

- Ubuntu Xenial 16.04 (LTS)
- Ubuntu Wily 15.10
- Ubuntu Trusty 14.04 (LTS)
- Ubuntu Precise 12.04 (LTS)

在安裝Docker之前，他有幾項聲明:

- 需要64-bit的Ubuntu系統

- Kernel必須不小於於3.10

- 3.10次要或更新維護版本是可以接受的

若沒有這些前提，安裝後可能會造成Docker無法使用

如果你不知道你的內核

可以使用以下指令

```
$ uname -r
```

可以透過系統內建套件安裝

```
$ sudo apt-get update                  //更新Ubuntu的套件
$ sudo apt-get install docker-engine   //安裝Docker
```

快速安裝

```
curl http://files.imaclouds.com/scripts/docker_install.sh | sh
```

安裝後可以試試看如何開啟並建立Docker

```
$ sudo service docker start            //開啟Docker
$ sudo docker run hello-world          //Run一個Docker 確定是沒問題的
```


---

#映像檔

---

在前面我有先提到Docker是由三個部分所組成，首先是映像檔。

Docker 在執行Container前需要有本地端存在對應的Image，如果Image不存在本地端，Docker會從Image Repository下載（預設是 Docker Hub 公共註冊伺服器中的Repository）。

這邊會提到三件事：

- 如何從Repository取得Image
- 管理本地主機上的Image
- 介紹Image實作的基本原理

##取得映像檔

使用 ```docker pull ``` 命令從Repository取得所需要的Image。

下面的例子是從我自己的Docker Hub倉儲下載一個Image。

pull後面是你在Docker Hub上的名稱 Id/Repository。

```
$ sudo docker pull wolibohebadon/ca22006

latest: Pulling from wolibohebadon/ca22006 //最新的下載image位置在wolibohebadon/ca22006
759d6771041e: Download complete
8836b825667b: Download complete
c2f5e51744e6: Download complete
a3ed95caeb02: Download complete
4afafbda1c91: Download complete
d969199cf5fa: Download complete
a8b48361e793: Download complete
c9dfe10bdabc: Download complete
```

另一個例子是從Docker Hub倉儲下載一個Ubuntu14.04作業系統的映像檔。


```
$ sudo docker pull ubuntu:14.04
14.04: Pulling from library/ubuntu
943c334059c7: Pull complete 
a1acf99303d2: Pull complete 
27616aacb7b3: Pull complete 
35d12cd1c9fc: Pull complete 
a3ed95caeb02: Pull complete 
```

下載完畢後，就可以使用這個印象檔，可以建立一個容器,讓他去執行bash

```
$ sudo docker run -ti ubuntu:14.04 /bin/bash   //執行後會進入docker內
root@1133d5eb031f:/#
```

---

##列出

---

###列出本機映像檔

使用 docker images 顯示本機已有的映像檔。

```
$ sudo docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
<none>                  <none>              ac57e7603ebd        43 hours ago        427.1 MB
wolibohebadon/ca22006   latest              16a395dcdbb0        43 hours ago        427.1 MB
ubuntu                  14.04               8fa7f61732d6        5 days ago          188 MB
ca22006                 latest              bb986c5d7999        5 days ago          427 MB
node                    5.11.0              8593e962b570        9 days ago          644.3 MB
```

列出訊息中可以看到幾個訊息

- 來自哪一個倉儲(REPOSITORY)，ex: ubuntu

- 映像檔的標記(TAG),ex: 14.04

- Image ID(唯一),ex: 8fa7f61732d6

- 建立時間(CREATED),ex: 5 days ago

- 映像檔大小(SIZE),ex: 188 MB

映像檔的 ID 唯一標識了映像檔，注意到 ubuntu:14.04 和 wolibohebadon/ca22006 不具有相同的映像檔 ID，說明它們是不同樣的映像檔。

TAG 用來標記來自同一個倉儲的不同映像檔。例如 ubuntu 倉儲中有多個映像檔，通過 TAG 來區分發行版本，例如 10.04、12.04、12.10、13.04、14.04 等。

下面的命令指定使用映像檔 ubuntu:14.04 來啟動一個容器。

```
sudo docker run -ti ubuntu:14.04 /bin/bash
```
如果沒有指定Tag,預設會使用 latest (只在同一個Id底下最新的那一個)

---

##建立

---

###建立映像檔

建立Image有滿多方法的，User可以在Docker Hub取得已有的Image並Update，也可以在本機建立。

**修改已有映像檔**

使用下載的Image去啟動Container

```
$ sudo docker run -t -i ubuntu /bin/bash
root@0e50fa84f1bb:/# 
```

這邊的ID記一下

在容器中加入Json的gem套件

P.S.這邊不要複製root@id喔這是你自己的

```
root@0e50fa84f1bb:/#  gem install json
```

這邊在Docker內找不到指令
若沒有gem指令請先安裝

```
$ sudo apt-get install gem
$ sudo apt-get install ruby -y  && sudo apt-get install rubygems -y
$ sudo gem install json  //直接下命令
```
執行下面指令後，我們的Container已經被改變，```使用docker commit```命令來提交更新後的副本
```
$ sudo docker commit -m "Add json gem" -a "Docker" 0e50fa84f1bb ubuntu:v2
sha256:87f05893535ed2ca08589181cf3f1616951ef4b3ff55893750218689212e8309
```
其中，-m 指定提交的說明信息，跟我們使用的Git版本控制工具一樣；-a 可以指定更新的使用者信息；之後是用來建立映像檔的容器的 ID；最後指定新映像檔的名稱和 tag 。建立成功後會印出新映像檔的 ID。

使用 ```docker images``` 查看新建立的映像檔。

```
$ sudo docker images
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
ubuntu                  v2                  87f05893535e        3 minutes ago       188 MB
wolibohebadon/ca22006   latest              16a395dcdbb0        46 hours ago        427.1 MB
ubuntu                  14.04               8fa7f61732d6        5 days ago          188 MB
ca22006                 latest              bb986c5d7999        5 days ago          427 MB
node                    5.11.0              8593e962b570        9 days ago          644.3 MB

```

再來就可以使用新的Image來啟動Container

```
$ sudo docker run -ti ubuntu:v2
root@1cf2317c6e56:/#
```

**利用Dockerfile建立映像檔**

利用 ```docker commit``` 擴展Image 比較簡單，可是在團隊中並不方便分享，可以使用力一個方法```docker build```來建立一個新的映像檔。

再這之前，先建立一個Dockerfile，裏面包含一些用來建立Image的指令。

先來建立一個目錄和一個Dockerfile吧

```
$ mkdir sinatra
$ cd sinatra
$ touch Dockerfile    //若不知道[touch](http://linux.vbird.org/linux_basic/0220filemanager.php#touch)是什麼可以點這裡
```















































