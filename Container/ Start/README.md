# 5.1. 啟動

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
