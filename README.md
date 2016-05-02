#Docker 簡介

---

- Docker 是什麼？
- 為什麼要用Docker？ 
- 好處是什麼？



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

---

##映像檔

---

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
//顯示
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
//顯示
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
//顯示
root@1133d5eb031f:/#
```

---

##列出

---

###列出本機映像檔

使用 docker images 顯示本機已有的映像檔。

```
$ sudo docker images
//顯示
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
//顯示
root@0e50fa84f1bb:/# 
```

這邊的ID記一下

在容器中加入Json的gem套件

P.S.這邊不要複製root@id喔這是你自己的

```
//顯示
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
//顯示
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
$ touch Dockerfile   
```
這邊可以參考touch：
[連結](http://linux.vbird.org/linux_basic/0220filemanager.php#touch)

Dockerfile 中每一條指令都會建立一層Image

```
FROM ubuntu:14.04
MAINTAINER <wolibohebadon@gmail.com>    
RUN apt-get update && apt-get -y upgrade
RUN curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -
RUN apt-get install -y nodejs git npm
```
Dockerfile 基本的語法是

- 使用#來註釋

- FROM 指令告訴 Docker 使用哪個Image作為基底

- 接著是維護者的信息

- RUN開頭的指令會在建立中執行，比如安裝一個套件，在這裏使用 apt-get 來安裝了一些套件

完成 Dockerfile 後可以使用 docker build 建立Image。

```
$ sudo docker build -t="ubuntu:v2" .
//顯示
Sending build context to Docker daemon 2.048 kB
Step 1 : FROM ubuntu:14.04
 ---> 8fa7f61732d6
Step 2 : MAINTAINER <wolibohebadon@gmail.com>
 ---> Using cache
 ---> 2a36e155695b
Step 3 : RUN apt-get update && apt-get -y upgrade
 ---> Using cache
 ---> ce1215bc3de5
Step 4 : RUN curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -
 ---> Using cache
 ---> eedbe2998d71
Step 5 : RUN apt-get install -y nodejs git npm
 ---> Using cache
 ---> cbb6010622f8
Successfully built cbb6010622f8
```
其中 -t 標記添加 tag，指定新的Image的使用者信息。 “.” 是 Dockerfile 所在的路徑（當前目錄），也可以換成具體的 Dockerfile 的路徑。

可以看到 build 指令後執行的操作。第一件事情就是上傳這個 Dockerfile 內容，因為所有的操作都要依據 Dockerfile 來進行。 然後，Dockfile 中的指令被一條一條的執行。每一步都建立了一個新的容器，在容器中執行指令並提交修改（就跟之前介紹過的 docker commit 一樣）。當所有的指令都執行完畢之後，返回了最終的映像檔 Id。所有的中間步驟所產生的容器都會被刪除和清理。

P.S.Image 不能超過127行指令

現在可以用新建立的Image啟動一個容器。

```
$ sudo docker run -ti ubuntu:v2 /bin/bash
root@81b8fd65d871:/# 
```
還可以用 ```docker tag``` 命令修改Image的TAG。

```
$ sudo docker tag cbb6010622f8 ubuntu:devel
$ sudo docker images
//顯示
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
ubuntu                  devel               cbb6010622f8        13 minutes ago      408.1 MB
ubuntu                  v2                  cbb6010622f8        13 minutes ago      408.1 MB
<none>                  <none>              87f05893535e        57 minutes ago      188 MB
wolibohebadon/ca22006   latest              16a395dcdbb0        47 hours ago        427.1 MB
ubuntu                  14.04               8fa7f61732d6        5 days ago          188 MB
ca22006                 latest              bb986c5d7999        5 days ago          427 MB
node                    5.11.0              8593e962b570        9 days ago          644.3 MB
```

**上傳映像檔**

使用者可以通過 docker push 命令，把自己建立的Image上傳到倉儲中來共享。例如，使用者在 Docker Hub 上完成註冊後，可以推送自己的Image到倉儲中。

先登入Docker Hub

```
$ sudo docker login
```
上傳之前，有一點需要注意，Docker Hub 的格式為 UserName/Repository，所以這邊我們要先改名一下，不然會傳不上去，我們先用以下指令查看我們目前有哪些 Image。

```
$ sudo docker images
//顯示
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
ubuntu                  v2                  cbb6010622f8        31 minutes ago      408.1 MB
wolibohebadon/ca22006   latest              16a395dcdbb0        47 hours ago        427.1 MB
ubuntu                  14.04               8fa7f61732d6        5 days ago          188 MB
ca22006                 latest              bb986c5d7999        5 days ago          427 MB
node                    5.11.0              8593e962b570        9 days ago          644.3 MB

