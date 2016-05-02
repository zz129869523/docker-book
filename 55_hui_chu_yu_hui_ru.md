# 5.5. 匯出與匯入

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