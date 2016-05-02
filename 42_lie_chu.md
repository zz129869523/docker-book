# 4.2. 列出

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