$ sudo docker tag ubuntu:v2 wolibohebadon/ubuntu:v2
//顯示
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
wolibohebadon/ubuntu    v2                  cbb6010622f8        31 minutes ago      408.1 MB
wolibohebadon/ca22006   latest              16a395dcdbb0        47 hours ago        427.1 MB
ubuntu                  14.04               8fa7f61732d6        5 days ago          188 MB
ca22006                 latest              bb986c5d7999        5 days ago          427 MB
node                    5.11.0              8593e962b570        9 days ago          644.3 MB
```
改完名稱後就可以開始上傳了

```
$ sudo docker push wolibohebadon/ubuntu

//顯示
Sending image list
The push refers to a repository [docker.io/wolibohebadon/ubuntu]
```

---

##存取和載入

---

###儲存和載入映像檔

**儲存映像檔**

如果要建立Image到本地檔案，可以使用 ```docker save``` 命令。

```
$ sudo docker images
//顯示
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
wolibohebadon/ubuntu    v2                  cbb6010622f8        52 minutes ago      408.1 MB
$ sudo docker save -o ubuntu_14.04.tar ubuntu:14.04
```
**載入映像檔**

可以使用 ```docker load```從建立的本地檔案中再匯入到本地Image庫，例如

```
sudo docker load --input ubuntu_14.04.tar
//或
sudo docker load < ubuntu_14.04.tar
```
可以匯入之前儲存的Image

---

##移除

---

##移除本地端映像檔

如果要移除本地端的Image，可以使用 ```docker rmi``` 命令。注意 ```docker rm ```命令是移除容器。

```
$sudo docker rmi wolibohebadon/ubuntu:v2
//顯示
$ sudo docker rmi wolibohebadon/ubuntu:v2
Untagged: wolibohebadon/ubuntu:v2
Deleted: sha256:cbb6010622f87b6d012f6b05202b3e1cca54688746b3a52dd9cdce3ea1184fb5
Deleted: sha256:d5137fa1b9f404280a7cedbce21318309ba9de17061fee9be40211ccd48b8929
Deleted: sha256:eedbe2998d7104f25da20b2b4fcd19f03572dbb656d7ee4f5e27e0c51196bc7b
Deleted: sha256:ce1215bc3de5d63bca766e5321323a681538f9b558554101722d39e20e0920bd
Deleted: sha256:daa9093d9660b8078b2072a9489d62d8720d5aee629d2d59d99b85de4e33b19a
Deleted: sha256:2a36e155695be823372b0c975a45bbec2a027f1d9d4b962e37bfbfdc0297203c
```
P.S.：在刪除映像檔之前要先用 ```docker rm``` 刪掉依賴於這個Image的所有Container。

---

#容器

---

##啟動

---

###啟動容器


啟動容器有兩種方式，一種是將Image新建一個Container並啟動，另外一個是將終止狀態（stopped）的容器重新啟動。

因為 Docker 的容器實在太輕量級了，User可以隨時刪除和新建立Container。

**新增並啟動**

所需要的命令主要為 ```docker run```。

下面的命令輸出一個 “Hello World”，之後終止容器。

EX:
```
$ sudo docker run ubuntu:14.04 /bin/echo 'Hello world'
//顯示
Hello world
```

這跟在本地直接執行 /bin/echo 'hello world' 相同， 幾乎感覺不出任何區別。

下面的命令則啟動一個 bash 終端，允許使用者進行互動。

```
$ sudo docker run -ti ubuntu:14.04 /bin/bash
//顯示
root@4d829b6cb093:/# 
```
其中，-t 選項讓Docker分配一個虛擬終端（pseudo-tty）並綁定到Container的標準輸入上， -i則讓容器的標準輸入保持打開的狀態。

在互動模式下，使用者可以透過所建立的終端來輸入命令

EX：

```
root@af8bae53bdd3:/# pwd
/
root@af8bae53bdd3:/# ls
bin boot dev etc home lib lib64 media mnt opt proc root run sbin srv sys tmp usr var
```
參考資料：
[pwd](http://linux.vbird.org/linux_basic/0220filemanager.php#pwd)
[ls](http://linux.vbird.org/linux_basic/0220filemanager.php#ls)

當利用 ```docker run``` 來建立Container時，Docker 在後臺執行的標準操作包括：

- 檢查本地是否存在指定的Image，不存在就從公有倉儲下載

- 利用Image建立並啟動一個容器

- 分配一個檔案系統，並在唯讀的Image層外面掛載一層可讀寫層

- 從宿主主機設定的網路橋界面中橋接一個虛擬埠到Container中

- 從位址池中設定一個 ip 位址給容器

- 執行使用者指定的應用程式

- 執行完畢後Container被終止

**啟動已終止容器**

可以利用 ```docker start``` 命令，直接將一個已經終止的容器啟動執行。

Container的核心為所執行的應用程式，需要的資源都是應用程式執行所必需的。所以並沒有其它的資源。可以在虛擬終端中利用 ```ps``` 或 ```top``` 來查看程式訊息。

```
root@4d829b6cb093:/# ps
  PID TTY          TIME CMD
    1 ?        00:00:00 bash
   20 ?        00:00:00 ps
