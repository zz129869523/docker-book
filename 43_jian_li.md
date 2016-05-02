# 4.3. 建立

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