```
這邊可以看到ㄉContainer中僅執行了指定的 bash 應用。這個特點讓 Docker 對資源的使用率極高，果然是輕量級虛擬化。

---
##守護態執行

---

###守護態執行

---

更多的時候，需要讓 Docker Container在後臺以守護態（Daemonized）形式執行。此時，可以透過新增 -d 參數來實作。

下面的命令會在後臺執行Container。

EX:

```
$ sudo docker run -d ubuntu:14.04 /bin/sh -c "while true; do echo hello world; sleep 1; done"
//顯示
c18eb0e7e0a6281277c6135e5df5161ad70d03954b0949615cc94650ad745051
```
Container啟動後會返回一個唯一的 id，也可以透過 docker ps 命令來查看Container訊息。

```
$ sudo docker ps
//顯示
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
c18eb0e7e0a6        ubuntu:14.04        "/bin/sh -c 'while tr"   8 minutes ago       Up 8 minutes                            cranky_minsky
```
要取得Container的輸出訊息，可以透過```docker logs``` 命令。

```
$ sudo docker logs cranky_minsky
//顯示
hello world
hello world
hello world
. . .
```

---
##終止
---
###終止容器

可以使用 ```docker stop``` 來終止一個執行中的容器。

當Docker Container中指定的應用終結時，Container也自動終止。 例如對於上一章節中只啟動了一個終端機的Container，使用者透過 exit 命令或 Ctrl+d 來退出終端時，所建立的Container立刻終止。

終止狀態的Container可以用 ```docker ps -a``` 命令看到。

EX：

```
$ sudo docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                        PORTS               NAMES
ee3431ffe4b3        ubuntu:14.04        "/bin/sh -c 'while tr"   9 minutes ago       Up 9 minutes                                      kickass_swartz
4b4d2b481352        ubuntu:14.04        "/bin/sh -c 'while tr"   9 minutes ago       Up 9 minutes                                      cranky_panini
```
處於終止狀態的容器，可以透過 ```docker start``` 命令來重新啟動。

```
$ sudo docker start c10bdd5f2d28       //c10bdd5f2d28是你要開啟的id
```
此外，```docker restart``` 命令會將一個執行中的容器終止，然後再重新啟動它。

```
$ sudo docker restart 4b4d2b481352     //4b4d2b481352是你要重啟的id
```

---
##進入容器
---
###進入容器
---

在使用 ```-d``` 參數時，Container啟動後會進入後臺。 某些時候需要進入Container進行操作，有很多種方法，包括使用 ```docker attach``` 命令或 ```nsenter``` 工具等。

**exec 命令**
```
$ sudo docker run -tdi ubuntu
//顯示
80787210307a297f886c851e803a142a8fcb5a0f0b7aec1d1a7e2c772284d652
$ sudo docker ps
//顯示
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
80787210307a        ubuntu              "/bin/bash"         13 seconds ago      Up 12 seconds                           boring_easley
$ sudo docker exec -ti boring_easley bash
//顯示
root@80787210307a:/# 
```
**attach 命令**

```docker attach``` 亦是Docker內建的命令。下面示例如何使用該命令。

```
sudo docker run -idt ubuntu
//顯示
31f9479fec8be34fb782b5bbb6f6f90d341596fb605d274c90b3ebec9b215912
$ sudo docker ps
//顯示
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
31f9479fec8b        ubuntu              "/bin/bash"         24 seconds ago      Up 23 seconds                           cranky_visvesvaraya
$ sudo docker attach cranky_visvesvaraya
//顯示
root@31f9479fec8b:/#  
```
但是使用 attach 命令有時候並不方便。當多個窗口同時 attach 到同一個Container的時候，所有窗口都會同步顯示。當某個窗口因命令阻塞時,其他窗口也無法執行操作了。

**nsenter 命令**

**安裝**

```nsenter``` 直接下載最新版2.28版來使用

```
$ curl https://www.kernel.org/pub/linux/utils/util-linux/v2.28/util-linux-2.28.tar.gz | tar -zxf-; cd util-linux-2.28
$ ./configure --without-ncurses
$ make nsenter && sudo cp nsenter /usr/local/bin
```
**使用**

```nsenter``` 可以存取另一個程式的命名空間。```nsenter``` 要正常工作需要有 root 權限。


```
$ sudo docker run -tdi ubuntu
//顯示
dc947049c99b805ba705319c02ce76385794b1f5b3e5526e54aca04428bf417d
$ sudo docker ps
//顯示
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
dc947049c99b        ubuntu              "/bin/bash"         2 minutes ago       Up 2 minutes                            high_swartz
$ echo $(docker-pid dc947049c99b)
//顯示
13830
$ sudo nsenter --target 13830 --mount --uts --ipc --net --pid
顯示
root@dc947049c99b:/# 
```
再使用上面的指令之前，請先執行下面的命令

```
$ wget -P ~ https://github.com/yeasy/docker_practice/raw/master/_local/.bashrc_docker;
$ echo "[ -f ~/.bashrc_docker ] && . ~/.bashrc_docker" >> ~/.bashrc; source ~/.bashrc
```
透過上面這個指令就可以定義很多Docker的命令

---
##匯出與匯入
---
###匯出和匯入容器
---

**匯出容器**

匯出本地某個Container，可以使用 docker export 命令。

```
$ sudo docker ps -a
//建立
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
dc947049c99b        ubuntu              "/bin/bash"         17 minutes ago      Up 17 minutes                           high_swartz
$ sudo docker export dc947049c99b > ubuntu.tar
```
匯出Container快照到本機檔案

**匯入快照容器**

可以使用```docker import```從Container快照檔案中再匯入為Image

EX:

```
$ cat ubuntu.tar | sudo docker import - test/buntu:v1.0
$ sudo docker images
//建立
REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
test/buntu              v1.0                0228e522e40c        3 minutes ago       108.8 MB
ubuntu                  14.04               8fa7f61732d6        5 days ago          188 MB
```
此外，也可以透過指定 URL 或者某個目錄來匯入

EX：

```
$ sudo docker import http://example.com/exampleimage.tgz example/imagerepo
```
P.S.：使用者既可以使用 ```docker load ```來匯入映像檔儲存檔案到本地映像檔庫，也可以使用 ```docker import``` 來匯入一個Container快照到本機Image。這兩者的區別在於Container快照檔案僅保存Container當時的快照狀態，而Image儲存檔案將保存完整記錄，檔案體積也跟著變大。此外，從Container快照檔案匯入時可以重新指定標籤等原始資料訊息。

---
##刪除
---
###刪除容器
---
可以使用```docker rm```來刪除一個處於終止狀態的Container。

EX：

```
$ sudo docker rm 9e5b1a1c60ae
9e5b1a1c60ae
```
如果要刪除一個執行中的容器，可以新增 -f 參數。Docker 會發送 ```SIGKILL``` 信號給容器。

---

#倉儲
---
##倉儲
---

倉儲（Repository）是集中存放Image的地方。

容易混淆的大概是註冊伺服器（Registry）。註冊伺服器是管理Repository的具體伺服器，每個伺服器上有很多個Repository，而每個Repository下面有多個Image。從這方面來說，Repository可以被認為是一個具體的專案或目錄。

EX:

Repository位址：dl.dockerpool.com/ubuntu

dl.dockerpool.com是註冊伺服器位址

ubuntu 是Repository名稱。

其實有些時候，並不用太區分他們

---
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
##私有倉庫
---
###私有倉庫
---

有時候使用 Docker Hub 這樣的公共Repository可能不方便，使用者可以建立一個本機Repository供私人使用。

本節介紹如何使用本地Repository。

```docker-registry``` 是官方提供的工具，可以用於建立私有的Image Repository 。

**安裝執行 docker-registry**

**容器執行**

安裝了 Docker 後，可以透過取得官方 registry Image來執行。

```
$ sudo docker run -d -p 5000:5000 registry
```
這可以使用官方的 registry Image來啟動本機的私有Repository。

使用者可以透過指定參數來設定私有Repository位置，例如設定Image儲存到 Amazon S3 服務。

```
sudo docker run \
         -e SETTINGS_FLAVOR=s3 \
         -e AWS_BUCKET=acme-docker \
         -e STORAGE_PATH=/registry \
         -e AWS_KEY=AKIAHSHB43HS3J92MXZ \
         -e AWS_SECRET=xdDowwlK7TJajV1Y7EoOZrmuPEJlHYcNP2k4j49T \
         -e SEARCH_BACKEND=sqlalchemy \
         -p 8080:8080 \
         registry
.
```
此外，還可以指定本機路徑（如 /home/user/registry-conf ）下的設定檔案。

```
$ sudo docker run -d -p 8080:8080 -v /home/user/registry-conf:/registry-conf -e DOCKER_REGISTRY_CONFIG=/registry-conf/config.yml registry
```
假設Repository會被建立在Container的 /tmp/registry 下。可以透過 -v 參數來將Image檔案存放在本地的指定路徑。 例以下面的例子將上傳的Image放到 /opt/data/registry 目錄。

```
$ sudo docker run -d -p 8080:8080 -v /opt/data/registry:/tmp/registry registry
```
**本地安裝**

Ubuntu 或 CentOS 等發行版，可以直接透過套件庫安裝。

這邊只介紹Ubuntu

- Ubuntu
```
$ sudo apt-get install -y build-essential python-dev libevent-dev python-pip liblzma-dev swig
$ sudo pip install docker-registry
```
另一種方式可以到  [docker-registry](https://github.com/docker/docker-registry) 專案下載原始碼進行安裝。

```
$ sudo apt-get install build-essential python-dev libevent-dev python-pip libssl-dev liblzma-dev libffi-dev
$ git clone https://github.com/docker/docker-registry.git
$ cd docker-registry
$ sudo python setup.py install
```
再來修改設定檔案，主要修改 dev 模板段的 ```storage_path``` 到本地的儲存Repository的路徑。

```
$ cp config/config_sample.yml config/config.yml
```



















